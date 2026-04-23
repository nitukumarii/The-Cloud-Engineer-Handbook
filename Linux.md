Explanation of Swap Space and the swappiness Parameter in Linux

Swap Space:

Swap space is a part of the hard drive or SSD that is designated to act as "virtual memory" when the physical RAM (Random Access Memory) of a system runs out. In a nutshell, it is used to extend the amount of memory available to the system when physical RAM is exhausted. Swap can be in the form of a swap partition or a swap file.
During partitioning, when you install a Linux distribution, you might notice an entry for "swap space" (e.g., /dev/sda5), which is dedicated to handling virtual memory. Typically, this space is set to at least twice the size of the RAM in the system, though this ratio can vary depending on the system’s needs and the user’s preference.
When the system runs out of physical memory (RAM), it moves less frequently used data or inactive processes from RAM to the swap space, freeing up RAM for active processes. This process is called paging.

Swappiness Parameter:

Swappiness is a kernel parameter that controls how aggressively the Linux kernel will swap out pages from physical memory to swap space. It determines how often and under what conditions the system will use swap space when the system is under memory pressure.
The swappiness value can range from 0 to 100, where:
0 means the kernel will avoid swapping as much as possible and will only swap out data when absolutely necessary (i.e., when RAM is exhausted).
100 means the kernel will swap out data more aggressively, even when there is still available RAM.
By adjusting the swappiness value, you can control how the system behaves under heavy memory load. For example:
Lower values (e.g., 10) mean the system will prioritize keeping data in RAM and use swap space only when RAM is really exhausted.
Higher values (e.g., 60 or 100) mean the system will swap data to the disk more aggressively, which can be useful for certain workloads that rely heavily on large datasets.
Checking the Current Swappiness Value:

To view the current swappiness value, you can run the following command:

cat /proc/sys/vm/swappiness

This will return the current value set for swappiness (typically 60 by default in most Linux distributions).

Changing the Swappiness Value:

The swappiness value can be modified temporarily by using the following command (the change will last until the system is rebooted):

sudo sysctl vm.swappiness=10

This command sets the swappiness value to 10, which means the kernel will swap less aggressively.

If you want to make the change permanent across reboots, you can modify the /etc/sysctl.conf file:

Open the file with a text editor:

sudo nano /etc/sysctl.conf

Add or modify the following line:

vm.swappiness = 10
Save the file and exit the editor.

Apply the change immediately with:

sudo sysctl -p
Why Adjust Swappiness?
The default swappiness value of 60 is typically suitable for most general-purpose systems, but you might want to change it depending on your use case:
If you have plenty of RAM and want to avoid the use of swap unless necessary, you can reduce the swappiness value (e.g., swappiness=10).
If your system has limited RAM and you want to make better use of swap space, you may increase the swappiness value to make the kernel swap more aggressively, even with some free RAM.
Conclusion:
Swap space allows Linux to handle memory more effectively when physical RAM runs out.
The swappiness parameter controls the kernel’s behavior when it comes to swapping data out of RAM and into the swap space.
Adjusting swappiness can optimize the performance of your system based on your hardware and workload requirements.


Explanation of Swap Space and the swappiness Parameter in Linux

Swap Space:

Swap space is a part of the hard drive or SSD that is designated to act as "virtual memory" when the physical RAM (Random Access Memory) of a system runs out. In a nutshell, it is used to extend the amount of memory available to the system when physical RAM is exhausted. Swap can be in the form of a swap partition or a swap file.
During partitioning, when you install a Linux distribution, you might notice an entry for "swap space" (e.g., /dev/sda5), which is dedicated to handling virtual memory. Typically, this space is set to at least twice the size of the RAM in the system, though this ratio can vary depending on the system’s needs and the user’s preference.
When the system runs out of physical memory (RAM), it moves less frequently used data or inactive processes from RAM to the swap space, freeing up RAM for active processes. This process is called paging.

Swappiness Parameter:

Swappiness is a kernel parameter that controls how aggressively the Linux kernel will swap out pages from physical memory to swap space. It determines how often and under what conditions the system will use swap space when the system is under memory pressure.
The swappiness value can range from 0 to 100, where:
0 means the kernel will avoid swapping as much as possible and will only swap out data when absolutely necessary (i.e., when RAM is exhausted).
100 means the kernel will swap out data more aggressively, even when there is still available RAM.
By adjusting the swappiness value, you can control how the system behaves under heavy memory load. For example:
Lower values (e.g., 10) mean the system will prioritize keeping data in RAM and use swap space only when RAM is really exhausted.
Higher values (e.g., 60 or 100) mean the system will swap data to the disk more aggressively, which can be useful for certain workloads that rely heavily on large datasets.
Checking the Current Swappiness Value:

To view the current swappiness value, you can run the following command:

cat /proc/sys/vm/swappiness

This will return the current value set for swappiness (typically 60 by default in most Linux distributions).

Changing the Swappiness Value:

The swappiness value can be modified temporarily by using the following command (the change will last until the system is rebooted):

sudo sysctl vm.swappiness=10

This command sets the swappiness value to 10, which means the kernel will swap less aggressively.

If you want to make the change permanent across reboots, you can modify the /etc/sysctl.conf file:

Open the file with a text editor:

sudo nano /etc/sysctl.conf

Add or modify the following line:

vm.swappiness = 10
Save the file and exit the editor.

Apply the change immediately with:

sudo sysctl -p
Why Adjust Swappiness?
The default swappiness value of 60 is typically suitable for most general-purpose systems, but you might want to change it depending on your use case:
If you have plenty of RAM and want to avoid the use of swap unless necessary, you can reduce the swappiness value (e.g., swappiness=10).
If your system has limited RAM and you want to make better use of swap space, you may increase the swappiness value to make the kernel swap more aggressively, even with some free RAM.
Conclusion:
Swap space allows Linux to handle memory more effectively when physical RAM runs out.
The swappiness parameter controls the kernel’s behavior when it comes to swapping data out of RAM and into the swap space.
Adjusting swappiness can optimize the performance of your system based on your hardware and workload requirements.


Zombie process explanation and killing:
A zombie process is a process that has completed execution, but its parent process hasn't acknowledged its exit status (through wait()).
You can't directly kill a zombie process, but you can terminate its parent process to clean up the zombie process.
To identify zombie processes: ps aux | grep 'Z'
To find the parent process ID (PPID) of the zombie: ps -o ppid= -p <zombie_pid>
Then, kill the parent process using: kill -9 <PPID>
List all running processes, including background processes:
ps -aux
Difference between kill and killall:
kill: Terminates a specific process by its PID.
killall: Terminates all processes matching a specific name.
Difference between fg, bg, and jobs in managing processes:
fg: Brings a background job to the foreground.
bg: Resumes a suspended job in the background.
jobs: Lists all jobs (both running and suspended).
To manage processes, you can use ps to list processes, identify their PIDs, and use kill -9 <PID> to terminate them.

How do you monitor system resources in Linux?
You can use top and htop to monitor system resources in real time. htop is more user-friendly, showing resources like CPU, memory, and processes with color coding.
What command would you use to check memory usage, and what does the output indicate?
free -m: It shows memory statistics in megabytes, including free, used, total, available RAM, and cache memory.
Free memory indicates unused memory, while available memory includes both unused and memory that can be reclaimed for new processes.
Swap usage: If the swap memory is used heavily, the system might be underperforming, as accessing swap memory is slower than RAM.
Explain how you would analyze system performance using vmstat, iostat, free, and top.
iostat -x: Displays extensive statistics on read/write operations. If write and wait times are high, the system might be slow.
vmstat: Shows detailed information on system processes, memory, paging, and CPU activity. It can be used to diagnose resource bottlenecks.
free: Displays memory usage including used, free, available, and swap memory.
top: Provides real-time monitoring of system resources, CPU usage, and process statistics.
How would you check the swap usage on a Linux system?
Use free -m or swapon -s to check swap usage.
What are some methods to diagnose high CPU usage or resource exhaustion on a system?
Use top to identify processes consuming the most CPU. Once identified, you can kill the process using kill -9 <PID> if necessary.

**VMSTAT**
The vmstat command in Linux reports virtual memory statistics, system performance, and resource usage. When you run vmstat without any options, you will get an output with several columns of information. Below is an example output and an explanation of each field.
<img width="555" height="95" alt="image" src="https://github.com/user-attachments/assets/673238c3-7319-4167-a761-8656b8268006" />

Explanation of columns:
1. procs (processes)
r: Number of processes waiting for run time (ready to run).
b: Number of processes in uninterruptible sleep (e.g., waiting on I/O).
2. memory
swpd: Amount of virtual memory used (in KB).
free: Amount of idle memory (in KB).
buff: Memory used as buffers (in KB).
cache: Memory used as cache (in KB).
3. swap
si: Amount of memory swapped in from disk (in KB).
so: Amount of memory swapped out to disk (in KB).
4. io (I/O)
bi: Blocks received from a block device (e.g., disk reads) (in KB).
bo: Blocks sent to a block device (e.g., disk writes) (in KB).
5. system
in: Number of interrupts per second (including clock interrupts).
cs: Number of context switches per second.
6. cpu (CPU)
us: Percentage of CPU time spent on user processes (user space).
sy: Percentage of CPU time spent on kernel processes (system space).
id: Percentage of CPU time spent idle.
wa: Percentage of CPU time spent waiting for I/O.
st: Percentage of CPU time stolen from virtual machines (if applicable).
Notes:
The vmstat output is continuously updated when you specify an interval (e.g., vmstat 1 for 1-second intervals).
The values shown are averages over the time since the last update.

What is the purpose of /var/log? Name some important log files located in it.
Purpose: The /var/log directory contains log files for system, application, and kernel events. These logs help administrators monitor the health and performance of the system and troubleshoot issues.
Important Log Files:
/var/log/syslog: System messages, including kernel logs.
/var/log/messages: General system activity logs.
/var/log/auth.log: Authentication logs.
/var/log/kern.log: Kernel logs.
/var/log/dmesg: Boot and hardware-related logs.
/var/log/apache2/access.log: Web server access logs (for Apache).
/var/log/apache2/error.log: Web server error logs (for Apache).
/var/log/boot.log: Boot process logs.
/var/log/cron: Cron job logs.
/var/log/mysql/error.log: MySQL error logs.
2. How do you check system logs in Linux? What is the role of journalctl?
Checking System Logs: You can check system logs using the following:
cat /var/log/syslog or cat /var/log/messages for general system activity.
dmesg for kernel and boot logs.
journalctl for querying and viewing logs.
Role of journalctl: journalctl is used to query and display logs collected by the systemd journal service. It can display logs in real-time, filter logs by date, service, and severity, and show logs from multiple sources in a structured format.
Example: journalctl -u <service-name> to view logs specific to a service.
3. Explain how to view kernel logs in Linux.
You can view kernel logs using the dmesg command, which displays the messages from the kernel ring buffer, including boot logs, hardware-related events, and driver messages.
Example: dmesg | less to view the kernel logs in a scrollable format.
4. How do you filter logs using grep? Provide an example of how you would search for a specific error in logs.
You can use grep to filter logs for specific keywords or patterns.
Example: grep "error" /var/log/syslog to find all lines containing the word "error" in the syslog file.
Alternatively, to monitor logs in real-time for errors: tail -f /var/log/syslog | grep "error".
5. What are core dumps, and how can they be useful in debugging application failures?
Core Dumps: A core dump is a file that captures the memory contents of a running process when it crashes. It helps developers analyze the state of the application at the time of the crash, which can assist in diagnosing bugs or issues.
Usefulness: Core dumps allow developers to inspect the process's memory, stack, and other details to identify the root cause of a crash or unexpected behavior.
6. What is the purpose of the dmesg command? How would you use it to troubleshoot hardware issues?
Purpose of dmesg: dmesg displays the kernel ring buffer, which contains information about system events, hardware detection, and driver issues. It is especially useful for troubleshooting hardware-related problems.
Usage: To troubleshoot hardware issues, you can run dmesg | grep <hardware-name> to search for specific hardware logs, such as disk or network device errors.
Example: dmesg | grep -i error to find hardware-related errors.
7. Explain the process of troubleshooting a failed service using logs.
Troubleshooting Process:
Use journalctl -u <service-name> to get logs related to the failed service.
Check the service status with systemctl status <service-name> for any recent errors.
Review the logs to identify error messages, such as missing files, permission issues, or configuration errors.
Check the associated configuration files for any misconfigurations.
Resolve the issue and restart the service with systemctl restart <service-name>.
8. How do you configure and manage log rotation in Linux?
Log Rotation is typically managed through the logrotate utility, which rotates, compresses, and removes old logs to prevent them from consuming too much disk space.
Configuration: The configuration files for logrotate are usually located in /etc/logrotate.conf and /etc/logrotate.d/. You can specify the frequency of rotation, number of backups to keep, compression options, and more.
Example: logrotate /etc/logrotate.conf to manually rotate logs.
9. How can you analyze a kernel crash dump? What tools would you use?
Analyzing Kernel Crash Dumps: When the system crashes due to kernel issues, the kernel crash dump can be analyzed using tools like kdump, crash, and gdb.
Tools:
kdump: The Linux kernel crash dumping mechanism, which saves a dump of the system's memory when a crash occurs.
crash: A command-line utility for analyzing crash dumps.
gdb: A debugger that can be used to analyze the kernel's memory dump.
10. How do you interpret a crash dump using kdump?
kdump captures memory dumps of a system crash and stores them in a crash dump file. After a crash, you can analyze this file using the crash tool.
Steps:
Ensure kdump is configured and enabled on the system.
After a crash, the dump will be saved in the location specified by kdump's configuration (e.g., /var/crash).
Use the crash utility to analyze the dump file: crash /var/crash/vmcore.
Inspect the dump for the cause of the crash, such as kernel bugs or hardware issues.

These commands and concepts will help you effectively troubleshoot and manage system, kernel, and application issues using logs and crash dumps.

How kdump Works: A Simple Explanation
What is kdump?
kdump is a Linux feature that captures the state of the system's memory (a crash dump) when the kernel crashes. This helps in diagnosing the cause of the crash.
How kdump Works: Step-by-Step Flow
Enable kdump:
kdump relies on a second (crash) kernel. This is a minimal kernel reserved for capturing the crash data.
When enabled, a portion of the system's memory is reserved for this crash kernel.
Crash Occurs:
If the primary (main) kernel crashes due to a critical error, the system automatically switches to the crash kernel.
Crash Dump Captured:
The crash kernel collects a snapshot of the main kernel's memory and saves it as a crash dump file (usually in /var/crash).
Reboot System:
After capturing the dump, the system reboots to restore normal operations.
Analyze the Dump:
The crash dump can be analyzed using tools like crash or gdb to identify what caused the kernel to crash.
Hypothetical Scenario for Using kdump
Scenario:

Imagine you're a Linux admin managing a critical server that hosts a database. Suddenly, the server crashes, and you need to figure out what caused the issue to prevent it from happening again.

Steps a Linux Admin Would Follow
Check if kdump is Enabled:
Run systemctl status kdump to verify if kdump is active.

If not, enable it:

sudo systemctl enable kdump
sudo systemctl start kdump
Configure kdump:

Open the kdump configuration file:

sudo nano /etc/kdump.conf
Ensure the dump location is set, e.g., /var/crash.
Reserve Crash Kernel Memory:

Check the memory reserved for the crash kernel using:

cat /proc/cmdline

Update the GRUB configuration if needed to allocate memory:

sudo nano /etc/default/grub

Add: crashkernel=256M.

Reboot the System:

After configuring, reboot the server for changes to take effect:

sudo reboot
Wait for a Crash:
If the server crashes, the crash kernel captures the memory dump and saves it in /var/crash.
Analyze the Dump:

Use the crash tool to analyze the dump:

sudo crash /usr/lib/debug/vmlinux-<kernel_version> /var/crash/vmcore
Investigate for errors like faulty drivers, hardware issues, or kernel bugs.
What to Do in an Interview if Asked About kdump
Task: "Set up kdump on a Linux system and explain the flow."
Enable kdump:

Run the following:

sudo systemctl enable kdump
sudo systemctl start kdump
Check Reserved Memory:

Verify memory for the crash kernel:

cat /proc/cmdline
Configure kdump:
Modify /etc/kdump.conf to set the dump location (e.g., /var/crash).
Simulate a Crash (if asked):

Force a crash using the sysrq trigger:

echo c | sudo tee /proc/sysrq-trigger
Explain Post-Crash Steps:

After the crash, analyze the dump using:

sudo crash /usr/lib/debug/vmlinux-<kernel_version> /var/crash/vmcore
Highlight Benefits:
Show how this prevents future crashes by identifying issues like driver bugs or memory leaks.

The output of cat /proc/cmdline shows the kernel boot parameters that were passed during system startup, such as root filesystem, crashkernel reservation, and debugging options. These parameters are useful when analyzing crash dumps because they tell you how the kernel was configured at boot time. To analyze a crash dump, we use the crash utility along with the uncompressed kernel image (vmlinux) that matches the running kernel version and the vmcore file generated after a system crash. The command typically looks like sudo crash /usr/lib/debug/vmlinux-<kernel_version> /var/crash/vmcore, and yes, you must provide the correct matching vmlinux and vmcore files for proper analysis.

Once inside the crash shell, we focus on examining system state at the time of the crash. Common checks include bt (backtrace) to see the call stack of crashed processes, ps to view running processes at crash time, vm for memory usage, log to inspect kernel logs, and files or mount for filesystem-related issues. These help identify root causes such as kernel panic, out-of-memory (OOM), or driver failures.

For deeper debugging, gdb can also be used with the vmcore and vmlinux, but the crash tool is essentially a specialized wrapper around gdb tailored for kernel crash analysis, making it easier to interpret kernel data structures.

Finally, a core dump and a crash dump are related but different: a core dump is generated when a user-space application crashes and is used to debug that application, while a crash dump (vmcore) is generated after a kernel crash and is used to analyze the entire system state at the time of failure.


ps -eo pid,comm,user,args,%cpu,%mem --sort=-%mem | head
ps -eo ... → custom format output.
pid → Process ID.
comm → Command name (short executable name).
user → User who owns the process.
args → Full command with arguments.
%cpu → CPU usage percentage.
%mem → Memory usage percentage.
--sort=-%mem → Sort processes by memory usage in descending order (highest first).
| head → Show only the top 10 results.

📌 Example Output:

  PID COMMAND  USER   %CPU %MEM COMMAND
 2345 java     tomcat 20.5 45.0 /usr/bin/java -jar myapp.jar
 1876 postgres pgsql   5.0 12.3 /usr/lib/postgresql/12/bin/postgres -D /var/lib/postgresql
 1423 nginx    root    1.2  3.0 nginx: worker process
  987 python3  ubuntu  3.1  2.5 python3 app.py

  🔹 What is nice?
nice is a user-level command in Unix/Linux used to start a process with a specific niceness (priority hint).
It maps to the kernel scheduler, which uses this niceness value when deciding CPU time allocation.
🔹 Niceness range
Linux: -20 (highest priority) → 19 (lowest priority).
BSD/others: -20 → 20.
Default: 0, inherited from the parent process.
🔹 Meaning
A lower niceness (negative value) → process gets more CPU time (higher priority).
A higher niceness (positive value) → process runs only when CPU is otherwise idle.
🔹 Example usage
nice -n 10 myscript.sh     # run with lower priority
renice -n -5 -p 1234        # increase priority of PID 1234
🔹 Interview one-liner

👉 “nice and renice are used to adjust process scheduling priority. The niceness value ranges from -20 (highest priority) to 19/20 (lowest). Lower niceness means the process will get more CPU share compared to others.”


CPU State Percentages
us (user) → Time CPU spends running user processes (apps, commands).
sy (system) → Time CPU spends on kernel tasks (OS operations, drivers).
ni (nice) → Time CPU spends on processes with adjusted “nice” priority.
id (idle) → Time CPU is not doing anything (free CPU).
wa (IO-wait) → Time CPU is idle because it’s waiting for I/O (disk, network).
hi (hardware interrupts) → Time handling hardware interrupts (e.g., NIC, disk controller).
si (software interrupts) → Time handling software interrupts (e.g., kernel-level services).
st (steal) → Time “stolen” by hypervisor in a virtualized environment (means host is busy with other VMs).


Interview-Ready Answer: How I Troubleshoot Performance Issues in Linux

1. Start Broad – Identify the Symptom
"First, I clarify what ‘performance issue’ means. Is the system completely slow, is CPU spiking, memory exhausted, disk I/O bottlenecked, or is it network latency? I also confirm if the issue is isolated to a single user or affecting multiple users."

2. Check System Load

uptime → to see load averages and how long the system has been up.
top / htop → for a real-time overview of CPU, memory, and processes.

3. Break It Down by Resource

CPU: top, mpstat, pidstat → check if one process is consuming abnormal CPU.
Memory: free -m, vmstat, cat /proc/meminfo → look for swap usage, cache vs free memory.
Disk I/O: iostat -x, iotop, sar -d → check read/write latency and wait time.
Network: ifconfig / ip addr, ss -tulwn, sar -n DEV, ping → check bandwidth, dropped packets, connectivity.

4. Narrow Down to the Culprit Process

ps -aux --sort=-%cpu or ps -aux --sort=-%mem → identify top consumers.
Once identified → check logs of that service (journalctl -u <service> or /var/log/<app>.log).

5. Investigate Deeper if Needed

Kernel logs: dmesg → check for OOM killer events, hardware/driver issues, disk I/O errors.
Application-level checks: look at query logs, thread dumps, or error logs.
Advanced tools: strace (syscalls), perf (profiling), systemd-analyze (boot issues).

6. Conclude with Corrective Action
Depending on findings, I might:

Kill/restart a runaway process.
Tune configurations (e.g., DB queries, JVM heap).
Add resources (CPU/RAM/disk).
Fix network/firewall/DNS issues.
If it’s a recurring issue, set up monitoring and alerting to proactively catch it.
🔑 Interview Tip – One-Liner Summary

"I follow a layered approach: start with system load, then drill into CPU, memory, disk I/O, and network. I use tools like top, vmstat, iostat, and journalctl to identify the bottleneck, then check application or kernel logs. Finally, I take corrective action, whether that’s restarting a process, tuning configs, or adding resources."



Basic Linux Questions
1. What is Linux?
Solution: Linux is an open-source operating system kernel that acts as a bridge between the hardware and applications. It provides multitasking, multiuser capabilities, and security features. Popular distributions include Ubuntu, CentOS, and Fedora.
2. What are inodes?
Solution: An inode is a data structure used to store information about a file or directory, such as its size, permissions, owner, group, timestamps, and pointers to data blocks. The ls -i command displays the inode number.
3. How to check disk usage?
Solution: Use the df command to display disk usage and du for directory size.
Example: df -h (human-readable disk usage).
Example: du -sh /var/log (size of /var/log).
4. What are symbolic and hard links?
Solution:
Symbolic Link: A shortcut pointing to another file or directory. Deleting the original file breaks the link.
Example: ln -s /path/to/file symlink_name
Hard Link: A direct reference to the data block of a file. Deleting the original file doesn't affect the link.
Example: ln /path/to/file hardlink_name
5. How to find a process and kill it?
Solution:
Use ps or top to list processes.
Example: ps aux | grep process_name
Kill a process using kill or killall.
Example: kill -9 PID or killall process_name
Intermediate Linux Questions
6. Explain the difference between cron and at.
Solution:
cron: Schedules recurring tasks. Edit using crontab -e.
Example: 0 3 * * * /path/to/script.sh (Run daily at 3:00 AM).
at: Schedules one-time tasks.
Example: at 5:00 PM → Write the command, press Ctrl+D.
7. How do you monitor logs in real-time?
Solution: Use tail with the -f option.
Example: tail -f /var/log/syslog
For multiple files: tail -f /var/log/{file1,file2}
8. How to check open ports on a server?
Solution:
Use netstat or ss:
Example: netstat -tuln or ss -tuln
Use nmap:
Example: nmap localhost
9. What is the difference between apt and yum?
Solution:
apt: Used in Debian-based systems like Ubuntu for package management.
yum: Used in Red Hat-based systems like CentOS.
Both install, update, and remove packages but work with different package types (.deb for apt, .rpm for yum).
10. How to secure a Linux server?
Solution:
Disable root login: Edit /etc/ssh/sshd_config and set PermitRootLogin no.
Use firewalls: Configure iptables or ufw.
Update packages: apt-get update && apt-get upgrade or yum update.
Restrict file permissions: Use chmod and chown.
Monitor logs: /var/log/auth.log, /var/log/messages.
Advanced Linux Questions
11. Explain LVM (Logical Volume Manager).
Solution: LVM allows flexible disk management by abstracting physical storage into logical volumes.
Commands:
Create physical volume: pvcreate /dev/sdb
Create volume group: vgcreate vg_name /dev/sdb
Create logical volume: lvcreate -L 10G -n lv_name vg_name
Format and mount: mkfs.ext4 /dev/vg_name/lv_name and mount /dev/vg_name/lv_name /mnt
12. How to troubleshoot high CPU usage?
Solution:
Use top or htop to identify resource-intensive processes.
Use ps:
Example: ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head
Analyze logs for anomalies: /var/log/syslog, /var/log/messages.
13. What is SELinux, and how does it work?
Solution: Security-Enhanced Linux is a security module that enforces mandatory access control (MAC) policies.
Commands:
Check status: sestatus
Change mode: setenforce 0 (permissive) or setenforce 1 (enforcing).
Modify policy: Use semanage or /etc/selinux/config.
14. How does a kernel panic occur, and how do you troubleshoot it?
Solution: A kernel panic happens when the Linux kernel detects a fatal error it can't recover from.
Check logs in /var/log/kern.log or /var/log/messages.
Verify hardware components like RAM and disks.
Boot in recovery mode and check boot loader configurations.
15. Explain the difference between fork() and exec().
Solution:
fork(): Creates a new child process that is a copy of the parent process.
exec(): Replaces the current process image with a new one.

Example:

pid = fork();
if (pid == 0) {
  execvp("./program", args);
}
16. How to troubleshoot disk I/O issues?
Solution:
Use iostat to monitor disk I/O.
Use iotop to identify processes causing high I/O.
Check disk health with smartctl or fsck.
17. What are cgroups in Linux?
Solution: Cgroups (Control Groups) manage and limit resources like CPU, memory, and I/O for processes.
Create a cgroup: mkdir /sys/fs/cgroup/cpu/test_cgroup
Assign tasks: echo PID > /sys/fs/cgroup/cpu/test_cgroup/tasks
Limit resources: echo 50000 > /sys/fs/cgroup/cpu/test_cgroup/cpu.shares
18. How does RAID work?
Solution:
RAID (Redundant Array of Independent Disks) provides redundancy, performance, or both.
Types:
RAID 0: Striping, no redundancy.
RAID 1: Mirroring.
RAID 5: Striping with parity.
RAID 10: Combination of 1 and 0.
Configure using mdadm.
19. What are namespaces in Linux?
Solution: Namespaces isolate resources for processes. Examples include:
Mount (mnt): Isolate file systems.
Network (net): Isolate network interfaces.
Use unshare to create namespaces.
20. How to troubleshoot boot issues?
Solution:
Check GRUB configurations: /boot/grub/grub.cfg.
Boot into recovery mode.
Rebuild initramfs: dracut --force or mkinitcpio.
Check /var/log/boot.log.
