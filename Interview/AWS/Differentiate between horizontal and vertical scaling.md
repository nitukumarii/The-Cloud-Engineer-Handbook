**Differentiate between horizontal and vertical scaling.**


| Horizontal Scaling (Scale Out/In)                              | Vertical Scaling (Scale Up/Down)                                |
| -------------------------------------------------------------- | --------------------------------------------------------------- |
| Add or remove more servers/instances                           | Increase or decrease resources (CPU, RAM) of an existing server |
| Improves capacity by distributing load                         | Improves capacity by making one server more powerful            |
| Better for high availability                                   | Single point of failure remains                                 |
| Can handle very high traffic                                   | Limited by maximum instance size                                |
| Usually requires a Load Balancer                               | No load balancer required                                       |
| Example: Increase EC2 instances from 2 to 5 using Auto Scaling | Example: Change EC2 from t3.medium to t3.xlarge                 |
