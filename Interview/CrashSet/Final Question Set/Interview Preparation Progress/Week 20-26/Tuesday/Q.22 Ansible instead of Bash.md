


# Why Ansible instead of Bash scripting?

Bash scripting is useful for small automation tasks, such as performing configuration changes or repetitive activities on a single server.

However, when we need to perform the same task across multiple servers, such as patching, 
package installation, or configuration changes, managing it through Bash scripts becomes difficult to maintain and scale.

In such cases, we use Ansible because it provides centralized automation, ensures consistency across 
multiple servers, and follows an idempotent approach, meaning the same playbook can be executed multiple times without causing unwanted changes.
