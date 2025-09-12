# 09 - Prerequisites for a Penetration Test
	
## 1. Legal Authorization & Documentation

This is the absolute cornerstone of any ethical hacking engagement. **Testing without explicit, written permission is illegal.**

*   **Statement of Work (SOW):** A project-specific document that defines the **scope, objectives, timeline, and deliverables** for a single penetration test.
*   **Master Services Agreement (MSA):** A broader, long-term contract that outlines the overall terms of the business relationship for multiple engagements.
*   **Rules of Engagement (RoE):** Often part of the SOW, this document details the "ground rules" of the test, including permitted and forbidden techniques, testing windows, and emergency contact information.
*   **Non-Disclosure Agreement (NDA):** A legal contract that obligates the testing team to maintain the confidentiality of all sensitive information discovered during the assessment.

---

## 2. Scope Definition and Boundaries

A clearly defined scope prevents misunderstandings and protects critical systems.

*   **In-Scope:** An explicit list of all systems, applications, and IP ranges that are **authorized for testing**.
*   **Out-of-Scope:** An explicit list of all assets that **must not be tested**. This often includes critical production systems, industrial control systems, or systems with regulated data that require special handling.
*   **Testing Windows:** The specific dates and times during which testing is permitted (e.g., only after business hours or on weekends) to minimize disruption.

---

## 3. Technical Information Gathering

The amount of information gathered beforehand depends on the test type (Black, Gray, or White Box). This may include:
*   Network diagrams and asset inventories.
*   Source code for applications.
*   Knowledge of the technology stack (OS versions, applications, security controls).
*   Identification of highly sensitive systems (e.g., medical devices, systems under HIPAA/GDPR) that require special care or exclusion.

---

## 4. Communication Channels and Emergency Procedures

Clear communication is vital to a smooth engagement.
*   **Key Contacts:** A list of primary technical and management contacts on the client side.
*   **Escalation Procedures:** A defined plan for how to report critical vulnerabilities immediately upon discovery.
*   **Incident Response Plan:** An agreed-upon procedure for what to do if the testing inadvertently causes a system outage or other issue, including who to contact and how to safely halt testing.

---

## 5. Testing Environment and Data Handling

### Testing Environment
*   Ensure all testing tools are up-to-date and properly licensed.
*   Use a secure, isolated testing environment to prevent cross-contamination with other projects.
*   Set up robust logging to create a clear audit trail of all testing activities.

### Confidentiality & Data Handling
*   **Data Extraction:** Only exfiltrate the minimum amount of data required to prove impact, as defined by the scope.
*   **Data Security:** All client data collected during the test must be stored securely (e.g., in an encrypted volume).
*   **Data Disposal:** At the end of the engagement, all client data must be securely and permanently destroyed according to the procedures outlined in the SOW or NDA.

---

## 6. Business and Legal Protections

*   **Backup and Recovery:** Confirm with the client that they have recent, tested backups of all in-scope systems before beginning any potentially disruptive testing.
*   **Professional Liability Insurance:** The testing firm must have adequate insurance (often called "Errors and Omissions" or "Cyber Liability" insurance) that specifically covers penetration testing activities. This protects both parties from financial repercussions in the event of an accidental negative impact.
