# 16 - Threat Actors


A **Threat Actor** is any individual or group that performs a malicious cyber action. They are the "adversaries" in the cybersecurity landscape. Threat actors can range from a single, independent hacker to a highly organized, state-sponsored team.

**Important Distinction:**
*   **Threat Actor (Malicious):** Intends to cause harm, steal data, or disrupt systems.
*   **Red Team (Ethical):** Simulates the techniques of a threat actor *with permission* to test and improve an organization's defenses. They use the same tools but for a defensive purpose.

### The Bank Heist Crew Analogy
Think of a sophisticated threat actor team like a crew of bank robbers.

*   **The Goal:** Plan and execute a heist to steal valuable assets (money/data).
*   **The Team:** Each member has a specialized role.
    *   **The Scout (Reconnaissance):** Studies the bank's layout, guards, and security systems. In cyber, this involves using tools like **Nmap** and **OSINT** (Open-Source Intelligence) to find vulnerabilities.
    *   **The Lockpicker (Exploitation):** Bypasses the locks and alarms. In cyber, this is the expert who uses malware or exploits software bugs to gain initial access.
    *   **The Getaway Driver (Exfiltration & Obfuscation):** Ensures a clean escape without a trace. In cyber, this specialist stealthily extracts stolen data and covers the team's tracks by deleting logs.
    *   **The Leader (Strategist):** Coordinates the entire operation, ensuring all actions are aligned.

---

## Types of Threat Actors

Threat actors are often categorized by their motivations, skills, and resources.

| Type | Description | Primary Motivation | Skill Level |
| :--- | :--- | :--- | :--- |
| **Script Kiddies** | Amateurs who use pre-made scripts and tools created by others without understanding how they work. | Curiosity, notoriety, bragging rights. | Low |
| **Hacktivists** | Individuals or groups who use hacking to promote a political or social agenda. Their goal is to make a statement. | Ideology, political/social change. | Low to Medium |
| **Cybercriminals / Organized Crime**| Professional criminals focused on illegal profit. They are responsible for most ransomware, phishing, and financial fraud. | **Financial Gain.** | Medium to High |
| **Nation-States / APTs** | Government-sponsored groups with significant funding and resources. They conduct long-term espionage and strategic attacks. | Espionage, strategic advantage, sabotage. | Very High (Expert) |
| **Insider Threats** | Individuals from within the organization (employees, contractors) who misuse their authorized access. | Revenge, financial gain, or negligence. | Varies |

---

## Common Objectives of Threat Actors

While methods vary, the end goals of threat actors usually fall into a few key categories.

*   **Financial Gain:** The most common motive. This includes direct theft, ransomware extortion, and selling stolen data (credit cards, credentials) on the dark web.
*   **Espionage:** Stealing confidential information from governments (political secrets) or corporations (intellectual property, trade secrets) to gain a strategic advantage.
*   **Disruption:** Causing chaos by shutting down critical services, deleting data, or spreading misinformation. The goal is to damage the target's operations or reputation.
*   **Ideology:** Hacking to promote a political, religious, or social cause.
*   **Revenge:** Disgruntled individuals (often insiders) attacking an organization for a perceived wrong.

### "Low and Slow" Methodology
Sophisticated threat actors (especially APTs) prioritize stealth over speed. They avoid "noisy" techniques like brute-force attacks that could trigger security alarms. Instead, they use **"low and slow"** methods, moving carefully and deliberately within a network over a long period to remain undetected.
