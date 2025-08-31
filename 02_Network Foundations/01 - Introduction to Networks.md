# Introduction to Networks 

A **network** is a collection of two or more interconnected devices that can communicate with each other to share data and resources.

### Key Networking Concepts

| Concept | Description | Analogy |
| :--- | :--- | :--- |
| **Nodes** | The individual devices connected to the network. | The people in a room. |
| **Links** | The communication pathways that connect the nodes. These can be wired (Ethernet) or wireless (Wi-Fi). | The air that carries the sound of people talking. |
| **Data Sharing**| The primary purpose of the network—the exchange of information. | The conversation happening between the people. |

Networks are essential for everything from sharing a printer in an office to accessing a website on the other side of the world.

---

## The Two Primary Types of Networks

Networks are primarily categorized by their geographical size and scope.

### 1. Local Area Network (LAN)

A **LAN** connects devices over a *short distance*, like within a single home, office building, or school.

*   **Geographical Scope:** Small and localized.
*   **Ownership:** Typically owned and managed by a single person or organization.
*   **Speed:** Very high data transfer speeds.
*   **Example:** Your home Wi-Fi network that connects your laptop, phone, and smart TV.

### 2. Wide Area Network (WAN)

A **WAN** connects multiple LANs over a *large geographical area*, such as across cities, countries, or even continents.

*   **Geographical Scope:** Large and widespread.
*   **Ownership:** Often has collective or distributed ownership (e.g., multiple Internet Service Providers).
*   **Speed:** Slower speeds compared to a LAN due to the vast distances data must travel.
*   **Example:** **The Internet** is the largest and most well-known example of a WAN.

### Comparing LAN and WAN

| Aspect | LAN | WAN |
| :--- | :--- | :--- |
| **Size** | Small, localized area | Large, broad area |
| **Ownership** | Single organization | Multiple organizations / ISPs |
| **Speed** | High | Lower than LAN |
| **Example** | Home / Office Network | The Internet |

---

## How LANs and WANs Work Together

LANs and WANs are not mutually exclusive; they work together to provide global connectivity.

*   **The Connection:** Your home or office LAN connects to the global WAN (the Internet) through an **Internet Service Provider (ISP)**.
*   **The Bridge Device:** A **modem** is the device that acts as a bridge between your LAN and the ISP's WAN. It translates the digital signals from your network into a format that can be transmitted over the ISP's infrastructure (like cable or fiber optic lines).

**The Workflow:**
1.  Your laptop (on your LAN) wants to access `google.com`.
2.  The request goes from your laptop to your router.
3.  The router sends the request to the modem.
4.  The modem sends the request out to your ISP's network (the WAN).
5.  The ISP routes your request across the Internet (the global WAN) to Google's servers.
6.  The response comes back following the same path in reverse.
