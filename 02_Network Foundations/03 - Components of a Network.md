# 03 - Components of a Network


A network is built from four primary types of components:

1.  **End Devices:** The devices that users interact with.
2.  **Intermediary Devices:** The "traffic cops" that manage and direct data flow.
3.  **Network Media:** The physical pathways that carry the data signals.
4.  **Servers:** Powerful computers that provide services to end devices.

---

## 1. End Devices (Hosts)

An **end device** (or **host**) is any device that is at the beginning or end of a network communication. They are the devices that send and receive data.

*   **Examples:** Computers, smartphones, tablets, printers, IoT/Smart Devices.
*   **Role:** They serve as the user's interface to the network, allowing them to generate and consume data (e.g., browsing a website, sending an email).

---

## 2. Intermediary Devices

An **intermediary device** connects end devices and other networks, facilitating the flow of data between them. They are responsible for directing traffic efficiently and securely.

### Key Intermediary Devices

| Device | OSI Layer | Primary Function | Analogy |
| :--- | :--- | :--- | :--- |
| **Router** | **Layer 3 (Network)** | Connects **different** networks together and forwards packets between them based on **IP addresses**. It determines the best path for traffic to take across the internet. | The postal service sorting office that directs mail between different cities. |
| **Switch** | **Layer 2 (Data Link)** | Connects multiple devices **within the same** local network (LAN). It forwards data frames only to the specific device it's intended for, based on **MAC addresses**. | An office mailroom clerk who delivers mail directly to the correct person's desk. |
| **Hub** | **Layer 1 (Physical)** | A legacy device that connects multiple devices in a LAN. It broadcasts any incoming data to **all** connected devices, regardless of the destination. It is inefficient and insecure. | An office mailroom clerk who shouts every message out loud for the whole office to hear. |
| **Access Point (AP)** | Layer 2 | Allows wireless devices (Wi-Fi) to connect to a wired network. | A wireless "on-ramp" to the main network highway. |
| **Modem** | N/A | Connects a local network (LAN) to a wide area network (WAN), like the internet, by translating signals for the ISP's infrastructure. | A translator between your computer's digital language and the ISP's cable/fiber language. |

### Network Interface Card (NIC)
*   **What it is:** A hardware component inside every networked device (computer, phone, server) that provides the physical connection to the network.
*   **Unique Identifier:** Every NIC has a unique, hard-coded **MAC (Media Access Control) address**, which is used by switches for local communication on a LAN.

---

## 3. Network Media and Software

### Network Media
This is the physical medium used to transmit data signals.
*   **Wired Media:**
    *   **Ethernet Cables (Twisted Pair):** The most common for LANs. Use **RJ-45 connectors**.
    *   **Fiber Optic Cables:** Used for high-speed, long-distance connections.
*   **Wireless Media:**
    *   **Wi-Fi (Radio Waves):** The most common for wireless LANs.

### Software Components
*   **Network Protocols:** The set of rules that govern how data is formatted, addressed, transmitted, and received (e.g., **TCP/IP**, **HTTP**).
*   **Network Management Software:** Tools used by administrators to monitor, configure, and maintain the network.
*   **Software Firewalls (Host-based):** Security software installed on an individual end device to monitor and control its incoming and outgoing traffic.

---

## 4. Servers

A **server** is a powerful computer or program that provides a service to other computers (known as **clients**) on the network. This is known as the **Client-Server Model**.

### Common Types of Servers
| Server Type | Purpose |
| :--- | :--- |
| **Web Server** | Hosts websites and serves web pages to clients (browsers). |
| **File Server** | Stores and manages files, allowing clients to access them over the network. |
| **Mail Server** | Handles the sending, receiving, and storing of emails. |
| **Database Server** | Stores and manages data in a structured database, responding to queries from clients. |
