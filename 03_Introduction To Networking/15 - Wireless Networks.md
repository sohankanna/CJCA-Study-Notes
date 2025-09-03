# Wireless Networks

## What is a Wireless Network?

A **wireless network** uses radio frequency (RF) signals to connect devices without the need for physical cables. **Wi-Fi** is the most common technology for creating a Wireless Local Area Network (WLAN).

*   **How it Works:** Devices with wireless adapters communicate with a central **Wireless Access Point (WAP)**, which is typically part of a wireless router. The WAP acts as a gateway, connecting the wireless devices to the wired network and the internet.
*   **Frequencies:** Wi-Fi primarily operates on the **2.4 GHz** and **5 GHz** frequency bands.

### The Wi-Fi Connection Process
1.  A device scans for available networks by listening for **beacon frames**, which are broadcast by WAPs and contain the network's name (**SSID**).
2.  The user selects an SSID and provides a password (if required).
3.  The device sends an **association request frame** to the WAP. This frame includes the device's MAC address and its supported security protocols.
4.  The WAP and the device perform an authentication handshake.
5.  If successful, the device is associated with the network and can then request an IP address via DHCP.

---

## Wireless Security Protocols

Securing a wireless network is critical because its signals are broadcast through the air and can be easily intercepted.

### 1. WEP (Wired Equivalent Privacy)
*   **Description:** An old and **highly insecure** encryption standard.
*   **Encryption:** Uses the weak RC4 stream cipher with a small, static key.
*   **Vulnerabilities:** Suffers from a flawed implementation of its Initialization Vector (IV), which allows attackers to crack the encryption key in minutes.
*   **Status:** **Completely deprecated. Do not use.**

### 2. WPA / WPA2 / WPA3 (Wi-Fi Protected Access)
This is the modern family of security protocols designed to replace WEP.

*   **WPA:** The first version, which introduced **TKIP** (Temporal Key Integrity Protocol) to fix WEP's flaws. It is now also considered insecure.
*   **WPA2:** The long-standing industry standard. It introduced the **AES (Advanced Encryption Standard)** cipher, which is very strong. This is the minimum level of security that should be used today.
*   **WPA3:** The latest standard, offering even stronger encryption and protection against modern attacks.

### WPA Modes
*   **WPA-Personal (WPA-PSK):** Designed for home and small office use. It uses a single **Pre-Shared Key (PSK)**—the Wi-Fi password that everyone uses to connect.
*   **WPA-Enterprise (802.1X):** Designed for corporate environments. It does not use a single shared password. Instead, each user authenticates with their own unique credentials (e.g., username and password) against a central authentication server like **RADIUS** or **TACACS+**.

---

## Common Wireless Attacks

| Attack | Description |
| :--- | :--- |
| **Cracking WEP/WPA-PSK** | Attackers capture a large number of wireless packets and use specialized tools to perform a statistical or brute-force attack to recover the encryption key or password. |
| **Disassociation Attack** | An attacker sends spoofed "disassociation" frames to a connected client, pretending to be the WAP. This forces the client to disconnect from the network, disrupting service. This is often used as a preliminary step to capture the WPA handshake when the client tries to reconnect. |
| **Evil Twin Attack** | An attacker sets up a rogue WAP with the same SSID as a legitimate network (e.g., "Free_Airport_WiFi"). Unsuspecting users connect to the attacker's network, allowing the attacker to perform a **Man-in-the-Middle (MITM)** attack and intercept all their traffic. |

---

## Wireless Network Hardening (Best Practices)

These are essential steps to secure a wireless network.

1.  **Use Strong Encryption (WPA2/WPA3):**
    *   This is the most important step. Always use **WPA2-AES** at a minimum. WPA3 is even better if your devices support it.
    *   Use a long, complex, and unique password (passphrase) for WPA-Personal.

2.  **MAC Filtering:**
    *   **What it is:** A security feature that allows you to create a "whitelist" of MAC addresses. Only devices with an approved MAC address can connect to the network.
    *   **Effectiveness:** Provides a basic layer of security but can be easily bypassed by an attacker using **MAC spoofing**. It should not be relied upon as the sole security measure.

3.  **Disable SSID Broadcasting (Hiding the Network):**
    *   **What it is:** A setting that stops the WAP from broadcasting its network name (SSID) in beacon frames. The network becomes "hidden."
    *   **Effectiveness:** A minor security measure that can deter casual snoops but is trivially bypassed by any serious attacker, as the SSID is still transmitted in other management frames. It is considered "security through obscurity."

4.  **Deploy WPA-Enterprise (802.1X):**
    *   For corporate environments, this is the most secure method. It eliminates the risk of a shared password being compromised and provides individual accountability.
    *   **EAP-TLS** is a very strong authentication method within this framework, using digital certificates on both the client and server side for mutual authentication.

5.  **Network Segmentation:**
    *   Create a separate, isolated guest network for visitors. This prevents guests from having any access to your trusted internal network resources.
