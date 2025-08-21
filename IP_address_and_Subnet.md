# IP address and Subnet 

# What is IP Address 
An IP address (Internet Protocol address) is a unique numerical label assigned to each device connected to a computer network that uses the Internet Protocol for communication. It acts like a "digital address", allowing devices to find and communicate with each other over the internet or local networks.

# Types of IP Addresses
 There are several types of IP addresses, primarily categorized by their version, scope, and allocation method. 
 
# IPv4 
<img width="2688" height="1307" alt="image" src="https://github.com/user-attachments/assets/c31fc42a-1cb7-4139-a327-442ec13d78c8" />

## IPv4 (Internet Protocol version 4)
- Format: Four decimal numbers separated by dots, e.g., 192.168.1.1.
- Range: Each number ranges from 0 to 255.
- Capacity: Around 4.3 billion unique addresses.
- Example: 172.16.0.1
- Usage: Most common today for homes, businesses, and websites.
- Limitation: Limited number of addresses; requires techniques like NAT (Network Address Translation) to allow multiple devices to share one public
- IP.Development started: 1970s
- Standardized: 1981

# Categories 
- Public IP addresses are assigned to a device by the internet service provider (ISP) and are used to identify the device on the public internet.
- Private IP addresses are assigned to devices on a private network, such as a home or office network.

---

# IPv6 
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/3061b26e-bfd0-4ddb-8018-1ee73294607e" />

# IPv6 (Internet Protocol version 6)
- Format: Eight groups of four hexadecimal digits separated by colons, e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334.
- Capacity: About 340 undecillion addresses (~3.4 × 10³⁸).
- Example: fe80::1ff:fe23:4567:890a.
- Usage: Designed to handle the growth of the internet, including billions of IoT devices.
- Advantages: Better security, efficiency, and auto-configuration without the need for NAT.
- Development started: 1994
- Standardized: 1998

# Categories 
- Public IP addresses are assigned to a device by the internet service provider (ISP) and are used to identify the device on the public internet.
- Private IP addresses are assigned to devices on a private network, such as a home or office network.


# Why we are not fully able to adopt IPv6

Even though IPv6 solves the IP shortage problem, global adoption has been slow due to several practical challenges:
| **Reason**               | **Explanation**                                                                                                                                              |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Legacy systems**       | Many old devices, servers, and applications still only support IPv4. Upgrading them can be costly or impossible.                                             |
| **Compatibility issues** | IPv6 is **not backward-compatible** with IPv4, so dual-stack setups are required, adding complexity.                                                         |
| **Infrastructure cost**  | ISPs and organizations need to upgrade routers, firewalls, and other network gear to handle IPv6.                                                            |
| **Lack of urgency**      | NAT (Network Address Translation) extended the life of IPv4 by allowing multiple devices to share a single public IP, reducing the pressure to move to IPv6. |
| **Training gap**         | Many network admins are still more familiar with IPv4, leading to hesitation in transitioning.                                                               |

# What is subnet 
A subnet (subnetwork) is a logical subdivision of an IP network. Subnets are created by dividing a larger network into smaller, more manageable pieces. This process is called subnetting.

## Why Subnets Are Created

- Efficient IP Address Utilization
  - Helps avoid wasting IP addresses by dividing the network as per actual requirements.
- Example: Instead of giving 254 addresses to a small department needing only 30, you can create a smaller subnet.
- Improved Network Performance
  - Reduces network congestion because fewer devices share the same broadcast domain.
- Enhanced Security
  - Sensitive areas like HR or Finance can be placed in isolated subnets to restrict access.
- Simplified Management
  - Easier to troubleshoot and maintain smaller, logically separated networks.

- How Subnetting Works
An IP address consists of:
  -Network Portion: Identifies the network.
  -Host Portion: Identifies the device within that network.
Subnet masks define how much of the address is used for the network vs. host.
