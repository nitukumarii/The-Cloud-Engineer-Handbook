# Ansible Role

An Ansible role is a way to organize and reuse Ansible automation code in a structured format.

Instead of keeping all tasks, variables, handlers, and templates in one large playbook, we separate them into different directories inside a role.

A role can contain:
- Tasks → actions to perform
- Handlers → actions triggered by changes (for example, restart a service)
- Variables → configuration values
- Templates → configuration files
- Files → static files to copy

Roles help make Ansible automation more reusable, maintainable, and easier to manage across multiple environments.
