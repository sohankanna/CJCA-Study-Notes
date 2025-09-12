# 11 - Methodologies & Frameworks

## 1. What is a Pentesting Methodology?

A **methodology** is a formal, step-by-step process that provides a roadmap for conducting a penetration test. It breaks down the complex assessment into distinct, logical phases, ensuring that all critical areas are covered and no steps are overlooked.

**Why Use a Methodology?**
*   **Completeness:** Ensures a thorough assessment.
*   **Consistency:** Provides a repeatable process for every engagement.
*   **Professionalism:** Demonstrates a structured, industry-standard approach to clients.
*   **Efficiency:** Guides the tester's efforts, making the process more efficient.

---

## 2. Key Industry Standard Methodologies

### Penetration Testing Execution Standard (PTES)
*   **What it is:** A comprehensive standard designed to provide a common language and methodology for conducting penetration tests.
*   **Seven Phases:**
    1.  Pre-engagement Interactions
    2.  Intelligence Gathering
    3.  Threat Modeling
    4.  Vulnerability Analysis
    5.  Exploitation
    6.  Post-Exploitation
    7.  Reporting

### OWASP Web Security Testing Guide (WSTG)
*   **What it is:** The **industry-standard methodology** specifically for **web application** penetration testing.
*   **Focus:** Provides a detailed framework for testing all aspects of a web application's security, from information gathering to specific vulnerability classes like SQL Injection and XSS.
*   **Value:** It is continuously updated by a global community of security experts to address the latest threats and technologies.

### NIST Special Publication 800-115
*   **What it is:** The "Technical Guide to Information Security Testing and Assessment" from the U.S. National Institute of Standards and Technology.
*   **Focus:** A more formal, high-level framework that provides guidance on planning, executing, and reporting on security assessments.
*   **Use Case:** Often referenced when conducting tests for government agencies or organizations that follow NIST cybersecurity guidelines.

---

## 3. The MITRE ATT&CK® Framework

While not a linear methodology like PTES, the **MITRE ATT&CK® framework** has become an essential resource for modern penetration testing, especially for **adversary emulation**.

*   **What it is:** A globally accessible, curated knowledge base of **adversary tactics, techniques, and procedures (TTPs)** based on real-world observations.
*   **How Pentesters Use It:**
    *   **Planning:** To design test scenarios that mimic the behavior of specific, real-world threat actors (like a particular ransomware group or APT).
    *   **Execution:** To ensure that the test covers a wide range of realistic attack techniques, beyond just common vulnerabilities.
    *   **Reporting:** To map the successful attack paths back to the ATT&CK matrix, providing a clear and standardized way to communicate the tested TTPs to the defensive team (Blue Team).

---

## 4. Developing a Personal Methodology

While standard frameworks are the starting point, experienced penetration testers develop their own **personal methodology**.

*   **What it is:** A customized approach that blends the best parts of established frameworks with the tester's own experience, preferred tools, and custom scripts.
*   **How to Build It:**
    1.  **Start with a Foundation:** Use a standard like PTES or OWASP WSTG as your base.
    2.  **Document Everything:** Meticulously take notes on every engagement. Document what techniques worked, which tools were most effective, and what custom scripts you wrote.
    3.  **Create Checklists:** Develop detailed checklists for different types of assessments (e.g., a network pentest checklist, a web app checklist, an information gathering checklist).
    4.  **Iterate and Refine:** Continuously update your methodology with new techniques and lessons learned from each engagement.

A personal methodology is a living document that evolves with your skills and experience, making you a more efficient and effective tester.
