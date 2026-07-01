**Why Ansible instead of shell scripting?**



Shell scripts are good for simple tasks, but Ansible is better for configuration management and large-scale automation because it's agentless, idempotent, scalable, and easier to maintain.



Idempotent – avoids making unnecessary changes.


Easy to read – uses simple YAML instead of complex shell scripts.


Agentless – works over SSH; no software needed on target servers.


Scalable – manages hundreds or thousands of servers at once.


Reusable & maintainable – playbooks and roles make automation organized.


Better error handling – provides clear task status and reporting.
