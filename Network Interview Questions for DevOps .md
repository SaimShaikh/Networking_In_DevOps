

---

### 1️⃣ Your application is running, but users cannot access it from the browser. How do you debug?

First, I don’t panic — I break it down layer by layer.

I check:
- Is the application process running?
- Is the service listening on the correct port (`netstat` / `ss`)?
- Is the firewall or security group allowing inbound traffic?
- Is DNS resolving to the correct IP?
- Is the load balancer forwarding traffic properly?

Most of the time, the issue is **network rules**, not the app.

---

### 2️⃣ The app works on the server but not from outside. What could be wrong?

This usually means:
- The app is bound to `localhost` instead of `0.0.0.0`
- Firewall / Security Group blocks inbound traffic
- Port is open on server but not on cloud firewall
- NAT or routing issue

Classic mistake: app runs fine locally, but no public access.

---

### 3️⃣ Same service works in dev but fails in production. What do you compare first?

I compare:
- Security groups / firewall rules
- Subnet (public vs private)
- Load balancer config
- DNS records
- TLS / HTTPS setup

Dev is usually open and relaxed. Prod is strict — that’s where things break.

---

### 4️⃣ Traffic suddenly drops to zero, but servers are healthy. How do you investigate?

I check:
- Load balancer target health
- DNS records (TTL, recent changes)
- Firewall or WAF changes
- Route table changes

If servers are healthy but traffic is zero, traffic is getting blocked **before** reaching them.

---

### 5️⃣ Website works sometimes and fails randomly. What network issues come to mind?

Random failures usually mean:
- Load balancer health check misconfiguration
- One backend instance is unhealthy
- Intermittent DNS issues
- Packet loss or flaky network

If one bad server exists, users randomly hit it.

---

### 6️⃣ Load balancer is healthy, but backend servers are not receiving traffic. Why?

Possible reasons:
- Wrong target group port
- Security group doesn’t allow LB → backend traffic
- Backend service not listening on expected port
- Health checks pass, but routing rules are wrong

LB being “healthy” doesn’t mean traffic is flowing correctly.

---

### 7️⃣ DNS is resolving correctly, but users still can’t access the app. What next?

DNS only gives IP — it doesn’t guarantee access.

Next checks:
- Is the IP reachable (`ping`, `curl`)?
- Is port open?
- Firewall / security group
- Application logs

DNS success ≠ application success.

---

### 8️⃣ Application works on HTTP but not on HTTPS. What could be the reason?

Common reasons:
- SSL certificate not attached correctly
- Expired or invalid certificate
- Wrong TLS policy
- Application not listening on HTTPS port

HTTPS issues are usually **certificate or listener problems**.

---

### 9️⃣ Service is accessible internally but not publicly. Where do you check?

This screams **network exposure issue**.

I check:
- Is it in a private subnet?
- Is there an Internet Gateway?
- Is NAT / routing correct?
- Is public IP assigned?

Internal access means app is fine — exposure is missing.

---

### 🔟 One specific region cannot access the app, while others can. Why?

Possible causes:
- Geo-blocking rules
- CDN edge issues
- Region-specific DNS
- ISP routing problems

If only one region fails, it’s rarely the app.

---

### 1️⃣1️⃣ After deployment, the app becomes unreachable. Network or app issue?

I roll back mentally:
- Did ports change?
- Did service bind address change?
- Did firewall rules change?
- Did load balancer config change?

If deployment touched configs → could be both.  
Logs decide the winner.

---

### 1️⃣2️⃣ Firewall rules were updated, and the app went down. How do you debug?

I:
- Compare old vs new rules
- Check inbound and outbound both
- Look for missing ports
- Verify source CIDR blocks

Firewalls fail silently — logs matter.

---

### 1️⃣3️⃣ A new port was opened, but traffic is still blocked. What’s missing?

Classic:
- OS firewall still blocking
- App not listening on that port
- Security group updated but NACL blocks it
- Load balancer not updated

Opening a port in one place is never enough.

---

### 1️⃣4️⃣ Latency suddenly increases, but CPU and memory are normal. What do you check?

I check:
- Network latency
- Packet drops
- Load balancer response time
- Database network delay

High latency with low CPU = network bottleneck.

---

### 1️⃣5️⃣ Users report slow responses only during peak traffic. Network causes?

Likely:
- Bandwidth saturation
- Load balancer max connections
- Connection limits on backend
- Network throttling

Peak traffic exposes weak network design.

---

### 1️⃣6️⃣ Application cannot connect to the database. Where do you start?

I check:
- DB endpoint DNS
- Port open between app and DB
- Security group rules
- Network ACL
- Credentials last

Most DB issues are network, not passwords.

---

### 1️⃣7️⃣ Multiple services communicate internally. One service stops responding. Why?

Could be:
- Service down
- Port change
- Firewall rule added
- DNS record outdated

Microservices fail loudly — logs + network tracing help.

---

### 1️⃣8️⃣ How do you trace a request from user to database?

Step by step:
User → DNS → Load Balancer → App → Internal Network → DB

At each hop:
- Check logs
- Check latency
- Check failures

Never jump directly to conclusions.

---

### 1️⃣9️⃣ Network changes were made manually in production. Risks?

Huge risk:
- No rollback
- No audit trail
- Human error
- Inconsistent environments

Infrastructure should be code — always.

---

### 2️⃣0️⃣ How do you confirm network issue vs app issue?

Simple rule:
- If app works locally but not remotely → network
- If traffic reaches app but errors appear → app
- If logs show nothing → network

Logs never lie.

---

## 🔥 BONUS: 10 ADVANCED / SENIOR-LEVEL QUESTIONS

---

### 2️⃣1️⃣ How would you design a highly available production network?

- Multi-AZ setup
- Load balancer
- Auto scaling
- Redundant routes
- Health checks

Design for failure, not perfection.

---

### 2️⃣2️⃣ One AZ goes down. How does traffic continue?

- Load balancer routes to healthy AZ
- Auto scaling replaces instances
- DNS remains unchanged

If traffic stops, HA was fake.

---

### 2️⃣3️⃣ How do you debug intermittent packet loss?

I check:
- Network metrics
- ISP issues
- Instance network limits
- Load balancer stats

Packet loss is sneaky — monitoring saves lives.

---

### 2️⃣4️⃣ Important network metrics for production?

- Latency
- Packet loss
- Throughput
- Error rates
- Connection count

If you don’t measure it, you can’t fix it.

---

### 2️⃣5️⃣ How do you handle zero-downtime network changes?

- Blue-green routing
- Gradual rollout
- Health checks
- Fast rollback

Never change everything at once.

---

### 2️⃣6️⃣ Cloud bill spikes due to data transfer. How do you investigate?

I check:
- Cross-AZ traffic
- Public egress
- Chatty services
- Logs for abnormal usage

Networking mistakes are expensive.

---

### 2️⃣7️⃣ How do you secure service-to-service communication?

- Private networking
- TLS
- Security groups
- Identity-based access

Security without breaking performance.

---

### 2️⃣8️⃣ How would you debug networking issues in Kubernetes?

- Pod to pod connectivity
- Service endpoints
- Network policies
- CNI logs

K8s networking is just Linux networking with extra steps.

---

### 2️⃣9️⃣ Common networking mistakes you’ve seen?

- Open everything in prod
- No monitoring
- Manual changes
- No documentation

Experience is paid in outages.

---

### 3️⃣0️⃣ How do you balance security and performance?

- Least privilege
- Smart caching
- Private traffic
- Efficient routing

Secure doesn’t mean slow if designed right.

---
