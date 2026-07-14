# Linux `/etc` Filesystem Hierarchy

## Definition

`/etc` is a Linux directory that contains **system-wide configuration files**.  
It stores configuration used by the operating system, services, and applications.

## Important `/etc` Directories and Files

| Path | Purpose |
|------|---------|
| `/etc/passwd` | User account information |
| `/etc/shadow` | Encrypted user passwords |
| `/etc/group` | Group information |
| `/etc/hostname` | System hostname |
| `/etc/hosts` | Local hostname-to-IP mapping |
| `/etc/resolv.conf` | DNS resolver configuration |
| `/etc/fstab` | Filesystem mount configuration |
| `/etc/ssh/` | SSH server/client configuration |
| `/etc/systemd/` | Systemd service configuration |
| `/etc/nginx/` | Nginx configuration |
| `/etc/apache2/` | Apache web server configuration |
| `/etc/security/` | Security-related configurations |
| `/etc/security/limits.conf` | User resource limits (`ulimit`) |
| `/etc/profile` | Global shell environment settings |
| `/etc/bashrc` or `/etc/bash.bashrc` | Bash shell configuration |
| `/etc/cron.*` | Scheduled job configurations |
| `/etc/logrotate.conf` | Log rotation configuration |
| `/etc/yum.conf` / `/etc/apt/` | Package manager configuration |

## Example Structure

```
/etc
├── passwd
├── shadow
├── group
├── hostname
├── hosts
├── fstab
├── ssh/
│   └── sshd_config
├── systemd/
│   └── system/
├── security/
│   └── limits.conf
├── nginx/
│   └── nginx.conf
└── cron.d/
```

## Interview Points

- `/etc` = **Editable system configuration files**
- `/bin` = Essential user commands
- `/sbin` = System administration commands
- `/var` = Variable data (logs, cache, spool)
- `/home` = User home directories
- `/proc` = Kernel and process information (virtual filesystem)
- `/tmp` = Temporary files
- `/usr` = User applications and libraries
- `/dev` = Device files
- `/boot` = Kernel and bootloader files
