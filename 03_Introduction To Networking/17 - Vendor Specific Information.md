# Vendor Specific Information
## 1. Cisco IOS

**Cisco IOS (Internetwork Operating System)** is the proprietary operating system that runs on the vast majority of Cisco's routers and switches. Understanding its basics is crucial as Cisco devices are extremely common in corporate networks.

### Key Features of Cisco IOS
*   **Management:** Primarily managed via a **Command Line Interface (CLI)**, though graphical interfaces (GUIs) exist. Remote access is typically provided via SSH (secure) or Telnet (insecure).
*   **Routing & Switching:** Supports all major routing protocols (e.g., OSPF, BGP) and switching protocols (e.g., VTP, STP).
*   **Network Services:** Can act as a DHCP server, a firewall (using ACLs), and more.

### Cisco IOS Password Types
Cisco devices use a tiered password system for security.

| Password Type | Purpose | Security Level |
| :--- | :--- | :--- |
| **User Password** | For initial login to the device in a limited, non-privileged mode. | Basic |
| **Enable Password**| Used to enter "enable" or "privileged" mode, which grants administrative access. Stored in cleartext in the configuration. | Low |
| **Enable Secret**| A more secure password for entering "enable" mode. It is always stored in an encrypted (hashed) format, making it much stronger than the `enable password`. If both are set, the `enable secret` takes precedence. | High |

---

## 2. VLANs (Virtual Local Area Networks)

A **VLAN** is a technology that allows a single physical network switch to be logically segmented into multiple, separate, virtual networks.

**Core Idea:** VLANs create logical **broadcast domains**. Traffic broadcast on one VLAN (e.g., VLAN 10) will *not* be seen by any device on another VLAN (e.g., VLAN 20), even if they are plugged into the same physical switch. Each VLAN functions as its own separate subnet.

### Benefits of Using VLANs
*   **Increased Security:** By segmenting the network, you can isolate different groups of users or devices. A compromised device in the "Guest" VLAN cannot directly access servers in the "Production" VLAN.
*   **Increased Performance:** Reduces unnecessary broadcast traffic, which frees up bandwidth.
*   **Simplified Administration:** Devices can be grouped logically (by department, function) regardless of their physical location in the building.

### VLAN Memberships & Port Types
*   **VLAN Assignment:**
    *   **Static (Port-Based):** The most common and secure method. A network administrator manually assigns each switch port to a specific VLAN.
    *   **Dynamic:** The switch automatically assigns a device to a VLAN based on its MAC address. This is more flexible but less secure, as it can be bypassed with MAC spoofing.
*   **Port Types:**
    *   **Access Port:** Belongs to and carries traffic for **only one** VLAN. This is where end devices like workstations and printers connect.
    *   **Trunk Port:** Can carry traffic for **multiple** VLANs simultaneously. Trunk ports are used to connect switches to other switches or to routers, allowing VLANs to span across the entire network.

### VLAN Tagging (IEEE 802.1Q)
To keep track of which traffic belongs to which VLAN as it crosses a trunk link, a "tag" is added to the Ethernet frame.

*   **IEEE 802.1Q ("dot1q"):** The industry standard for VLAN tagging. It inserts a 4-byte tag into the Ethernet frame header.
*   **VLAN ID (VID):** A 12-bit field within the 802.1Q tag that identifies the VLAN (allowing for up to 4094 VLANs).
*   **Native VLAN:** On a trunk port, one VLAN can be designated as the "native" VLAN. Traffic for this VLAN is sent *untagged* across the trunk link.

---

## 3. VLAN Security & Attacks

While VLANs improve security, they are not immune to attacks.

| Attack | Description |
| :--- | :--- |
| **VLAN Hopping (Switch Spoofing)**| An attacker exploits the **Dynamic Trunking Protocol (DTP)**, a Cisco-proprietary protocol that automatically negotiates trunk links. The attacker configures their host to pretend it's a switch, tricking the real switch into forming a trunk link with them. This gives the attacker access to traffic from *all* VLANs allowed on that trunk. |
| **Double Tagging**| A more advanced attack where an attacker crafts a packet with two VLAN tags. The first switch strips off the outer tag (for the native VLAN) and forwards the packet, which still contains the inner tag. The second switch then sees the inner tag and forwards the packet to the victim's VLAN, bypassing Layer 2 segmentation. |

---

## 4. Other Vendor-Specific Protocols

*   **Cisco Discovery Protocol (CDP):** A Cisco-proprietary Layer 2 protocol used by Cisco devices to share information about themselves (device ID, IP address, IOS version) with directly connected Cisco neighbors. This is very useful for network mapping but can also leak sensitive information if not properly secured.
*   **VXLAN (Virtual eXtensible Local Area Network):** An overlay technology designed to overcome the 4094 VLAN limit. It encapsulates Layer 2 frames within UDP packets, allowing for the creation of up to 16 million logical segments. It is a key technology in modern data centers and cloud environments.
