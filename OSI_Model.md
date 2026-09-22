<img width="500" height="620" alt="image" src="https://github.com/user-attachments/assets/7c651606-7581-47be-9ff7-6a2eabe60ae9" />


# OSI Model — Detailed Notes

## What Is the OSI Model?

- OSI stands for **Open Systems Interconnection**.
- Development began under **ISO (International Organization for Standardization)** in 1977; the model was formally published as a standard in **1984**.
- It is a general, theoretical reference model used to understand and design how networks communicate.
- The OSI model explains how computers talk to each other over a network by breaking the process into **seven layers**.

---

## The 7 Layers in Depth

### 7. Application Layer

- The top layer of the OSI model. Provides services that let user applications communicate over a network.
- Supplies the interface for sending and receiving data, but does not handle the actual transfer — that's left to the lower layers.
- **What it does:**
  - Interfaces directly with user-facing software.
  - Provides services like email, web browsing, and file transfer.
- **Protocols:** HTTP, HTTPS, FTP, SMTP, DNS
- **Example:** You type `www.youtube.com` in your browser. The browser (application-layer software) creates an HTTP/HTTPS request asking for YouTube's page.

---

### 6. Presentation Layer

- Translates data into a format the application layer can understand.
- Responsible for data translation, compression, and encryption/decryption.
- **What it does:**
  - Data translation
  - Data compression (reduces size for transmission)
  - Data encryption/decryption (SSL/TLS)
- **Example:** When you visit an HTTPS website, encryption/decryption (via SSL/TLS) happens at this layer.

---

### 5. Session Layer

- Responsible for opening and closing communication sessions between two devices.
- The time between when a connection opens and closes is called a "session."
- Keeps track of connections so multiple requests (e.g., a homepage, videos, and ads loading at once) are managed in an organized way.
- Handles authentication, session checkpointing, and recovery if a connection is lost.
- **What it does:**
  - Establishes, maintains, and terminates sessions.
  - Synchronizes dialogue between two applications.
- **Example:** When you log into a website, the session layer maintains your login session until you log out. If you open three videos in three tabs, each has its own independent session.

---

### 4. Transport Layer

- Responsible for end-to-end communication between two devices.
- Takes data from the session layer and breaks it into chunks called **segments** before passing it to Layer 3.
- Handles flow control and error control, ensuring reliable delivery through error checking, acknowledgements, and retransmission when needed.
- **Protocols:** TCP, UDP
- **Example:**
  - TCP — used for email and web browsing (guaranteed delivery).
  - UDP — used for online gaming and video streaming (prioritizes speed over reliability; **no guaranteed delivery**).

---

### 3. Network Layer

- Plays a key role in data transmission across networks.
- Its main job is to maintain the integrity of the data and move it from source to destination.
- Handles **routing** — choosing the best path to transmit data from source to destination.
- **Protocols:** IP (IPv4/IPv6), ICMP, OSPF, BGP
- **What it does:**
  - Breaks data into packets.
  - Assigns IP addresses.
  - Decides the best path (routing) for data.
- **Example:** When you open Google, your request travels through multiple routers across the internet to reach Google's servers.

---

### 2. Data Link Layer

- Ensures node-to-node delivery within the same local network, using MAC addresses.
- Takes packets from the network layer and breaks them into smaller pieces called **frames**.
- Like the network layer, it handles flow control and error control.
- Organizes data into frames and provides error detection (e.g., via CRC).
- **Protocols:** Ethernet, PPP, ARP
- **Example:** If two PCs on the same office LAN communicate, the data link layer ensures data reaches the correct PC using its MAC address.

---

### 1. Physical Layer

- Covers the physical equipment involved in data transfer, such as cables and switches.
- Responsible for transmitting raw bits (0s and 1s) as electrical signals, light pulses, or radio waves.
- Deals with hardware — cables, connectors, voltage, data rates, and network topology.
- **Example:** When you connect your laptop to a LAN via cable, the physical layer ensures signals travel correctly through the wire.
