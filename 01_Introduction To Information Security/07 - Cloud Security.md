# 07 - Cloud Security

Cloud security is the set of policies, technologies, and controls used to protect data and systems in the cloud. It addresses the unique challenges of a shared, multi-tenant environment.

### The Storage Facility Analogy
Think of the cloud like a high-tech, shared storage facility.

*   **The Cloud Provider (AWS, Azure):** The owner of the storage facility. They are responsible for the security *of the facility itself*—the walls, gates, security guards, and surveillance cameras.
*   **You (The Customer):** The person renting a storage unit. You are responsible for the security *of your own unit*—using a strong lock and deciding who gets a key.
*   **Data Breach:** A thief picks the lock on your unit and steals your belongings.
*   **Misconfiguration:** You forget to lock your unit, leaving it open for anyone to walk in and take things. This is a very common cause of cloud data breaches.
*   **Account Hijacking:** A thief steals your keycard and pretends to be you to get into the facility.

---

## The Shared Responsibility Model

This is the **most important concept** in cloud security. It defines which security tasks are handled by the cloud provider and which are handled by you, the customer.

*   **Cloud Provider's Responsibility (Security *of* the Cloud):**
    *   **Physical Security:** Securing the physical data centers (fences, guards, cameras).
    *   **Hardware & Infrastructure:** Securing the servers, storage, and networking hardware.
    *   **Virtualization Layer:** Securing the hypervisor that separates different customers' virtual machines.

*   **Customer's Responsibility (Security *in* the Cloud):**
    *   **Data:** Encrypting your own sensitive data.
    *   **Applications:** Securing the code you write and deploy.
    *   **Identity & Access Management:** Managing who has access to your cloud resources.
    *   **Network Configuration:** Configuring your own virtual firewalls and network rules.
    *   **Operating System:** Patching and securing the OS on your virtual machines.

---

## Key Areas of Cloud Security

Cloud security focuses on several key domains to protect against common threats.

| Area | Description | Analogy |
| :--- | :--- | :- |
| **Data Protection** | Protecting data both **at rest** (while stored) and **in transit** (while moving across the network). The primary tool for this is **encryption**. | Using a strong lock on your storage unit and a safe inside it. |
| **Identity & Access Management (IAM)** | The "gatekeeper" of the cloud. It controls who can access what resources and what actions they can perform. This is where you configure users, roles, and permissions. | The personalized key or access code to your specific storage unit. |
| **Network Security** | Securing the virtual network within the cloud. This includes configuring **Security Groups** (virtual firewalls) and **Virtual Private Clouds (VPCs)** to isolate your resources from other customers. | The secure, monitored hallways and entrances within the storage facility. |
| **Compliance & Governance** | Ensuring that your use of the cloud adheres to relevant laws (like GDPR), industry regulations (like HIPAA), and internal company policies. | Following the rules of the storage facility (e.g., not storing hazardous materials). |

---

## Responsibility and Testing

*   **Cloud Service Provider (CSP):** Manages the overall security of the cloud infrastructure.
*   **The Customer (You/Administrator):** Responsible for configuring security controls correctly, managing user access, and securing the data you place in the cloud.
*   **Internal Security Teams:** Plan, oversee, and audit the organization's cloud security posture.
*   **Penetration Testers:** Hired to test the security of the *customer's* implementation in the cloud. They simulate attacks to find misconfigurations, weak IAM policies, or vulnerable applications before malicious actors do.
