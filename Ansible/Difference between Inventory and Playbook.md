**Difference between Inventory and Playbook.**


| **Inventory**                                                 | **Playbook**                                                 |
| ------------------------------------------------------------- | ------------------------------------------------------------ |
| Defines **where** Ansible runs.                               | Defines **what** Ansible does.                               |
| Contains the list of managed hosts (servers).                 | Contains automation tasks written in YAML.                   |
| Can be static (`inventory.ini`) or dynamic (AWS, Azure, GCP). | Contains one or more plays, each with tasks.                 |
| Organizes hosts into groups.                                  | Executes modules like `yum`, `copy`, `service`, `user`, etc. |
| No automation logic.                                          | Contains the automation logic and workflow.                  |
