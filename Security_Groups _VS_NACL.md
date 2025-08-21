# Security Groups and NACL

# What is Security Groups
A Security Group (SG) in AWS is a virtual firewall that controls inbound and outbound traffic for EC2 instances, RDS, Load Balancers, and other AWS resources. Unlike a traditional hardware firewall, Security Groups operate at the instance level and are stateful, meaning if you allow traffic in, the response is automatically allowed out — no extra configuration is needed.

### Example Scenario
- Scenario 1: Web Server Deployment
   - You launch an EC2 instance to host a website.
   - You create a security group with:
     # Inbound Rules
     - Allow HTTP traffic on port 80 from 0.0.0.0/0 (anywhere)
     - Allow HTTPS traffic on port 443 from 0.0.0.0/0
     - Allow SSH traffic on port 22 only from your office IP, e.g., 203.0.113.25/32
     # Outbound Rules
     - Allow all outbound traffic (default)
- Outcome:
  - Anyone can access the website,
<img width="2806" height="828" alt="image" src="https://github.com/user-attachments/assets/c8592288-3f7e-4cec-b44f-c8feb02266f6" />

### Disadvantages of Security Groups
| **Disadvantage**               | **Explanation**                                                             |
| ------------------------------ | --------------------------------------------------------------------------- |
| **No Deny Rules**              | You can’t explicitly block traffic; you can only allow.                     |
| **Region/Resource Specific**   | Security Groups are region-specific and tied to the VPC.                    |
| **Limit on Rules**             | There’s a limit to the number of rules per group (default is **60 rules**). |
| **Complexity in Large Setups** | Managing many SGs in enterprise environments can get complicated.           |

---
## So what is the Solution on this issue 
# NACL (Network Access Control List)
In AWS (Amazon Web Services), a NACL (Network Access Control List) is a stateless firewall at the subnet level that controls inbound and outbound traffic.
It acts as an additional layer of security to control the flow of traffic in and out of one or more subnets within a VPC (Virtual Private Cloud).

### Example Scenario
- Scenario: Company with a Public Website and Internal Database
   - Imagine you are hosting a company application on AWS with the following setup:
   - Public Subnet: Hosts your web servers (accessible to users on the internet).
- Private Subnet: Hosts your database servers (only internal communication allowed).
   - Your NACL configuration can look like this:
   - Public Subnet NACL
- Inbound Rules:
  - Allow HTTP (80) and HTTPS (443) from 0.0.0.0/0 (anywhere).
  - Allow SSH (22) only from your office IP (e.g., 203.0.113.10/32) for management.
- Outbound Rules:
  - Allow all outbound traffic to 0.0.0.0/0 so the server can reach the internet for updates.
- Effect:
  - Anyone can visit your website.
  - Only your admin can SSH into the server.
  - No other inbound traffic is allowed, keeping it secure.

---

- Private Subnet NACL
- Inbound Rules:
  - Allow MySQL (3306) traffic only from the web server’s private IP range (e.g., 10.0.1.0/24).
- Outbound Rules:
  - Allow responses back to the web servers.
  - Block all internet access.
- Effect:
  - Database is protected from direct internet access.
  - Only the application server can communicate with it.
<img width="3101" height="1226" alt="image" src="https://github.com/user-attachments/assets/0d0118e3-f4d9-4b91-8b03-a8ef686c1bef" />

### Benefits of NACL

- Additional Layer of Security – Acts as a firewall for the subnet, adding protection beyond security groups.
- Stateless Filtering – You can explicitly allow or deny traffic, giving more granular control.
- Defense in Depth – Even if a security group is misconfigured, NACL rules can still block malicious traffic.
- Subnet-Wide Protection – Applies rules to all resources in that subnet without needing per-instance configuration.
