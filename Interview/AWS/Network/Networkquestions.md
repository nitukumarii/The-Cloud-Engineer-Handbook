
# AWS Networking (SRE Interview Notes + Questions)

---

## 1. VPC Internal Communication

### Notes
- Traffic within same VPC uses **local route**
- Default route:
  - `VPC CIDR → local`
- No NAT Gateway or Internet Gateway involved

### Questions
- How does communication happen between subnets in same VPC?
- What is the purpose of the local route?
- Does internal traffic go through NAT Gateway?

---

## 2. NAT Gateway

### Notes
- Used for **private subnet → internet (outbound only)**
- Placed in **public subnet**
- Requires **Elastic IP**
- Cannot accept inbound traffic

### Not Used For
- Public → private communication
- Internal VPC traffic
- Direct inbound connections

### Questions
- What is NAT Gateway?
- Why is NAT Gateway placed in public subnet?
- Can NAT Gateway allow inbound traffic?
- Difference between NAT Gateway and Internet Gateway?
- Can public subnet use NAT Gateway?

---

## 3. Traffic Flow Scenarios

### Scenario 1: Web (Public) → DB (Private)

#### Notes
- Uses **local route**
- Uses **private IP**
- Controlled by **Security Groups**
- NAT Gateway NOT used

#### Questions
- How does web app connect to DB in private subnet?
- Is NAT Gateway used in this flow?

---

### Scenario 2: Private EC2 → Internet

#### Notes
- Flow:
  - EC2 → NAT Gateway → Internet Gateway → Internet

#### Questions
- How does private subnet access internet?
- What happens if NAT Gateway is removed?

---

### Scenario 3: Internet → Public EC2

#### Notes
- Flow:
  - Internet → Internet Gateway → EC2

#### Questions
- What makes a subnet public?
- How does Internet Gateway work?

---

### Scenario 4: Internet → Private DB

#### Notes
- Direct access not allowed
- Use:
  - Load Balancer
  - Bastion Host
  - API layer

#### Questions
- Can private subnet resources be accessed from internet?
- How do you securely access private DB?

---

## 4. Security Groups

### Notes
- Stateful
- Control instance-level traffic

### Example
- DB SG:
  - Allow inbound from Web SG on DB port
- Web SG:
  - Allow outbound to DB

### Best Practice
- Use **SG reference**, not IP

### Questions
- Difference between Security Group and NACL?
- Are Security Groups stateful?
- How to allow web → DB communication?

---

## 5. NACL (Network ACL)

### Notes
- Stateless
- Applied at subnet level
- Requires explicit allow rules for both inbound and outbound

### Questions
- Difference between NACL and Security Group?
- Why is NACL stateless?

---

## 6. Route Tables

### Notes
- Define traffic direction
- Key routes:
  - `VPC CIDR → local`
  - `0.0.0.0/0 → IGW` (public subnet)
  - `0.0.0.0/0 → NAT` (private subnet)

### Questions
- What is a route table?
- How does routing work in VPC?
- What happens if route table is misconfigured?

---

## 7. Internet Gateway (IGW)

### Notes
- Enables internet access for public subnet
- Required for inbound + outbound internet traffic

### Questions
- What is Internet Gateway?
- Difference between IGW and NAT Gateway?

---

## 8. Common Misconceptions

### Notes
- NAT Gateway handles all traffic ❌
- Public → private goes via NAT ❌
- Private subnet cannot access internet ❌
- IGW used for private subnet ❌

### Questions
- Does NAT Gateway handle internal traffic?
- Can private subnet directly access internet?

---

## 9. Troubleshooting (SRE Focus)

### Notes
Check in order:
1. Security Groups
2. NACL
3. Route Table
4. Instance status / port
5. DNS / IP

### Questions
- EC2 cannot access internet — why?
- Cannot connect to DB — what to check?
- NAT Gateway not working — possible issues?

---

## 10. Key Interview Statements

- “Internal VPC traffic uses local routing.”
- “NAT Gateway is only for outbound internet access from private subnets.”
- “Security Groups control access between application tiers.”
- “Private resources are not directly accessible from the internet.”

---
