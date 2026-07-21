# Last Application Worked On - Flow, Upstream and Downstream

## Answer

The last application I worked on at Mastercard was a **payment file transfer platform built around IBM Sterling B2B Integrator**.

The main purpose of the platform was to securely exchange payment files between Mastercard and partner banks. Mastercard acted as a mediator between the consumer systems and banking partners.

## High-Level Application Flow

```text
Consumer / Client System
        |
        ↓
Mastercard Payment Platform
(IBM Sterling + Application Services)
        |
        ↓
Partner Bank Systems

The upstream systems were the consumer applications or client systems that generated and sent payment files or transaction requests to our platform.

The downstream systems were the partner bank systems where Mastercard forwarded the payment files for processing and received the processing status.

Our application handled the file exchange, validation, routing, and tracking of transaction status. Based on the response from downstream banks, the status was communicated back to the consumer system.

As an SRE, my responsibility was to ensure the platform availability, monitor transaction flows, troubleshoot failures, analyze logs, and handle production incidents related to file transfer delays, failed transactions, or connectivity issues.
