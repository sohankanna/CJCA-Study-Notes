# 06 -  Network Address Translation (NAT)

The Problem: IPv4 Address Exhaustion

The original internet protocol, **IPv4**, provides approximately 4.3 billion unique addresses. With the explosive growth of internet-connected devices, this number is not nearly enough for every device to have its own globally unique address. **NAT** is a primary solution to this problem.

---

## Public vs. Private IP Addresses

To understand NAT, you must first understand the two types of IP addresses.

| Type | Description | Routable on Internet? | Example Ranges (RFC 1918) |
| :--- | :--- | :--- | :--- |
| **Public IP Address** | A globally unique address assigned by an Internet Service Provider (ISP). It is directly accessible from anywhere on the internet. | **Yes** | N/A (e.g., Google's DNS server at `8.8.8.8`) |
| **Private IP Address** | An address used only within a local, private network (like your home or office). It is **not** routable on the public internet. | **No** | `10.0.0.0` - `10.255.255.255` <br> `172.16.0.0` - `172.31.255.255` <br> `192.168.0.0` - `192.168.255.255` |

---

## What is NAT?

**Network Address Translation (NAT)** is the process, typically performed by a router, of modifying the source or destination IP address in a packet's header as it passes from a private network to a public one (or vice versa).

**Core Idea:** The router acts as a translator or receptionist for the entire private network. It takes all outgoing traffic from multiple private IP addresses and makes it appear as if it's all coming from its single public IP address.

## How NAT Works

1.  **Outgoing Request:** Your laptop (`192.168.1.10`) sends a request to `google.com`. The packet has your private IP as the source.

2.  **Router Translation:** The packet reaches your home router. The router's NAT function does two things:
    *   It replaces the **source IP** in the packet from your private IP (`192.168.1.10`) to the router's public IP (`203.0.113.50`).
    *   It records this translation in a **NAT table**, noting the original private IP and port, so it knows where to send the response later.

3.  **Travel Across Internet:** The modified packet, now with a public source IP, travels across the internet to Google's server.

4.  **Server Response:** Google's server sends the webpage back, addressed to your router's public IP (`203.0.113.50`).

5.  **Router Reverse Translation:** The response arrives at your router. The router checks its NAT table, sees that this traffic is meant for your laptop at `192.168.1.10`, replaces the destination IP with your private address, and forwards the packet to your laptop.

---

## Types of NAT

| Type | Description |
| :--- | :--- |
| **Static NAT** | A **one-to-one** mapping. One private IP address is always translated to the same public IP address. Used when a specific internal device (like a web server) needs to be consistently accessible from the internet. |
| **Dynamic NAT** | A **many-to-many** mapping. The router has a pool of public IP addresses and assigns one to a private device on a first-come, first-served basis. |
| **Port Address Translation (PAT) / NAT Overload** | A **many-to-one** mapping. This is the **most common type** of NAT, used in virtually all home and small office networks. Multiple private IP addresses are mapped to a single public IP address. The router uses unique **port numbers** to keep track of which response belongs to which internal device. |

---

## Benefits and Trade-offs of NAT

### Benefits
*   **Conserves IPv4 Addresses:** The primary benefit. Allows thousands of devices in an organization to use only a handful of public IP addresses.
*   **Provides Basic Security:** By hiding the internal network structure, NAT acts as a natural firewall. Devices on the private network are not directly accessible from the internet unless explicitly configured (e.g., via port forwarding).
*   **Flexibility:** Organizations can design their internal IP address schemes without needing to coordinate with external bodies.

### Trade-offs
*   **Breaks End-to-End Connectivity:** Certain protocols that require a direct, unmodified connection between two hosts can have issues with NAT.
*   **Complexity for Hosting Services:** To run a server (like a game server or web server) behind NAT, you must configure **port forwarding**, which manually tells the router to send all incoming traffic on a specific port to a specific internal device.
*   **Troubleshooting:** Can add a layer of complexity when diagnosing network connectivity problems.
