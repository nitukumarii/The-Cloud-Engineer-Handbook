# Last Application Worked On - Flow, Upstream and Downstream

## Answer

The last application I worked on at Mastercard was a **payment file transfer platform built around IBM Sterling B2B Integrator**.

The platform was responsible for securely transferring payment files between consumer systems and partner banks. Mastercard acted as a mediator, receiving payment files from consumers, processing and routing them, and forwarding them to the respective partner banks.

The high-level flow was:

```text
Consumer / Client System
        |
        ↓
Mastercard Payment Platform
(IBM Sterling + Application Services)
        |
        ↓
Partner Bank Systems


The upstream systems were the consumer or client applications that generated and sent payment files or transaction requests to the Mastercard platform.

The downstream systems were the partner bank systems where Mastercard forwarded the payment files for processing and received the transaction status response.

The application handled activities like secure file transfer, validation, routing, transaction tracking, and communicating the final transaction status back to the consumer system.

As an SRE, my role was to maintain production reliability by monitoring application health, analyzing logs using Splunk, monitoring performance using Dynatrace, troubleshooting file transfer failures, handling P1/P2 incidents, supporting deployments, and automating repetitive tasks using Bash and Python.

The common production issues we handled included file transfer delays, failed transactions, application latency, deployment issues, pod failures, certificate-related issues, and downstream connectivity problems.

The overall goal was to maintain a highly available, reliable, and secure payment processing platform while minimizing downtime and reducing MTTR.
