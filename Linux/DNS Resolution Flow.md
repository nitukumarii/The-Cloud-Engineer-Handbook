# How Linux Resolves a Hostname (DNS Resolution Flow)

## Overview

When an application needs to communicate with another service, it usually uses a **hostname** instead of an IP address.

Example:

```text
database.company.com
```

The application needs to convert this hostname into an IP address:

```text
database.company.com → 10.20.30.15
```

This process is called **hostname resolution** or **DNS resolution**.

Linux follows a defined lookup process to resolve the hostname.

---

# Linux Hostname Resolution Flow

```text
Application
      │
      ▼
Resolver Library
      │
      ▼
/etc/nsswitch.conf
      │
      │
      │  Defines lookup order
      │
      ├───────────────
      │               │
      ▼               ▼
/etc/hosts          DNS Lookup
(Local Mapping)        │
                       ▼
              /etc/resolv.conf
                       │
                       ▼
              Configured DNS Server
                       │
                       ▼
              DNS Response (IP Address)
                       │
                       ▼
             Application Connects
```

---

# Step 1 — Application Requests Hostname

An application usually does not directly use an IP address.

Example:

```text
Application wants to connect to:

database.company.com
```

The application asks the operating system:

> "What is the IP address of this hostname?"

---

# Step 2 — Resolver Library Handles the Request

The application uses the Linux resolver library.

The resolver library is responsible for:

* Checking local hostname mappings
* Querying DNS servers
* Returning the final IP address to the application

The application does not directly read `/etc/hosts` or `/etc/resolv.conf`.

The operating system handles this process.

---

# Step 3 — Check /etc/nsswitch.conf

Linux checks:

```bash
cat /etc/nsswitch.conf
```

Example:

```text
hosts: files dns
```

This line defines the hostname lookup order.

Meaning:

1. Check local files
2. If not found, check DNS

---

## What does "files" mean?

`files` refers to:

```bash
/etc/hosts
```

---

## What does "dns" mean?

`dns` means:

Use the DNS servers configured in:

```bash
/etc/resolv.conf
```

---

# Step 4 — Check /etc/hosts

Linux first checks:

```bash
cat /etc/hosts
```

Example:

```text
127.0.0.1 localhost
10.20.30.15 database.company.com
```

This is a local hostname-to-IP mapping.

Linux asks:

> "Do I already know this hostname locally?"

If the entry exists:

```text
database.company.com → 10.20.30.15
```

Linux uses this IP immediately.

DNS is not contacted.

---

# Why Can /etc/hosts Cause Problems?

Because `/etc/hosts` has higher priority than DNS.

Example:

DNS has:

```text
database.company.com → 10.20.30.15
```

But `/etc/hosts` contains:

```text
database.company.com → 192.168.1.50
```

Linux will use:

```text
192.168.1.50
```

because it checks `/etc/hosts` first.

The application may connect to:

* Wrong server
* Old server
* Unavailable server

---

# Step 5 — Check DNS Configuration (/etc/resolv.conf)

If the hostname is not found in `/etc/hosts`, Linux checks DNS.

It reads:

```bash
cat /etc/resolv.conf
```

Example:

```text
nameserver 10.10.1.5
search company.local
```

---

## What is nameserver?

Example:

```text
nameserver 10.10.1.5
```

This tells Linux:

> "Send DNS queries to this DNS server."

---

## What is search domain?

Example:

```text
search company.local
```

Allows short names.

Example:

User enters:

```text
database
```

Linux can try:

```text
database.company.local
```

---

# Step 6 — Query DNS Server

Linux sends a DNS query:

```text
Question:

What is the IP address of database.company.com?
```

DNS server responds:

```text
Answer:

database.company.com → 10.20.30.15
```

Common DNS query tools:

```bash
nslookup database.company.com
```

or

```bash
dig database.company.com
```

---

# Step 7 — Application Connects

After receiving the IP address:

```text
database.company.com
        |
        ↓
10.20.30.15
```

The application uses the IP address to establish the connection.

Example:

```text
Application
     |
     |
     ↓
Database Server
10.20.30.15
```

---

# Complete Resolution Example

Application requests:

```text
api.company.com
```

---

## Check nsswitch.conf

```text
hosts: files dns
```

Order:

1. /etc/hosts
2. DNS

---

## Check /etc/hosts

No entry found.

Continue.

---

## Check /etc/resolv.conf

DNS server:

```text
10.10.1.5
```

---

## Query DNS

DNS returns:

```text
api.company.com → 10.20.30.25
```

---

## Application connects

Connection:

```text
Application → 10.20.30.25
```

---

# Interview Answer

## Question:

**How does Linux resolve a hostname?**

## Answer:

> "When an application needs to connect to a hostname, it uses the Linux resolver library. The resolver checks the lookup order defined in `/etc/nsswitch.conf`. Typically, it first checks `/etc/hosts` for local hostname mappings. If the hostname is not found, it uses the DNS servers configured in `/etc/resolv.conf` to query the DNS server. Once the DNS server returns the IP address, the application uses that IP address to establish the connection."

---

# Memory Flow

Remember:

```text
Application
      ↓
nsswitch.conf
      ↓
/etc/hosts
      ↓
/etc/resolv.conf
      ↓
DNS Server
      ↓
IP Address
      ↓
Application Connects
```

Simple rule:

**hosts file = local shortcut**

**DNS = external directory**

Linux checks the shortcut first, then asks DNS.
