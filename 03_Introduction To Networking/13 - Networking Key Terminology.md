# Networking Key Terminology

 1. Core Application & File Sharing Protocols

These are the fundamental protocols used for everyday internet and network activities.

| Acronym  | Full Name                     | Description                                                                                                    |
| :------- | :---------------------------- | :------------------------------------------------------------------------------------------------------------- |
| **HTTP** | Hypertext Transfer Protocol   | The foundation of the World Wide Web. Used by browsers to request and receive web pages.                       |
| **FTP**  | File Transfer Protocol        | A standard protocol for transferring files between a client and a server on a network.                         |
| **SMTP** | Simple Mail Transfer Protocol | The primary protocol used for sending emails between servers.                                                  |
| **SMB**  | Server Message Block          | A protocol primarily used by Windows for sharing files, printers, and other resources on a local network.      |
| **NFS**  | Network File System           | The equivalent of SMB for Unix/Linux systems, used for accessing files over a network.                         |
| **SSH**  | Secure Shell                  | A secure protocol for remote command-line access, remote command execution, and other secure network services. |
| **RSH**  | Remote Shell                  | An older, **insecure** predecessor to SSH for remote command execution.                                        |

## 2. Routing & Switching Protocols (Infrastructure)

These protocols are used by network devices to manage traffic flow and network topology.

| Acronym | Full Name | Description |
| :--- | :--- | :--- |
| **RIP** | Routing Information Protocol | An older, simple distance-vector routing protocol for small networks. |
| **OSPF** | Open Shortest Path First| A modern, efficient interior gateway routing protocol used within a single autonomous system (like a corporate network). |
| **IGRP / EIGRP** | (Enhanced) Interior Gateway Routing Protocol | Cisco-proprietary routing protocols. EIGRP is an advanced distance-vector protocol. |
| **STP** | Spanning Tree Protocol | A Layer 2 protocol that prevents network loops in topologies with redundant switch connections. |
| **VLAN** | Virtual Local Area Network| A method for logically segmenting a single physical network switch into multiple, separate broadcast domains. |
| **VTP** | VLAN Trunking Protocol| A Cisco protocol used to manage and synchronize VLAN information across multiple switches. |
| **HSRP / VRRP** | Hot Standby Router Protocol / Virtual Router Redundancy Protocol | Protocols that provide router redundancy, allowing for automatic failover if a primary router fails. HSRP is Cisco-proprietary. |

## 3. Security & Authentication Protocols

These protocols are specifically designed to provide security services like encryption and authentication.

| Acronym | Full Name | Description |
| :--- | :--- | :--- |
| **WEP** | Wired Equivalent Privacy | An old and **highly insecure** Wi-Fi encryption standard. **Do not use.** |
| **WPA** | Wi-Fi Protected Access| A family of security protocols (WPA, WPA2, WPA3) that are much more secure than WEP for protecting wireless networks. |
| **TKIP** | Temporal Key Integrity Protocol | An encryption protocol used with the original WPA. Now considered insecure and deprecated in favor of AES. |
| **IPsec** | Internet Protocol Security| A suite of protocols that provides encryption and authentication at the IP (Network) layer. A core component of many VPNs. |
| **PGP** | Pretty Good Privacy | An encryption program used to secure emails and files through cryptographic privacy and authentication. |
| **EAP** | Extensible Authentication Protocol | An authentication framework used in wireless networks and point-to-point connections. It supports multiple authentication methods. |
| **LEAP / PEAP** | Lightweight EAP / Protected EAP | Specific implementations of EAP. LEAP is a less secure, Cisco-proprietary version. PEAP is more secure and creates an encrypted tunnel. |
| **TACACS** | Terminal Access Controller Access-Control System | A protocol (often `TACACS+`) that provides centralized authentication, authorization, and accounting (AAA) for network devices like routers and switches. |

## 4. VPN & Tunneling Protocols

These are used to create secure, private connections over public networks.

| Acronym | Full Name | Description |
| :--- | :--- | :--- |
| **VPN** | Virtual Private Network| A technology that creates a secure, encrypted connection over the internet. |
| **PPTP** | Point-to-Point Tunneling Protocol | An older and now insecure VPN protocol. |
| **IKE** | Internet Key Exchange| A protocol used within IPsec to set up a secure, authenticated communication channel. |
| **GRE** | Generic Routing Encapsulation | A tunneling protocol that can encapsulate a wide variety of network layer protocols inside virtual point-to-point links. |
| **NAT** | Network Address Translation| A technology that allows multiple devices on a private network to share a single public IP address. |

## 5. Management & Other Protocols

| Acronym | Full Name | Description |
| :--- | :--- | :--- |
| **SNMP** | Simple Network Management Protocol | A protocol used for monitoring and managing network devices (routers, switches, servers). |
| **NTP** | Network Time Protocol | Used to synchronize the clocks of computers over a network, which is critical for logging and security. |
| **SIP** | Session Initiation Protocol| A signaling protocol used to establish, manage, and terminate real-time sessions like **VoIP** calls. |
| **VOIP** | Voice Over IP | A technology that allows voice calls to be made over an IP network like the internet. |
| **CDP** | Cisco Discovery Protocol| A Cisco-proprietary protocol used by Cisco devices to discover information about other directly connected Cisco devices. |

## 6. Web & Development Terminology

| Acronym | Full Name | Description |
| :--- | :--- | :--- |
| **URI / URL**| Uniform Resource Identifier / Locator | A string of characters used to identify a resource on the internet. A URL is a type of URI that also specifies how to access it (e.g., `https://`). |
| **CRLF** | Carriage Return Line Feed | A sequence of two control characters (`\r\n`) used to signify the end of a line in some protocols, notably HTTP. |
| **AJAX** | Asynchronous JavaScript and XML | A web development technique for creating dynamic, interactive web applications without needing to reload the entire page. |
| **ISAPI** | Internet Server Application Programming Interface | A Microsoft API for web servers that allows for high-performance web extensions. |

## 7. Industrial & Systems Management

| Acronym | Full Name | Description |
| :--- | :--- | :- |
| **SCADA**| Supervisory Control and Data Acquisition | A type of Industrial Control System (ICS) used to monitor and control large-scale industrial processes (e.g., power grids, water treatment plants). |
| **SMS / MBSA**| Systems Management Server / Microsoft Baseline Security Analyzer| Microsoft tools for managing systems and analyzing their security posture for vulnerabilities. |
