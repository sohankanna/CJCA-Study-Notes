# 10 Network Security

## 1. Firewalls

A **firewall** is a network security device (hardware or software) that monitors and controls incoming and outgoing network traffic based on a predefined set of security rules.

**Core Idea:** A firewall acts as a security guard at the border of a network. It inspects all traffic passing through and decides whether to **allow** it or **block** it based on its rulebook (the firewall policy).

### Types of Firewalls
Firewalls have evolved over time, becoming more intelligent and capable. They are categorized by the OSI layer at which they operate and the sophistication of their inspection.

| Type | OSI Layer(s) | How it Works | Analogy |
| :--- | :--- | :--- | :--- |
| **Packet Filtering**| 3 (Network) & 4 (Transport) | The most basic type. Makes decisions based only on the packet header (Source/Destination IP, Port, Protocol). It doesn't know the context of the conversation. | A security guard who only checks the mailing address on an envelope, not what's inside. |
| **Stateful Inspection**| 3, 4 | More advanced. It tracks the "state" of active connections. It understands if an incoming packet is part of an established, legitimate conversation that was initiated from inside the network. | A security guard who remembers who has already entered and only lets in responses they are expecting. |
| **Application Layer (Proxy)**| 7 (Application) | The most sophisticated. It can inspect the actual content of the data traffic. It understands application-specific commands (like HTTP GET/POST) and can block malicious requests. | A security guard who not only checks the address but also opens and reads the letter inside to look for dangerous content. |
| **Next-Generation Firewall (NGFW)**| Multiple | A modern firewall that combines stateful inspection with advanced features like **Deep Packet Inspection (DPI)**, **IDS/IPS capabilities**, and application awareness. | A high-tech security checkpoint with ID scanners, metal detectors, and bomb-sniffing dogs. |

### Firewall Placement
*   **Home Network:** Usually built into the wireless router.
*   **Corporate Network:** Often a dedicated hardware appliance that sits between the internet and the internal network. All traffic must pass through it.

---

## 2. Intrusion Detection & Prevention Systems (IDS/IPS)

**IDS/IPS** are security solutions that monitor network or system activity for malicious behavior or policy violations.

### The Key Difference: Detect vs. Prevent
*   **Intrusion Detection System (IDS):** Acts like a security camera with an alarm. It **detects** suspicious activity and generates an **alert** for a security analyst to investigate. It is a passive, "out-of-band" system.
*   **Intrusion Prevention System (IPS):** Acts like a security guard who can actively intervene. It **detects** suspicious activity and can automatically **block** or **prevent** the malicious traffic in real-time. It is an active, "in-line" system.

### Detection Techniques
| Technique | How it Works |
| :--- | :--- |
| **Signature-Based**| Matches network traffic against a database of known attack patterns ("signatures"). It is very effective against known threats but cannot detect new, "zero-day" attacks. |
| **Anomaly-Based**| First, it builds a baseline of what "normal" network traffic looks like. Then, it alerts on any activity that deviates significantly from this baseline. It can detect new attacks but may also generate more false positives. |

### Types of IDS/IPS
*   **Network-Based (NIDS/NIPS):** A device placed at a strategic point in the network (e.g., behind the firewall) to monitor all traffic passing through that point.
*   **Host-Based (HIDS/HIPS):** Software that runs on an individual device (like a server or workstation) to monitor its specific activity, system files, and logs.

---

## Network Security Best Practices

*   **Define Clear Policies:** Use the **Principle of Least Privilege**. Deny all traffic by default and only allow what is absolutely necessary for business operations.
*   **Regular Updates:** Keep all security devices, software, and signatures up to date to protect against the latest threats.
*   **Monitor and Log Events:** Regularly review logs and alerts to identify suspicious patterns and investigate potential incidents.
*   **Layered Security (Defense in Depth):** Use multiple layers of security (firewall, IDS/IPS, antivirus, etc.) so that if one layer fails, another is there to stop the attack.
*   **Periodic Penetration Testing:** Actively test the effectiveness of your security controls by simulating real-world attacks.
