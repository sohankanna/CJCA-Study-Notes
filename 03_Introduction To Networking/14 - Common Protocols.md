# Common Protocols

## TCP vs. UDP: The Two Transport Protocols

All application-layer protocols are built on top of one of these two transport protocols.

*   **TCP (Transmission Control Protocol):**
    *   **Connection-Oriented:** Establishes a reliable, three-way handshake before sending data.
    *   **Reliable:** Guarantees that all data packets are received in the correct order and without errors by using acknowledgments and retransmissions.
    *   **Slower:** The overhead of ensuring reliability makes it slower than UDP.
    *   **Use Case:** Web browsing (HTTP/S), file transfers (FTP), email (SMTP). Reliability is more important than speed.

*   **UDP (User Datagram Protocol):**
    *   **Connectionless:** Sends data packets ("datagrams") without establishing a prior connection. It's a "fire and forget" protocol.
    *   **Unreliable:** Does not guarantee delivery, order, or error checking.
    *   **Faster:** The lack of overhead makes it much faster than TCP.
    *   **Use Case:** Video streaming, online gaming, VoIP, DNS. Speed is more important than perfect reliability; losing a single frame of video is acceptable.

---

## Common Protocols (Grouped by Function)

### 1. Web & Data Transfer

| Protocol | Acronym | Port(s) | Transport | Description |
| :--- | :--- | :--- | :--- | :--- |
| Hypertext Transfer Protocol | HTTP | 80 | TCP | The foundation of the World Wide Web, used to transfer web pages. |
| Hypertext Transfer Protocol Secure| HTTPS | 443 | TCP | The secure, encrypted version of HTTP. |
| File Transfer Protocol | FTP | 20, 21 | TCP | A standard protocol for transferring files between a client and server. |
| Trivial File Transfer Protocol | TFTP | 69 | UDP | A simplified, less secure version of FTP. |
| Secure Copy Protocol | SCP | 22 | TCP | A secure method of transferring files, built on top of SSH. |

### 2. Remote Access & Management

| Protocol | Acronym | Port(s) | Transport | Description |
| :--- | :--- | :--- | :--- | :--- |
| Secure Shell | SSH | 22 | TCP | A secure protocol for remote command-line access and management. |
| Telnet | Telnet | 23 | TCP/UDP | An older, **insecure** protocol for remote command-line access. All data is sent in cleartext. |
| Remote Desktop Protocol | RDP | 3389 | TCP | A Microsoft protocol for accessing a remote computer's graphical desktop. |
| Virtual Network Computing | VNC | 5900+ | UDP | A graphical desktop sharing system. |
| X Window System | X11 | 6000+ | TCP/UDP | A system for providing graphical user interfaces on networked computers, common in Unix/Linux. |

### 3. Email

| Protocol | Acronym | Port(s) | Transport | Description |
| :--- | :--- | :--- | :--- | :--- |
| Simple Mail Transfer Protocol | SMTP | 25 | TCP | The standard protocol for **sending** emails between servers. |
| Post Office Protocol v3 | POP3 | 110 | TCP | Used by email clients to **retrieve** emails from a server. Typically deletes the email from the server after download. |
| Internet Message Access Protocol | IMAP | 143 | TCP | Used by email clients to **access and manage** emails on a server. Keeps emails on the server, allowing for synchronization across multiple devices. |

### 4. Naming, Addressing & Time

| Protocol | Acronym | Port(s) | Transport | Description |
| :--- | :--- | :--- | :--- | :--- |
| Domain Name System | DNS | 53 | TCP/UDP | Translates human-readable domain names into IP addresses. |
| Dynamic Host Configuration Protocol | DHCP | 67, 68 | UDP | Automatically assigns IP addresses and network configurations to devices. |
| Network Time Protocol | NTP | 123 | UDP | Synchronizes the clocks of computers on a network. |
| Lightweight Directory Access Protocol | LDAP | 389 | TCP | Used for accessing and maintaining distributed directory information services (e.g., Microsoft Active Directory). |

### 5. Windows Networking

| Protocol | Acronym | Port(s) | Transport | Description |
| :--- | :--- | :--- | :--- | :--- |
| Remote Procedure Call | RPC | 135 | TCP | Allows a program on one computer to execute a procedure on another computer. |
| NetBIOS | netbios-ns/ssn | 137-139 | TCP/UDP | A legacy protocol suite for name resolution and file/printer sharing on Windows LANs. |
| Server Message Block | SMB | 445 | TCP | The modern protocol for file sharing, printer sharing, and other network services in Windows environments. |

### 6. Voice and Session Management (VoIP)

| Protocol | Acronym | Port(s) | Transport | Description |
| :--- | :--- | :--- | :--- | :--- |
| Session Initiation Protocol | SIP | 5060, 5061| TCP | A signaling protocol used to establish, manage, and terminate real-time sessions like **VoIP** calls. |
| Voice Over IP | VoIP | Varies | Both | A technology that allows voice calls to be made over an IP network like the internet. |

### 7. Diagnostics & Control (ICMP)

**Internet Control Message Protocol (ICMP)** is a Layer 3 protocol used for error reporting and network diagnostics. It does not use ports.
*   **Key Function:** The `ping` and `traceroute` utilities use ICMP to test connectivity and map network paths.
*   **Time-To-Live (TTL):** An ICMP packet header field that limits a packet's lifetime. Each router decrements the TTL by 1. When it reaches 0, the packet is discarded, and an ICMP "Time Exceeded" message is sent back.
*   **OS Fingerprinting:** The initial TTL value is often default to the OS, which can be used to guess the target's operating system:
    *   **Windows:** Default TTL is often **128**.
    *   **Linux / macOS:** Default TTL is often **64**.
    *   **Solaris:** Default TTL is often **255**.
