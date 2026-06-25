# Networking

Computer networking is the process of connecting computing devices (like computers, phones, and servers) to share data, resources, and applications. It serves as the backbone of modern digital communication, allowing for everything from local file sharing to accessing global cloud services.

---

## How Networking Works

### Basic Network Architecture
<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/e2eecdf3-0f56-44cb-ae01-6764cd52a799" />

**How Data Travels:**

1. Computer A sends data to its default gateway (Router).
2. Router forwards the data to the Internet.
3. Internet routes the data to the destination network.
4. Destination router receives and forwards the data to the local network.
5. Switch delivers the data to Computer B.

### How it Works

At its core, a computer network relies on three fundamental elements:

- **Devices (Nodes):** The computers, printers, smartphones, or servers that send and receive data.
- **Connection Media:** The physical cables (Ethernet, fiber-optic) or wireless signals (Wi-Fi, cellular) that link the devices together.
- **Protocols:** The predefined sets of rules (e.g., TCP/IP, HTTP) that standardize how data is formatted, transmitted, and received so different devices can understand each other.

### Core Components

To keep traffic moving accurately and securely, networks use specialized hardware and software:

- **Routers:** Devices that direct data packets between different networks (such as connecting your home network to the internet).
- **Switches:** Devices that connect multiple computers and servers within a single local network.
- **Firewalls:** Security systems that monitor and control incoming and outgoing network traffic, protecting devices from unauthorized access or cyber threats.

---

## What is IP

An IP (Internet Protocol) address is a unique numerical label assigned to every device connected to a computer network. It functions just like a digital mailing address, ensuring that data sent over the internet or a local network reaches the correct device.

An IP Address is a combination of **Network ID** and **Host ID**:

- **Network ID:** Identifies the specific network or community a device belongs to. Every device on the exact same physical network segment shares the same Network ID.
- **Host ID:** Identifies the specific, individual device (like your phone, laptop, or printer) on that network. Every device sharing a Network ID must have a unique Host ID.

> Example IP: `192.168.39.240`

Each IP is divided into blocks called **octets**. Each octet has **8 bits**, so the total is **32 bits**.

### IP Class Structure

```
Network bit = 1
Host Bit    = 0

Class A:  N H H H
Class B:  N N H H
Class C:  N N N H
```

**Example:** Find the Network ID of `115.10.0.15`

- `115` falls in **Class A** (1–126)
- Class A has 1 Network bit and 3 Host bits
- Replace Host bits with `0`
- **Network ID = `115.0.0.0`**

**Example:** Find the Network ID of `196.10.10.1`

- `196` falls in **Class C** (192–223)
- Class C has 3 Network bits and 1 Host bit
- Replace Host bit with `0`
- **Network ID = `196.10.10.0`**

---

## What is a Broadcast Address?

A **Broadcast Address** is the **last IP address** in a subnet. It is used to send data to **all devices** in the subnet at the same time.

**Example:**

```
Network: 192.168.1.0/24

192.168.1.0    → Network Address
192.168.1.1    → Host
192.168.1.2    → Host
...
192.168.1.254  → Host
192.168.1.255  → Broadcast Address
```

**Broadcast: `192.168.1.255`**

---

## Types of Addressing in Networking

| Type | Description | Address Used | Example | OSI Layer |
|------|-------------|--------------|---------|-----------|
| **Physical Addressing** | Unique hardware address assigned to a NIC | MAC Address | `00:1A:2B:3C:4D:5E` | Layer 2 (Data Link) |
| **Logical Addressing** | Address assigned by software (OS, DHCP, administrator) | IP Address | `192.168.1.10` | Layer 3 (Network) |

---

## Types of IP Addresses

| Type | Version | Example | Scope | Purpose |
|------|---------|---------|-------|---------|
| Public IPv4 | IPv4 | `8.8.8.8` | Internet | Communication over the internet |
| Private IPv4 | IPv4 | `192.168.1.10` | Internal Network | Communication within private networks |
| Public IPv6 | IPv6 | `2001:4860:4860::8888` | Internet | Global internet communication |
| Private IPv6 (ULA) | IPv6 | `fd00::1` | Internal Network | Private communication within an organization |

---

## IPv4 vs IPv6

| Feature | IPv4 | IPv6 |
|---------|------|------|
| Address Length | 32-bit (4 Octets) | 128-bit (16 Octets) |
| Example | `192.168.1.10` | `2001:db8::1` |
| Format | Decimal | Hexadecimal |
| Total Addresses | ~4.3 Billion | ~340 Undecillion |
| NAT Required? | Yes (often) | Usually No |
| Current Usage | Most Common | Growing Rapidly |

---

## IP Class Ranges

| Class | First Octet Range | IP Range | Default Subnet Mask | CIDR | Network Bits | Host Bits | Total Hosts/Network | Purpose |
|-------|-------------------|----------|----------------------|------|--------------|-----------|----------------------|---------|
| A | 1 – 126 | `1.0.0.0 – 126.255.255.255` | `255.0.0.0` | /8 | 8 | 24 | 16,777,214 | Large Networks |
| B | 128 – 191 | `128.0.0.0 – 191.255.255.255` | `255.255.0.0` | /16 | 16 | 16 | 65,534 | Medium Networks |
| C | 192 – 223 | `192.0.0.0 – 223.255.255.255` | `255.255.255.0` | /24 | 24 | 8 | 254 | Small Networks |
| D | 224 – 239 | `224.0.0.0 – 239.255.255.255` | N/A | N/A | N/A | N/A | N/A | Multicast |
| E | 240 – 255 | `240.0.0.0 – 255.255.255.255` | N/A | N/A | N/A | N/A | N/A | Research & Experimental |

### How to Find the IP Class

To identify the IP Class, **only check the first octet** — no calculations needed.

| IP Address | First Octet | Range | Class |
|------------|-------------|-------|-------|
| `137.20.20.10` | 137 | 128–191 | Class B |
| `115.0.0.0` | 115 | 1–126 | Class A |
| `192.22.0.0` | 192 | 192–223 | Class C |

### Special IP Address Ranges

| IP Range | Type | Purpose |
|----------|------|---------|
| `127.0.0.0/8` | Loopback | Self-communication |
| `169.254.0.0/16` | APIPA | DHCP failure fallback |
| `224.0.0.0 – 239.255.255.255` | Multicast | One-to-many communication |
| `240.0.0.0 – 255.255.255.255` | Reserved | Experimental use |
| `0.0.0.0` | Default Route | Represents unknown/default network |
| `255.255.255.255` | Broadcast | Broadcast to all hosts |

---

## What is a Loopback Address?

A **loopback address** is a special IP address that a computer uses to communicate with itself.

The most common loopback address is:

```
127.0.0.1
Hostname: localhost

127.0.0.1 = localhost
```

---

## Subnet Mask

A **Subnet Mask** is a 32-bit number used by network devices to distinguish between the Network ID and the Host ID within an IP address. (It represents the maximum number of IPs in the subnet.)

We calculate this using the Host bit and Network bit.

**Steps:** First, check which class the IP belongs to, then replace Network octets with `255` and Host octets with `0`.

**Example 1:** `115.10.10.20` → **Class A**

```
115  10  10  20
 N    H   H   H

11111111 00000000 00000000 00000000
  255       0       0       0
```

**Subnet Mask of `115.10.10.20` = `255.0.0.0`**

**Example 2:** `160.10.20.10` → **Class B**

```
160  10  20  10
 N    N   H   H

11111111 11111111 00000000 00000000
  255      255       0       0
```

**Subnet Mask of `160.10.20.10` = `255.255.0.0`**

---

## Binary Conversion

To convert any IP into binary, use the **bit position chart** (powers of 2):

```
Bit Position:  128 | 64 | 32 | 16 | 8 | 4 | 2 | 1
```

- Put `1` under values you **use**.
- Put `0` under values you **don't use**.

**Example:** Convert `192.168.37.200` to binary

| Octet | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | Binary |
|-------|-----|----|----|----|----|---|---|---|--------|
| 192 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | `11000000` |
| 168 | 1 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | `10101000` |
| 37  | 0 | 0 | 1 | 0 | 0 | 1 | 0 | 1 | `00100101` |
| 200 | 1 | 1 | 0 | 0 | 1 | 0 | 0 | 0 | `11001000` |

---

## How to Find Network ID and Broadcast ID

**Example:** `150.10.20.30`

**Step 1: Find the class** → `150` is **Class B** (N N H H)

### Network ID

Replace Host bits with `0`:

```
150  10  20  30
 N    N   H   H
150  10   0   0
```

**Network ID of `150.10.20.30` = `150.10.0.0`**

### Broadcast ID

Replace Host bits with `255`:

```
150  10  20  30
 N    N   H   H
150  10  255  255
```

**Broadcast ID of `150.10.20.30` = `150.10.255.255`**

---

## How to Find Usable IP Addresses

### Without CIDR Block

**Formula:**

```
2^(Number of Host Bits) - 2 = Usable IPs
```

> **Why -2?** First reserved address = **Network Address**. Second reserved address = **Broadcast Address**.

| IP | Class | Host Bits | Calculation | Usable IPs |
|----|-------|-----------|-------------|------------|
| `150.10.0.0` | B | 16 | 2^16 - 2 | **65,534** |
| `11.0.0.0` | A | 24 | 2^24 - 2 | **16,777,214** |
| `179.10.0.0` | B | 16 | 2^16 - 2 | **65,534** |

### With CIDR Block

**Formula:**

```
Host Bits = 32 - CIDR Number
2^(Host Bits) - 2 = Usable IPs
```

**Example:** `150.10.0.0/20`

```
Host Bits = 32 - 20 = 12
2^12 - 2 = 4,094 usable IPs
```

---

## Subnetting
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/e4cdd835-54e8-4905-b779-6827d3a744d9" />

**Subnetting** is the logical process of dividing a single large IP network into multiple, smaller interconnected sub-networks called **subnets**. It works by "borrowing" bits from the host portion of an IP address to expand the network portion, allowing network administrators to segment traffic, optimize IP allocation, and boost performance.

### Why Do We Need Subnetting?

**Without subnetting** — all devices share one network; every broadcast reaches every device:

```
All 155 devices → One Network
```

**With subnetting** — each department gets its own network; broadcasts stay local:

```
HR Network
Finance Network
IT Network
Sales Network
```

**Benefits:**
- Better performance
- Better security
- Easier management

**Example — Instead of:**

```
192.168.1.0/24
```

**We create:**

```
HR      → 192.168.1.0/26
Finance → 192.168.1.64/26
IT      → 192.168.1.128/26
Sales   → 192.168.1.192/26
```

---

### The Host Calculation Formula

```
Step 1: Host Bits (n) = 32 - CIDR Block
Step 2: Usable Hosts  = 2^n - 2
```

**Example — Need 50 users:**

| CIDR | Host Bits | Calculation | Usable Hosts | Sufficient? |
|------|-----------|-------------|--------------|-------------|
| /27 | 5 | 2^5 - 2 | 30 | ❌ Not enough |
| /26 | 6 | 2^6 - 2 | 62 | ✅ Enough |

**Choose: `/26`**

> Always choose the **smallest subnet** (nearest value equal to or greater) that satisfies the requirement.

---

### CIDR Cheat Sheet

> **This table should be memorized.**

| CIDR | Total IPs | Usable Hosts |
|------|-----------|--------------|
| /24 | 256 | 254 |
| /25 | 128 | 126 |
| /26 | 64 | 62 |
| /27 | 32 | 30 |
| /28 | 16 | 14 |
| /29 | 8 | 6 |
| /30 | 4 | 2 |

---

## Business Requirement — Subnetting Example

**Parent Network:** `192.168.10.0/24`

| Department | Users |
|------------|-------|
| IT | 60 |
| HR | 25 |
| Finance | 12 |
| Sales | 5 |

### Step 1: Sort Largest to Smallest

Always start with the biggest department.

### Step 2: Find Suitable CIDR

**IT — Need 60 users:**

| CIDR | Usable Hosts | Sufficient? |
|------|--------------|-------------|
| /27 | 30 | ❌ |
| /26 | 62 | ✅ |

**Assign: `/26`**

**HR — Need 25 users:**

| CIDR | Usable Hosts | Sufficient? |
|------|--------------|-------------|
| /28 | 14 | ❌ |
| /27 | 30 | ✅ |

**Assign: `/27`**

**Finance — Need 12 users:**

| CIDR | Usable Hosts | Sufficient? |
|------|--------------|-------------|
| /28 | 14 | ✅ |

**Assign: `/28`**

**Sales — Need 5 users:**

| CIDR | Usable Hosts | Sufficient? |
|------|--------------|-------------|
| /29 | 6 | ✅ |

**Assign: `/29`**

### Step 3: Allocate Networks Sequentially

| Department | CIDR | Range |
|------------|------|-------|
| IT | /26 | `192.168.10.0` → `192.168.10.63` |
| HR | /27 | `192.168.10.64` → `192.168.10.95` |
| Finance | /28 | `192.168.10.96` → `192.168.10.111` |
| Sales | /29 | `192.168.10.112` → `192.168.10.119` |

---

## How to Transfer Host Bits into Network Bits

**Steps:**

1. Find value of `n` using the nearest or greater number.

**Example — Want 40 IPs:**

```
2^6 - 2 = 62  →  62 > 40  →  n = 6
```

2. Reserve 6 bits for host and 2 bits for network from the right side of the last octet.

```
197.10.0.00000000
→ Convert 2 leftmost bits to network bits
→ 197.10.0.11000000
→ 128 + 64 = 192
→ 197.10.0.192
```

> **Note:** The subnet mask value `192` here refers to the borrowed-bit pattern (`11000000` = 192), not the IP's first octet. The final subnet address becomes `197.10.0.192`.

**Final result: `197.10.0.192`**

---

## Final Design

| Department | Users | CIDR | Network Address | First Host | Last Host | Broadcast |
|------------|-------|------|-----------------|------------|-----------|-----------|
| IT | 60 | /26 | `192.168.10.0` | `192.168.10.1` | `192.168.10.62` | `192.168.10.63` |
| HR | 25 | /27 | `192.168.10.64` | `192.168.10.65` | `192.168.10.94` | `192.168.10.95` |
| Finance | 12 | /28 | `192.168.10.96` | `192.168.10.97` | `192.168.10.110` | `192.168.10.111` |
| Sales | 5 | /29 | `192.168.10.112` | `192.168.10.113` | `192.168.10.118` | `192.168.10.119` |

---

## Golden Algorithm (Use This Every Time)

Whenever someone asks you to subnet a network:

1. Write the **parent network** (e.g., `192.168.10.0/24`).
2. List the **departments** and required hosts.
3. **Sort** them from largest to smallest.
4. Choose the **smallest CIDR** that can accommodate each department using the host table.
5. **Allocate subnets sequentially**, starting from the beginning of the address space.
6. For each subnet, calculate:
   - Network Address
   - First Host
   - Last Host
   - Broadcast Address
7. **Verify** that each subnet has enough usable hosts.
