# The TCPIP Model

The TCP/IP model is a more condensed version of the OSI model, combining several layers to reflect a more practical implementation.

| TCP/IP Layer | Corresponding OSI Layers | Key Function | Core Protocols |
| :--- | :--- | :--- | :--- |
| **4. Application** | 7, 6, 5 (Application, Presentation, Session) | Provides network services directly to applications and defines the protocols they use to exchange data. This is the layer that users interact with. | HTTP, FTP, SMTP, DNS |
| **3. Transport** | 4 (Transport) | Responsible for end-to-end communication between hosts. It provides session (TCP) and datagram (UDP) services to the Application Layer. | **TCP**, **UDP** |
| **2. Internet** | 3 (Network) | Responsible for logical addressing, packaging, and routing functions. It moves packets from their source to their destination across different networks. | **IP**, ICMP |
| **1. Link (or Network Access)**| 2, 1 (Data Link, Physical) | Responsible for placing TCP/IP packets onto the physical network medium and receiving them. It deals with the hardware aspects of the network. | Ethernet, Wi-Fi |

**Key Takeaway:** The TCP/IP model is designed to be independent of the underlying hardware. This means it can run over any physical medium (Ethernet, Wi-Fi, fiber optics), making it universally adaptable.

---

## The Core Tasks of the TCP/IP Protocol Suite

The TCP/IP suite is a collection of protocols, with TCP and IP being the most important. Together, they perform the essential tasks needed for global internet communication.

| Task | Primary Protocol(s) | Description |
| :--- | :--- | :--- |
| **Logical Addressing** | **IP (Internet Protocol)** | IP is responsible for assigning a unique logical address (the IP address) to every device on a network. This allows for the structuring of large networks and ensures data packets are sent to the correct destination network. Techniques like subnetting and CIDR are used to manage this addressing. |
| **Routing** | **IP (Internet Protocol)** | As packets travel from a source to a destination, routers at each "hop" use the destination IP address to determine the next best path to forward the packet. This allows data to cross multiple, independent networks to reach its goal, even if the sender doesn't know the exact location of the receiver. |
| **Error & Flow Control (Reliability)**| **TCP (Transmission Control Protocol)**| TCP establishes a reliable, connection-oriented "virtual circuit" between the sender and receiver. It ensures that all data arrives in the correct order and without errors by using acknowledgments and retransmitting lost packets. It also manages flow control to prevent the sender from overwhelming the receiver. |
| **Application Support** | **TCP** and **UDP (User Datagram Protocol)**| The Transport layer uses **port numbers** to direct data to the correct application on a host. This allows a single device with one IP address to run multiple network services (like a web server and an email server) simultaneously. |
| **Name Resolution** | **DNS (Domain Name System)**| DNS is an Application layer protocol within the TCP/IP suite that translates human-readable domain names (e.g., `www.hackthebox.com`) into their corresponding IP addresses, which are required for routing at the Internet layer. |
