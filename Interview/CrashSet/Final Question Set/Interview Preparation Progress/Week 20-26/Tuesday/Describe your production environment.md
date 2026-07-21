## Production Environment

The production environment I supported at Mastercard was a payment file transfer platform built around **IBM Sterling B2B Integrator**, which was responsible for securely exchanging payment files between Mastercard and partner banks.

Alongside IBM Sterling, the platform included **Java Spring Boot**-based backend services running on **AWS EKS**, **React** frontend applications, databases, and integrations with multiple downstream banking systems, making it a **distributed system**.

> **Note:** IBM Sterling itself was **not** built using Spring Boot or React. Those technologies were used by the surrounding applications and services integrated with the Sterling platform.
