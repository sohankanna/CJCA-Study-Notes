# 02- Network Concepts


Network models are conceptual frameworks that standardize how network communication works by breaking it down into a series of layers. Each layer has a specific job and only communicates with the layer directly above and below it.

### 1. The OSI Model (Open Systems Interconnection)
The **OSI model** is a 7-layer theoretical framework. It's primarily used as a teaching and reference tool to understand the complete process of network communication.

| Layer # | Layer Name | Key Function | PDU | Devices / Protocols |
| :--- | :--- | :--- | :--- | :--- |
| **7** | **Application** | Provides network services directly to end-user applications. | Data | HTTP, FTP, SMTP, DNS |
| **6** | **Presentation**| Acts as a data translator. Handles encryption, compression, and formatting. | Data | SSL/TLS, JPEG, ASCII |
| **5** | **Session** | Establishes, manages, and terminates connections (sessions) between applications. | Data | APIs, NetBIOS |
| **4** | **Transport** | Provides reliable (or unreliable) end-to-end data delivery between hosts. | Segments (TCP) <br> Datagrams (UDP) | TCP, UDP |
| **3** | **Network** | Handles logical addressing (IP addresses) and routing of packets across networks. | Packets | Routers, IP, ICMP |
| **2** | **Data Link** | Provides node-to-node data transfer. Handles physical addressing (MAC addresses). | Frames | Switches, MAC addresses |
| **1** | **Physical** | Transmits raw bits over a physical medium. | Bits | Cables, Hubs, NICs |

*PDU = Protocol Data Unit, the name for a "chunk" of data at a specific layer.*

<img width="319" height="229" alt="Screenshot 2025-08-31 114951" src="https://github.com/user-attachments/assets/628b90d4-2ba8-414b-8ba1-9af5acd0d3cb" />


### 2. The TCP/IP Model
The **TCP/IP model** is a 4-layer practical model that is the foundation of the modern internet. It is a more condensed and real-world implementation of the concepts in the OSI model.

| Layer # | Layer Name | Key Function | OSI Layers |
| :--- | :--- | :--- | :--- |
| **4** | **Application** | User-facing protocols and services. | 5, 6, 7 |
| **3** | **Transport** | End-to-end data delivery (TCP/UDP). | 4 |
| **2** | **Internet** | Packet routing and logical addressing (IP). | 3 |
| **1** | **Link / Network Interface** | Physical transmission and hardware addressing. | 1, 2 |

**Key Takeaway:** The OSI model is the "theory," and the TCP/IP model is the "practice." A network analyst uses the OSI model to conceptualize problems, but works with the protocols of the TCP/IP model.
<br>
<img width="160" height="275" alt="Screenshot 2025-08-31 115044" src="https://github.com/user-attachments/assets/0575fbc6-b23f-415e-8aa8-d9f2a33d03c2" />

<img width="446" height="318" alt="Screenshot 2025-08-31 115150" src="https://github.com/user-attachments/assets/bf937e13-5a1a-4d62-a81e-6a998e8e6b82" />

## Protocols

**Protocols** are the standardized sets of rules that allow devices to communicate. Each protocol has a specific job and operates at a specific layer of the network models.

### Common Network Protocols

| Protocol | Full Name | Layer | Purpose |
| :--- | :--- | :--- | :--- |
| **HTTP** | Hypertext Transfer Protocol | Application | Used for transferring web pages. |
| **FTP** | File Transfer Protocol | Application | Used for transferring files between systems. |
| **SMTP** | Simple Mail Transfer Protocol | Application | Used for sending emails. |
| **TCP** | Transmission Control Protocol | Transport | **Reliable**, connection-oriented data delivery. It guarantees that all data arrives in the correct order. |
| **UDP** | User Datagram Protocol | Transport | **Unreliable**, connectionless data delivery. It is fast but does not guarantee delivery. Used for streaming video or online gaming. |
| **IP** | Internet Protocol | Internet / Network | Handles the logical addressing and routing of packets to ensure they reach the correct destination network. |

---

## Transmission

Transmission is the physical process of sending data signals over a medium.

### Transmission Modes
This defines the direction of communication flow.

*   **Simplex:** One-way communication only (e.g., a radio broadcast).
*   **Half-Duplex:** Two-way communication, but not at the same time (e.g., a walkie-talkie).
*   **Full-Duplex:** Two-way communication simultaneously (e.g., a telephone call).

### Transmission Media
This is the physical path the data travels on.

*   **Wired Media:**
    *   **Twisted Pair (Ethernet Cable):** Most common for LANs.
    *   **Coaxial Cable:** Used for cable TV and internet.
    *   **Fiber Optic Cable:** Transmits data as pulses of light. Used for high-speed backbones and long distances.
*   **Wireless Media:**
    *   **Radio Waves:** Used for Wi-Fi and cellular networks.
    *   **Microwaves:** Used for satellite and point-to-point communications.
