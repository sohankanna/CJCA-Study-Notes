# 16 - Public Vulnerabilities

## 1. What are Public Vulnerabilities (CVEs)?

When a security vulnerability is discovered in a publicly used software (like WordPress, Apache, or a specific plugin), it is often reported to the vendor. Once a patch is available, the details of the vulnerability are typically disclosed publicly and assigned a unique identifier.

*   **CVE (Common Vulnerabilities and Exposures):** The industry standard for identifying and tracking publicly known cybersecurity vulnerabilities. Each CVE has a unique ID (e.g., `CVE-2014-6271` for Shellshock).
*   **Exploit Databases:** Many security researchers and penetration testers create and publish **Proof of Concept (PoC)** exploits for these CVEs. These are invaluable resources for testing if a system is vulnerable.
    *   **Popular Databases:** Exploit-DB, Rapid7 DB (Metasploit), Vulnerability Lab.

### The Reconnaissance Process
1.  **Identify Software and Version:** The crucial first step is to accurately identify the web application, its plugins, the web server, and any other components, along with their exact version numbers. This information can often be found in the page's source code, HTTP headers, or specific files (e.g., `readme.html` for WordPress).
2.  **Search for Exploits:** Use the identified software and version as a search term in Google and public exploit databases to find any known vulnerabilities and associated exploits.

---

## 2. Common Vulnerability Scoring System (CVSS)

**CVSS** is an open industry standard for assessing the severity of a vulnerability and assigning it a numerical score. This helps organizations prioritize which vulnerabilities to fix first.

*   **Score Range:** 0.0 to 10.0.
*   **Provider:** The **National Vulnerability Database (NVD)** provides CVSS base scores for almost all public CVEs.

### CVSS v3.1 Severity Ratings

| Severity | Base Score Range |
| :--- | :--- |
| **None** | 0.0 |
| **Low** | 0.1 - 3.9 |
| **Medium** | 4.0 - 6.9 |
| **High** | 7.0 - 8.9 |
| **Critical** | 9.0 - 10.0 |

As a penetration tester, you should prioritize vulnerabilities with **High** or **Critical** scores, especially those that lead to **Remote Code Execution (RCE)**.

### CVSS Metric Groups
A CVSS score is calculated from three metric groups:
1.  **Base Score:** Represents the inherent qualities of a vulnerability that are constant over time and across user environments (e.g., Attack Vector, Complexity, Privileges Required, Impact). **This is the score you see on the NVD.**
2.  **Temporal Score:** Represents characteristics of a vulnerability that may change over time (e.g., Is an exploit available? Has a patch been released?).
3.  **Environmental Score:** Represents the characteristics of a vulnerability that are unique to a particular organization's environment (e.g., How critical is the affected system to our business?).

Organizations can use the NVD's CVSS calculator to adjust the base score with temporal and environmental metrics to get a final score that is more relevant to their specific risk posture.

---

## 3. Back-End Server Vulnerabilities

Vulnerabilities are not limited to the web application code itself. The underlying back-end components can also have critical flaws.

*   **Web Server Vulnerabilities:** The web server software (Apache, Nginx, IIS) is directly exposed to the internet and is a primary target. A famous example is **Shellshock (CVE-2014-6271)**, a vulnerability in the Bash shell that could be exploited through Apache's CGI scripts to gain RCE on the server.
*   **Database and OS Vulnerabilities:** Vulnerabilities in the database software or the underlying server operating system are also critical. While often not directly exploitable from the internet, they are a primary target for **privilege escalation** after an attacker has gained an initial foothold on the web server.

**Key Takeaway:** A comprehensive security assessment must consider the entire technology stack—the web application, its plugins and libraries, the web server, the database, and the operating system—as any component can be a potential entry point for an attacker.
