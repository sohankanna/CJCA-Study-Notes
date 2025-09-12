# 13 - Network Security Testing

## 1. The Foundation: Understanding Network Architecture

To effectively test a network, a penetration tester must first understand its core components and how they interact. This includes:
*   **Intermediary Devices:** Routers, switches, and firewalls.
*   **Endpoints:** Servers and user workstations.
*   **Protocols:** The languages devices use to communicate (TCP/IP, HTTP, SMB, etc.).
*   **Architecture:** How the network is logically divided (e.g., internal vs. DMZ, network segmentation).

---

## 2. Common Network Security Vulnerabilities

The goal of a network penetration test is to identify and exploit common weaknesses like these:

| Vulnerability | Description |
| :--- | :--- |
| **Misconfigured Services** | Services running with default credentials, unnecessary features enabled, or excessive permissions. |
| **Unpatched Systems** | Running outdated software or firmware with publicly known and exploitable vulnerabilities (CVEs). |
| **Weak Authentication** | Use of weak or default passwords, lack of Multi-Factor Authentication (MFA), or insecure credential storage. |
| **Insecure Protocols** | Use of unencrypted, cleartext protocols like **Telnet**, **FTP**, or **HTTP**, which allows for eavesdropping. |
| **Poor Network Segmentation**| A "flat" network where a compromise on one low-value machine (like a printer) can easily lead to an attack on a high-value server. |
| **Exposed Management Interfaces**| Administrative interfaces (like SSH, RDP, or a router's web portal) being accessible from untrusted networks or the public internet. |
| **Missing Security Controls**| The complete absence of critical security devices like firewalls or Intrusion Detection/Prevention Systems (IDS/IPS). |

---

## 3. The Network Penetration Testing Process

A network pentest follows the standard testing methodology:

1.  **Reconnaissance:** Gather information about the target network, including IP ranges and domain names (both passively and actively).
2.  **Scanning & Enumeration:** Use tools like **Nmap** to map the network, discover live hosts, identify open ports, and enumerate the services running on those ports.
3.  **Vulnerability Analysis:** Use scanners like **Nessus** or **OpenVAS** to find known vulnerabilities in the identified services, but always **manually verify** the findings to eliminate false positives.
4.  **Exploitation:** Actively attempt to exploit the verified vulnerabilities to gain a foothold on a system. This could involve using an exploit from a framework like **Metasploit** or testing for weak credentials on an open service.
5.  **Post-Exploitation:** After gaining initial access, attempt to escalate privileges, harvest credentials, and perform **lateral movement** to other systems on the network to demonstrate the full impact of a breach.

---

## 4. Essential Tools and Technologies

### a) Core Tools
*   **Network Mapping:** **Nmap** (the undisputed king for network discovery and port scanning).
*   **Vulnerability Scanners:** Nessus, OpenVAS.
*   **Exploitation Frameworks:** **Metasploit Framework**.
*   **Packet Analysis:** **Wireshark** (for deep-diving into network traffic).
*   **Password Cracking:** John the Ripper, Hashcat.

### b) Wireless Network Testing
This is a specialized subset of network testing.
*   **Focus:** Assessing the security of Wi-Fi networks (WEP, WPA/2/3), authentication mechanisms, and identifying rogue access points.
*   **Key Tool:** The **Aircrack-ng suite** is the standard for Wi-Fi auditing and cracking.

---

## 5. Common Pitfalls to Avoid

*   **Rushing Reconnaissance:** Failing to perform thorough information gathering is the most common cause of a failed penetration test.
*   **Over-reliance on Automated Tools:** Scanners are a starting point, not the entire test. Findings must be manually verified and creatively exploited.
*   **Poor Communication:** Failing to maintain regular contact with the client, especially when a critical vulnerability is found.
*   **Inadequate Documentation:** Not keeping meticulous notes of every command and action taken, which is essential for writing the final report.
