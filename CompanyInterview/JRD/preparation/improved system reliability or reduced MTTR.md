## Describe a time when you improved system reliability or reduced MTTR.

One initiative that significantly improved system reliability and reduced our Mean Time to Recovery (MTTR) was improving our SSL certificate management process.

In our production environment, we were responsible for managing more than **2,200 SSL certificates** across multiple applications and environments. Earlier, certificate expiry tracking involved significant manual effort, which increased the risk of missing renewals and could potentially lead to production outages.

To improve reliability, I worked on automating the certificate monitoring process. I developed a solution that periodically checked certificate expiry dates, generated reports for certificates nearing expiration, and notified the operations team well before the renewal window. This allowed us to plan renewals proactively instead of reacting to last-minute alerts.

In parallel, we standardized the certificate renewal procedure by creating detailed runbooks and validation checklists. This ensured every engineer followed the same process during renewals and reduced the chances of configuration errors.

As a result, we significantly reduced manual effort, eliminated unexpected certificate expiry incidents in production, and improved the team's response time whenever certificate-related issues occurred. The standardized process also reduced MTTR because engineers could quickly identify affected certificates, follow documented recovery steps, and restore services without unnecessary delays.

This experience reinforced that improving reliability isn't only about resolving incidents quickly; it's also about automating repetitive tasks, standardizing operational processes, and preventing incidents before they impact customers.
