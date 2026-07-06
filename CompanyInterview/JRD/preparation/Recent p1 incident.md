## P1 Production Incident – File Transfer Latency in IBM Sterling Integrator

### Situation

During a planned production deployment of IBM Sterling Integrator, a new application feature was released. Shortly after the deployment, we received multiple alerts indicating that file transfers were taking significantly longer than expected. At the same time, the business team reported that one of the partner banks in Denmark was experiencing delays in receiving transaction files. Since it was impacting production transactions, the incident was immediately classified as a **P1 (Priority 1)** incident.

---

### Impact

The issue affected the **Denmark region** and delayed the transfer of transaction files between Mastercard and the destination bank. This impacted the bank's file processing and settlement activities, making it a business-critical issue requiring immediate resolution.

---

### Investigation

As the SRE on call, my first responsibility was to determine whether the issue was infrastructure-related or application-related.

I followed a structured troubleshooting approach:

- Checked **Dynatrace** to analyze application response time, service flow, and identify whether the latency was affecting all regions or only a specific region.
- Verified through **Splunk** logs for application errors and exceptions after the latest deployment.
- Confirmed that the issue was isolated to the **Denmark region** and was not impacting other production environments.
- Checked Kubernetes pod health using:
  ```bash
  kubectl get pods
  kubectl describe pod <pod-name>
  kubectl logs <pod-name>
  ```
- Verified node health:
  ```bash
  kubectl get nodes
  ```
- Checked CPU and memory utilization to rule out infrastructure resource issues.
- Verified there were no networking or database connectivity issues.

Since the infrastructure was healthy and the issue started immediately after deployment, the investigation shifted toward the newly deployed application code.

---

### Root Cause

After analyzing the application logs and working with the development team, we identified that the newly introduced feature contained a bug where a database query was repeatedly executed inside a loop. This significantly increased database calls, resulting in higher application response times and delayed processing of file transfers for the affected region.

---

### Resolution

To restore the service as quickly as possible, we initiated the rollback process to the previous stable application version deployed on the EKS cluster.

After the rollback:

- Verified that all application pods were healthy.
- Monitored application response times in Dynatrace.
- Confirmed through Splunk that error logs had stopped.
- Validated successful file transfers with the business team.
- Continued monitoring the application until normal processing resumed.

The service was restored within the expected SLA, minimizing business impact.

---

### Prevention

After the incident, we conducted a Root Cause Analysis (RCA) and implemented several preventive measures:

- Added additional validation and testing for database-intensive features before production deployment.
- Enhanced monitoring dashboards and alerts for abnormal response times and database query spikes.
- Strengthened deployment validation during post-deployment health checks.
- Updated the deployment checklist to include performance validation before completing production releases.
- Shared the RCA with development and operations teams to prevent similar issues in future releases.
