# 02-Principles of Information Security


These are the fundamental rules that govern the protection of data. The first three (CIA) are the most critical.

### 1. The CIA Triad
*   **Confidentiality:** Ensures data is accessible only to authorized users. It's about keeping secrets.
    *   **Implemented with:** Encryption, Access Controls.
*   **Integrity:** Ensures data is accurate, complete, and has not been altered without permission.
    *   **Implemented with:** Hashing, Digital Signatures.
*   **Availability:** Ensures data and systems are accessible to authorized users when needed.
    *   **Implemented with:** Redundancy (backups, failover systems), Disaster Recovery Plans.

### 2. Non-repudiation
*   **What it is:** Provides proof of origin and integrity. A user cannot deny having sent a message or made a transaction.
*   **Relevance:** Crucial for legal contracts and e-commerce.
*   **Implemented with:** Digital Signatures, Audit Logs.

### 3. Authentication
*   **What it is:** The process of verifying a user's identity to prove they are who they say they are.
*   **Relevance:** The "front door" to accessing any secure system.
*   **Implemented with:** Passwords, Biometrics, Multi-Factor Authentication (MFA).

### 4. Privacy
*   **What it is:** The proper and ethical handling of sensitive personal information (PII).
*   **Relevance:** Governed by regulations like GDPR and CCPA.
*   **Implemented with:** Data Minimization (only collecting what's necessary), Consent Management.

---

## The 7 Core Processes in Information Security

These are the recurring actions and cycles that make up a security program. It is a continuous loop, not a one-time setup.


1.  **Risk Assessment:** Identify and evaluate potential threats and vulnerabilities to prioritize what to fix first.
2.  **Security Planning:** Develop strategies, policies, and procedures to address the identified risks.
3.  **Implementation of Controls:** Deploy the security tools and enforce the policies defined in the planning phase.
4.  **Monitoring and Detection:** Continuously watch systems for security events or anomalies using tools like a SIEM.
5.  **Incident Response:** Execute a pre-defined plan to contain, eradicate, and recover from a security breach.
6.  **Disaster Recovery:** Restore systems and data after a major catastrophic event (e.g., fire, flood).
7.  **Continuous Improvement:** Learn from incidents and audits to update and strengthen security measures.

---

## The Purpose of Information Security

Why do organizations invest in InfoSec? It's about more than just technology.

*   **Protecting Sensitive Data:** Safeguard confidential information (personal data, trade secrets) from theft.
*   **Ensuring Business Continuity:** Keep the business running during and after a cyberattack.
*   **Maintaining Regulatory Compliance:** Adhere to laws and industry standards (e.g., HIPAA, PCI-DSS) to avoid fines.
*   **Preserving Brand Reputation:** Protect customer trust and avoid the public damage of a data breach.
*   **Safeguarding Intellectual Property:** Prevent the theft of valuable ideas and inventions.
*   **Enabling Secure Digital Transformation:** Safely adopt new technologies like cloud computing and IoT.

---

## Common Tools in Information Security

InfoSec professionals use a wide array of tools. They can be categorized as defensive (Blue Team) or offensive (Red Team).

### Defensive Tools (Blue Team)
*   **Firewalls:** Act as a traffic cop for network traffic.
*   **Intrusion Detection/Prevention Systems (IDS/IPS):** Act as a security alarm for the network.
*   **Security Information & Event Management (SIEM):** A central dashboard for collecting and analyzing logs from all other security tools.
*   **Access Control Systems:** Manage who is allowed to access what.

### Offensive Tools (Red Team / Penetration Testers)
*   **Operating Systems:** Linux (especially Kali Linux), Windows, macOS.
*   **Nmap:** For network scanning and host discovery. The first step in mapping out a target.
*   **Wireshark:** For capturing and analyzing network traffic in detail.
*   **Metasploit:** A framework for developing and executing exploit code against a target.
*   **Burp Suite:** The standard tool for testing web application security.
*   **John the Ripper:** A popular password cracking tool.

**Ethical Note:** Penetration testing tools are powerful and must only be used with explicit, written authorization on systems you have permission to test.
