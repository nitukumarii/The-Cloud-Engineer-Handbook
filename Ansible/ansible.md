# Ansible Interview Questions and Answers (Most Frequently Asked)

> **Interview Level:** DevOps / SRE (3–8+ Years)
>
> These are the most commonly asked Ansible interview questions covering beginner, intermediate, and senior-level concepts.

---

# 1. What is Ansible?

### Answer

Ansible is an open-source IT automation and configuration management tool used for:

- Configuration Management
- Application Deployment
- Infrastructure Provisioning
- Orchestration

It is **agentless**, meaning no software agent is required on managed hosts. It communicates using:

- SSH (Linux)
- WinRM (Windows)

### Interview Tip

> "Ansible is a push-based, agentless automation tool that uses YAML playbooks to automate infrastructure provisioning, configuration management, and application deployment."

---

# 2. Why Ansible instead of Shell Scripting?

### Answer

Shell scripts work well for small tasks but become difficult to maintain as infrastructure grows.

Ansible provides:

- Idempotency
- Inventory management
- Parallel execution
- Error handling
- Reusable roles
- Better readability
- Cross-platform support

Example:

Instead of writing a 500-line shell script to install and configure Nginx, Ansible can accomplish it using reusable modules in a few YAML tasks.

---

# 3. Why Ansible instead of Puppet or Chef?

| Ansible | Puppet/Chef |
|----------|-------------|
| Agentless | Agent required |
| Uses SSH | Uses Agents |
| YAML | Ruby DSL |
| Push Model | Mostly Pull Model |
| Easy to Learn | Higher Learning Curve |
| Simple Setup | Complex Setup |

---

# 4. Explain Ansible Architecture.

### Components

- Control Node
- Managed Nodes
- Inventory
- Playbooks
- Modules
- Plugins
- Collections

### Flow

```
            Control Node
                 │
                 │ SSH
                 ▼
         Managed Nodes
                 │
          Execute Modules
                 │
          Return Results
```

---

# 5. What is Inventory?

Inventory is a file that contains information about managed hosts.

Example:

```ini
[web]
10.0.1.10
10.0.1.11

[database]
10.0.2.10
```

Types:

- Static Inventory
- Dynamic Inventory

---

# 6. Static vs Dynamic Inventory

### Static Inventory

- Hosts manually added
- Suitable for small environments

### Dynamic Inventory

Hosts are automatically discovered from:

- AWS
- Azure
- GCP
- VMware

Mostly used in production where instances are created and terminated automatically.

---

# 7. What is a Playbook?

A Playbook is a YAML file that defines automation tasks.

Example

```yaml
---
- hosts: web
  become: yes

  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present
```

---

# 8. What are Modules?

Modules are reusable units of work executed on managed nodes.

Common Modules:

- yum
- apt
- package
- service
- copy
- template
- file
- shell
- command
- user
- git
- systemd

---

# 9. What are Roles?

Roles organize playbooks into reusable components.

Directory Structure

```
roles/

nginx/

tasks/

handlers/

templates/

files/

vars/

defaults/

meta/
```

Benefits

- Modular
- Reusable
- Easier maintenance
- Better project structure

---

# 10. What is Idempotency?

Idempotency means running the same playbook multiple times always produces the same desired state.

Example

First Run

```
changed
```

Second Run

```
ok
```

No duplicate installation or configuration occurs.

---

# 11. Explain Ad-hoc Commands.

Used for quick one-time tasks.

Examples

```bash
ansible all -m ping

ansible web -m shell -a "uptime"

ansible all -m reboot
```

---

# 12. Difference between Command and Shell Module

| Command | Shell |
|-----------|---------|
| No Shell | Uses Shell |
| More Secure | Less Secure |
| No Pipes | Supports Pipes |
| No Redirection | Supports Redirection |
| No Environment Variables | Supports Variables |

Examples

```yaml
command: ls
```

```yaml
shell: ps -ef | grep nginx
```

---

# 13. What is Ansible Galaxy?

Ansible Galaxy is the official repository for reusable roles and collections.

Example

```bash
ansible-galaxy install geerlingguy.nginx
```

---

# 14. What are Facts?

Facts are system information automatically gathered from managed hosts.

Examples

```yaml
ansible_hostname

ansible_os_family

ansible_distribution

ansible_memtotal_mb

ansible_default_ipv4.address
```

---

# 15. What is register?

Used to store task output.

Example

```yaml
- shell: uptime
  register: result

- debug:
    var: result.stdout
```

---

# 16. What is when Condition?

Used for conditional execution.

Example

```yaml
when:
  ansible_os_family == "RedHat"
```

---

# 17. Difference between vars and defaults

| vars | defaults |
|------|----------|
| High Priority | Lowest Priority |
| Difficult to Override | Easy to Override |

---

# 18. Variable Precedence (Highest → Lowest)

```
Extra Variables

Task Variables

Block Variables

Role Variables

Inventory Variables

Play Variables

Role Defaults
```

---

# 19. What are Handlers?

Handlers execute only when notified by another task.

Example

```yaml
tasks:

- name: Copy Config
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
  notify:
    - Restart Nginx

handlers:

- name: Restart Nginx
  service:
    name: nginx
    state: restarted
```

---

# 20. What is become?

Used for privilege escalation.

```yaml
become: yes

become_user: root
```

Equivalent to sudo.

---

# 21. Difference between include_tasks and import_tasks

| include_tasks | import_tasks |
|----------------|--------------|
| Dynamic | Static |
| Runtime | Parse Time |
| Conditional Loading | Always Loaded |

---

# 22. What is Ansible Vault?

Used to encrypt:

- Passwords
- Secrets
- API Keys
- SSH Keys

Example

```bash
ansible-vault encrypt secrets.yml
```

---

# 23. How do you Debug Playbooks?

Common methods:

```bash
ansible-playbook play.yml -v

ansible-playbook play.yml -vv

ansible-playbook play.yml -vvv

ansible-playbook play.yml --syntax-check

ansible-playbook play.yml --check
```

Useful module:

```yaml
debug:
```

---

# 24. What are Tags?

Tags allow execution of selected tasks.

Example

```yaml
tasks:

- name: Install Package
  yum:
    name: nginx
    state: present
  tags:
    - install
```

Execute

```bash
ansible-playbook play.yml --tags install
```

---

# 25. What are Templates?

Templates are dynamic configuration files using Jinja2.

Example

```
server_name {{ inventory_hostname }}
```

Uses

```yaml
template:
```

---

# 26. Difference between Copy and Template

| Copy | Template |
|------|-----------|
| Static File | Dynamic File |
| No Variables | Supports Variables |
| Faster | Slightly Slower |

---

# 27. What is Check Mode?

Check Mode performs a dry run.

```bash
ansible-playbook play.yml --check
```

Useful before production deployments.

---

# 28. What is --limit?

Executes playbook on selected hosts only.

Example

```bash
ansible-playbook play.yml --limit web

ansible-playbook play.yml --limit server01
```

---

# 29. What is Serial Deployment?

Deploys servers in batches.

Example

```yaml
serial: 2
```

Used for:

- Rolling Updates
- Zero Downtime Deployments

---

# 30. How do you Rollback in Ansible?

Ansible has no automatic rollback.

Production approaches:

- Restore previous package version
- Restore backup configuration
- Redeploy previous application version
- Restore VM Snapshot
- Blue-Green Deployment
- Canary Deployment

---

# Senior-Level Interview Questions

---

# 31. Explain an Ansible Project You Worked On.

### Sample Answer

> We managed around 250 AWS EC2 instances across Development, QA, and Production environments. We used dynamic AWS inventory, reusable roles for Nginx, Docker, monitoring agents, and application deployments. Secrets were encrypted using Ansible Vault. Deployments were triggered through Jenkins pipelines with rolling deployments using `serial` to avoid downtime. Handlers ensured services restarted only when configuration files changed, and all playbooks were validated with `--syntax-check` and `--check` mode before production deployment.

---

# 32. How do you achieve Zero Downtime Deployment?

### Answer

1. Remove server from Load Balancer.
2. Deploy application.
3. Run health checks.
4. Add server back to Load Balancer.
5. Continue deployment using `serial`.
6. Verify monitoring and logs.

---

# 33. A Playbook Fails on One Server. How Do You Troubleshoot?

### Answer

1. Run playbook with `-vvv`.
2. Verify SSH connectivity.
3. Check inventory.
4. Compare gathered facts.
5. Validate permissions (`become`).
6. Review logs and task output.
7. Execute only the failed host using `--limit`.
8. Fix the issue and rerun.

---

# 34. How Do You Manage Secrets?

### Answer

- Store credentials in Ansible Vault.
- Never store passwords in Git.
- Encrypt variables and files.
- Pass Vault password securely through CI/CD.
- Rotate secrets regularly.

---

# 35. How Do You Organize Large Production Playbooks?

### Answer

- Use Roles.
- Separate inventories by environment.
- Store variables in `group_vars` and `host_vars`.
- Keep secrets in Ansible Vault.
- Maintain code in Git.
- Integrate with Jenkins/GitHub Actions.
- Validate using `--syntax-check`.
- Execute `--check` mode before Production.

---

# Common Ansible Commands

```bash
ansible all -m ping

ansible-playbook playbook.yml

ansible-playbook playbook.yml --check

ansible-playbook playbook.yml --syntax-check

ansible-playbook playbook.yml --limit web

ansible-playbook playbook.yml --tags install

ansible-playbook playbook.yml -vvv

ansible-galaxy install role_name

ansible-vault encrypt secrets.yml

ansible-inventory --list
```

---

# Senior Interview Tips

Interviewers expect you to explain:

- Real production use cases.
- Why you chose Ansible over other tools.
- Idempotency.
- Inventory management.
- Roles and reusable code.
- Ansible Vault.
- Rolling deployments.
- Zero-downtime deployments.
- Troubleshooting failed playbooks.
- Integration with Jenkins, Git, Docker, Kubernetes, and AWS.
- Best practices for large-scale infrastructure automation.
