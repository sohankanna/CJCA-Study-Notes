# 14 - Cloud Security Testing

## 1. The Foundation: Cloud Service Models

Understanding the service model is crucial as it defines the scope of a penetration test.

| Model | Acronym | Description | Tester's Focus |
| :--- | :--- | :--- | :--- |
| **Infrastructure as a Service**| **IaaS** | The provider offers fundamental computing resources (virtual machines, storage, networking). The customer manages the OS and applications. | OS-level vulnerabilities, network configurations, storage permissions. |
| **Platform as a Service** | **PaaS** | The provider offers a platform for developing and deploying applications (e.g., a database service or a web app hosting platform). The customer manages their application and data. | Application-level vulnerabilities, access control to the platform's services. |
| **Software as a Service** | **SaaS** | The provider offers a complete, ready-to-use software application (e.g., Microsoft 365, Salesforce). The customer manages their data and user access. | Application-level security (e.g., broken access control), data protection, and configuration of security features. |

---

## 2. Key Differences from Traditional Penetration Testing

*   **Shared Responsibility Model:** The most critical difference. A pentester must operate strictly within the **customer's** area of responsibility and adhere to the cloud provider's acceptable use policy. You are testing the customer's *configuration*, not the cloud provider's infrastructure.
*   **Dynamic Nature:** Cloud environments are highly dynamic and automated. Resources can be created and destroyed in minutes, requiring a testing approach that can adapt quickly.
*   **API-Centric:** Most cloud services are managed and interact via APIs, making API security testing a core component of a cloud assessment.

---

## 3. The Cloud Penetration Testing Process

A cloud pentest adapts the standard methodology to focus on cloud-specific components.

1.  **Reconnaissance & Enumeration:** Discovering the organization's cloud footprint (e.g., identifying active services, storage buckets, and databases).
2.  **Access Control Testing:** Auditing **Identity and Access Management (IAM)** policies. This is the most critical phase, looking for overly permissive roles, weak authentication, and potential privilege escalation paths.
3.  **Configuration Assessment:** Scrutinizing the configuration of all cloud services for common security misconfigurations, such as publicly accessible storage buckets or unencrypted databases.
4.  **Network Security Testing:** Reviewing virtual network configurations, Security Groups (virtual firewalls), and Network Access Control Lists (NACLs).
5.  **Data Security Testing:** Evaluating the implementation of encryption for data at rest and in transit, and assessing key management practices.
6.  **Application Security Testing:** Assessing the security of cloud-native applications, serverless functions, and containers.

---

## 4. Common Cloud Vulnerabilities

*   **Publicly Exposed Storage Buckets:** The most common and high-impact misconfiguration, leading to massive data breaches.
*   **Excessive IAM Permissions:** Overly permissive roles and policies that violate the Principle of Least Privilege.
*   **Insecure APIs:** APIs with weak authentication, authorization, or input validation.
*   **Insufficient Logging & Monitoring:** Disabled or misconfigured logging (like AWS CloudTrail) that makes it impossible to detect or investigate a breach.
*   **Container Security Issues:** Running containers with root privileges, using vulnerable base images, or having an insecure container registry.

---

## 5. Essential Tools for Cloud Testing

| Tool Category | Examples |
| :--- | :--- |
| **Cloud Provider CLIs** | `AWS CLI`, `Azure CLI`, `gcloud CLI` (Essential for programmatic interaction) |
| **Cloud Security Posture Management (CSPM)**| **Scout Suite**, **Prowler**, **CloudSploit** (For automated misconfiguration scanning) |
| **Container Security Scanners**| **Trivy**, Clair, Anchore (For scanning container images for known vulnerabilities) |
| **Traditional Pentesting Tools**| Nmap, Metasploit, Burp Suite (Still relevant, but must be used within the cloud provider's rules of engagement) |
