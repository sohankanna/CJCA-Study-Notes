# Mac Addresses
A **MAC address** is a 48-bit (6-byte) unique, physical address assigned to a **Network Interface Card (NIC)** by the manufacturer. It is used to identify devices for communication *within a single, local network segment (LAN)*.

*   **Format:** Typically represented as six pairs of hexadecimal digits, separated by colons or hyphens (e.g., `DE:AD:BE:EF:13:37`).
*   **Standards:** Used by various Layer 2 technologies, including Ethernet, Wi-Fi, and Bluetooth.
*   **Mutability:** Although burned into the hardware, a MAC address can be changed or "spoofed" temporarily in software.

### Structure of a MAC Address
The 48-bit address is split into two halves:
1.  **Organizationally Unique Identifier (OUI):**
    *   The **first 24 bits** (3 bytes).
    *   Assigned by the IEEE to a specific manufacturer (e.g., Dell, Intel, Apple). This part identifies who made the network card.
2.  **Network Interface Controller (NIC) Specific:**
    *   The **last 24 bits** (3 bytes).
    *   A unique serial number assigned by the manufacturer to that specific device.

This combination ensures that, in theory, every MAC address in the world is unique.

---

## Special MAC Addresses and Bits

### Unicast, Multicast, and Broadcast
MAC addresses can be used to send frames to a single device, a group of devices, or all devices on the LAN.

*   **Unicast:** A standard MAC address that points to a **single, specific device**. This is the most common type of communication.
*   **Multicast:** A special address that sends a frame to a **specific group of devices** that have subscribed to that multicast group. The first octet will have its last bit set to `1`.
*   **Broadcast:** A special, reserved address (`FF:FF:FF:FF:FF:FF`) that sends a frame to **every single device** on the local network segment. This is used by protocols like ARP and DHCP when a device's specific address is unknown.

### Global vs. Local Bit
The second-to-last bit in the first octet determines if the address is globally unique (assigned by the IEEE) or locally administered (manually set by a network administrator).

---

## Address Resolution Protocol (ARP)

**ARP** is the critical protocol that bridges the gap between Layer 3 (IP addresses) and Layer 2 (MAC addresses) on a local network.

*   **Purpose:** To discover the MAC address associated with a known IP address.
*   **Process (ARP Resolution):**
    1.  **ARP Request:** A host (e.g., Computer A) wants to send data to another host on the same LAN (e.g., Computer B at `192.168.1.5`). Computer A sends a **broadcast** ARP request to `FF:FF:FF:FF:FF:FF`, essentially shouting, "**Who has the IP address `192.168.1.5`? Tell me your MAC address.**"
    2.  **ARP Reply:** All devices on the LAN receive the request, but only Computer B recognizes its own IP address. Computer B sends a **unicast** ARP reply directly back to Computer A, saying, "**I have `192.168.1.5`, and my MAC address is `DE:AD:BE:EF:13:37`.**"
    3.  **ARP Cache:** Computer A now knows the mapping and stores it in its local **ARP cache** for a short period so it doesn't have to ask again immediately.

---

## MAC Address Attack Vectors

Because MAC addresses can be spoofed and ARP relies on trust, they are susceptible to several attacks on a local network.

| Attack | Description |
| :--- | :--- |
| **MAC Spoofing** | An attacker changes their device's MAC address to impersonate another legitimate device on the network. This can be used to bypass **MAC address filtering**, a basic security measure where a network is configured to only allow access to a pre-approved list of MAC addresses. |
| **MAC Flooding** | An attacker bombards a network switch with a huge number of frames, each with a different, random source MAC address. This overwhelms the switch's MAC address table, causing it to fail-open and act like a dumb hub, broadcasting all traffic to all ports. This allows the attacker to sniff all traffic on the network segment. |
| **ARP Spoofing / Poisoning**| A **Man-in-the-Middle (MITM)** attack. The attacker sends falsified ARP replies to two devices (e.g., a victim and the router). They tell the victim that the router's IP address is at the attacker's MAC address, and they tell the router that the victim's IP address is at the attacker's MAC address. All traffic between the victim and the router now passes through the attacker's machine, allowing them to intercept, read, or modify it. |
