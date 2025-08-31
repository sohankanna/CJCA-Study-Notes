# 04 - Network Communication

## 1. MAC Addresses (The Physical Address)

A **MAC (Media Access Control) address** is a unique, permanent hardware identifier assigned to a Network Interface Card (NIC). It is used for communication *within a single local network (LAN)*.

*   **OSI Layer:** Layer 2 (Data Link).
*   **Format:** A 48-bit number, typically shown as six pairs of hexadecimal digits (e.g., `00:1A:2B:3C:4D:5E`).
    *   The first half (24 bits) is the **OUI** (Organizationally Unique Identifier), which identifies the manufacturer.
    *   The second half (24 bits) is a unique serial number assigned by the manufacturer.
*   **Analogy:** A MAC address is like the **serial number** on a specific appliance. It's unique to that physical piece of hardware and doesn't change.
*   **Key Protocol:** **ARP (Address Resolution Protocol)** is used on a LAN to map a known IP address to its corresponding MAC address. It essentially asks, "Who has this IP address, and what is your MAC address?"

---

## 2. IP Addresses (The Logical Address)

An **IP (Internet Protocol) address** is a logical, numerical label assigned to a device on a network. It is used to identify devices and route traffic *across different networks* (like the internet).

*   **OSI Layer:** Layer 3 (Network).
*   **Versions:**
    *   **IPv4:** The most common. A 32-bit address, shown as four decimal numbers (e.g., `192.168.1.1`).
    *   **IPv6:** A newer, 128-bit address designed to overcome the shortage of IPv4 addresses. Shown as eight groups of hexadecimal digits (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).
*   **Analogy:** An IP address is like your **home's mailing address**. It tells the postal service (routers) how to deliver mail to your specific house on your specific street. It can change if you move to a new house (connect to a new network).
*   **Key Function:** Routers use IP addresses to make decisions on how to forward packets from one network to another to reach their final destination.

---

## 3. Ports (The Application Address)

A **port** is a number used to identify a specific application or service running on a device. It allows a single device with one IP address to handle multiple network communications simultaneously.

*   **OSI Layer:** Layer 4 (Transport).
*   **Analogy:** A port is like an **apartment number** in a large apartment building. The IP address gets the mail to the building, but the port number ensures it gets to the correct apartment (application) inside.
*   **Port Ranges:** Ports are numbered from 0 to 65535 and are divided into three categories.

| Port Range | Name | Description | Examples |
| :--- | :--- | :--- | :--- |
| **0 - 1023** | **Well-Known Ports**| Reserved by IANA for standard, universally recognized services. | **80** (HTTP), **443** (HTTPS), **22** (SSH), **21** (FTP) |
| **1024 - 49151**| **Registered Ports**| Assigned by IANA for specific applications or services (e.g., database servers). | **3306** (MySQL), **1433** (Microsoft SQL) |
| **49152 - 65535**| **Dynamic / Private / Ephemeral Ports**| Used for temporary, outbound connections from a client. When your browser connects to a web server, your OS assigns a random port from this range for the session. | Varies (e.g., 51234) |

---

## Putting It All Together: Browsing a Website

Here’s how MAC addresses, IP addresses, and ports work in concert when you visit `example.com`:

1.  **Application Layer:** Your browser creates an HTTP request for `example.com`.
2.  **DNS Lookup:** Your computer asks a DNS server for the IP address of `example.com` and gets back `93.184.216.34`.
3.  **Transport Layer:** The HTTP request is wrapped in a **TCP segment**.
    *   **Destination Port:** `443` (for HTTPS).
    *   **Source Port:** A random dynamic port, e.g., `51234`, is assigned by your OS.
4.  **Network Layer:** The TCP segment is wrapped in an **IP packet**.
    *   **Destination IP:** `93.184.216.34`.
    *   **Source IP:** Your computer's public IP address.
5.  **Data Link Layer:** The IP packet is wrapped in an **Ethernet frame** for transmission on your local network.
    *   **Destination MAC:** Your computer uses **ARP** to find the MAC address of your local router (the default gateway).
    *   **Source MAC:** Your computer's NIC MAC address.
6.  **Transmission:** The frame is sent to your router. The router strips off the frame, looks at the destination IP address, and forwards the packet to the next router on the path to `example.com`. This process repeats across the internet.
7.  **Server Processing:** The `example.com` server receives the packet. Its OS sees the destination port `443` and delivers the data to the web server application. The web server processes the request and sends the webpage back, following the same path in reverse to your IP address and the source port `51234`.
