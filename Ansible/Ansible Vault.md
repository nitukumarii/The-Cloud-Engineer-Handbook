# How to Use Ansible Vault in a Playbook

Ansible Vault is used to **encrypt sensitive information** such as:

- Passwords
- API Keys
- SSH Keys
- Database Credentials
- Cloud Secrets

Instead of storing secrets in plain text, they are encrypted and decrypted only during playbook execution.

---

# Step 1: Create a Secrets File

Create a file named `secrets.yml`.

```yaml
db_user: admin
db_password: MySecurePassword123
```

---

# Step 2: Encrypt the File

```bash
ansible-vault encrypt secrets.yml
```

You will be prompted to enter a Vault password.

After encryption, the file looks like this:

```yaml
$ANSIBLE_VAULT;1.1;AES256
6632363235653935633535353438...
```

The contents are unreadable without the Vault password.

---

# Step 3: Include the Vault File in the Playbook

```yaml
---
- hosts: database_servers
  become: yes

  vars_files:
    - secrets.yml

  tasks:

    - name: Display database username
      debug:
        msg: "{{ db_user }}"

    - name: Create configuration file
      template:
        src: db.conf.j2
        dest: /etc/myapp/db.conf
```

The variables from the encrypted file are available just like normal variables.

---

# Step 4: Run the Playbook

Prompt for the Vault password:

```bash
ansible-playbook playbook.yml --ask-vault-pass
```

Or use a Vault password file:

```bash
ansible-playbook playbook.yml --vault-password-file vault.pass
```

---

# Example: Using Vault Variables

Encrypted file:

```yaml
db_user: admin
db_password: Password@123
```

Playbook:

```yaml
---
- hosts: all

  vars_files:
    - secrets.yml

  tasks:

    - name: Configure application
      template:
        src: app.conf.j2
        dest: /etc/app.conf
```

Template (`app.conf.j2`):

```text
username={{ db_user }}
password={{ db_password }}
```

During execution, Ansible decrypts the variables and generates:

```text
username=admin
password=Password@123
```

---

# Useful Vault Commands

Encrypt a file:

```bash
ansible-vault encrypt secrets.yml
```

Decrypt a file:

```bash
ansible-vault decrypt secrets.yml
```

Edit an encrypted file:

```bash
ansible-vault edit secrets.yml
```

View an encrypted file:

```bash
ansible-vault view secrets.yml
```

Change the Vault password:

```bash
ansible-vault rekey secrets.yml
```

---

# Real-Time Production Example

A Jenkins pipeline deploys an application to production.

The playbook needs:

- Database username
- Database password
- AWS Access Key
- API Token

Instead of storing these secrets in Git, they are kept in an encrypted `secrets.yml` file.

```yaml
---
- hosts: production

  vars_files:
    - secrets.yml

  tasks:

    - name: Deploy Application
      template:
        src: application.properties.j2
        dest: /opt/app/application.properties
```

The CI/CD pipeline provides the Vault password securely, allowing Ansible to decrypt the file only during execution.

---

# Interview Answer (Senior Level)

> **Ansible Vault is used to securely store sensitive information such as passwords, API keys, and database credentials. In a playbook, we typically encrypt a variables file using `ansible-vault encrypt` and include it with `vars_files`. During execution, Ansible decrypts the file using `--ask-vault-pass` or `--vault-password-file`, making the variables available to tasks without exposing secrets in plain text. In production, Vault helps ensure that sensitive data is not stored unencrypted in source control.**
