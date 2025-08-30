# 05- Operational Security
OpSec is a continuous security and risk management process that focuses on protecting small, individual pieces of information that, when pieced together, could reveal a larger, more sensitive picture to an adversary.

**Core Idea:** Think like the attacker. Identify what information they would want and figure out how to protect it.

### The House Party Analogy
Planning OpSec is like securing your valuables during a house party.

1.  **Identify Assets:** You decide which items are most valuable (heirloom, game console).
2.  **Identify Threats:** You think about what could go wrong (a guest could spill a drink, someone could wander into your room).
3.  **Identify Vulnerabilities:** You realize your bedroom door doesn't lock.
4.  **Implement Controls:** You move your valuables into a locked closet and tell guests which rooms are off-limits.
5.  **Monitor:** During the party, you keep an eye out to make sure no one is going where they shouldn't.

---

## The 5-Step OpSec Process

OpSec is a cyclical process, not a one-time task.

1.  **Assets Identification:** Identify the organization's "crown jewels"—the most critical information that, if compromised, would cause the most damage (e.g., trade secrets, customer data, financial records).
2.  **Threat Identification:** Determine who the adversaries are and what their goals might be (e.g., a competitor trying to steal a product design, a cybercriminal trying to deploy ransomware).
3.  **Vulnerability Identification:** Analyze the organization's daily operations to find weaknesses that could expose critical information.
4.  **Risk Assessment:** Evaluate the likelihood and impact of a threat exploiting a vulnerability. This helps prioritize which weaknesses to fix first.
5.  **Implementation of Countermeasures (Controls):** Apply protective measures to close the identified security gaps.

---

## Key Components of a Strong OpSec Program

Several key practices are central to good operational security.

| Component | Description |
| :--- | :--- |
| **Access Control** | Enforcing the **Principle of Least Privilege**: users should only have access to the information and systems absolutely necessary to do their jobs. This is managed through Authentication and Authorization. |
| **Asset Management** | Maintaining a complete and up-to-date inventory of all hardware, software, and data assets. You can't protect what you don't know you have. |
| **Change Management**| A formal process for managing and documenting all changes to IT systems. This prevents accidental security holes from being introduced during updates or configuration changes. |
| **Security Awareness Training**| Educating all employees about their security responsibilities. This is the primary defense against threats like **phishing** and **social engineering**. |

---

## OpSec Responsibility

While the formal program is managed by the security team, the responsibility for practicing good OpSec lies with **everyone** in the organization.

*   **Strategy & Management:**
    *   The **Information Security Team**, led by the **CISO**, develops and manages the OpSec program, working with other departments like IT, HR, and Legal.
*   **Implementation & Practice:**
    *   **All Employees:** Every person in the company is responsible for handling sensitive information correctly, following policies, and reporting suspicious activity.
*   **Testing & Validation:**
    *   **Penetration Testers** and security auditors test the effectiveness of OpSec controls by trying to bypass them, often using techniques like social engineering.
