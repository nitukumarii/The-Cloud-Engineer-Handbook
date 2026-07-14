# Debugging High CPU Usage — Interview Q&A (Senior Linux Admin / SRE)

## Q1: A customer reports the server is "slow." You SSH in — walk me through how you debug high CPU usage.

**A:** I don't jump straight to `top`. I follow a funnel: confirm the problem is real and quantify it, find the process, find the function inside the process, then find the root cause.

**Step 1 — Confirm and classify the CPU usage**

```bash
uptime                # load average trend (1/5/15 min)
mpstat -P ALL 1 5      # per-core breakdown
vmstat 1 5             # user/sys/wait/idle/steal split
```

The critical first question is *what kind* of CPU time is high:

| Column | Meaning | Points to |
|--------|---------|-----------|
| `us` | user time | Application code burning cycles |
| `sy` | system time | Kernel/syscalls, context switching |
| `wa` | iowait | Not CPU-bound — disk/IO starved |
| `si/hi` | interrupts | Interrupt storm (NIC, hardware) |
| `st` | steal | Noisy neighbor on a hypervisor — not your box's fault |

**Step 2 — Identify the culprit process**

```bash
top -o %CPU
ps aux --sort=-%cpu | head -20
pidstat -u 1 5          # per-process CPU over time — spike or sustained?
```

**Step 3 — Drill into the process**

```bash
top -H -p <PID>         # per-thread CPU
strace -c -p <PID>      # syscall summary
```

**Step 4 — Profile it**

```bash
perf top -p <PID>
perf record -F 99 -p <PID> -g -- sleep 30 && perf report
```

Or a language-specific profiler (`jstack`/JFR for Java, `py-spy` for Python, `pprof` for Go).

**Step 5 — Check systemic causes**

```bash
dmesg -T | tail -50      # OOM killer, hardware errors
cat /proc/interrupts      # interrupt distribution
```

Then correlate with deploys, cron jobs, traffic graphs.

---

## Follow-up Q&A

### Q2: What's the difference between load average and CPU usage percentage? Can load average be high while CPU usage is low?

**A:** Yes, and this trips people up constantly. Load average on Linux counts processes that are *runnable or uninterruptibly waiting* — not just CPU-bound processes. A process stuck in `D` state waiting on disk IO counts toward load average but consumes near-zero CPU. So you can have load average of 40 on an 8-core box while `mpstat` shows CPU mostly idle — that's almost always an IO bottleneck (slow disk, NFS hang, DB lock contention), not a CPU problem. I always cross-check load average against `vmstat`'s `wa` column and `ps aux` for processes in `D` state before assuming it's CPU-bound.

---

### Q3: You find that `sy` (system time) is high, not `us`. What does that tell you and what do you check next?

**A:** High `sy` means the kernel is doing the work, not the application logic itself. Common causes:
- Excessive syscalls (e.g., a chatty app doing tiny reads/writes instead of buffered IO) — confirm with `strace -c`
- Heavy context switching — check `vmstat`'s `cs` column, or `pidstat -w`
- Network stack overhead — check `ksoftirqd` CPU usage and `/proc/interrupts` for an imbalanced or flapping NIC
- Page faults — `sar -B` or `ps -o min_flt,maj_flt`
- Container/cgroup throttling overhead in containerized environments

If `ksoftirqd` itself is consuming significant CPU, that's a strong signal it's network interrupt load, not application code — I'd check `irqbalance` status and NIC interrupt distribution across cores next.

---

### Q4: What's CPU steal time and why do you care about it?

**A:** Steal time (`st` in `top`/`vmstat`) is CPU time your VM *wanted* but the hypervisor gave to another tenant instead. It only shows up in virtualized environments. If steal time is significant, no amount of tuning inside my VM will fix it — the problem is at the hypervisor/host level, likely a noisy neighbor or an oversubscribed host. My action there is to escalate to the cloud provider or infra team, and short-term, consider migrating the workload to a different host/instance type. I explicitly call this out early in triage so I don't waste time profiling application code that isn't the actual bottleneck.

---

### Q5: How would you debug high CPU usage on a process you can't restart and can't `strace` (e.g., strace is blocked by security policy or adds too much overhead in prod)?

**A:** A few options depending on constraints:
- `perf top -p <PID>` or `perf record` — much lower overhead than strace since it uses sampling, not full interception, and works without special seccomp permissions in most setups
- Read `/proc/<PID>/stack` (kernel stack) and `/proc/<PID>/task/*/stat` to see per-thread state without attaching a debugger
- For managed runtimes, use non-invasive built-in profilers: JFR for Java (can attach live), `py-spy dump` for Python (reads process memory without ptrace in some modes, though it typically still needs ptrace access)
- `eBPF`-based tools like `execsnoop`, `profile-bpfcc`, or `bpftrace` scripts — very low overhead, good for prod, since they hook into kernel tracepoints rather than intercepting every syscall like strace does

The key trade-off I'm managing is observability vs. overhead vs. permissions — `perf` and eBPF tools are usually my first choice in prod because they're sampling-based and lightweight.

---

### Q6: Walk me through a real incident: CPU spikes to 100% every day at 2 AM for about 10 minutes. How do you approach this differently than an ongoing spike?

**A:** Since it's not happening right now, I can't just run `top` and catch it live — I need historical data and correlation.

1. Check `sar -u -f /var/log/sa/saXX` (if `sysstat` is installed and collecting) for historical per-interval CPU stats around 2 AM
2. Check `crontab -l` for all users and `/etc/cron.d/`, `/etc/cron.daily`, etc. — 2 AM is prime cron territory (backups, log rotation, batch jobs)
3. Check application-level schedulers too (Celery beat, Quartz jobs, Kubernetes CronJobs) — not just system cron
4. If it's reproducible, set up a lightweight always-on capture ahead of the next occurrence: `perf record -F 99 -a -g -- sleep 600` scheduled via cron just before 2 AM, or leave `pidstat -u 1` logging to a file
5. Cross-reference with monitoring (Prometheus/Grafana) for anything else correlated — cache eviction, connection pool resets, GC full pauses

Most of the time this ends up being a backup job, a log rotation + compression job, or a batch/reporting job all firing at the same cron boundary and competing for CPU. I'd either stagger the schedules or move the heavy one to a quieter window or a separate host.

---

### Q7: What's the difference between `perf top` and a flamegraph, and when would you generate one over the other?

**A:** `perf top` gives a live, real-time view of which functions/symbols are consuming CPU right now — great for "what's hot at this moment" during an active incident. A flamegraph is a static visualization built from a `perf record` capture over a time window, showing the full call stack depth and relative width = CPU time. 

I use `perf top` for quick live triage when I'm SSH'd in during an active spike. I generate a flamegraph when I need to: (a) capture evidence for a postmortem, (b) share findings with a team that isn't comfortable reading raw `perf report` output, or (c) spot a deep call chain issue (e.g., recursive function, N+1 pattern) that's easier to see visually as stack width than as a flat symbol list.

---

### Q8: If you had to give a one-line summary of your triage philosophy for this kind of problem, what would it be?

**A:** Classify before you drill down — figure out *what kind* of CPU time (user/sys/wait/steal) and *whose* process it is before you start profiling functions, because profiling the wrong layer wastes time and can send you chasing application code when the real problem is the hypervisor, the kernel, or a scheduling collision.

