
---

### 1️⃣ Your application is running, but users cannot access it from the browser. How do you debug?

First, I confirm whether the issue is network-related or application-related.

I check:
- Whether the application process is running and listening on the expected port  
- Whether the port is reachable from outside using curl or telnet  
- Firewall or security group rules for inbound access  
- Load balancer health and routing  
- DNS resolution and IP mapping  

This layered approach helps isolate exactly where traffic is getting blocked.

---

### 2️⃣ The app works on the server but not from outside. What could be wrong?

If it works locally but not externally, it’s usually a network exposure issue.

Possible causes:
- Application is bound to localhost instead of all interfaces  
- Firewall or security group blocks inbound traffic  
- Missing public IP or incorrect routing  
- Port not opened at the cloud or OS level  

The app is fine — access is restricted.

---

### 3️⃣ Same service works in dev but fails in production. What do you compare first?

I compare the **network and security configurations**, not the code.

Specifically:
- Security groups and firewall rules  
- Subnet type (public vs private)  
- Load balancer configuration  
- DNS and TLS settings  

Production environments are more restrictive, so differences usually exist there.

---

### 4️⃣ Traffic suddenly drops to zero, but servers are healthy. How do you investigate?

If servers are healthy, traffic is likely blocked upstream.

I check:
- Load balancer target health and routing rules  
- Recent DNS or WAF changes  
- Firewall or network ACL updates  
- Route table changes  

A zero-traffic issue is almost always a networking or routing problem.

---

### 5️⃣ Website works sometimes and fails randomly. What network issues come to mind?

Intermittent failures usually indicate:
- One or more unhealthy backend servers  
- Load balancer health check misconfiguration  
- Network instability or packet loss  

I check backend health and ensure all targets behave consistently.

---

### 6️⃣ Load balancer is healthy, but backend servers are not receiving traffic. Why?

Possible reasons include:
- Backend security group doesn’t allow traffic from the load balancer  
- Wrong port configured in the target group  
- Application not listening on the expected port  

LB health alone doesn’t guarantee traffic flow.

---

### 7️⃣ DNS is resolving correctly, but users still can’t access the app. What next?

DNS resolution only confirms name-to-IP mapping.

Next, I verify:
- Network reachability to the IP  
- Open ports  
- Firewall rules  
- Application responsiveness  

DNS success does not mean application availability.

---

### 8️⃣ Application works on HTTP but not on HTTPS. What could be the reason?

Common causes are:
- SSL certificate misconfiguration  
- Expired or invalid certificate  
- Incorrect HTTPS listener or port  
- TLS policy mismatch  

HTTPS issues are usually certificate or listener related.

---

### 9️⃣ Service is accessible internally but not publicly. Where do you check?

I check:
- Subnet type and routing  
- Internet Gateway attachment  
- Public IP assignment  
- Firewall or security group rules  

Internal access confirms the app works; public access is missing.

---

### 🔟 One specific region cannot access the app, while others can. Why?

Likely causes:
- Geo-blocking rules  
- CDN edge issues  
- Region-specific routing problems  

Since other regions work, the issue isn’t with the core application.

---

### 1️⃣1️⃣ After deployment, the app becomes unreachable. Network or app issue?

I review deployment changes:
- Port or binding changes  
- Firewall updates  
- Load balancer config changes  

Logs help decide quickly whether traffic reaches the app or not.

---

### 1️⃣2️⃣ Firewall rules were updated, and the app went down. How do you debug?

I:
- Compare old and new rules  
- Verify inbound and outbound traffic  
- Check missing ports or source ranges  

Firewall misconfigurations often block traffic silently.

---

### 1️⃣3️⃣ A new port was opened, but traffic is still blocked. What could be missing?

Possible gaps:
- OS-level firewall not updated  
- Application not listening on the port  
- Network ACL blocking traffic  
- Load balancer not configured for that port  

Ports must be opened at every layer.

---

### 1️⃣4️⃣ Latency suddenly increases, but CPU and memory are normal. What do you check?

I check:
- Network latency and packet drops  
- Load balancer response time  
- Database network latency  

High latency with low resource usage usually indicates a network issue.

---

### 1️⃣5️⃣ Users report slow responses only during peak traffic. Possible network causes?

Common causes:
- Bandwidth saturation  
- Connection limits on load balancer or backend  
- Network throttling  

Peak traffic exposes network bottlenecks.

---

### 1️⃣6️⃣ Application cannot connect to the database. Where do you start?

I start with networking:
- DNS resolution of DB endpoint  
- Port connectivity  
- Security group rules  
- Network ACL  

Credentials are checked only after network validation.

---

### 1️⃣7️⃣ Multiple services communicate internally. One service stops responding. Why?

Possible reasons:
- Service crash  
- Port change  
- Firewall or network policy update  
- DNS issues  

Internal communication depends heavily on stable networking.

---

### 1️⃣8️⃣ How do you trace a request from user to database?

I trace each hop:
User → DNS → Load Balancer → Application → Internal Network → Database

At each step, I verify connectivity, logs, and latency.

---

### 1️⃣9️⃣ Network changes were made manually in production. What risks does this introduce?

Risks include:
- No rollback  
- Human error  
- Configuration drift  
- Lack of audit trail  

Manual changes in production are always risky.

---

### 2️⃣0️⃣ How do you confirm whether an issue is network-related or application-related?

I check:
- Whether traffic reaches the application  
- Application logs  
- Network connectivity  

If logs show no requests, it’s a network issue.

---

## 🔥 BONUS: 10 ADVANCED / SENIOR-LEVEL QUESTIONS

---

### 2️⃣1️⃣ How would you design a highly available production network?

I design with:
- Multiple availability zones  
- Load balancers  
- Redundant routing  
- Health checks  

High availability means no single point of failure.

---

### 2️⃣2️⃣ One AZ goes down. How does traffic continue flowing?

Traffic is routed by the load balancer to healthy AZs.  
Auto-scaling replaces failed instances automatically.

---

### 2️⃣3️⃣ How do you debug intermittent packet loss issues?

I analyze:
- Network metrics  
- Load balancer statistics  
- Instance network limits  

Packet loss requires monitoring and correlation.

---

### 2️⃣4️⃣ What network metrics are most important in production?

Key metrics:
- Latency  
- Packet loss  
- Throughput  
- Error rate  

These directly affect user experience.

---

### 2️⃣5️⃣ How do you handle zero-downtime network changes?

I use:
- Blue-green routing  
- Gradual rollouts  
- Health checks  
- Fast rollback  

Never change everything at once.

---

### 2️⃣6️⃣ Cloud bill spikes due to data transfer. How do you investigate?

I analyze:
- Cross-AZ traffic  
- Public data egress  
- Chatty internal services  

Network design impacts cost heavily.

---

### 2️⃣7️⃣ How do you secure service-to-service communication?

I use:
- Private networking  
- TLS encryption  
- Strict firewall rules  

Security without breaking communication.

---

### 2️⃣8️⃣ How would you debug networking issues in Kubernetes?

I check:
- Pod-to-pod connectivity  
- Service endpoints  
- Network policies  
- CNI logs  

Kubernetes networking failures are usually configuration-related.

---

### 2️⃣9️⃣ What are common networking mistakes you’ve seen?

- Overly open firewall rules  
- No monitoring  
- Manual production changes  
- Poor documentation  

Most outages are avoidable.

---

### 3️⃣0️⃣ How do you balance security and performance in network design?

I apply:
- Least privilege access  
- Efficient routing  
- Caching where needed  

Security and performance must coexist.

---

## ✅ Final Note

Interviewers don’t want commands —  
They want **clear thinking, correct order, and confidence**.

If you can explain networking like this, you’re interview-ready.
