# 07 - Domain Name System (DNS)

The **Domain Name System (DNS)** is a global, hierarchical, and decentralized naming system for computers, services, or any resource connected to the internet.

**Core Idea:** DNS acts as the **phonebook of the internet**. It allows us to use easy-to-remember names (like `www.google.com`) instead of having to memorize complex numerical IP addresses (like `142.251.46.174`).

### Domain Names vs. IP Addresses

| Type | Description | Example |
| :--- | :--- | :--- |
| **Domain Name** | A human-readable, memorable name for a resource on the internet. | `www.hackthebox.com` |
| **IP Address** | The numerical address that computers use to find each other on a network. | `104.22.60.128` |

---

## The DNS Hierarchy

DNS is organized in a tree-like structure, with each level managed by different entities.

*   **(.) The Root:** The top of the hierarchy, represented by a single dot. There are a small number of root server clusters distributed globally that know where to find the TLD servers.
*   **Top-Level Domain (TLD):** The last part of a domain name.
    *   *Examples:* `.com`, `.org`, `.net`, and country codes like `.uk` or `.de`.
*   **Second-Level Domain:** The unique name that an individual or organization registers.
    *   *Example:* `hackthebox` in `hackthebox.com`.
*   **Subdomain / Hostname:** Prefixes added to the second-level domain to organize a site or point to specific servers.
    *   *Example:* `www` in `www.hackthebox.com` or `academy` in `academy.hackthebox.com`.

---
<img width="1018" height="350" alt="https___external-content duckduckgo com_iu__u=https_3A_2F_2Flh4 googleusercontent com_2F-Lx69aIsa078_2FTXuNzpIGRbI_2FAAAAAAAAACw_2F95JWAs_yYsw_2Fs1600_2FURL" src="https://github.com/user-attachments/assets/fecdcfa7-73c5-4aa5-ab61-962d92843bbd" />

## The DNS Resolution Process

This is the step-by-step process of translating a domain name into an IP address.

### The Key Players
*   **Your Computer (DNS Client):** The device initiating the request.
*   **Recursive DNS Server:** Usually provided by your ISP or a third-party service (like Google's `8.8.8.8`). Its job is to do all the work of finding the final answer for the client.
*   **Root Server:** Knows where to find the TLD servers.
*   **TLD Server:** Knows where to find the authoritative name servers for a specific TLD (e.g., the `.com` TLD server knows about `google.com`, `hackthebox.com`, etc.).
*   **Authoritative Name Server:** The final authority. This is the server that holds the actual DNS records for a specific domain (e.g., Google's own DNS server, which knows the IP address for `www.google.com`).

### The Steps
Let's say you type `www.example.com` into your browser:

1.  **Local Cache Check:** Your computer first checks its own local DNS cache to see if it has recently looked up this domain. If the answer is found here, the process stops.
2.  **Query Recursive Server:** If not in the local cache, your computer sends the query to its configured **recursive DNS server**.
3.  **Recursive Server Queries Root:** The recursive server, which doesn't know the answer, starts at the top. It asks a **root server**, "Where can I find the servers for `.com`?" The root server replies with the address of the `.com` TLD server.
4.  **Recursive Server Queries TLD:** The recursive server then asks the **.com TLD server**, "Where can I find the authoritative name server for `example.com`?" The TLD server replies with the address of the `example.com` authoritative server.
5.  **Recursive Server Queries Authoritative Server:** The recursive server makes its final query to the **`example.com` authoritative name server**, asking, "What is the IP address for `www.example.com`?"
6.  **Final Answer:** The authoritative server responds with the final IP address (e.g., `93.184.216.34`).
7.  **Response to Client:** The recursive server sends this IP address back to your computer. It also **caches** this answer for a short time (the TTL, or Time-To-Live) so that if another user asks for the same domain, it can answer immediately without repeating the whole process.
8.  **Connection:** Your computer now has the IP address and can establish a direct connection to the `example.com` web server.

<img width="1600" height="640" alt="unnamed" src="https://github.com/user-attachments/assets/748f8d28-b3ff-441e-a2c7-a77e3c4d60e3" />
