# 01 - Networking Overview


While a network's basic function is to allow computers to communicate, *how* that network is designed is critical for security. A poorly designed network can make an attacker's job easy, while a well-designed one can slow them down, expose their activity, and limit the damage they can do.

### Flat vs. Segmented Networks
The core principle of secure network design is moving away from a "flat" network to a "segmented" one.

| Feature | Flat Network | Segmented Network |
| :--- | :--- | :--- |
| **Structure** | All devices (servers, workstations, printers) exist on a single, large network. | The network is divided into smaller, isolated sub-networks (segments) based on function or trust level. |
| **Communication**| Any device can freely communicate with any other device. | Communication between segments is restricted and controlled by a firewall or Access Control Lists (ACLs). |
| **Security** | Very poor. If one device (like a printer) is compromised, the attacker can immediately access and attack critical servers. | Much stronger. If a printer is compromised, the attacker is trapped within the low-trust "Printer" segment and cannot directly reach the high-trust "Server" segment. |
| **Analogy** | A large, open-plan house with no internal doors. | A house with many rooms, each with a locked door. |

### The Layered Defense Analogy
Segmenting a network is like adding layers of physical security to a property.

| Security Control | Real-World Analogy | Security Question It Answers |
| :--- | :--- | :--- |
| **Network Segmentation (ACLs)** | A fence around the property with a single, guarded gate. | *Why is the printer network talking to the server network over HTTP?* (Suspicious activity). |
| **Network Documentation & Monitoring** | Bright lights illuminating the entire property. | *Why is the printer network talking to the internet at all?* (Unauthorized activity). |
| **Intrusion Detection Systems (IDS)**| Thorny bushes planted under all the windows. | *Why did a port scan originate from the printer network?* (Deterrent and detection). |

---

## The Importance of Subnetting: `/24` vs. `/25`
The "Pentester's Oversight" story highlights a critical and often overlooked aspect of networking: **subnetting**. Failing to understand it can cause you to miss entire sections of a network.

**CIDR (Classless Inter-Domain Routing) notation** (e.g., `/24`) is a shorthand way to represent a subnet mask. The number indicates how many bits are used for the network portion of the address.

#### The `/24` Subnet (The Common Default)
*   **IP Address:** `192.168.1.0/24`
*   **Subnet Mask:** `255.255.255.0`
*   **Network Bits:** 24
*   **Host Bits:** 8 (32 total bits - 24 network bits)
*   **Total Hosts:** 2⁸ - 2 = 254 usable IP addresses.
*   **Range:** All devices from `192.168.1.1` to `192.168.1.254` can talk to each other directly.

#### The `/25` Subnet (Splitting the Network in Half)
A `/25` subnet uses one extra bit for the network, effectively splitting a `/24` network into two smaller, separate networks.

*   **Subnet Mask:** `255.255.255.128`
*   **Host Bits:** 7 (32 - 25)
*   **Total Hosts per Subnet:** 2⁷ - 2 = 126 usable IP addresses.

Let's split `10.20.0.0/24` into two `/25` subnets:
1.  **First Subnet (Server Network):**
    *   **Network ID:** `10.20.0.0/25`
    *   **Usable IP Range:** `10.20.0.1` to `10.20.0.126`
2.  **Second Subnet (Client Network):**
    *   **Network ID:** `10.20.0.128/25`
    *   **Usable IP Range:** `10.20.0.129` to `10.20.0.254`

**The Pentester's Mistake:** The pentester assumed a `/24` network. Their IP (`10.20.0.252/24`) allowed them to see the Client Workstation (`10.20.0.200`), but their machine's networking stack would not allow them to directly communicate with the Domain Controller (`10.20.0.10`) because it was on a *different subnet*. They incorrectly concluded the server was offline.

---

## The Demilitarized Zone (DMZ)
A **Demilitarized Zone (DMZ)** is a perimeter network that protects an organization's internal LAN from untrusted, external traffic. It is a small, isolated sub-network that sits between the internet and the trusted internal network.

### The Office Building Lobby Analogy
Think of a DMZ like the **lobby of a secure office building.**

*   **The Internet:** The public street outside. Anyone can walk in from the street.
*   **The DMZ (The Lobby):** A controlled, public-facing area. Visitors can talk to the receptionist (the web server), but they cannot get past the security turnstiles to enter the main office area.
*   **The Internal Network (The Secure Offices):** The private, trusted area where the real work happens and sensitive information is stored. Access is strictly controlled.

### Purpose of a DMZ
*   **To host public-facing services:** Any server that needs to be accessible from the internet (like a web server, email server, or DNS server) should be placed in the DMZ.
*   **To add a layer of security:** If a server in the DMZ is compromised, the attacker is still trapped within that isolated network. They must breach a *second* firewall to get from the DMZ to the valuable internal network, giving the security team more time to detect and respond to the attack.

---

## Network Segmentation Best Practices
A secure corporate network should be divided into multiple, isolated segments.

*   **Web Servers (in a DMZ):** Public-facing servers should be in a DMZ, separated from the internal network by a firewall.
*   **Workstations:** All employee computers should be on their own network, separate from servers. Ideally, workstations should be prevented from communicating directly with each other to stop malware from spreading laterally.
*   **Administration Network:** Network devices like routers and switches should be on a dedicated management network, inaccessible from standard user workstations.
*   **IP Phones (VoIP):** Phones should be on their own network (a VLAN) to ensure call quality (by prioritizing their traffic) and to prevent a compromised computer from eavesdropping on phone calls.
*   **Printers:** Printers are notoriously insecure and should be on their own isolated network. This prevents a compromised printer from being used as a pivot point to attack the rest of the network.
    > **Real-World Example:** A penetration tester once shipped an expensive, pre-hacked printer to a company as a "gift." An employee helpfully plugged it into the network. Because the network was flat, the printer was able to capture the domain administrator's credentials when they printed a document, giving the tester full control of the network. Proper segmentation would have prevented this attack.
