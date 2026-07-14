# ulimit in Linux

## Definition

`ulimit` is a Linux command used to **view and set resource limits** for a user or process.

These limits help prevent a single user or application from consuming all system resources.

---

## Common Commands

```bash
ulimit -a
```
Shows all resource limits for the current user.

```bash
ulimit -u
```
Shows the maximum number of processes a user can create.

```bash
ulimit -n
```
Shows the maximum number of open files.

---

## How ulimit Works

1. Limits are configured in:

```
/etc/security/limits.conf
```

or:

```
/etc/security/limits.d/
```

Example:

```conf
nitu    soft    nproc    2048
nitu    hard    nproc    4096
```

2. When a user logs in, **PAM (Pluggable Authentication Module)** reads these configurations.

3. The limits are applied to the user's session.

4. The Linux kernel enforces these limits for processes created by that user.

---

## Soft vs Hard Limit

| Type | Meaning |
|------|---------|
| Soft limit | Active limit. User can increase it up to the hard limit. |
| Hard limit | Maximum allowed limit. Only root can increase it. |

Example:

```
soft limit = 2048
hard limit = 4096
```

User can change:

```bash
ulimit -u 3000
```

but cannot exceed:

```bash
ulimit -u 4096
```

---

## ulimit and fork()

When a process calls:

```c
fork()
```

the kernel checks the user's process limit.

Flow:

```
fork()
  |
  v
Check ulimit -u
  |
  +---- Limit not reached → Create child process
  |
  +---- Limit reached → fork() returns -1
```

---

## Important Files

| File | Purpose |
|------|---------|
| `/etc/security/limits.conf` | User resource limits |
| `/etc/security/limits.d/` | Additional limit configurations |

---

## Interview Answer

`ulimit` defines resource limits for users and processes. These limits are configured in `/etc/security/limits.conf` and applied during login through PAM. The kernel enforces these limits; if a user exceeds limits like maximum processes (`ulimit -u`), system calls such as `fork()` fail and return `-1`.
