# `/etc/nsswitch.conf`

## Definition

`/etc/nsswitch.conf` (**Name Service Switch**) controls the **order Linux uses to search for system information** like users, groups, and hostnames.

---

## Example

```bash
cat /etc/nsswitch.conf
```

Output:

```text
passwd:     files
group:      files
hosts:      files dns
```

---

## Meaning

### Hostname Lookup

```text
hosts: files dns
```

Order:

```
1. /etc/hosts
2. DNS server (/etc/resolv.conf)
```

---

### User Lookup

```text
passwd: files
```

Linux checks:

```
/etc/passwd
```

for local users.

---

## Interview Point

> `/etc/nsswitch.conf` defines the lookup order for services like users, groups, and hostnames. For hostname resolution, `hosts: files dns` means Linux checks `/etc/hosts` first and then DNS.
