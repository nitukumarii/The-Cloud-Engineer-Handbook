## Scenario 1: Temporary CPU Spike (No Production Impact)

A CPU utilization spike to **100%** does **not always indicate a production incident**. The first step is to determine whether the spike is **temporary (transient)** or **sustained**.

### Common Reasons for a Temporary CPU Spike

- A scheduled **cron job** starts.
- A **backup** process begins.
- **Log rotation** or an antivirus/security scan is running.
- A sudden burst of **legitimate user traffic**.
- A short **JVM Garbage Collection (GC)** cycle.
- A container or application startup process.
- Scheduled monitoring or housekeeping tasks.

### Observation

After a few seconds:

- CPU utilization returns to **20–30%**.
- Application response time remains normal.
- No increase in error rates.
- No customer complaints.
- No alerts indicating service degradation.

### Conclusion

- ✅ CPU utilization briefly reached **100%**.
- ✅ The spike was **transient**.
- ❌ There is **no production incident**.
- ✅ Continue monitoring to ensure CPU returns to normal.
- ✅ Verify whether the activity was expected (cron job, backup, deployment, GC, etc.).
- ✅ No immediate mitigation is required unless the spikes become frequent or start affecting application performance.

> **Senior SRE Approach:** Never assume that a CPU alert automatically means there is an incident. Always validate whether the spike is temporary or sustained and correlate it with application health, response times, error rates, and user impact before initiating production troubleshooting.
