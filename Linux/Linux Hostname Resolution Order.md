# Linux Hostname Resolution Order

Linux checks hostname resolution based on:

```bash
/etc/nsswitch.conf
```

Example:

```text
hosts: files dns
```

Flow:

```
Hostname request
       |
       v
/etc/hosts
       |
       |-- Found → Use IP
       |
       |-- Not found
       v
DNS server (/etc/resolv.conf)
       |
       v
Return IP address
```

## Files

| File | Purpose |
|---|---|
| `/etc/hosts` | Local hostname-to-IP mapping |
| `/etc/resolv.conf` | DNS server addresses |
| `/etc/nsswitch.conf` | Controls lookup order |

**Interview Point:**

> Linux usually checks `/etc/hosts` first, then queries DNS servers configured in `/etc/resolv.conf`.
