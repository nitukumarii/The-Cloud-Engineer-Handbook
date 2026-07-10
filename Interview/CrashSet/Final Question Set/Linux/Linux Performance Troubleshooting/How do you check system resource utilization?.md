
To check system resource utilization, I first use top to get a real-time overview of CPU usage, memory utilization, load average, and running processes. This helps me quickly identify whether the system is CPU-bound, memory-bound, or experiencing high disk I/O.

If CPU utilization is high, I identify the processes consuming the most CPU using ps aux --sort=-%cpu. If memory is the concern, I use free -m to check RAM and swap utilization and determine whether the system is under memory pressure or relying heavily on swap.

For disk-related issues, I use df -h to verify filesystem utilization and du -sh * to identify directories consuming the most disk space.

If I suspect a CPU or disk I/O bottleneck, I further investigate using tools such as vmstat, iostat, and iotop to identify the root cause. Based on my findings, I troubleshoot the issue and take the appropriate corrective action.
