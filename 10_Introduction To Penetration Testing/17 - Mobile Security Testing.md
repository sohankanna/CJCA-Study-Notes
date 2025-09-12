# 17 - Mobile Security Testing

## 1. Why Mobile Security is Critical

Mobile devices are central to modern business and personal life, making them high-value targets. Key risk factors include:
*   **BYOD (Bring Your Own Device) Policies:** Personal employee devices often access sensitive corporate data.
*   **Remote Work:** The shift to remote work has increased the number of mobile devices connecting to corporate networks.
*   **Data Breach Costs:** A mobile breach can lead to significant financial loss, regulatory fines (GDPR, HIPAA), and reputational damage.
*   **Advanced Threats:** Mobile devices are targeted by specialized malware, phishing attacks, and exploits.

---

## 2. Setting Up a Mobile Testing Environment

A mobile penetration tester needs a specialized lab environment.
*   **Devices:** It's ideal to have both **physical devices** and **emulators/simulators**.
    *   **Android:** Both **rooted** (providing full administrative access) and non-rooted devices are essential for comprehensive testing.
    *   **iOS:** Both **jailbroken** and non-jailbroken devices are beneficial.
*   **Essential Tools:**
    *   **Device Management:** **Android Debug Bridge (ADB)** is the fundamental command-line tool for interacting with Android devices.
    *   **Reverse Engineering:** **JADX** (for decompiling Android apps) and **Ghidra** (for analyzing native code).
    *   **Network Analysis:** An intercepting proxy like **Burp Suite** or **OWASP ZAP**, often with a mobile assistant to handle certificate pinning.
    *   **Runtime Manipulation:** **Frida** and **Objection** are powerful frameworks for "hooking" into a running application to inspect its behavior, bypass security controls, and modify its logic in real-time.

---

## 3. The Mobile Testing Process

### Android Security Testing
*   **Application Package:** Android apps are distributed as **APK** files.
*   **Manifest File:** The `AndroidManifest.xml` file within the APK is a critical starting point, as it declares the app's permissions, components, and security configurations.
*   **Static Analysis:** Decompiling the APK with a tool like **JADX** to read the Java/Kotlin source code. This is used to find hardcoded credentials, insecure data storage practices, and logic flaws.
*   **Dynamic Analysis:** Running the application on a device or emulator and observing its behavior. This includes monitoring network traffic, analyzing file system interactions, and using **Frida** to manipulate the app at runtime.

### iOS Security Testing
*   **Application Package:** iOS apps are distributed as **IPA** files. These are typically encrypted, and testing often requires decrypting them first.
*   **Security Model:** iOS is a more restricted, "sandboxed" environment than Android. Testing requires a deep understanding of its security features like app sandboxing, code signing, and the Keychain.
*   **Key Areas of Focus:**
    *   **Keychain Storage:** How the app uses the secure Keychain to store sensitive data.
    *   **Certificate Pinning:** Verifying the implementation that prevents MITM attacks.
    *   **URL Scheme Handling:** How the app handles custom URL schemes, which can be a vector for attack.

---

## 4. Common Mobile Vulnerabilities

While mobile apps can have web-like vulnerabilities, they also have unique, platform-specific issues.

| Vulnerability Category | Description |
| :--- | :--- |
| **Insecure Data Storage**| **The most common mobile vulnerability.** Sensitive information (credentials, API keys, personal data) is stored in plaintext or with weak encryption in local files, databases, or logs on the device itself. |
| **Weak Network Security**| The app communicates with its backend server over insecure channels (HTTP instead of HTTPS) or fails to properly validate SSL/TLS certificates, making it vulnerable to **Man-in-the-Middle (MITM)** attacks. |
| **Client-Side Injection**| Similar to web vulnerabilities, but on the device. This includes SQL injection into local SQLite databases or JavaScript injection into `WebViews`. |
| **Bypassable Client-Side Controls**| Security checks like **root/jailbreak detection** or anti-debugging measures are implemented purely on the client side. A skilled attacker can use tools like **Frida** to hook into the app and bypass these checks entirely. **Security decisions should always be made on the server.** |
