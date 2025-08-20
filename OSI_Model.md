<img width="690" height="747" alt="image" src="https://github.com/user-attachments/assets/336eb36a-946b-46df-b3b7-ec8b62e91467" />

---
# OSI MODEL WITH DETAILS 

## What is OSI Model 
- OSI model stands for open system interconnection
- OSI Model is a way to explain how computers talk to each other over the network by breaking the process into seven simple steps or called layer.

## 7 Layer in Depth 

---

1. Application Layer :
- The Applications Layer of OSI model is the top layer in this model and takes care of network communication .
- This Application layer provides the functionality to send and receive data from users
  - What it does:
     - Interface directly with user software
     - Provides service like eamil,web browsers file transfer
- Protocol :
   - HTTPS, HTTP,FTP, SMTP,DNS
- eg :
   - You type www.youtube.com in your browser
   - Then Browse (Application Layer Software) creates on HTTP/HTTPS request asking for youtube  
---

2. Presentation Layer (Layer 6) :
- Translate data into a formal the application can understand
- Presentation layer is responsible for translation encryption and compression of data.
    - what is does:
      - Data translation
      - Data Compress (reduce the size for transmission )
      - Data encryption / Decryption (SSL/TLS)
- eg:
    - When you vist on HTTPS website , encryption & decryption happens here.

---

3. Session Layer :
- Session Layer responsible for opening and closings communication between two devices
- The time between when the Communications is opend and closed is known as sessions.
- This keeps track of your connections so multiple requests (Homepage , Videos ,ads are managed in organised way)
    - What is does:
       - Establishes , Maintain and Terminates session.
       - Synchronizes dialogue between two applications.
 - eg:
 - When you log into a website the sessions layer maintain your login session until you log out.
 - Even if you open 3 video in 3 tabs each has its own session   

---

4. Transport Layer :
- Transport Layer is responsible for the end-to-end communication between the two devices.
- This Included taking data form sessions layer braking it up into chunks called segments before sending to the layer 3
- The Transport layer is also responsible for flow control and error controls
- It ensures reliable delivery with error checking acknowledgement and retransmission id needed
- Protocol: TCP , UDP
- eg:
    - TCP :  Used in email , web Browsing (Guaranteed Delivery )
    - UDP :  Used in online gaming , video streaming (Speed over reliability but **No Guaranteed Delivery**).    

---

5. Network Layer :
- This Layer play key role in data transmissions.
- The main job of this layer is maintain the quality of the data and pass and transmit if from source to destinations .
- It also handles routing which means that it chooses the best path to transmit the data from the source to destinations.
- Protocol: IP(IPv4 and IPv6) ICMP ,OSPE ,BGP.
    - What is dose :
        - Break data into packets.
        - Assigne IP Address
        - Decides the best path (Routing) for data.
- eg:
    - When you open Google , your request travel through multiple routers across the internet to research google servers.

---

6. Data Link Layer :
- Data Link Layer is very similar to network layer.
- This layer responsible for node-to-node delivery on the same network.
- The data link layer takes packets from the network layer and breaks them into smaller pieces called frames
- Like the network layer the data link layer is also responsible for flow control and error controls
- Protocol: Ethernet , PPP ,ARP.
- eg:
    - If two PC in the same office LAN communicate the data link layer ensure the data reaches the correct pc using its MAC address

---

7. Physical Layer :
- This Layer includes the physical equipment involved in data transfer such as the cable and switch.
- This Responsibility of this layer transmit raw bits (0 and 1) as a electrical signals , light pules or radio waves.
- This layer deals with Hardware , cables ,connectors , voltage ,data refers , topology.
- eg:
   - When you connect your laptop with a LAN the physical layer ensures signals travel through the wires.   
