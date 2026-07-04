# What are Templates in Ansible?

Templates in Ansible are **dynamic configuration files** that use the **Jinja2 templating engine**. They allow you to create configuration files by replacing placeholders with variables during playbook execution.

Instead of maintaining separate configuration files for different servers or environments, you create **one template** and Ansible generates the final configuration using variables.

---

# Why Do We Use Templates?

Templates are useful when configuration files contain values that change between servers or environments, such as:

- Hostnames
- IP Addresses
- Environment (Dev, QA, Prod)
- Database Credentials
- Application Ports
- Domain Names

Instead of creating multiple static files, a single template can generate customized configurations.

---

# How Templates Work

```
Template File (.j2)
        │
        ▼
Contains Variables
        │
        ▼
Ansible Template Module
        │
        ▼
Replaces Variables
        │
        ▼
Final Configuration File
```

---

# Example Template

**nginx.conf.j2**

```jinja
server {

    listen 80;

    server_name {{ inventory_hostname }};

    root /var/www/html;

}
```

Here,

```jinja
{{ inventory_hostname }}
```

is a Jinja2 variable.

---

# Playbook Example

```yaml
---
- hosts: webservers
  become: yes

  tasks:

    - name: Copy nginx configuration
      template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
```

When executed on different servers:

Server 1

```
web01.company.com
```

Generated file

```text
server_name web01.company.com;
```

Server 2

```
web02.company.com
```

Generated file

```text
server_name web02.company.com;
```

The same template generates different configuration files based on the target host.

---

# Template Module Syntax

```yaml
template:
  src: app.conf.j2
  dest: /etc/app/app.conf
```

Common Parameters

| Parameter | Description |
|-----------|-------------|
| `src` | Source template file (`.j2`) |
| `dest` | Destination file on the managed host |
| `owner` | File owner |
| `group` | File group |
| `mode` | File permissions |

Example

```yaml
template:
  src: app.conf.j2
  dest: /etc/app/app.conf
  owner: root
  group: root
  mode: "0644"
```

---

# Jinja2 Variables

Templates support variables using double curly braces.

Example

```jinja
Application={{ app_name }}

Environment={{ env }}

Port={{ app_port }}
```

If the variables are:

```yaml
app_name: MyApp

env: Production

app_port: 8080
```

Generated file:

```text
Application=MyApp

Environment=Production

Port=8080
```

---

# Template vs Copy Module

| Template | Copy |
|----------|------|
| Dynamic file | Static file |
| Supports Jinja2 variables | No variable substitution |
| Generates different output for different hosts | Copies the same file to every host |
| Best for configuration files | Best for static files |

---

# Real-Time Production Example

Suppose your application is deployed to:

- Development
- QA
- Production

Each environment has a different database server.

Instead of maintaining three configuration files:

```
application-dev.properties

application-qa.properties

application-prod.properties
```

You create one template:

```jinja
db.host={{ database_host }}

db.port={{ database_port }}

environment={{ env }}
```

Variables

Development

```yaml
database_host: dev-db.company.com
env: Development
```

Production

```yaml
database_host: prod-db.company.com
env: Production
```

Ansible generates the correct configuration for each environment automatically.

---

# Production Benefits

Templates help:

- Eliminate duplicate configuration files.
- Manage multiple environments with a single template.
- Reduce manual errors.
- Keep configuration consistent.
- Improve automation and scalability.

---

# Interview Questions

## Q1. What are Templates in Ansible?

**Answer:**

Templates are dynamic configuration files written using the Jinja2 templating engine. They allow variables to be substituted at runtime, enabling a single template to generate different configuration files for different servers or environments.

---

## Q2. Why do we use Templates?

**Answer:**

Templates are used when configuration files contain values that vary between systems, such as hostnames, IP addresses, ports, database credentials, or environment-specific settings. This avoids maintaining multiple versions of the same configuration file.

---

## Q3. What is the difference between Template and Copy?

**Answer:**

The `copy` module transfers a static file exactly as it is, while the `template` module processes a Jinja2 template, replacing variables with their actual values before copying the file to the target host.

---

# Senior-Level Interview Answer

> **Templates in Ansible are dynamic configuration files that use the Jinja2 templating engine. They allow us to generate environment-specific or host-specific configuration files from a single source by replacing variables during playbook execution. In production, templates are commonly used for configuration files such as Nginx, Apache, HAProxy, application properties, and database settings. Compared to the `copy` module, templates provide flexibility, improve maintainability, and eliminate the need to maintain multiple versions of the same configuration file.**
