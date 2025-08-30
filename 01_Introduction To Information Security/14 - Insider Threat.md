# 14 - Insider Threat



An **insider threat** is a security risk that comes from a current or former employee, contractor, or business partner who has legitimate access to an organization's resources and misuses that access to compromise data or systems.

**Core Idea:** The danger comes from inside the "castle walls." Because insiders already have a level of trust and access, their malicious or negligent actions can be harder to detect than those of an external attacker.

### The Cafe Analogy
Imagine you own a popular cafe with a secret coffee recipe.

*   **External Threat:** A burglar trying to break in at night to steal the recipe (this is what firewalls and alarms protect against).
*   **Insider Threat:** One of your trusted baristas, who knows the recipe as part of their job, secretly copies it and sells it to a rival cafe. This is much harder to detect and prevent.

---

## The Three Types of Insider Threats

Insider threats are not always malicious. They can be broken down into three main categories.

| Type | Motivation / Cause | Example |
| :--- | :--- | :--- |
| **1. Malicious Insider** | **Intentional harm.** Motivated by revenge, financial gain, or ideology. | A disgruntled employee who was just fired deletes critical company files on their way out. |
| **2. Negligent Insider** | **Unintentional harm.** Caused by carelessness, mistakes, or a lack of security awareness. This is the **most common** type of insider threat. | An employee accidentally emails a spreadsheet containing sensitive customer data to an external, public mailing list. |
| **3. Compromised Insider** | **External actor with internal access.** An external attacker steals an employee's credentials (e.g., through a phishing attack) and uses them to operate on the network while appearing to be a legitimate employee. | A hacker logs into the company VPN using a stolen password and begins to exfiltrate data. The system logs show the activity as coming from a valid user account. |

---

## The Insider Threat Kill Chain

Malicious insider actions often follow a predictable pattern.

1.  **Motivation:** The insider develops a reason to act (e.g., passed over for a promotion, financial hardship).
2.  **Planning:** The insider identifies the valuable data they want to target and assesses their current level of access.
3.  **Preparation:** They may gather tools or information, like searching for how to bypass security controls or copying data to a USB drive.
4.  **Execution:** The malicious act occurs (e.g., data is stolen, a system is sabotaged).
5.  **Concealment:** The insider attempts to cover their tracks by deleting logs or disguising their actions.

---

## Impact of an Insider Threat

The damage from an insider threat can be catastrophic and long-lasting.

*   **Financial Loss:** Direct theft of money, costs of remediation, regulatory fines.
*   **Data Breach:** Theft of sensitive customer data, intellectual property, or trade secrets.
*   **Reputational Damage:** Loss of customer trust, which can be harder to recover from than financial loss.
*   **Operational Disruption:** Sabotage of critical systems can bring business operations to a halt.
*   **Legal & Regulatory Consequences:** Failure to protect data can lead to severe fines under regulations like **GDPR** (for personal data) and **HIPAA** (for health information), as well as lawsuits.

**Key Takeaway:** Defending against insider threats requires a different approach than defending against external threats. It relies heavily on monitoring user behavior, enforcing the **Principle of Least Privilege**, and fostering a strong security culture through training.
