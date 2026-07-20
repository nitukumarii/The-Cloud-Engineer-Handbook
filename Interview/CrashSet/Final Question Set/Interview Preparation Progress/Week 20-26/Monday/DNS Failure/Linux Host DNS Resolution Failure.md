### DNS resolution is failing — how do you troubleshoot it?


# Linux Host DNS Resolution Failure – Complete Interview Guide

> **Goal:** Learn how to troubleshoot DNS resolution failures on a Linux server in a structured, production-ready manner. This guide explains **why** each step is performed, **what** you're trying to prove, **where to stop**, and **how to answer in an interview**.

---

# Understanding DNS Resolution

Before troubleshooting, understand what happens when an application tries to connect to:

```
database.company.com
```

Instead of an IP like:

```
10.20.30.15
```

Linux follows this sequence:

```
Application
      │
      ▼
Name Service Switch (nsswitch.conf)
      │
      ├── Check /etc/hosts
      │
      └── Check DNS Server
               │
               ▼
        /etc/resolv.conf
               │
               ▼
        Configured DNS Server
               │
               ▼
Returns IP Address
               │
               ▼
Application connects
```

If any step fails, DNS resolution fails.

---

# Interview Troubleshooting Flow

Always troubleshoot in this order:

```
1. Determine scope
        ↓
2. Verify network is healthy
        ↓
3. Confirm it is actually a DNS problem
        ↓
4. Check local DNS configuration
        ↓
5. Check DNS server
        ↓
6. Check network path to DNS server
        ↓
7. Check resolver service (if applicable)
        ↓
8. Review logs
        ↓
9. Confirm root cause
        ↓
10. Fix and prevent recurrence
```

Never jump directly to changing configuration files.

---

# Step 1 — Determine the Scope

## Why?

Before touching the server, understand **how big the problem is**.

Ask yourself:

* Is only one server affected?
* Are multiple servers affected?
* Is every hostname failing?
* Is only one hostname failing?
* Did this begin after a deployment?

This helps determine whether the issue is:

* Local to one machine
* A shared infrastructure problem
* A DNS server outage
* An application issue

---

## How?

Use monitoring tools:

* Prometheus
* Grafana
* Splunk
* Dynatrace
* CloudWatch

Review:

* Alerts
* Error spikes
* Failed connections
* Recent deployments

At this stage, **do not run Linux commands yet**. You're understanding the impact.

---

# Step 2 — Verify Basic Network Connectivity

## Why?

Many people assume every connection failure is DNS.

It isn't.

If the machine has no network connectivity, DNS cannot work either.

So first prove:

> **Can this server communicate over the network?**

---

## Command

```bash
ping 8.8.8.8
```

---

## Possible Results

### Works

```
64 bytes from 8.8.8.8
```

Network is working.

Continue.

---

### Fails

```
Destination Host Unreachable
```

Stop DNS troubleshooting.

This is now a networking problem.

Investigate:

* NIC
* Routing
* Firewall
* Gateway
* VPC
* Security Groups

---

# Step 3 — Confirm It Is Really DNS

Now verify:

Can I reach hosts by **name**?

```bash
ping google.com
```

---

## If it works

DNS is functioning.

Problem lies elsewhere.

Stop DNS investigation.

---

## If it fails

Example:

```
Temporary failure in name resolution
```

Now you have confirmed:

> Network works, but DNS resolution fails.

Continue.

---

# Step 4 — Check /etc/resolv.conf

This is the first configuration file Linux uses to locate DNS servers.

View it:

```bash
cat /etc/resolv.conf
```

Example:

```
nameserver 10.10.1.5
search company.local
```

---

## What are you checking?

### 1. nameserver

This tells Linux **which DNS server to ask**.

Example:

```
nameserver 10.10.1.5
```

If missing:

Linux has nobody to query.

---

### 2. Wrong IP

Example:

```
nameserver 192.168.100.100
```

If this DNS server doesn't exist,

DNS fails.

---

### 3. Search Domain

Example:

```
search company.local
```

Allows:

```
database
```

to become

```
database.company.local
```

Incorrect search domains can cause resolution issues.

---

## When do you stop here?

If you find:

* Missing nameserver
* Incorrect DNS IP
* Corrupted configuration

you've likely found the root cause.

Correct it and verify.

Otherwise continue.

---

# Step 5 — Check /etc/hosts

Linux always checks this file **before DNS**.

View it:

```bash
cat /etc/hosts
```

Example:

```
127.0.0.1 localhost
10.10.1.20 database.company.com
```

---

## Why?

Sometimes someone manually adds an entry.

If it's incorrect,

Linux never contacts the DNS server.

It immediately uses the wrong IP.

---

## Interview Tip

Many production incidents are caused by stale `/etc/hosts` entries after migrations.

Always check this file.

---

# Step 6 — Test the DNS Server

Now verify:

Is the DNS server answering?

Use:

```bash
nslookup google.com
```

or

```bash
dig google.com
```

---

## Why both?

### nslookup

Simple.

Shows whether DNS works.

---

### dig

Preferred by Linux administrators.

Provides:

* response time
* DNS server used
* answer section
* authority section
* additional records

---

## Example

```
Server: 10.10.1.5

Address: 10.10.1.5

Name: google.com

Address: 142.x.x.x
```

DNS server responded correctly.

---

## If timeout occurs

Example:

```
connection timed out
```

Continue to next step.

---

# Step 7 — Can We Reach the DNS Server?

Even if DNS is configured,

the server itself may be unreachable.

First:

```bash
ping 10.10.1.5
```

If reachable,

test DNS port.

```bash
nc -zv 10.10.1.5 53
```

or

```bash
telnet 10.10.1.5 53
```

---

## Why Port 53?

DNS communicates over:

* UDP 53
* TCP 53

If blocked,

DNS cannot function.

---

## Possible causes

* Firewall
* Security Group
* ACL
* Network outage

---

# Step 8 — Check Resolver Service (Modern Linux)

Many Linux distributions use:

```
systemd-resolved
```

Verify:

```bash
systemctl status systemd-resolved
```

Then:

```bash
resolvectl status
```

---

## Why?

Even if the DNS server is healthy,

the local resolver service may have crashed.

Restarting it often restores resolution.

---

# Step 9 — Review Logs

If everything appears correct,

look for evidence.

Common locations:

```bash
journalctl
```

```
/var/log/syslog
```

```
/var/log/messages
```

Look for:

* timeout
* resolver failures
* unreachable nameserver
* network errors

Logs often provide the final clue.

---

# Step 10 — Confirm Root Cause

Never assume.

Verify:

* Hostname now resolves
* Application connects successfully
* Monitoring alerts disappear
* Logs show no further DNS failures

Only then consider the issue resolved.

---

# Common Root Causes

| Root Cause                | Typical Fix                |
| ------------------------- | -------------------------- |
| Missing nameserver        | Correct `/etc/resolv.conf` |
| Wrong DNS server          | Update configuration       |
| Bad `/etc/hosts` entry    | Remove incorrect mapping   |
| Firewall blocking port 53 | Allow DNS traffic          |
| DNS server down           | Restore DNS service        |
| Resolver service stopped  | Restart `systemd-resolved` |
| Network outage            | Fix networking             |

---

# Where Should You Stop?

The investigation stops **as soon as you identify a root cause that explains the symptoms and you can verify the fix**.

Example:

* `/etc/resolv.conf` has no `nameserver` entry.
* You add the correct DNS server.
* `nslookup google.com` succeeds.
* The application reconnects.

At this point, there's no need to continue checking `systemd-resolved` or logs unless the issue persists. In production, avoid unnecessary investigation once you've confirmed the root cause.

---

# 60-Second Interview Answer

> **First, I'd determine the scope of the issue using monitoring tools like Grafana, Prometheus, Splunk, or CloudWatch to understand whether the problem is isolated to one server or affecting multiple systems. Next, I'd verify basic network connectivity by checking whether the server can reach an IP address. If network connectivity is healthy but hostname resolution fails, I'd confirm it's a DNS issue. Then I'd inspect `/etc/resolv.conf` to verify the configured nameservers and search domains, followed by `/etc/hosts` to ensure there are no incorrect local hostname mappings. If the configuration looks correct, I'd test DNS resolution using `nslookup` or `dig`, verify connectivity to the DNS server on port 53, and check the local resolver service such as `systemd-resolved` if applicable. Finally, I'd review system logs to identify resolver errors, confirm the root cause by successfully resolving hostnames again, restore the application, and document the RCA with preventive monitoring if needed.**
