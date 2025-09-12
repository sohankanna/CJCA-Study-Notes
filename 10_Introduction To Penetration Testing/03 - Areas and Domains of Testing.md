# 03 - Areas and Domains of Testing

## 1. Network Infrastructure Testing

*   **Focus:** The foundational hardware and software that make up the network. This is one of the most fundamental types of penetration testing.
*   **Targets:** Routers, switches, firewalls, and other network-connected devices.
*   **Common Activities:**
    *   **Port Scanning and Service Enumeration:** Discovering open ports and identifying the services running on them.
    *   **Vulnerability Scanning:** Looking for known vulnerabilities in firmware or service configurations.
    *   **Protocol Analysis:** Examining network traffic for weaknesses.
    *   **Segmentation Testing:** Verifying that network segments (like a guest network and a corporate network) are properly isolated from each other.

## 2. Web Application Security Testing

*   **Focus:** Websites, web applications, and their associated APIs. This is a massive and critical domain due to the public-facing nature of web apps.
*   **Targets:** Front-end code (HTML, CSS, JS) and back-end application logic and databases.
*   **Common Activities:**
    *   Testing for the **OWASP Top 10** vulnerabilities (e.g., SQL Injection, Cross-Site Scripting (XSS), Broken Access Control).
    *   Analyzing session management and authentication mechanisms.
    *   Fuzzing user input fields to find unexpected behavior.
    *   Assessing the security of API endpoints.

## 3. Mobile Application Security Testing

*   **Focus:** Applications running on mobile operating systems (Android and iOS).
*   **Targets:** The mobile application itself, how it stores data locally, and how it communicates with back-end servers.
*   **Common Activities:**
    *   **Static Analysis:** Examining the application's code without running it.
    *   **Dynamic Analysis:** Testing the application while it is running to observe its behavior.
    *   **Insecure Data Storage:** Checking if sensitive data (like passwords or API keys) is stored insecurely on the device.
    *   **Insecure Communication:** Intercepting traffic between the app and its server to check for a lack of encryption or certificate pinning.

## 4. Cloud Infrastructure Security Testing

*   **Focus:** The security of resources and services hosted by a cloud provider.
*   **Targets:** Virtual machines, storage buckets (like AWS S3), serverless functions, and containerized applications.
*   **Common Activities:**
    *   **Configuration Review:** The most critical part. Checking for misconfigurations in cloud services, as these are the leading cause of cloud breaches.
    *   **Identity and Access Management (IAM) Review:** Auditing user and role permissions to ensure the Principle of Least Privilege is followed.
    *   **Network Security Group / Firewall Rule Analysis:** Verifying that network access to cloud resources is properly restricted.

## 5. Physical Security Testing and Social Engineering

*   **Focus:** The "human element" and the physical security controls of an organization.
*   **Targets:** Employees, office buildings, data centers, and physical security measures.
*   **Common Activities:**
    *   **Social Engineering:**
        *   **Phishing:** Sending deceptive emails to trick employees.
        *   **Vishing (Voice Phishing):** Attempting to gain sensitive information over the phone.
    *   **Physical Security:**
        *   **Tailgating/Piggybacking:** Following an authorized employee through a secure door.
        *   **Badge Cloning:** Attempting to clone an employee's access card.
        *   **Dumpster Diving:** Searching through trash for sensitive documents.

## 6. Wireless Network Security Testing

*   **Focus:** The security of Wi-Fi networks and other wireless communication protocols.
*   **Targets:** Wireless Access Points (WAPs), encryption protocols, and authentication mechanisms.
*   **Common Activities:**
    *   **Identifying Rogue Access Points:** Finding unauthorized WAPs connected to the corporate network.
    *   **Cracking Wi-Fi Passwords:** Attempting to crack weak WPA/WPA2-Personal (PSK) passwords.
    *   **Evil Twin Attacks:** Setting up a malicious access point with the same name as a legitimate one to perform a Man-in-the-Middle attack.
    *   **Assessing Network Segmentation:** Ensuring that guest and corporate wireless networks are properly isolated.

## 7. Software Security Testing

*   **Focus:** The security of custom-developed software, operating systems, and firmware.
*   **Targets:** The application's source code or compiled executables.
*   **Common Activities:**
    *   **Static Application Security Testing (SAST):** Analyzing the source code for vulnerabilities without executing it.
    *   **Dynamic Application Security Testing (DAST):** Testing the running application for vulnerabilities.
    *   **Reverse Engineering:** Decompiling an executable to understand its logic and find flaws.
    *   **Fuzzing:** Sending large amounts of malformed, unexpected data to an application to try and make it crash, revealing potential vulnerabilities like buffer overflows.
