# 08 - Structure of a Penetration Test

## The Penetration Testing Lifecycle

### 1. Pre-Engagement Phase
This is the foundational planning stage. It is arguably the most important phase as it defines the entire engagement.
*   **Goal:** To establish a clear understanding between the testers and the client.
*   **Key Activities:**
    *   **Scoping:** Defining exactly what will be tested (IP ranges, applications, etc.) and what is off-limits.
    *   **Objective Setting:** Determining the goals of the test (e.g., gain domain admin, exfiltrate a specific file).
    *   **Rules of Engagement (RoE):** Outlining the permitted testing times, contact points, and emergency procedures.
    *   **Legal Documents:** Signing contracts and Non-Disclosure Agreements (NDAs).

### 2. Information Gathering (Reconnaissance)
The goal is to collect as much information about the target as possible to identify potential attack vectors.
*   **Passive Reconnaissance:** Gathering information from public sources without directly interacting with the target.
    *   **Methods:** OSINT (Open Source Intelligence), social media analysis, company website review, DNS records.
*   **Active Reconnaissance:** Directly interacting with the target systems to gather technical information.
    *   **Methods:** Port scanning (`nmap`), service enumeration, banner grabbing.

### 3. Vulnerability Assessment Phase
Analyzing the information gathered to identify potential security weaknesses.
*   **Goal:** To create a list of potential vulnerabilities to investigate further.
*   **Key Activities:**
    *   Running automated vulnerability scanners.
    *   Manually correlating information to identify potential attack paths.
    *   Analyzing scan results to eliminate false positives.

### 4. Exploitation Phase
This is the phase that distinguishes a penetration test from a vulnerability assessment.
*   **Goal:** To actively attempt to exploit the identified vulnerabilities to gain unauthorized access.
*   **Key Activities:**
    *   Using public exploits or custom scripts to compromise a service.
    *   Bypassing security controls.
    *   Gaining an initial foothold on a system (e.g., a reverse shell).
*   **Crucial Rule:** All exploitation must be done carefully, following the RoE to avoid causing damage to production systems.

### 5. Post-Exploitation Phase
This phase covers all actions taken *after* gaining initial access to a system.
*   **Goal:** To determine the full potential impact of a breach and achieve the test's objectives.
*   **Key Activities:**
    *   **Privilege Escalation:** Attempting to elevate permissions from a standard user to an administrator or `root`.
    *   **Persistence:** Establishing a method to maintain access to the compromised system across reboots.
    *   **Data Exfiltration (Testing):** Identifying and attempting to extract sensitive data to demonstrate impact.
    *   **Pivoting:** Using the compromised host as a beachhead to attack other systems on the internal network.

### 6. Lateral Movement Phase
A subset of post-exploitation focused on expanding access within the network.
*   **Goal:** To move from the initial compromised host to other systems, especially high-value targets like database servers or Domain Controllers.
*   **Key Activities:**
    *   Internal network scanning and reconnaissance.
    *   Harvesting credentials (passwords, hashes, tokens) from memory or files.
    *   Using harvested credentials to access other machines (e.g., "pass-the-hash" attacks).

### 7. Post-Engagement Phases
These phases occur after the hands-on testing is complete.
*   **Proof of Concept (PoC) Development:** Creating detailed, step-by-step instructions or scripts that reliably demonstrate how a vulnerability was exploited. This validates the finding and helps the client's team reproduce and fix the issue.
*   **Reporting:** This is a critical deliverable. A good report includes:
    *   An **Executive Summary** explaining the business risk in non-technical terms.
    *   **Detailed Technical Findings** for each vulnerability.
    *   **Risk Ratings** (e.g., Critical, High, Medium, Low) to help with prioritization.
    *   Clear, actionable **Remediation Recommendations**.
*   **Remediation Support & Retesting:**
    *   Working with the client's team to answer questions and help them fix the vulnerabilities.
    *   Performing a **retest** after the fixes have been applied to verify that the vulnerabilities have been successfully remediated.
