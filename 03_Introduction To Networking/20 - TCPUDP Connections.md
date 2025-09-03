# TCPUDP Connections

## TCP vs. UDP: A Core Comparison

| Feature | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
| :--- | :--- | :--- |
| **Connection Type** | **Connection-Oriented** | **Connectionless** |
| **How it Works** | Establishes a reliable **Three-Way Handshake** before sending data, creating a virtual connection. | Sends data packets ("datagrams") immediately without establishing a prior connection. |
| **Reliability** | **High.** Guarantees that all packets are received in the correct order and without errors by using sequence numbers and acknowledgments. Lost packets are retransmitted. | **Low.** No guarantees of delivery, order, or error checking. It's a "fire and forget" protocol. |
| **Speed** | **Slower** due to the overhead of ensuring reliability. | **Faster** due to the lack of connection setup and error-checking overhead. |
| **Use Cases** | Web browsing (HTTP/S), email (SMTP), file transfers (FTP) — anywhere reliability is critical. | Video streaming, online gaming, VoIP, DNS — anywhere speed is more important than perfect reliability. |
| **Analogy** | A telephone call. | Sending a postcard. |

---

## The IP Packet (Layer 3)

Both TCP segments and UDP datagrams are encapsulated inside an **IP Packet** for transmission across networks. Think of the IP packet as the "envelope" that carries the data.

### The IP Header
The IP header contains crucial information for routing the packet.

| Field | Description |
| :--- | :--- |
| **Version** | Indicates the IP version (e.g., `4` for IPv4). |
| **Source / Destination IP** | The logical addresses of the sending and receiving hosts. |
| **Time to Live (TTL)** | A counter that prevents packets from looping endlessly on the network. Each router decrements this value by 1. |
| **Protocol** | A number that identifies the protocol of the payload. **`6` indicates TCP**, and **`17` indicates UDP**. |
| **Identification (ID)** | A unique 16-bit number for each packet sent from a host. This value typically increments sequentially. It is primarily used to reassemble fragmented packets. |
| **Checksum** | An error-checking value for the header itself. |
| **Options** | Optional fields, such as the **Record Route** option. |

#### Using the IP ID Field for Host Discovery
Because the IP ID field usually increments for each packet a host sends, you can sometimes infer that multiple source IP addresses belong to the **same physical machine** (a multi-homed host) if you observe a continuous, sequential stream of IP ID values coming from those different IPs.

#### The `ping -R` (Record Route) Option
The Record Route option in the IP header instructs each router along the path to add its IP address to the packet. This allows you to see the path a packet took to its destination, similar to a `traceroute`.

### The IP Payload
This is the actual data being carried inside the IP packet. For Layer 4, the payload will be either a **TCP segment** or a **UDP datagram**.

---

## The TCP Segment (Layer 4)

The TCP "payload" itself has its own header with important fields for managing a reliable connection.
*   **Source / Destination Port:** Identifies the sending and receiving applications.
*   **Sequence Number:** A number used to track and reorder the data segments correctly on the receiving end.
*   **Acknowledgment Number:** Confirms that data has been successfully received.
*   **Control Flags:** Bits that control the state of the connection (e.g., `SYN`, `ACK`, `FIN`, `RST`).
*   **Window Size:** Used for flow control, indicating how much data the receiver can accept.
*   **Checksum:** An error-checking value for both the header and the payload data.

---

## UDP Datagram (Layer 4)

A UDP datagram has a much simpler header, reflecting its connectionless nature. It contains a source port, destination port, length, and checksum, but none of the complex fields for sequencing or acknowledgments that TCP has.

---

## Attacks Related to TCP/UDP

### Traceroute
The `traceroute` (or `tracert` on Windows) utility cleverly uses network protocols to map the route to a destination.
*   **How it Works (Unix/Linux):** It sends UDP datagrams with an initial TTL of 1. The first router discards the packet and sends back an ICMP "Time Exceeded" message. `traceroute` records that router's IP. It then sends another UDP datagram with a TTL of 2, and so on, until the packet reaches the final destination, which responds with an ICMP "Port Unreachable" message.

### Blind Spoofing
This is a type of attack where an attacker sends packets to a target with a **spoofed (fake) source IP address**.
*   **The "Blind" Part:** Because the source IP is fake, the attacker does not receive the direct responses from the target.
*   **The Goal:** It can be used to disrupt connections (e.g., by sending forged TCP Reset packets) or to try and establish a connection by predicting the target's TCP sequence numbers.
