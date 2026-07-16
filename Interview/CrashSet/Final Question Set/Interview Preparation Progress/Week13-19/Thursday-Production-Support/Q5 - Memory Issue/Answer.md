# How do you troubleshoot memory issues?

When I observe high memory utilization or memory-related issues, I follow a structured approach to identify the root cause, restore application stability, and prevent recurrence.

---

## 1. Check Monitoring Metrics

First, I check monitoring tools like **Prometheus, Grafana, CloudWatch, or Splunk** to confirm the memory issue and understand the impact.

### Metrics I check:

- **Memory Utilization**
  
  **Why:** To identify which server, node, or pod is consuming high memory and confirm the severity of the issue.

- **Memory Usage Trend**

  **Why:** To understand whether memory usage is continuously increasing, indicating a possible memory leak.

- **CPU Utilization**

  **Why:** High memory pressure can increase CPU usage due to garbage collection or swapping.

- **Application Response Time / Latency**

  **Why:** To check whether memory pressure is impacting application performance.

- **Error Rate**

  **Why:** To identify failures caused by memory exhaustion, such as timeouts or application crashes.

---

## 2. Identify the Process Consuming Memory

After confirming the affected system, I identify which process is consuming excessive memory.

### Commands:

    top

**Why:**
- Provides real-time memory and CPU usage
- Identifies high memory-consuming processes

---

    ps aux --sort=-%mem | head

**Why:**
- Lists processes based on memory consumption
- Identifies the Process ID (PID)

---

## 3. Analyze the Memory-Consuming Process

Once I identify the process, I investigate further.

### Command:

    top -p <PID>

**Why:**
- Monitors the specific process consuming memory
- Helps identify whether memory usage is continuously increasing

---

## 4. Check System Memory Health

I verify overall memory usage and system pressure.

### Memory Usage

    free -m

**Why:**
- Checks total, used, and available memory
- Identifies memory exhaustion

---

### Virtual Memory Statistics

    vmstat

**Why:**
- Checks memory pressure
- Identifies swapping activity
- Shows CPU and process impact

---

### Check Swap Usage

    swapon --show

**Why:**
- Identifies whether the system is using swap due to insufficient memory

---

## 5. Check Application-Level Memory Issues

I investigate whether the issue is caused by the application.

I check:

- Memory leaks
- Increasing heap usage
- Long-running processes
- Excessive object creation
- Garbage collection issues (Java applications)
- Incorrect memory configuration

For Java applications:

    jstat -gc <PID>

**Why:**
- Checks garbage collection activity
- Helps identify heap memory issues

---

## 6. Check Container / Kubernetes Memory Usage

For Kubernetes workloads, I check pod memory usage and limits.

Commands:

    kubectl top pods -n <namespace>

**Why:**
- Identifies pods consuming high memory

---

    kubectl describe pod <pod-name> -n <namespace>

**Why:**
- Checks memory requests, limits, and events

---

I also check for:

- OOMKilled containers
- Memory limit exceeded events
- Container restarts

---

## 7. Check Recent Changes

I investigate possible causes from recent changes.

Things I check:

- **Recent deployments**

  **Why:** A new release may introduce memory leaks or increased memory usage.

- **Configuration changes**

  **Why:** Incorrect memory limits or application settings can cause memory pressure.

- **Traffic increase**

  **Why:** Higher workload can increase memory consumption.

---

## 8. Mitigate the Issue

Based on the root cause, I take corrective actions.

Possible actions:

- **Restart unhealthy services**

  **Why:** To temporarily release memory and restore service.

- **Scale application instances**

  **Why:** To distribute workload across multiple instances.

- **Increase memory limits/resources**

  **Why:** If the application requires more memory capacity.

- **Fix memory leaks**

  **Why:** To prevent continuous memory growth.

- **Optimize application configuration**

  **Why:** To reduce unnecessary memory consumption.

---

## 9. Monitor Recovery and Prevent Recurrence

After resolving the issue, I monitor:

- Memory utilization
- Application latency
- Error rates
- Restart count
- Garbage collection metrics

Then I perform:

- Root Cause Analysis (RCA)
- Update runbooks
- Improve monitoring and alerting
- Implement preventive actions

---

# Quick Memory Flow

    High Memory
        ↓
    Check Metrics
        ↓
    Find Memory-Heavy Process (top / ps)
        ↓
    Analyze Application Memory
        ↓
    Check Swap / OOM
        ↓
    Check Kubernetes Limits
        ↓
    Check Recent Changes
        ↓
    Fix & Monitor
        ↓
    RCA


# Interview Short Answer

"When troubleshooting memory issues, I first check monitoring dashboards to confirm memory utilization and correlate it with application latency, error rates, and restart events. Then I identify the process consuming memory using commands like top and ps aux, check system memory using free and vmstat, and investigate application-level issues such as memory leaks or garbage collection problems. In Kubernetes, I check pod memory usage, limits, and OOMKilled events. Based on the root cause, I restart services, scale the application, adjust resources, or fix the memory issue. After recovery, I perform RCA and implement preventive measures."
