# Describe a Major P1 Production Incident - Certificate Expiry Issue (STAR)

## Situation


While working as an SRE at Mastercard, we faced a P1 incident where a production certificate used for secure communication with an external partner had expired, causing certificate validation failures and transaction processing issues.

The monitoring alerts showed increased transaction failures, and some file transfer requests were failing because the application was unable to establish secure communication with the external system.

---

## Task

As the SRE on-call, my responsibility was to identify the impact, coordinate with the certificate management and application teams, restore the service quickly, and ensure secure communication was restored.

---

## Action

I acknowledged the P1 alert and joined the incident bridge.

I first checked Dynatrace dashboards to understand the impact, such as the affected service, transaction failures, error rate, and when the issue started.

I then reviewed Splunk logs to identify the exact error details and found certificate validation failures and SSL communication errors while connecting with the external system.

I verified the certificate details, including expiry date and validity, and confirmed that the certificate had expired, which was causing the communication failure.

I coordinated with the certificate management and application teams to renew and deploy the updated certificate through the required change process.

After the certificate update, I validated application connectivity, monitored transaction success rate, application health, and logs to confirm that the issue was resolved.

---

## Result

The certificate was successfully renewed and deployed, transaction processing recovered, and the service was restored within the SLA.

As a preventive measure, we improved certificate expiry monitoring, renewal tracking, and alerting processes to avoid similar incidents in the future.
