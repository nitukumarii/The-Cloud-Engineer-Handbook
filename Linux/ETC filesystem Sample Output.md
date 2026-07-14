# Linux /etc Important Files - Sample Output

## 1. /etc/passwd
**Purpose:** User account information

```bash
cat /etc/passwd
```

Output:

```
root:x:0:0:root:/root:/bin/bash
nitu:x:1001:1001:Nitu User:/home/nitu:/bin/bash
ubuntu:x:1002:1002:Ubuntu User:/home/ubuntu:/bin/bash
```

Format:

```
username:x:UID:GID:comment:home:shell
```

---

## 2. /etc/shadow
**Purpose:** Encrypted user passwords

```bash
sudo cat /etc/shadow
```

Output:

```
root:$6$xyz123$encrypted_password_hash:19800:0:99999:7:::
nitu:$6$abc456$encrypted_password_hash:19800:0:99999:7:::
```

Only root can read this file.

---

## 3. /etc/group
**Purpose:** Group information

```bash
cat /etc/group
```

Output:

```
root:x:0:
sudo:x:27:nitu
docker:x:999:nitu
developers:x:1002:nitu
```

Format:

```
group_name:x:GID:members
```

---

## 4. /etc/hostname
**Purpose:** System hostname

```bash
cat /etc/hostname
```

Output:

```
prod-web-server-01
```

---

## 5. /etc/hosts
**Purpose:** Local hostname-to-IP mapping

```bash
cat /etc/hosts
```

Output:

```
127.0.0.1       localhost
127.0.1.1       prod-web-server-01

10.10.1.20      database-server
10.10.1.30      app-server
```

---
# Difference Between `/etc/hostname` and `/etc/hosts`

| File | Purpose | Example |
|------|---------|---------|
| `/etc/hostname` | Stores the **system's own hostname** | `prod-web-server-01` |
| `/etc/hosts` | Maps **hostnames to IP addresses locally** | `10.10.1.20 database-server` |

## `/etc/hostname`

- Defines the name of the machine.
- Used during system boot to set the hostname.

Example:

```bash
cat /etc/hostname

Output

prod-web-server-01

# `/etc/hosts` Example

## Check Hosts File

```bash
cat /etc/hosts
```

Output:

```
127.0.0.1       localhost
10.10.1.20      database-server
10.10.1.30      app-server
```

## Scenario

- Testing before DNS setup
- Mapping internal servers
- Troubleshooting name resolution issues

## Test Name Resolution

```bash
ping database-server
```

Linux resolves:

```
database-server → 10.10.1.20
```


## 6. /etc/resolv.conf
**Purpose:** DNS resolver configuration

/etc/resolv.conf contains the IP addresses of DNS resolver servers that your machine will query.

```bash
cat /etc/resolv.conf
```

Output:

```
nameserver 8.8.8.8
nameserver 1.1.1.1
search company.local
```

---

## 7. /etc/fstab
**Purpose:** Filesystem mount configuration

It tells Linux: Which disk/partition to mount, where to mount it, what filesystem type it uses, and what options to apply during boot.

```bash
cat /etc/fstab
```

Output:

```
# Device        Mount Point   Type   Options
/dev/xvda1      /             ext4   defaults
/dev/xvdb1      /data         xfs    defaults
```

---

## 8. /etc/ssh/
**Purpose:** SSH server/client configuration

List files:

```bash
ls /etc/ssh
```

Output:

```
ssh_config
sshd_config
ssh_host_rsa_key
ssh_host_ed25519_key
```

Check SSH server config:

```bash
cat /etc/ssh/sshd_config
```

Output:

```
Port 22
PermitRootLogin no
PasswordAuthentication yes
```

---

## 9. /etc/systemd/
**Purpose:** Systemd service configuration

```bash
ls /etc/systemd/system
```

Output:

```
nginx.service
docker.service
kubelet.service
```

Example:

```bash
cat /etc/systemd/system/nginx.service
```

Output:

```
[Unit]
Description=Nginx Web Server

[Service]
ExecStart=/usr/sbin/nginx

[Install]
WantedBy=multi-user.target
```

---

## 10. /etc/nginx/
**Purpose:** Nginx configuration

```bash
ls /etc/nginx
```

Output:

```
nginx.conf
conf.d
sites-enabled
sites-available
```

Example:

```bash
cat /etc/nginx/nginx.conf
```

Output:

```
worker_processes auto;

events {
    worker_connections 1024;
}

http {
    include sites-enabled/*
}
```

---

## 11. /etc/apache2/
**Purpose:** Apache web server configuration

```bash
ls /etc/apache2
```

Output:

```
apache2.conf
ports.conf
sites-available
sites-enabled
mods-enabled
```

---

## 12. /etc/security/
**Purpose:** Security configurations

```bash
ls /etc/security
```

Output:

```
limits.conf
access.conf
faillock.conf
```

---

## 13. /etc/security/limits.conf
**Purpose:** User resource limits

```bash
cat /etc/security/limits.conf
```

Output:

```
*       soft    nofile     1024
*       hard    nofile     4096

nitu    soft    nproc      2048
nitu    hard    nproc      4096
```

---

## 14. /etc/profile
**Purpose:** Global shell environment settings

```bash
cat /etc/profile
```

Output:

```
PATH=/usr/local/bin:/usr/bin:/bin
export PATH

umask 022
```

---

## 15. /etc/bash.bashrc
**Purpose:** Bash shell configuration

```bash
cat /etc/bash.bashrc
```

Output:

```
alias ll='ls -alF'
alias grep='grep --color=auto'
```

---

## 16. /etc/cron.*
**Purpose:** Scheduled jobs

```bash
ls /etc/cron.*
```

Output:

```
/etc/cron.daily
/etc/cron.hourly
/etc/cron.weekly
/etc/cron.monthly
```

Example:

```bash
ls /etc/cron.daily
```

Output:

```
logrotate
apt-update
backup-script
```

---

## 17. /etc/logrotate.conf
**Purpose:** Log rotation configuration

```bash
cat /etc/logrotate.conf
```

Output:

```
weekly
rotate 4
create
compress

include /etc/logrotate.d
```

---

## 18. /etc/yum.conf (RHEL/CentOS)

```bash
cat /etc/yum.conf
```

Output:

```
[main]
cachedir=/var/cache/yum
keepcache=0
gpgcheck=1
```

---

## 19. /etc/apt/ (Ubuntu/Debian)

# `/etc/apt/` (Ubuntu/Debian)

**Definition:**
`/etc/apt/` contains **APT package manager configuration** files used to manage software packages.

## Important Files

| Path | Purpose |
|---|---|
| `/etc/apt/sources.list` | Software repository URLs |
| `/etc/apt/sources.list.d/` | Additional repositories |
| `/etc/apt/apt.conf.d/` | APT settings |

## Commands

```bash
apt update     # Refresh package list
apt install    # Install packages
apt upgrade    # Update packages
```

```bash
ls /etc/apt
```

Output:

```
apt.conf.d
sources.list
trusted.gpg.d
```

Example:

```bash
cat /etc/apt/sources.list
```

Output:

```
deb http://archive.ubuntu.com/ubuntu jammy main restricted
deb http://archive.ubuntu.com/ubuntu jammy-updates main
```
