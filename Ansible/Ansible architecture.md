**Explain Ansible architecture.**


Ansible consists of a control node, where playbooks are executed, and managed nodes, which are the target systems. It communicates using standard protocols SSH for Linux/Unix and WinRM for Windows without requiring any agent installation. This push-based model allows the control node to initiate tasks directly. The simplicity of this setup is central to Ansible’s appeal.
