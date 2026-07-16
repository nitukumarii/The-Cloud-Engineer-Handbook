# Monitoring Metrics to Remember

## Application Outage Metrics

Availability → Errors → Latency → Traffic → Resources → Dependencies

- Availability: Service UP/DOWN, health checks, load balancer health
- Errors: 4xx/5xx errors, failed transactions, exceptions
- Latency: Response time, P95/P99 latency
- Traffic: Requests per second, transaction volume
- Resources: CPU, memory, disk, network
- Dependencies: Database, cache, message queue, external APIs


## Application Slowness Metrics

Latency → Traffic → Resources → Dependencies → Application

- Latency: Average response time, P95/P99 latency
- Traffic: Requests per second, sudden traffic increase
- Resources: CPU, memory, disk I/O, network latency
- Dependencies: Database query time, cache response time, API latency
- Application: Slow API calls, logs, exceptions, thread usage


Quick memory:

**Outage = Is it DOWN? → Errors → Where is failing?**

**Slowness = Why is it SLOW? → Latency → Bottleneck**
