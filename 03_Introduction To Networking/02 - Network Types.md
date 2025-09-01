# 02: Network Types


---

## Common Terminology

These are the essential network types you will encounter and use regularly in the field.

| Type | Full Name | Description | Key Characteristics |
| :--- | :--- | :--- | :--- |
| **WAN** | Wide Area Network | A network that spans a large geographical area, connecting multiple LANs together. | The **Internet** is the most common example. Often uses public, routable IP addresses and WAN-specific routing protocols like BGP. |
| **LAN** | Local Area Network | A network confined to a small, local area like a single home, school, or office building. | Typically owned by a single entity. Uses private IP addresses from **RFC 1918** ranges (`10.x.x.x`, `172.16-31.x.x`, `192.168.x.x`). |
| **WLAN**| Wireless Local Area Network| A LAN that uses wireless technology (Wi-Fi) for connectivity instead of physical cables. | Functionally the same as a LAN but introduces wireless-specific security considerations. |
| **VPN** | Virtual Private Network| A technology that creates a secure, encrypted connection (a "tunnel") over a public network like the internet, making it seem as if the user is directly connected to a private network. | Its purpose is to make a remote user or network "feel" local. |

### The Three Main Types of VPNs

1.  **Site-to-Site VPN:**
    *   **What it is:** Connects two or more entire office networks together over the internet.
    *   **Use Case:** A company with offices in New York and London uses a site-to-site VPN so that employees in both locations can access shared resources as if they were in the same building.

2.  **Remote Access VPN:**
    *   **What it is:** Connects an individual user's computer to a remote private network.
    *   **Use Case:** **Hack The Box** uses OpenVPN to give your machine a `tun` adapter, placing it directly on the HTB lab network so you can access the target machines.
    *   **Split-Tunnel vs. Full-Tunnel:**
        *   **Split-Tunnel (like HTB):** Only traffic for the specific VPN network (e.g., `10.10.10.0/24`) goes through the tunnel. Your normal internet browsing goes through your regular internet connection. This is good for privacy and performance.
        *   **Full-Tunnel (Corporate Standard):** **All** of your traffic, including normal internet browsing, is routed through the company's network. This is less private but allows the company to monitor and protect you from threats.

3.  **SSL VPN (Clientless VPN):**
    *   **What it is:** A VPN that operates entirely within a web browser, typically used to stream a specific application or an entire remote desktop session.
    *   **Use Case:** The **Hack The Box Pwnbox** is a perfect example. It provides a full Linux desktop environment directly in your browser without requiring you to install any VPN client software.

---

## Book Terms

These terms are technically correct but are less common in everyday conversation. They are useful to know for certifications and for understanding the precise scale of networks.

| Type | Full Name | Description |
| :--- | :--- | :--- |
| **GAN** | Global Area Network| A network that spans the entire globe, connecting multiple WANs. The Internet is the primary example, but large multinational corporations might have private GANs. |
| **MAN** | Metropolitan Area Network| A network that spans a city or a large campus, connecting multiple LANs. It's larger than a LAN but smaller than a WAN. |
| **PAN / WPAN**| Personal Area Network / Wireless PAN | A very small-scale network for connecting devices within a person's immediate vicinity (a few meters). |
| | | A wired PAN might use USB. A **WPAN** is wireless, with **Bluetooth** being the most common example. |
