# 11 - Data Flow Example


## Scenario: A User Visits `www.example.com`

Let's follow the complete journey of a data packet from a user's laptop to a web server and back.

### 1. Connecting to the Local Network
Before anything else, the laptop must connect to the local network (in this case, a home Wi-Fi network).

*   The user selects the correct Wi-Fi network (SSID).
*   They provide the WPA2/WPA3 password to authenticate.
*   The connection is established, and the laptop is now on the network but doesn't have an IP address yet.

### 2. Getting a Local IP Address (DHCP)
The laptop needs a valid IP address to communicate on the local network.

*   **DHCP Discover:** The laptop broadcasts a DHCP request, asking for an IP address.
*   **DHCP Offer/Request/Acknowledge:** The home router (acting as a DHCP server) assigns the laptop a **private IP address** (e.g., `192.168.1.10`), along with the subnet mask, default gateway (the router's own IP), and the DNS server address.

### 3. Translating the Domain Name (DNS)
The user types `www.example.com` into their browser. The laptop needs to find the server's public IP address.

*   **DNS Query:** The laptop sends a DNS query to its configured DNS server (provided by the ISP or a service like Google DNS).
*   **DNS Response:** After the resolution process, the DNS server responds with the public IP address for `www.example.com` (e.g., `93.184.216.34`).

### 4. Building the Packet (Data Encapsulation)
The laptop now has all the necessary addresses and prepares the data for transmission by encapsulating it through the network layers.

| Layer | Action | Source Address | Destination Address |
| :--- | :--- | :--- | :--- |
| **Application** | The browser creates an HTTP/HTTPS request for the webpage. | N/A | N/A |
| **Transport** | The request is wrapped in a TCP segment. | `51234` (random port) | `443` (HTTPS port) |
| **Internet** | The segment is wrapped in an IP packet. | `192.168.1.10` (laptop's private IP)| `93.184.216.34` (server's public IP)|
| **Link** | The packet is wrapped in a frame. The laptop uses ARP to find the router's MAC address. | Laptop's MAC Address | Router's MAC Address |

### 5. Leaving the Local Network (NAT)
The frame is sent to the home router (the default gateway).

*   The router receives the frame and inspects the IP packet inside.
*   It performs **Network Address Translation (NAT)**:
    *   It replaces the packet's source IP from the laptop's private IP (`192.168.1.10`) to the router's own **public IP address** (e.g., `203.0.113.45`).
    *   It records this translation in its NAT table.
*   The router forwards the modified packet out to the internet. The packet then travels through many other routers on its way to the destination.

### 6. Server Processing and Response
*   The packet arrives at the web server for `www.example.com` (`93.184.216.34`).
*   The server's firewall checks if incoming traffic on port 443 is allowed.
*   The server's OS receives the packet and sends the data to the web server application listening on port 443.
*   The web server processes the request and prepares the webpage data as a response.
*   The response packet is sent back, with the source and destination addresses flipped:
    *   **Source IP:** `93.184.216.34`
    *   **Destination IP:** `203.0.113.45` (your router's public IP)

### 7. Returning to the Laptop (NAT and Decapsulation)
*   The response packet arrives at the home router.
*   The router checks its NAT table, sees that this traffic is intended for the laptop at `192.168.1.10`, and translates the destination IP back to the laptop's private address.
*   The router forwards the packet to the laptop.
*   The laptop receives the packet and performs **decapsulation**—stripping away the headers at each layer (Link, Internet, Transport) until only the raw webpage data remains.
*   The browser renders the HTML, CSS, and JavaScript, and the user sees the webpage.
