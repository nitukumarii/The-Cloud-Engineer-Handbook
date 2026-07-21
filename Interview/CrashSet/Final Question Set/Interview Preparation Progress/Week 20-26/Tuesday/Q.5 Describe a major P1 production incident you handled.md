# Describe a Major P1 Production Incident - Certificate Expiry Issue (STAR)

## Situation

While working as an SRE at Mastercard, we faced a P1 incident where a production certificate used for secure communication with an external partner was approaching expiry and caused transaction failures.

The monitoring alerts showed increased failed transactions, and some file transfer requests were failing because the certificate validation was unsuccessful.

---

## Task

As the SRE on-call, my responsibility was to identify the impact, coordinate with the certificate management and application teams, restore the service quickly, and ensure secure communication was restored.

---

## Action

- I acknowledged the P1 alert and joined the incident bridge.
- I checked Dynatrace dashboards to understand the transaction impact and failure pattern.
- I reviewed Splunk logs and identified certificate validation errors during communication with the external system.
- I verified the certificate expiry details and confirmed that the issue was related to the expired/invalid certificate.
- I coordinated with the certificate management team and application team to deploy the renewed certificate.
- After the certificate update, I validated the application connectivity and monitored transaction success rate, logs, and application health.

---

## Result

The certificate was successfully renewed and deployed, transaction processing recovered, and the service was restored within the SLA.

As a preventive measure, we improved certificate expiry monitoring and renewal tracking to avoid similar incidents in the future.
