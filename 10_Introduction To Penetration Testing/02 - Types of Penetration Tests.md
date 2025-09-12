# 02 - Types of Penetration Tests


## 1. Classification by Knowledge

The most common way to classify a penetration test is by the amount of information and access given to the testing team beforehand. This is often described using the "box" analogy.

### Black Box Testing
*   **Knowledge Given:** **None.** The testers have no prior knowledge of the target's internal infrastructure, source code, or architecture. They start with only the name of the organization or a list of public IP addresses.
*   **Perspective:** Simulates an **external, opportunistic attacker** who is probing the organization from the internet with no inside information.
*   **Goal:** To identify vulnerabilities in the external, internet-facing perimeter that could be exploited by a typical attacker.
*   **Example:** Testing an online banking platform to find vulnerabilities like SQL Injection or outdated SSL certificates.

### White Box Testing (or "Crystal Box")
*   **Knowledge Given:** **Full.** The testers are provided with a wealth of information, including network diagrams, source code, system configurations, and potentially even administrative credentials.
*   **Perspective:** Simulates a **malicious insider** (like a disgruntled employee) or an attacker who has already achieved a deep, privileged compromise of the network.
*   **Goal:** To perform a comprehensive, deep-dive assessment to find as many vulnerabilities as possible in the shortest amount of time. It is less about simulating an attack and more about thorough code and configuration review.
*   **Example:** Analyzing an application's source code to find logic flaws or reviewing firewall rules for misconfigurations.

### Gray Box Testing
*   **Knowledge Given:** **Partial.** The testers are given some information, typically that of a standard, unprivileged user. They might be provided with a user-level account and some basic knowledge of the internal network.
*   **Perspective:** Simulates an attacker who has gained a **limited initial foothold** in the network (e.g., through a successful phishing attack that compromised a standard user's credentials) or a malicious standard employee.
*   **Goal:** To determine how much damage an attacker could do and how far they could move laterally through the network, starting from a position of limited access.
*   **Example:** Using a standard employee's network access to discover and exploit an unsecured internal Wi-Fi network.

---

## 2. Classification by Perspective

Another way to classify tests is by where the assessment is performed from.

### External Penetration Test
*   **Location:** Performed from **outside** the organization's network, over the public internet.
*   **Focus:** Targets all externally-facing assets, such as:
    *   Web servers and applications.
    *   Email servers.
    *   DNS servers.
    *   VPN endpoints.
*   **Goal:** To assess the strength of the organization's perimeter security and determine if an external attacker can breach it.

### Internal Penetration Test
*   **Location:** Performed from **inside** the organization's network, as if the tester is physically plugged into an office port.
*   **Focus:** Assumes the perimeter has already been breached. It tests for vulnerabilities that could be exploited by:
    *   A malicious insider.
    *   Malware that has made it onto a workstation.
    *   An external attacker who has successfully phished an employee.
*   **Goal:** To identify weaknesses in the internal network, such as a lack of network segmentation, weak internal passwords, or unpatched systems, and to see if an attacker can escalate privileges and gain access to critical assets like Domain Controllers.

---

## 3. Other Testing Types

*   **Social Engineering:** Tests the "human firewall." This involves using tactics like phishing emails, pretexting phone calls, or physical tailgating to trick employees into revealing sensitive information or granting unauthorized access.
*   **Physical Security Assessment:** An authorized attempt to bypass physical security controls, such as locks, fences, and security guards, to gain access to sensitive areas like server rooms or offices.
