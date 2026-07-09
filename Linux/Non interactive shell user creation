# Understanding Non-Interactive Shell in Linux

## What is a Shell?

A shell is a program that starts after a user successfully logs into a Linux system. It provides a command-line interface where users can execute commands like `ls`, `cd`, and `pwd`. Common interactive shells are `/bin/bash` and `/bin/sh`.

---

## Interactive vs Non-Interactive Shell

### Interactive Shell (`/bin/bash`)

- User can log in.
- Gets a command prompt.
- Can execute Linux commands.

Example:

```text
john:x:1001:1001::/home/john:/bin/bash
```

After login:

```bash
john@appserver:~$
```

---

### Non-Interactive Shell (`/sbin/nologin`)

- User account exists.
- User **cannot** log in.
- No command prompt is provided.

Example:

```text
jim:x:1002:1002::/home/jim:/sbin/nologin
```

---

## What Happens During Login?

When a user logs in using SSH or PuTTY:

1. User enters username and password.
2. `sshd` searches for the user in `/etc/passwd`.
3. If the user is not found → Login fails.
4. If the user is found → Authentication succeeds.
5. Linux reads the last field (login shell) from `/etc/passwd`.
6. Linux executes that shell.

Example:

```text
jim:x:1002:1002::/home/jim:/sbin/nologin
```

Since the shell is `/sbin/nologin`, Linux runs that program instead of Bash.

---

## Does Linux Look for `/sbin/nologin` If User Doesn't Exist?

**No.**

Linux first checks whether the user exists.

- User not found → Login fails immediately.
- User found → Linux reads the login shell and executes it.

---

## What Does `/sbin/nologin` Do?

`/sbin/nologin` is a small program.

When executed, it:

- Displays:

```text
This account is currently not available.
```

- Immediately exits.
- Closes the SSH session.

Flow:

```text
SSH/PuTTY
    │
    ▼
Authenticate User
    │
    ▼
Read /etc/passwd
    │
    ▼
Shell = /sbin/nologin
    │
    ▼
Run nologin
    │
    ▼
Display Message
    │
    ▼
Session Closed
```

---

## Why Use Non-Interactive Users?

Service accounts need a Linux user but should never allow human logins.

Examples:

- nginx
- mysql
- backup
- jenkins

These users:

- Own files
- Run services
- Cannot log in

This improves security by preventing interactive access.

---

## Interview Answer

> A non-interactive shell prevents a user from getting a command prompt. During login, Linux authenticates the user, checks `/etc/passwd`, reads the configured login shell, and executes it. If the shell is `/bin/bash`, the user gets a terminal. If the shell is `/sbin/nologin`, Linux runs the `nologin` program, which displays a message and immediately closes the session. These accounts are typically used for applications and services rather than human users.
