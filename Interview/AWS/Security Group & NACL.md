**Security Group & NACL**



| Feature              | **Security Group (SG)**                                  | **Network ACL (NACL)**                                    |
| -------------------- | -------------------------------------------------------- | --------------------------------------------------------- |
| **Level**            | Instance level                                           | Subnet level                                              |
| **State**            | Stateful                                                 | Stateless                                                 |
| **Rules**            | Allow rules only                                         | Allow and Deny rules                                      |
| **Traffic**          | Return traffic is automatically allowed                  | Return traffic must be explicitly allowed                 |
| **Application**      | Attached to EC2 instances, ENIs, and other AWS resources | Applied to all resources in a subnet                      |
| **Evaluation**       | Evaluates all rules before deciding                      | Evaluates rules in ascending rule number order            |
| **Default Behavior** | By default, denies inbound and allows all outbound       | Default NACL allows all inbound and outbound traffic      |
| **Typical Use**      | Secure individual instances                              | Secure an entire subnet with an additional security layer |
