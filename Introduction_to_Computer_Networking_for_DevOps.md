# Networking in DevOps
Networking in DevOps is the practice of designing, configuring, automating, and monitoring the connectivity between systems, services, and environments so that applications can communicate reliably, securely, and efficiently throughout the software delivery lifecycle. It encompasses fundamentals like IP addressing, routing, DNS, load balancing, firewalls, and TLS; cloud constructs such as VPCs/VNets, subnets, NAT, peering, and private endpoints; and platform layers including container/Kubernetes networking, service discovery, and network policies. Its goal is to enable scalable architectures, enforce security and compliance, support CI/CD pipelines, and reduce incident risk by ensuring predictable, observable, and resilient service-to-service communication.

---
# What is Network 
 A Network is a collection of interconnected devices like computers , servers , switches and routers that communicate with each other to share resources , data and service .
 <img width="2556" height="1264" alt="image" src="https://github.com/user-attachments/assets/ed73c903-a075-4c39-b7c4-0786c2491592" />

# Satellite System 
<img width="1456" height="695" alt="image" src="https://github.com/user-attachments/assets/d91a1f98-dfd0-4ee4-9473-86685dd5dd3b" />


# The Solution Underwater Cable Map (website link - https://www.submarinecablemap.com/)
 <img width="2611" height="1627" alt="image" src="https://github.com/user-attachments/assets/7770bf22-b23f-492a-9d37-94d084ade5cc" />


# But Now We Have Starlink (website link - https://www.starlink.com/us/technology)
<img width="3029" height="1293" alt="image" src="https://github.com/user-attachments/assets/f110c809-b6d5-4022-a9ba-d1a0f2bf1dda" />

# How Internets Works 
- The Internet Works by connecting millions of devices worldwide through a system of network .
-  when you request a website your device sends data and passes through routers .
-  And DNS (Domain Name System ) to locate the server and the server responds with the requested data using protocols like TCP/IP

<img width="2602" height="869" alt="image" src="https://github.com/user-attachments/assets/c2c4941c-74a7-45de-a655-2d3488276733" />

 ### Here’s is the Details flow
 1. User (Your Device) :
    - when You type a URL like www.google.com in your browser.
    -  Your Browser prepares a request (HTTP/HTTPS) and needs the severs ip address to send it
 2. Router (Home/Office) :
    - Your Request first goes to your local router.
    - Then router :
    - assign your private IP address like 192.168.x.x
    - Uses NAT (Network Address Translation) to map your private IP to public (Given by ISP)
    - This is Necessary because private IPs can’t used directly on the Internet 
 3.  ISP (Interest Service Provider) :
   - The Request then goes to your ISP (Jio ,BSNL,VI).
   - The ISP does two main jobs
   - 1 Provides You a Public IP address to access the internet
   - 2 Forward your request into larger internet infrastructure 
 
 4. DNS (Domain Name System) :
   - Your ISP checks if it already know the ip www.google.com
   - The DNS translates the domain name into an IP address (like 142.250.190.78) so computers can locate the server.
 5.  Web Server (Destination Server)
   - The Packets finally reach Google Data Centers
   - Google Servers receive the request and prepare a respons (search home page html)
 6. Return to user using same path      
