# What is `become` in Ansible?

`become` is an Ansible keyword used for **privilege escalation**. It allows Ansible to execute tasks as another user (typically `root`) instead of the SSH login user.

In Linux, `become` is equivalent to using **`sudo`**.

---

# Why do we use `become`?

Many system administration tasks require elevated privileges, such as:

- Installing packages
- Starting or stopping services
- Creating users and groups
- Editing files under `/etc`
- Changing system configurations
- Managing firewall rules

Without `become`, these tasks will fail if the connected user does not have the required permissions.

---

# Syntax

```yaml
become: yes
```

or

```yaml
become: true
```

---

# Example 1: Use `become` for the Entire Playbook

```yaml
---
- hosts: webservers
  become: yes

  tasks:

    - name: Install Nginx
      yum:
        name: nginx
        state: present
```

Here, all tasks execute with elevated privileges.

---

# Example 2: Use `become` for a Single Task

```yaml
tasks:

- name: Install Nginx
  become: yes

  yum:
    name: nginx
    state: present
```

Only this task runs as the privileged user.

---

# Example 3: Run as Another User

```yaml
tasks:

- name: Execute command as oracle user
  become: yes
  become_user: oracle

  shell: whoami
```

Output

```
oracle
```

---

# Common `become` Parameters

| Parameter | Description |
|-----------|-------------|
| `become` | Enables privilege escalation |
| `become_user` | User to switch to (default: root) |
| `become_method` | Method used for privilege escalation (sudo, su, pbrun, doas, etc.) |
| `become_flags` | Additional options for the privilege escalation method |

Example

```yaml
become: yes
become_user: root
become_method: sudo
```

---

# Real-Time Production Example

Suppose Jenkins connects to an EC2 instance using the user `ec2-user`.

The deployment requires:

- Installing Docker
- Updating `/etc/docker/daemon.json`
- Restarting the Docker service

Since `ec2-user` doesn't have permission to perform these operations, the playbook uses `become`.

```yaml
---
- hosts: docker_servers
  become: yes

  tasks:

  - name: Install Docker
    yum:
      name: docker
      state: present

  - name: Start Docker Service
    service:
      name: docker
      state: started
```

Flow:

```
Jenkins
    │
    ▼
SSH Login (ec2-user)
    │
    ▼
become: yes
    │
    ▼
Switch to root (sudo)
    │
    ▼
Execute administrative tasks
```

---

# Difference Between `become` and `become_user`

| become | become_user |
|---------|-------------|
| Enables privilege escalation | Specifies which user to switch to |
| Usually switches to `root` | Can switch to any valid user |
| Equivalent to `sudo` | Equivalent to `sudo -u <user>` |

Example

```yaml
become: yes
become_user: oracle
```

This executes the task as the **oracle** user instead of **root**.

---

# Common Interview Questions

## Q1. What is `become` in Ansible?

**Answer:**

`become` is Ansible's privilege escalation mechanism. It allows tasks to run as another user, usually `root`, even if Ansible connects using a non-root account. Internally, it commonly uses `sudo` on Linux systems.

---

## Q2. Why do we use `become`?

**Answer:**

We use `become` whenever administrative privileges are required, such as:

- Installing packages
- Restarting services
- Editing system configuration files
- Creating users
- Managing system-level resources

Without `become`, these operations fail for non-privileged users.

---

## Q3. What is the difference between `become` and `sudo`?

**Answer:**

`sudo` is the Linux command used for privilege escalation.

`become` is the Ansible abstraction for privilege escalation. By default, it uses the `sudo` method on Linux, but it can also use other methods such as:

- su
- doas
- pbrun
- pfexec

---

# Senior-Level Interview Answer

> "`become` is Ansible's privilege escalation feature. In production, we typically connect to servers using a non-root account such as `ec2-user` or `ansible`, following security best practices. Whenever administrative operations like package installation, service management, or configuration changes are required, we use `become: yes` to temporarily elevate privileges, usually through `sudo`. This approach avoids direct root logins while allowing automation to perform privileged tasks securely."
