# Ansible Interview Question: Deploy an Application to Multiple Environments

## Interview Answer (1–2 minutes)

> "To deploy an application to multiple environments such as Development, Testing, Staging, and Production, I use separate inventory files and environment-specific variables. The same Ansible playbook is reused across all environments, while configuration values like database endpoints, API URLs, and application settings are stored in inventory or `group_vars`. Sensitive information such as passwords and API keys is encrypted using Ansible Vault.
>
> In the CI/CD pipeline, deployments follow the promotion flow: **Development → Testing → Staging → Production**. After validating the application in each environment, I promote it to the next stage. For production, I use rolling deployments with the `serial` keyword so that only a subset of servers is updated at a time, minimizing downtime. After each batch, I perform health checks before continuing. This approach ensures consistency, reusability, security, and safe deployments across all environments."

---

## Example Directory Structure

```text
inventory/
├── dev
├── test
├── staging
└── production

group_vars/
├── dev.yml
├── test.yml
├── staging.yml
└── production.yml

roles/
playbooks/
```

---

## Example Inventory

### Development

```ini
[webservers]
10.0.1.10
10.0.1.11
```

### Production

```ini
[webservers]
10.0.2.10
10.0.2.11
10.0.2.12
```

---

## Deployment Commands

### Deploy to Development

```bash
ansible-playbook -i inventory/dev deploy.yml
```

### Deploy to Testing

```bash
ansible-playbook -i inventory/test deploy.yml
```

### Deploy to Production

```bash
ansible-playbook -i inventory/production deploy.yml
```

---

## Best Practices

- Use a **single reusable playbook** for all environments.
- Store environment-specific values in **inventory** or **group_vars**.
- Protect secrets using **Ansible Vault**.
- Promote deployments through **Dev → Test → Staging → Production**.
- Use **rolling deployments (`serial`)** in production.
- Perform application health checks after each deployment batch.
- Have a rollback strategy if validation fails.

---

## Follow-up Interview Question

### How do you avoid maintaining multiple playbooks?

**Answer:**

> "I maintain a single playbook and use different inventory files and variable files for each environment. This avoids duplication, improves consistency, and makes maintenance easier."

---

## Key Interview Points

- Single reusable playbook
- Separate inventories per environment
- Environment-specific variables
- Ansible Vault for secrets
- CI/CD integration
- Rolling deployments using `serial`
- Health checks after deployment
- Rollback strategy
