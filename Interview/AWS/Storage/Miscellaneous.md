# AWS Security – Deep Dive (Senior SRE Interview Style)

---

## 1. IAM Privilege Escalation via AssumeRole

### Q: Explain how privilege escalation happens in AWS IAM in real systems.

### A:

#### What actually happens (not theory)

In AWS, **permissions are not just attached—they are composable**.

If a role has:

* `sts:AssumeRole` on another role
* And that target role has broader permissions

Then:

> You’ve created an indirect privilege escalation path.

#### Real-world chain:

1. App runs on EC2 with IAM role A
2. Role A has:

   ```
   sts:AssumeRole → RoleB
   ```
3. RoleB has:

   ```
   AdministratorAccess
   ```
4. Attacker gets EC2 access → queries metadata service → gets temporary creds
5. Calls:

   ```
   aws sts assume-role --role-arn RoleB
   ```
6. Now attacker is effectively admin

---

### Why this happens

Because IAM evaluation is:

> “Can this principal call this API?” — not “Should they indirectly become more powerful?”

AWS does NOT prevent:

* Role chaining
* Privilege amplification

That’s your job.

---

### Fix (practical, not textbook)

#### Immediate:

* Invalidate sessions (STS tokens live up to 12 hours)
* Remove `sts:AssumeRole` or restrict it

#### Structural Fix:

Use **condition keys**:

```
"Condition": {
  "StringEquals": {
    "aws:PrincipalArn": "expected-role"
  }
}
```

#### Critical Control:

* Disable IMDSv1 → move to IMDSv2

---

### Why IMDSv2 matters

IMDSv1:

* No authentication
* Any SSRF → credential theft

IMDSv2:

* Requires session token (PUT request)
* Breaks most SSRF-based attacks

---

## 2. SSRF → Credential Theft → Data Exfiltration

### Q: How does SSRF actually compromise AWS?

### A:

#### The core issue:

Your app can make HTTP calls → attacker controls URL

#### Attack path:

```
User input → backend fetch() → attacker URL → internal AWS metadata endpoint
```

Metadata endpoint:

```
http://169.254.169.254/latest/meta-data/iam/security-credentials/
```

Returns:

* Access key
* Secret key
* Session token

---

### Why this is dangerous

Because:

> IAM roles are assumed to be “safe” since they’re not exposed externally

But SSRF makes internal resources external.

---

### Real impact:

* Read S3 data
* Dump DynamoDB
* Trigger Lambdas
* Pivot further

---

### Fix

#### Immediate:

* Rotate IAM role credentials (force new session)
* Block metadata endpoint via:

  * iptables OR
  * VPC routing OR
  * proxy restrictions

#### Long-term:

1. **IMDSv2**
2. Deny outbound traffic except required:

   * Use VPC + NAT + egress filtering
3. Input validation is NOT enough

---

### Key SRE Insight:

> Security failure here is not SSRF — it’s unrestricted egress.

---

## 3. EKS Compromise via RBAC

### Q: What’s the most common real-world EKS security failure?

### A:

Not Kubernetes bugs — **RBAC misconfiguration**

---

### Attack reality:

Bad config:

```
ClusterRoleBinding:
  subjects:
    - kind: ServiceAccount
      name: default
  roleRef:
    kind: ClusterRole
    name: cluster-admin
```

Effect:

> Any pod = cluster admin

---

### Attack chain:

1. Attacker gets shell in any pod
2. Uses service account token
3. Calls Kubernetes API
4. Reads:

   * Secrets
   * ConfigMaps
5. Modifies deployments

---

### Why this happens

Because:

* Teams treat Kubernetes like VMs
* Ignore identity layer

---

### Fix

#### Immediate:

* Remove cluster-admin bindings
* Rotate service account tokens

#### Structural:

* Use **IRSA (IAM Roles for Service Accounts)**
* Separate:

  * node role
  * pod role

---

### Critical concept:

> Kubernetes security = API security, not network security

---

## 4. S3 Pre-Signed URL Abuse

### Q: Why are pre-signed URLs risky?

### A:

Because:

> They bypass authentication entirely

---

### Mechanics:

Pre-signed URL = signed request with:

* access key
* signature
* expiry

Anyone with URL = authorized

---

### Real issue:

* Logs leak URLs
* URLs cached
* Expiry too long (hours/days)

---

### Fix

#### Immediate:

* Change object or revoke key

#### Structural:

* Expiry ≤ 5 min
* Bind to IP (if possible)

---

### Important Insight:

> You cannot revoke a pre-signed URL — only invalidate underlying permission.

---

## 5. KMS Abuse (Decrypt Misuse)

### Q: How does KMS become a security risk?

### A:

KMS does NOT store data
It only protects keys

If IAM allows:

```
kms:Decrypt
```

Then:

> Any encrypted data can be decrypted

---

### Attack:

1. Attacker gets IAM access
2. Reads encrypted blob (S3, DB)
3. Calls KMS decrypt
4. Gets plaintext

---

### Why people miss this

They think:

> Encryption = security

Reality:

> Access to key = access to data

---

### Fix

#### Immediate:

* Disable key
* Re-encrypt data

#### Structural:

* Key policy must restrict:

  * who
  * from where
  * via which service

Example:

```
"Condition": {
  "StringEquals": {
    "kms:ViaService": "s3.region.amazonaws.com"
  }
}
```

---

## 6. CI/CD Pipeline Compromise

### Q: What’s the weakest point in cloud security?

### A:

> The pipeline — because it controls production.

---

### Real attack:

1. Developer token compromised
2. Push malicious code
3. Pipeline deploys automatically
4. Backdoor goes live

---

### Why dangerous

Because:

> It bypasses all runtime security

---

### Fix

#### Immediate:

* Stop pipeline
* Rollback deployment

#### Structural:

1. Require manual approval for prod
2. Restrict IAM:

   * pipeline role cannot be admin
3. Use artifact signing

---

### Key Insight:

> Production trust = pipeline trust

---

## 7. Malicious AMI Supply Chain Attack

### Q: Why is using public AMIs dangerous?

### A:

AMI = full OS snapshot

If compromised:

* hidden cron jobs
* reverse shells
* data exfiltration agents

---

### Attack:

1. Engineer uses public AMI
2. Deploys EC2
3. Attacker already has access

---

### Fix

#### Immediate:

* Terminate instances
* Rotate secrets

#### Structural:

* Use:

  * golden AMIs
  * EC2 Image Builder

---

### Key Insight:

> This is a supply chain attack, not misconfiguration

---

## 🔥 Final Senior-Level Takeaways

### 1. Identity is the perimeter

* IAM > Network security

### 2. Every permission must be justified

* Not just “works”

### 3. Assume compromise

* Design blast radius reduction

### 4. Logs are useless without action

* CloudTrail ≠ security
* Detection + response matters

### 5. Most breaches are:

* Misconfiguration
* Over-permission
* Lack of isolation

---

## 💡 How to Answer in Interview

Structure every answer like:

1. **How attack works (step-by-step)**
2. **Why system allowed it**
3. **Immediate containment**
4. **Long-term fix (design level)**

---


# AWS Security Architecture – Advanced Scenario (Senior SRE / Architect Level)

## Scenario Context

A financial institution is migrating to AWS with strict compliance requirements (PCI DSS, GDPR). The architecture includes:

* Multi-account setup using AWS Organizations
* Hybrid + multi-region deployment
* Services: EC2, Lambda, EKS, RDS, S3, API Gateway
* Security services: KMS, WAF, Shield, Macie
* DevSecOps pipelines

The system must enforce:

* Zero trust
* Least privilege
* End-to-end encryption
* Threat detection and automated remediation

---

# 1. IAM & ZERO TRUST

## Q1: How do you design IAM for zero trust in multi-account AWS?

### Answer

Zero trust means **no implicit trust based on network or identity location**. Every request must be authenticated, authorized, and verified.

### Implementation

* Use **AWS Organizations + SCPs**

  * SCPs act as *guardrails*, not permissions
  * Deny risky actions globally (e.g., disabling CloudTrail)

* Use **IAM Roles instead of users**

  * Short-lived credentials via STS
  * Federation with IdP (Azure AD / Okta)

* Enforce:

  * `aws:MultiFactorAuthPresent`
  * `aws:SourceIp`
  * `aws:PrincipalTag`

* Use **Attribute-Based Access Control (ABAC)**

  * Tag resources: `env=prod`
  * Match with IAM conditions

### Why

* Eliminates static credentials
* Reduces blast radius
* Enforces dynamic, contextual access

---

## Q2: How do you prevent IAM privilege escalation?

### Answer

Privilege escalation happens when a user can indirectly gain higher permissions.

### Controls

* Explicit deny on:

  * `iam:PassRole`
  * `iam:AttachRolePolicy`
  * `iam:PutRolePolicy`

* Restrict:

  * Role assumption (`sts:AssumeRole`)
  * Policy modifications

* Use **permissions boundaries**

* Monitor via:

  * CloudTrail
  * GuardDuty (detect anomalous IAM behavior)

### Why

IAM is the **primary control plane attack surface**. If compromised, all resources are exposed.

---

## Q3: S3 access only via CloudFront?

### Answer

### Implementation

* Use **CloudFront Origin Access Control (OAC)**
* Block public access on S3
* Bucket policy:

```json
{
  "Effect": "Allow",
  "Principal": {"Service": "cloudfront.amazonaws.com"},
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::bucket/*",
  "Condition": {
    "StringEquals": {
      "AWS:SourceArn": "arn:aws:cloudfront::<account-id>:distribution/<id>"
    }
  }
}
```

### Why

* Prevents direct S3 exposure
* Forces traffic through controlled edge layer

---

# 2. NETWORK SECURITY & ZERO TRUST

## Q4: Zero trust network in AWS?

### Answer

### Design

* No flat networks
* Every service authenticated and authorized

### Implementation

* Private subnets only

* No public IPs

* Use:

  * VPC endpoints (PrivateLink)
  * Service mesh (Istio in EKS)
  * mTLS between services

* API Gateway + WAF for ingress

### Why

Network location is not trusted. Identity + encryption is enforced.

---

## Q5: Prevent lateral movement?

### Answer

### Controls

* Micro-segmentation:

  * Security Groups per service
  * No wide CIDR rules

* Disable default SG rules

* Use:

  * NACLs for coarse filtering
  * VPC Flow Logs for detection

### Why

Attackers move laterally after compromise. Segmentation limits blast radius.

---

## Q6: Transit Gateway vs VPC Peering risks?

### Answer

### Transit Gateway

Pros:

* Centralized routing
* Scalable

Cons:

* Misconfiguration = wide access
* Harder to isolate routes

### VPC Peering

Pros:

* Simpler
* Explicit connectivity

Cons:

* Poor scalability
* No transitive routing

### Decision

* Use TGW with strict route tables + segmentation

---

# 3. DATA SECURITY

## Q7: Encryption at rest strategy?

### Answer

* Use **KMS-backed encryption**:

  * S3 SSE-KMS
  * RDS encryption
  * EBS encryption

* Separate keys:

  * Per environment
  * Per data classification

### Why

* Limits blast radius
* Enables audit and revocation

---

## Q8: Enforce encryption in transit?

### Answer

* TLS 1.2+ everywhere

* API Gateway:

  * Enforce HTTPS only

* ALB:

  * Redirect HTTP → HTTPS

* Internal:

  * mTLS (service mesh)

### Why

Prevents MITM and data leakage.

---

## Q9: Can root decrypt KMS data?

### Answer

Yes by default — unless restricted.

### Control

* Key policy must explicitly deny root:

```json
{
  "Effect": "Deny",
  "Principal": {"AWS": "arn:aws:iam::<account-id>:root"},
  "Action": "kms:Decrypt",
  "Resource": "*"
}
```

### Why

Root is powerful but should not bypass data protection controls.

---

# 4. THREAT DETECTION & INCIDENT RESPONSE

## Q10: Detect S3 data exfiltration?

### Answer

### Detection stack

* Macie → detects PII access
* CloudTrail → logs access
* GuardDuty → anomaly detection

### Response

* Trigger Lambda:

  * Revoke IAM session
  * Block IP
  * Lock bucket

### Why

Detection must be **near real-time + automated**

---

## Q11: Compromised Lambda?

### Answer

### Steps

1. Disable function
2. Revoke IAM role
3. Analyze logs (CloudWatch + X-Ray)
4. Rotate secrets

### Why

Lambda is stateless → fast containment is critical

---

## Q12: Security Hub + GuardDuty + Macie?

### Answer

* GuardDuty → threat detection
* Macie → data classification
* Security Hub → central aggregation

### Flow

1. Alert generated
2. EventBridge triggers
3. Lambda auto-remediation

---

# 5. DEVSECOPS

## Q13: Embed security in CI/CD?

### Answer

* SAST → code scanning

* DAST → runtime scanning

* IaC scanning → Terraform security

* Enforce:

  * No public S3
  * No open SG

### Why

Shift-left reduces production risk.

---

## Q14: Enforce compliance programmatically?

### Answer

* AWS Config rules
* SCP policies
* Audit via Security Hub

### Why

Manual compliance does not scale.

---

## Q15: Auto-remediate open security groups?

### Answer

* AWS Config rule detects violation
* EventBridge triggers Lambda
* Lambda removes `0.0.0.0/0`

### Why

Mean-time-to-remediation must be near zero.

---

# 6. ADVANCED SECURITY

## Q16: Secure Lambda accessing databases?

### Answer

* Use Secrets Manager
* Rotate credentials
* VPC-enabled Lambda
* IAM role with least privilege

### Why

Avoid hardcoded secrets and uncontrolled access.

---

## Q17: Prevent cross-account data leakage?

### Answer

* Restrict AssumeRole
* External ID enforcement
* Resource policies validation

### Why

Cross-account access is a major breach vector.

---

## Q18: If KMS is compromised?

### Answer

Layered defense:

* Application-level encryption
* Tokenization
* Data masking

### Why

Never rely on a single control layer.

---

# 7. INCIDENT SCENARIO

## Scenario:

DDoS attack + IAM compromise + RDS data access

---

## Immediate Response

1. Enable Shield Advanced + WAF rules
2. Rotate IAM credentials
3. Disable compromised roles
4. Isolate RDS
5. Enable audit logging

---

## Forensics

* CloudTrail logs
* VPC Flow Logs
* GuardDuty findings

---

## Prevention

* Zero trust IAM
* Strict SCPs
* No public DB access
* Continuous monitoring

---

# FINAL PRINCIPLES

* Assume breach
* Enforce least privilege
* Automate detection and response
* Use layered security (defense in depth)
* Prefer short-lived credentials over static

---

This is the level of depth expected from a **Senior SRE / Cloud Security Architect**—every decision justified by **risk reduction, scalability, and failure containment**.

# AWS Security Architecture – Senior SRE / Architect Deep Dive

---

# 1. ARCHITECTURE SCENARIO

A financial institution is migrating to AWS with strict compliance requirements (PCI DSS, GDPR). The system handles sensitive PII and financial transactions.

## Architecture Design

### Multi-Account Strategy

* AWS Organizations with accounts:

  * Security Account (central logging, GuardDuty, Security Hub)
  * Shared Services Account (CI/CD, IAM federation)
  * Workload Accounts (Prod, Staging, Dev)

### Hybrid + Multi-Region

* On-prem connected via VPN / Direct Connect
* Active-active multi-region (e.g., us-east-1, eu-west-1)
* Failover via Route53 health checks

### Core Services

* Compute: EC2, Lambda, EKS
* Storage: S3, RDS
* API Layer: API Gateway + ALB
* Secrets: Secrets Manager
* Encryption: KMS

### Security Services

* WAF + Shield → edge protection
* GuardDuty → threat detection
* Macie → PII discovery
* Security Hub → centralized posture
* CloudTrail + Config → audit

---

# 2. IAM & ZERO TRUST

## Q1: How do you implement Zero Trust IAM in multi-account AWS?

### Answer

Zero trust means **no implicit trust even within internal networks**. Every request is verified based on identity, context, and policy.

### Implementation

1. Eliminate IAM users

   * Use SSO federation (IdP → STS AssumeRole)
   * Short-lived credentials only

2. Use SCPs at org level

   * Deny actions like:

     * Disable CloudTrail
     * Create root access keys

3. Implement ABAC

   * Tag resources: `env=prod`
   * IAM condition:

     ```
     "Condition": {
       "StringEquals": {
         "aws:ResourceTag/env": "prod"
       }
     }
     ```

4. Enforce MFA + device conditions

### Why

* Static credentials are primary breach vector
* Context-based access reduces misuse
* Limits lateral movement

---

## Q2: How do you prevent IAM privilege escalation?

### Answer

### Attack Paths

* Passing roles (`iam:PassRole`)
* Attaching admin policies
* Creating new roles

### Controls

1. Explicit Deny:

```
{
  "Effect": "Deny",
  "Action": [
    "iam:PassRole",
    "iam:AttachRolePolicy",
    "iam:PutRolePolicy"
  ],
  "Resource": "*"
}
```

2. Permissions Boundaries

* Restrict maximum privilege possible

3. Monitor:

* CloudTrail → API activity
* GuardDuty → anomalous IAM behavior

### Why

IAM is control plane. If compromised → full environment takeover.

---

## Q3: Restrict S3 access via CloudFront only?

### Answer

### Implementation

* Enable OAC (Origin Access Control)
* Block public access on S3
* Bucket policy:

```
{
  "Effect": "Allow",
  "Principal": {"Service": "cloudfront.amazonaws.com"},
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::bucket/*",
  "Condition": {
    "StringEquals": {
      "AWS:SourceArn": "arn:aws:cloudfront::<account>:distribution/<id>"
    }
  }
}
```

### Why

* Eliminates direct S3 exposure
* Prevents bypass of WAF/CDN

---

# 3. NETWORK SECURITY

## Q4: How do you implement Zero Trust network architecture?

### Answer

### Design Principles

* No trust based on IP or subnet
* Every service authenticated

### Implementation

1. Private subnets only
2. No public IPs for workloads
3. Use VPC Endpoints (PrivateLink)
4. Use mTLS (service mesh in EKS)
5. API Gateway as entry point

### Why

Network perimeter is no longer reliable → identity becomes boundary.

---

## Q5: Prevent lateral movement?

### Answer

### Implementation

* Security Groups per service (not shared)

* Deny wide CIDR ranges

* Disable default SG

* Add:

  * VPC Flow Logs
  * NACLs for coarse filtering

### Why

After initial breach, attacker spreads laterally. Segmentation limits blast radius.

---

## Q6: Transit Gateway vs VPC Peering risk?

### Answer

### Transit Gateway

* Risk: central misconfig exposes all VPCs
* Requires strict route isolation

### VPC Peering

* Risk: scaling complexity
* Safer for small environments

### Decision

Use TGW with:

* Dedicated route tables per domain
* No default route propagation

---

# 4. DATA SECURITY

## Q7: Encryption at rest strategy?

### Answer

* Use KMS for:

  * S3 (SSE-KMS)
  * RDS
  * EBS

* Separate keys:

  * Per environment
  * Per data sensitivity

### Why

* Key compromise blast radius reduced
* Enables audit and revocation

---

## Q8: Enforce encryption in transit?

### Answer

* API Gateway → HTTPS only
* ALB → redirect HTTP → HTTPS
* Internal services → mTLS

### Why

Prevents MITM and credential leakage.

---

## Q9: Can root decrypt KMS data?

### Answer

Yes unless explicitly denied.

### Control

```
{
  "Effect": "Deny",
  "Principal": {"AWS": "arn:aws:iam::<account>:root"},
  "Action": "kms:Decrypt"
}
```

### Why

Root must not bypass data protection.

---

# 5. THREAT DETECTION & RESPONSE

## Q10: Detect S3 data exfiltration?

### Answer

### Detection Stack

* Macie → PII detection
* GuardDuty → anomaly detection
* CloudTrail → audit logs

### Response Flow

1. EventBridge rule triggers
2. Lambda:

   * Revoke IAM session
   * Block IP
   * Lock bucket

### Why

Manual response is too slow → must be automated.

---

## Q11: Compromised Lambda?

### Answer

### Steps

1. Disable function
2. Revoke IAM role
3. Rotate secrets
4. Analyze logs

### Why

Lambda scales fast → attack spreads quickly.

---

## Q12: Security Hub + GuardDuty + Macie integration?

### Answer

* GuardDuty → detects threat
* Macie → identifies sensitive data
* Security Hub → aggregates findings

### Flow

Event → EventBridge → Lambda remediation

---

# 6. DEVSECOPS

## Q13: Embed security in CI/CD?

### Answer

* SAST (code scanning)

* IaC scanning (Terraform)

* DAST (runtime testing)

* Enforce:

  * No public S3
  * No open ports

### Why

Fixing in production is costly.

---

## Q14: Enforce compliance programmatically?

### Answer

* AWS Config rules
* SCPs for guardrails
* Security Hub for reporting

### Why

Manual audits don’t scale.

---

## Q15: Auto-remediate open security groups?

### Answer

1. Config detects violation
2. EventBridge triggers Lambda
3. Lambda removes rule

### Why

Reduce exposure window to seconds.

---

# 7. ADVANCED SECURITY

## Q16: Secure Lambda accessing databases?

### Answer

* Use Secrets Manager
* IAM least privilege
* VPC-enabled Lambda

### Why

Prevents credential leakage and over-permission.

---

## Q17: Prevent cross-account data leakage?

### Answer

* Restrict AssumeRole
* Use External ID
* Validate resource policies

### Why

Cross-account trust is common breach vector.

---

## Q18: If KMS is compromised?

### Answer

Mitigation layers:

* Application-level encryption
* Tokenization
* Data masking

### Why

Single layer failure must not expose data.

---

# 8. INCIDENT SCENARIO

## Scenario

DDoS + IAM compromise + RDS data access

---

## Immediate Response

1. Enable WAF rules + rate limiting
2. Activate Shield Advanced
3. Revoke IAM credentials
4. Disable compromised roles
5. Isolate RDS

---

## Containment

* Block attacker IPs
* Rotate all secrets
* Restrict network access

---

## Forensics

* CloudTrail logs
* VPC Flow Logs
* GuardDuty findings

---

## Long-Term Prevention

* Zero trust IAM
* Strict SCP enforcement
* Continuous monitoring
* No public DB exposure

---

# FINAL PRINCIPLES

* Assume breach
* Minimize blast radius
* Automate detection and response
* Prefer short-lived credentials
* Defense in depth over single controls

---

This reflects how a senior engineer designs systems:
Every control is mapped to a **specific threat model**, not best practice checklists.
