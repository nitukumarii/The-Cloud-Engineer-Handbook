# Disk is full — How do you troubleshoot it?

When I observe disk space exhaustion, I follow a structured approach to identify what is consuming the disk, restore service availability, and prevent recurrence.

---

## 1. Check Monitoring Metrics

First, I check monitoring tools like **Prometheus, Grafana, CloudWatch, or Splunk** to confirm the disk issue and understand the impact.

### Metrics I check:

- **Disk Utilization (%)**

  **Why:** To identify which server, node, or volume is running out of space.

- **Disk I/O Utilization**

  **Why:** To check whether high read/write activity is causing application performance issues.

- **Application Latency**

  **Why:** A full disk can slow down applications due to inability to write logs, temporary files, or data.

- **Error Rate**

  **Why:** To identify failures caused by disk exhaustion, such as application crashes, failed writes, or database errors.

---

## 2. Confirm Disk Usage on the Server

I check filesystem usage.

### Command:

```bash
df -h
```

**Why:**
- Shows filesystem-level disk utilization
- Identifies which partition is full

Example:

```
Filesystem      Size  Used  Avail  Use%
/dev/xvda1      100G  100G    0G   100%
```

---

## 3. Identify What Is Consuming Disk Space

After identifying the affected filesystem, I find large directories or files.

### Check directory usage:

```bash
du -sh /*
```

**Why:**
- Identifies which top-level directory is consuming space

---

### Check specific directory:

```bash
du -sh /var/*
```

**Why:**
- Helps locate large folders such as logs, cache, or application data

---

### Find large files:

```bash
find / -type f -size +1G
```

**Why:**
- Identifies very large files consuming disk space

---

## 4. Check Common Causes

I investigate common reasons for disk exhaustion.

### Log Files

Check:

```bash
/var/log
```

**Why:**
- Excessive application or system logs can fill the disk

Commands:

```bash
du -sh /var/log/*
```

---

### Deleted Files Still Used by Processes

Command:

```bash
lsof | grep deleted
```

**Why:**
- A deleted file may still consume disk space if a process keeps it open

---

### Temporary Files

Check:

```bash
/tmp
/var/tmp
```

**Why:**
- Temporary files can accumulate and consume storage

---

### Application Data

Check:

- Database files
- Cache files
- Backup files
- Uploaded files

**Why:**
- Application-generated data can grow unexpectedly

---

## 5. Check Kubernetes Disk Usage (If Applicable)

For Kubernetes environments:

### Check node disk pressure:

```bash
kubectl describe node <node-name>
```

**Why:**
- Identifies DiskPressure conditions on nodes

---

### Check pod logs:

```bash
kubectl logs <pod-name>
```

**Why:**
- Large container logs can consume node storage

---

### Check container storage:

```bash
docker system df
```

**Why:**
- Identifies unused images, containers, and volumes consuming space

---

## 6. Immediate Mitigation

Based on the cause, I take corrective actions.

Possible actions:

- Remove old log files

  **Why:** To immediately free disk space.

- Rotate and compress logs

  **Why:** To prevent future log growth.

- Remove unused Docker images/containers

  **Why:** To reclaim container storage.

- Clean temporary files

  **Why:** To remove unnecessary data.

- Increase disk volume size

  **Why:** If the application requires additional capacity.

- Restart services if required

  **Why:** To release deleted files still held by processes.

---

## 7. Prevent Recurrence

After resolving the issue, I implement preventive measures.

I:

- Configure log rotation
- Set disk usage alerts
- Review application log levels
- Implement retention policies
- Monitor disk growth trends
- Perform RCA and update runbooks

---

# Quick Memory Flow

```
Disk Full
    ↓
Check Metrics
    ↓
df -h (Which filesystem?)
    ↓
du -sh (Which directory?)
    ↓
Find Large Files
    ↓
Check Logs / Temp / App Data
    ↓
Free Space
    ↓
Prevent Recurrence
    ↓
RCA
```

---

# Interview Short Answer

"When troubleshooting a full disk issue, I first check monitoring dashboards to confirm disk utilization and identify the affected server or volume. Then I use `df -h` to identify the full filesystem and `du -sh` or `find` commands to locate large directories or files. I check common causes like application logs, temporary files, deleted files still held by processes, and container storage. After identifying the cause, I clean unnecessary data, rotate logs, remove unused files, or increase storage capacity if required. Finally, I configure alerts, retention policies, and perform RCA to prevent recurrence."
