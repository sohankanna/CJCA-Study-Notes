# 05 - Dynamic Host Configuration Protocol (DHCP)

The **Dynamic Host Configuration Protocol (DHCP)** is a network protocol used to automatically assign IP addresses and other critical network configuration parameters to devices on a network.

**Core Idea:** Instead of a network administrator manually configuring every single device (which is slow and prone to errors), DHCP acts like an automated receptionist, handing out network settings to each device as it connects.

### Why is DHCP Important?
*   **Simplifies Network Management:** It eliminates the need for manual IP address assignment, saving significant administrative effort.
*   **Prevents IP Conflicts:** It ensures that every device receives a unique IP address, preventing the communication issues that arise from duplicate addresses.
*   **Optimizes IP Address Usage:** It maintains a pool of available IP addresses and "leases" them to devices. When a device disconnects, its IP address is returned to the pool and can be recycled for a new device.

---

## How DHCP Works: The DORA Process

The DHCP process involves a four-step conversation between a client (a device needing an IP) and a DHCP server. This is commonly known as **DORA**.

### The Players
*   **DHCP Client:** Any device that connects to the network and needs an IP address (e.g., your laptop, smartphone).
*   **DHCP Server:** A network device (often a router or a dedicated server) that manages a pool of IP addresses and hands them out to clients.

### The Four Steps of DORA

| Step | Acronym | Description |
| :--- | :--- | :--- |
| 1. **Discover** | **D** | The **client** connects to the network and broadcasts a `DHCP Discover` message to everyone, essentially shouting, "Is there a DHCP server out there that can give me an IP address?" |
| 2. **Offer** | **O** | Any **DHCP server** that hears the broadcast responds with a `DHCP Offer` message, saying, "I have an IP address for you. Here is an offer to use `192.168.1.10`." |
| 3. **Request** | **R** | The **client** receives one or more offers and chooses one (usually the first one it receives). It then broadcasts a `DHCP Request` message, announcing, "I would like to accept the offer for IP address `192.168.1.10` from that server." |
| 4. **Acknowledge** | **A** | The **DHCP server** that made the offer sees the request and sends a final `DHCP Acknowledge` (ACK) message, confirming, "Great! The IP address `192.168.1.10` is now officially assigned to you." The client can now use this IP to communicate. |

---

## IP Address Leasing and Renewal

The IP address assigned by DHCP is not permanent; it's a **lease** for a specific period of time (e.g., 24 hours).

*   **Lease Time:** A pre-configured duration for which a client can use an IP address.
*   **Renewal Process:** Before the lease expires, the client must send another `DHCP Request` to the server to renew the lease. If the server agrees, it sends back a `DHCP Acknowledge`, and the lease time is extended.
*   **Purpose:** Leasing ensures that IP addresses from devices that are no longer on the network are eventually returned to the pool for reuse.
