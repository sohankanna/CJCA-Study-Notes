# 11 - Distributed Denial of Service

A **Distributed Denial of Service (DDoS)** attack is a malicious attempt to make an online service (like a website or server) unavailable to legitimate users by overwhelming it with a flood of internet traffic from **multiple sources**.

*   **Denial of Service (DoS):** An attack from a *single source*. Easier to block.
*   **Distributed Denial of Service (DDoS):** An attack from *many sources* simultaneously. Much harder to block because it's difficult to distinguish malicious traffic from legitimate traffic.

### The Bakery Analogy
Imagine you are opening a new bakery.

*   **The Bakery:** Your website or online service.
*   **Legitimate Customers:** Real users trying to access your service.
*   **The DDoS Attack:** An attacker sends a massive, coordinated crowd of people who have no intention of buying anything to swarm your bakery. They block the doors and fill the aisles, preventing real customers from getting in.
*   **The Result:** Your business is effectively shut down for the day.

---

## How a DDoS Attack Works

A typical DDoS attack has three main components.

1.  **The Attacker:** The individual or group who orchestrates the attack.
2.  **The Botnet:** A network of thousands of internet-connected devices (PCs, servers, and especially insecure **IoT devices**) that have been infected with malware without their owners' knowledge. These compromised devices are often called "zombies."
3.  **The Victim:** The target server, website, or network that the attacker wants to take offline.

**The Attack Process:**
1.  The attacker sends a single command to the botnet's "Command and Control" (C2) server.
2.  The C2 server instructs all the "zombie" devices in the botnet to send a flood of requests to the victim's IP address simultaneously.
3.  The victim's server is overwhelmed by the massive volume of traffic, consuming all its bandwidth, CPU, and memory.
4.  The server slows down to a crawl or crashes completely, becoming unavailable to legitimate users.

---

## Real-World Impact: The Dyn Attack (2016)

*   **What Happened:** A massive DDoS attack targeted Dyn, a major DNS provider.
*   **The Weapon:** The attack was launched using the **Mirai botnet**, which consisted primarily of hijacked, insecure IoT devices like security cameras and home routers.
*   **The Impact:** Major websites and services like Twitter, Netflix, Reddit, and Spotify were inaccessible for hours for millions of users. This attack demonstrated the immense destructive power of insecure IoT devices.

## The Consequences of a DDoS Attack

The impact of a DDoS attack goes beyond just taking a website offline.

| Impact Area | Description |
| :--- | :--- |
| **Financial Loss** | Direct loss of sales and revenue for e-commerce sites, banking platforms, and any business that relies on being online. |
| **Reputational Damage** | Frequent or prolonged outages erode customer trust, leading them to seek more reliable competitors. |
| **Operational Disruption** | Interrupts critical business functions and affects productivity. |
| **Smokescreen for Other Attacks**| This is a critical point. Attackers often launch a DDoS attack as a **distraction**. While the security team is busy trying to restore service, the attackers may be using the chaos to conduct a more stealthy attack, like stealing data or planting malware. |
