# 16 - Social Engineering

## 1. What is Social Engineering?

**Social engineering** is the art of psychological manipulation to deceive individuals into divulging confidential information or performing actions that compromise security.

*   **Core Idea:** Instead of hacking a computer, a social engineer "hacks" a person. It recognizes that humans are often the weakest link in the security chain.
*   **Key Distinction:** It is a non-technical attack vector that can bypass even the most sophisticated technological defenses.

### The Psychological Principles of Influence
Social engineering attacks are effective because they exploit predictable human behaviors and psychological triggers.

| Principle | Description |
| :--- | :--- |
| **Authority** | People are more likely to comply with a request if it appears to come from a person of authority (e.g., a CEO, an IT administrator, law enforcement). |
| **Urgency** | Creating a sense of urgency (e.g., "Your account will be locked in 5 minutes!") causes people to act hastily without critical thinking. |
| **Fear** | Suggesting a negative consequence (e.g., "You will be fired if you don't reset your password now") can override rational judgment. |
| **Curiosity** | Exploiting the natural human desire to know more (e.g., a USB drive labeled "Employee Salaries"). |
| **Trust / Helpfulness**| Abusing the general human tendency to be helpful and to trust others who seem credible or are in need of assistance. |

---

## 2. Common Social Engineering Techniques

### a) Digital Techniques
*   **Phishing:** The most common attack. Sending deceptive emails that appear to be from a legitimate source to trick recipients into clicking a malicious link or opening a malicious attachment.
*   **Spear Phishing:** A highly targeted form of phishing where the email is personalized to a specific individual or small group, often using information gathered during reconnaissance to make it extremely convincing.
*   **Pretexting:** Creating a fabricated scenario or "pretext" to build trust before making a request (e.g., posing as an IT technician over the phone who needs the user's password for "maintenance").
*   **Baiting:** Luring a victim into a trap by exploiting their curiosity or greed (e.g., leaving an infected USB drive in a public area).

### b) Physical Techniques
*   **Tailgating:** Following an authorized employee through a secure door before it closes.
*   **Impersonation:** Posing as a legitimate person, such as a delivery driver, a new employee, or a maintenance worker, to gain physical access to a facility.

---

## 3. The Social Engineering Assessment Process

1.  **Reconnaissance (OSINT):** This is the most critical phase. The tester meticulously gathers information about the target organization from public sources (company website, LinkedIn, social media) to build a credible pretext.
2.  **Scenario Development:** Based on the reconnaissance, the tester crafts a believable attack scenario designed to test specific controls or employee behaviors.
3.  **Execution:** The tester carries out the planned attack (e.g., sends the phishing email, makes the phone call, attempts physical entry).

---

## 4. CRITICAL Ethical Considerations

Social engineering is the most ethically sensitive domain of penetration testing and carries significant risk if not handled with extreme care.

*   **Explicit Authorization:** Due to the high potential for legal and psychological harm, the scope and methods for a social engineering test must be **explicitly and clearly defined** in the signed Statement of Work.
*   **"Do No Harm":** The primary principle. The goal is to **test awareness**, not to cause real psychological distress, damage professional relationships, or create a toxic work environment.
*   **De-escalation:** Testers must be prepared to immediately reveal their identity and halt the test if a situation becomes dangerous or overly stressful for the employee.
*   **Support Channels:** The client organization must have clear support channels in place for employees who may be affected by the test.
*   **Focus on Education:** The outcome should always be a positive learning experience that improves the organization's security culture, not a "gotcha" exercise that shames employees.
