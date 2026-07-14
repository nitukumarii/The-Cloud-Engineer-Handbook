# `/etc/hosts`

**Definition:**
`/etc/hosts` is a Linux file used for **local hostname-to-IP address mapping** without using DNS.

Example:

```
10.10.1.50   app.company.com
```

Meaning:

```
app.company.com → 10.10.1.50
```

## Use Cases

- Testing application changes before DNS update.
- Troubleshooting DNS resolution issues.
- Temporary mapping of internal servers.

## Interview Answer

> `/etc/hosts` provides local name resolution by mapping hostnames to IP addresses. It is useful for testing, troubleshooting, and temporary mappings before DNS changes are applied.
