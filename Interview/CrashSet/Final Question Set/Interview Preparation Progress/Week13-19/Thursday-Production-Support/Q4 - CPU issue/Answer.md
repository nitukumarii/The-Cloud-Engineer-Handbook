# How do you troubleshoot high CPU?

When I observe high CPU utilization, I follow a structured approach to identify the root cause, restore performance, and minimize application impact.

---

## 1. Check Monitoring Metrics

First, I check monitoring tools like **Prometheus, Grafana, CloudWatch, or Splunk** to confirm the CPU spike and understand the impact.

### Metrics I check:

- **CPU Utilization**  
  **Why:** To identify which server, node, or pod is consuming high CPU and confirm the severity of the issue.

- **Request Rate**  
  **Why:** To check whether increased traffic or a sudden spike in requests is causing higher CPU consumption.

- **Response Time / Latency**  
  **Why:** To understand whether high CPU is affecting application performance and user experience.

- **Error Rate**  
  **Why:** To check whether CPU saturation is causing failed requests, timeouts, or 5xx errors.

---

## 2. Identify the Process Consuming CPU

After confirming the affected system, I identify which process is consuming CPU.

### Commands:

    top

**Why:**
- Real-time view of CPU usage
- Identify high CPU-consuming processes


    ps aux --sort=-%cpu | head

**Why:**
- Lists processes based on CPU consumption
- Identifies the Process ID (PID)

---

## 3. Analyze the High CPU Process

Once I identify the process, I investigate further.

### Command:

    top -H -p <PID>

**Why:**
- Identifies CPU-consuming threads inside the process
- Useful for Java or multi-threaded applications

---

## 4. Check Application Logs

I review application logs to identify application-level problems.

### Command:

    journalctl -u <service-name>

**Why:**

To identify:
- Infinite loops
- Failed jobs
- Exceptions
- Application errors
- Recent changes

---

## 5. Check System Resource Health

I verify whether other system resources are contributing to CPU pressure.

### Load Average

    uptime

**Why:**
- Understand overall system pressure
- Check if processes are waiting for CPU


### System Performance

    vmstat

**Why:**
- Check CPU usage
- Memory pressure
- Process activity


### Disk I/O

    iostat

**Why:**
- Identify storage bottlenecks affecting application performance


### Memory Usage

    free -m

**Why:**
- Check memory pressure
- Identify swapping issues

---

## 6. Check Application and Recent Changes

I investigate possible application-level causes.

### Things I check:

- **Recent deployments**  
  **Why:** A new release may introduce performance issues.

- **Traffic increase**  
  **Why:** Higher workload can increase CPU consumption.

- **Long-running jobs**  
  **Why:** Background processes can consume excessive CPU.

- **Database query performance**  
  **Why:** Slow queries can increase application processing time.

---

## 7. Mitigate the Issue

Based on the root cause, I restore service.

### Possible actions:

- **Scale application instances**  
  **Why:** To distribute workload across more resources.

- **Restart unhealthy services**  
  **Why:** To recover stuck or failed processes.

- **Roll back deployment**  
  **Why:** If a recent change caused CPU spikes.

- **Optimize application/database queries**  
  **Why:** To reduce unnecessary CPU consumption.

- **Increase CPU resources**  
  **Why:** If the workload requires more capacity.

---

## 8. Monitor Recovery and Prevent Recurrence

After resolving the issue, I monitor:

- CPU utilization
- Application latency
- Error rates
- Request volume

Then I perform:

- Root Cause Analysis (RCA)
- Update runbooks
- Improve monitoring and alerting
- Implement preventive actions

---

# Quick Memory Flow

    High CPU
        ↓
    Monitoring Metrics
        ↓
    Find Process (top / ps)
        ↓
    Analyze Thread (top -H)
        ↓
    Check Logs
        ↓
    Check System Resources
        ↓
    Check Application Changes
        ↓
    Fix & Monitor
        ↓
    RCA


# Interview Short Answer

"When troubleshooting high CPU, I first check monitoring dashboards to confirm CPU utilization and correlate it with request rate, latency, and error rate. Then I identify the process consuming CPU using commands like top and ps aux, analyze logs, and check system resources like load average, memory, and disk I/O. Based on the root cause, I scale the application, restart services, optimize the application, or roll back changes. After recovery, I perform RCA and implement preventive measures."
