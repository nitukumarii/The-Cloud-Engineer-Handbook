# Linux Password Management in RHEL

## Can we get the actual password from `/etc/shadow`?

**No.** In RHEL, passwords are not stored as plain text.  
The system stores a **one-way encrypted hash** in `/etc/shadow`.

Example:

```bash
cat /etc/shadow
```

Output:

```
nitu:$6$abcXYZ$8f9a7c3d9e8f....:19800:0:99999:7:::
```

---

## `/etc/shadow` Format

```
username:password_hash:last_change:min:max:warn:inactive:expire
```

Example:

```
nitu:$6$abcXYZ$encrypted_hash:19800:0:99999:7:::
```

Breakdown:

```
nitu
 |
 |-- Username


$6$abcXYZ$encrypted_hash
 |
 |-- Password hash (NOT actual password)
```

---

## Hash Format

Example:

```
$6$abcXYZ$8f9a7c3d9e8f....
```

Meaning:

| Part | Meaning |
|------|---------|
| `$6$` | SHA-512 hashing algorithm |
| `abcXYZ` | Salt (random value added before hashing) |
| `8f9a7c3d...` | Generated password hash |

Common identifiers:

```
$1$ → MD5
$5$ → SHA-256
$6$ → SHA-512
```

---

## How Password Verification Works

During login:

```
User enters password
        |
        v
RHEL hashes the password using same algorithm + salt
        |
        v
Compares generated hash with /etc/shadow
        |
        +---- Match → Login successful
        |
        +---- No Match → Login failed
```

The system does **not decrypt the password**.

---

## If User Forgets Password

The password cannot be recovered.

An administrator resets it:

```bash
passwd username
```

Example:

```bash
passwd nitu
```

Output:

```
Changing password for user nitu.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

---

## Important RHEL Files

| File | Purpose |
|------|---------|
| `/etc/passwd` | User account information |
| `/etc/shadow` | Password hashes |
| `/etc/group` | Group information |
| `/etc/login.defs` | Default password policies |
| `/etc/security/pwquality.conf` | Password complexity rules |
| `/etc/security/` | Security configuration |

---

## RHEL Password Policy

Check default password settings:

```bash
cat /etc/login.defs
```

Example:

```
PASS_MAX_DAYS   99999
PASS_MIN_DAYS   0
PASS_WARN_AGE   7
```

Password complexity:

```bash
cat /etc/security/pwquality.conf
```

Example:

```
minlen = 8
minclass = 3
```

---

## Interview Answer

> In RHEL, user passwords are stored as one-way hashes in `/etc/shadow`, not as plain text. The `$6$` prefix indicates SHA-512 hashing. During authentication, RHEL hashes the entered password and compares it with the stored hash. If the password is forgotten, it cannot be recovered; an administrator must reset it using the `passwd` command.
