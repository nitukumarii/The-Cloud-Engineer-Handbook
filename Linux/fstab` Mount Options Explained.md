# `/etc/fstab` Mount Options Explained

Example:

```text
/dev/xvdb1   /data   xfs   defaults,nofail   0   2
```

Format:

```text
device   mount_point   filesystem   options   dump   fsck
```

---

# 1. `defaults` Option

`defaults` applies standard mount options:

```
rw,suid,dev,exec,auto,nouser,async
```

Meaning:

| Option | Meaning |
|---|---|
| `rw` | Mount as read-write |
| `suid` | Allow SUID/SGID permissions |
| `dev` | Allow device files |
| `exec` | Allow execution of binaries |
| `auto` | Mount automatically during boot |
| `nouser` | Only root can mount |
| `async` | Write data asynchronously |

Example:

```text
/dev/xvdb1 /data xfs defaults 0 2
```

is equivalent to:

```text
/dev/xvdb1 /data xfs rw,suid,dev,exec,auto,nouser,async 0 2
```

---

# Common Mount Options

## `nofail`

Allows the system to continue booting if the disk is missing.

Without `nofail`:

```
Boot
 |
 v
Read /etc/fstab
 |
 v
Disk missing
 |
 v
Boot failure/emergency mode
```

With:

```text
defaults,nofail
```

```
Disk missing
 |
 v
Ignore error
 |
 v
Continue boot
```

**Production use:**

Used for optional disks like AWS EBS data volumes.

---

## `noexec`

Prevents execution of binaries from a filesystem.

Example:

```text
/data xfs defaults,noexec
```

Security use:

```
User uploads script
        |
        v
Tries to execute
        |
        v
Blocked
```

---

## `rw` and `ro`

### Read-Write

```text
rw
```

Allows:

- Create files
- Modify files
- Delete files

---

### Read-Only

```text
ro
```

Allows only reading.

Used for:

- Backup disks
- Protecting important data

---

# Last Two Fields in `/etc/fstab`

Example:

```text
/dev/xvdb1 /data xfs defaults 0 2
```

The last two fields are:

```
dump   fsck
```

---

# 5th Field: Dump

Controls old backup utility behavior.

## `0`

Do not include in dump backup.

Most common:

```text
0
```

## `1`

Include in dump backup.

Rarely used today.

---

# 6th Field: fsck

Controls filesystem check order during boot.

## `0`

No filesystem check.

Example:

```text
/dev/xvdb1 /data xfs defaults 0 0
```

---

## `1`

Check first.

Usually used for root filesystem:

```text
/dev/xvda1 / ext4 defaults 0 1
```

Boot order:

```
Check root filesystem first
```

---

## `2`

Check after root filesystem.

Example:

```text
/dev/xvdb1 /data ext4 defaults 0 2
```

Used for additional disks.

---

# Production Example (AWS EC2)

```text
/dev/xvda1   /       ext4   defaults          0 1
/dev/xvdb1   /data   xfs    defaults,nofail   0 2
```

Meaning:

```
Root disk
 |
 |-- Check first during boot


Data disk
 |
 |-- Mount automatically
 |-- Do not fail boot if missing
 |-- Check after root filesystem
```

---

# Interview Answer

> In `/etc/fstab`, mount options define filesystem behavior. `defaults` enables standard options like read-write and auto-mount. Options like `nofail` prevent boot issues when optional disks are unavailable, while `noexec` improves security. The last two fields control dump backup and filesystem check order (`1` for root, `2` for other filesystems, `0` to skip).
