# 60-Second Interview Answer – DNS Resolution Failure (Linux)

> "Whenever I encounter a DNS resolution issue, I first determine the scope by checking monitoring tools like **Prometheus, Grafana, Splunk, or CloudWatch** to understand whether the problem is isolated to a single server or affecting multiple servers or applications. Based on that, my initial hypothesis would be a network issue, incorrect DNS configuration, a stale `/etc/hosts` entry, a DNS server outage, or a firewall blocking DNS traffic.

> I then start the investigation by first verifying basic network connectivity using an IP address. If IP connectivity works but hostname resolution fails, I confirm it's a DNS issue. Next, I check **`/etc/resolv.conf`** to verify that the correct DNS server is configured, followed by **`/etc/hosts`** to ensure there isn't a local hostname mapping overriding DNS. I then use **`nslookup`** or **`dig`** to verify whether the configured DNS server can resolve the hostname and, if needed, check connectivity to the DNS server on **port 53**. If everything appears correct, I'd review the resolver service and system logs for additional errors.

> Once I identify the root cause, I'd apply the fix, verify that hostname resolution and the application are working again, and finally document the RCA and implement monitoring or alerts to prevent similar issues in the future."
