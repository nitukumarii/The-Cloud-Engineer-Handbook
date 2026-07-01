**Modules**


Ansible modules are small, reusable programs that perform a specific task on a managed node. They are the core building blocks of Ansible automation. Instead of writing complex scripts, we use modules to perform operations like installing packages, managing services, creating users, copying files, or executing commands. When a playbook runs, Ansible transfers the required module to the target host, executes it, returns the result, and then removes the module. This is one reason why Ansible is agentless—it doesn't require a permanent agent on the managed nodes."



<img width="776" height="462" alt="image" src="https://github.com/user-attachments/assets/1802da84-72c4-4569-866c-e7e71a5dc919" />
