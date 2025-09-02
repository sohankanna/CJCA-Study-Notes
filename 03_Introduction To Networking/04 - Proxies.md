# Proxies 
## What is a Proxy?

A **proxy** is a server or service that acts as an **intermediary** or "mediator" for requests from clients seeking resources from other servers.

**The critical distinction:** A proxy must be able to **inspect and understand** the traffic passing through it, which is why proxies almost always operate at **Layer 7 (Application Layer)** of the OSI model. A device that simply forwards packets without understanding their content (like a router) is a gateway, not a proxy.

**Common Misconception:** Many people think a VPN is a proxy. While both can change your apparent IP address, a VPN typically operates at a lower network layer (like Layer 3) and encrypts *all* traffic, whereas a proxy is application-specific (e.g., for web traffic).

---

## The Main Types of Proxies

### 1. Forward Proxy (or Dedicated Proxy)
A **forward proxy** is an intermediary that a **client** uses to send requests out to the internet. The server on the internet sees the request as coming from the proxy, not the original client.

*   **Core Function:** It protects and controls **outgoing** traffic from clients on an internal network.
*   **Analogy:** A company mailroom. An employee (client) gives a letter to the mailroom (proxy). The mailroom sends the letter out. The recipient sees the letter as coming from the company's main address (the proxy's IP), not the individual employee's desk.
*   **Common Use Cases:**
    *   **Corporate Web Filtering:** Companies use forward proxies to block employees from accessing malicious or non-work-related websites.
    *   **Malware Defense:** A forward proxy can be a powerful defense. If malware on a compromised machine is not "proxy-aware," it may not be able to communicate with its command-and-control (C2) server, effectively neutralizing it.
    *   **Security Testing:** Tools like **Burp Suite** act as a forward proxy, allowing a penetration tester to intercept, inspect, and modify their own outgoing web traffic to test a web application.

### 2. Reverse Proxy
A **reverse proxy** is an intermediary that sits in front of one or more **web servers**, intercepting requests from clients on the internet. The client thinks it is talking directly to the web server, but it is actually communicating with the reverse proxy.

*   **Core Function:** It protects and manages **incoming** traffic destined for a server.
*   **Analogy:** The receptionist at a large company's front desk. A visitor (client) talks to the receptionist (proxy). The receptionist then finds the correct employee (web server) and relays the message. The visitor never needs to know the employee's direct extension.
*   **Common Use Cases:**
    *   **Load Balancing:** A reverse proxy can distribute incoming traffic across multiple backend servers to prevent any single server from being overloaded.
    *   **DDoS Protection:** Services like **Cloudflare** act as a massive reverse proxy to absorb and filter out malicious DDoS traffic before it ever reaches the organization's actual web server.
    *   **Web Application Firewall (WAF):** A specialized reverse proxy (like **ModSecurity**) that inspects incoming web requests for malicious patterns (like SQL injection or XSS) and blocks them.
    *   **Pivoting (for Pen Testers):** An attacker can set up a reverse proxy on a compromised machine inside a network to route their attack traffic through it, helping to bypass firewalls or evade detection by an IDS.

---

## Transparent vs. Non-Transparent Proxies

This distinction refers to whether the client needs to be configured to use the proxy.

| Type | Description |
| :--- | :--- |
| **Transparent Proxy** | The client is **unaware** of the proxy's existence. The network is configured to automatically route all relevant traffic (e.g., all web traffic on port 80) through the proxy without any configuration on the client's device. |
| **Non-Transparent Proxy (Explicit Proxy)**| The client **must be explicitly configured** to use the proxy. For example, in a web browser's settings, you would manually enter the IP address and port number of the proxy server. If this configuration is not set, the client cannot access the internet. |
