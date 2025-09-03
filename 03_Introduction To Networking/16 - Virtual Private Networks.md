# Virtual Private Networks
## What is a VPN?

A **Virtual Private Network (VPN)** is a technology that extends a private network across a public network. It establishes a secure, encrypted "tunnel" through which all communication between a remote client and the private network passes.

**Core Idea:** A VPN allows a remote user or office to securely access a company's internal resources (file servers, applications) from anywhere with an internet connection, making it appear as if they are physically present on the local network.

### Why are VPNs Used?
*   **Secure Remote Access:** This is the primary use case. It allows employees working from home or traveling to securely connect to the corporate network.
*   **Encryption:** A VPN encrypts all traffic within the tunnel, protecting sensitive data from being intercepted by attackers on public networks (like public Wi-Fi).
*   **Cost-Effectiveness:** It's much cheaper to use the public internet for connectivity than to lease expensive, dedicated private lines between locations.
*   **Site-to-Site Connectivity:** Connects multiple branch offices into a single, cohesive private network.

---

## Core Components of a VPN

| Component | Description |
| :--- | :--- |
| **VPN Client** | Software installed on the remote device (e.g., a laptop) that is used to initiate and maintain the connection to the VPN server. (e.g., OpenVPN client). |
| **VPN Server** | A dedicated server or network device (like a firewall) that accepts connections from VPN clients, authenticates them, and routes their traffic to the private network. |
| **Encryption** | The process of scrambling the data within the tunnel to ensure confidentiality. Strong algorithms like **AES** are used. |
| **Authentication** | The process of verifying the identity of both the client and the server before the secure connection is established. This can be done with a pre-shared key (password), digital certificates, or user credentials. |
| **Tunneling Protocol**| The set of rules that defines how the data is encapsulated and transmitted securely. |

---

## Key VPN Protocols

### 1. IPsec (Internet Protocol Security)
**IPsec** is a robust and widely used suite of protocols that provides security at the Network Layer (Layer 3). It is a core technology for many modern VPNs.

*   **Core Protocols within IPsec:**
    *   **Authentication Header (AH):** Provides data integrity and authenticity (ensures the data hasn't been tampered with) but **does not provide encryption**.
    *   **Encapsulating Security Payload (ESP):** Provides **encryption** (confidentiality) and optional authentication. This is the part that scrambles the data.
*   **Key Exchange Protocol:**
    *   **IKE (Internet Key Exchange):** Operates on **UDP port 500**. It is used to automatically negotiate the security parameters and generate the shared secret keys that IPsec will use to encrypt the data.
*   **IPsec Modes:**
    *   **Transport Mode:** Encrypts only the data payload of the IP packet. Used for end-to-end communication between two hosts.
    *   **Tunnel Mode:** Encrypts the **entire** original IP packet (including the header) and puts it inside a new IP packet. This is the mode used to create a VPN gateway-to-gateway or client-to-gateway tunnel.

### 2. PPTP (Point-to-Point Tunneling Protocol)
*   **Description:** An older VPN protocol that operates on **TCP port 1723**.
*   **Security Status:** It is now considered **insecure and obsolete** due to significant, known vulnerabilities in its authentication and encryption mechanisms (MS-CHAPv2). It should not be used in modern environments.
*   **Legacy:** Has been largely replaced by more secure protocols like IPsec/IKEv2 and OpenVPN.
