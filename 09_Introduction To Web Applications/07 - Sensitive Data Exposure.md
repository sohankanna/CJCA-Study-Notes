# 07 - Sensitive Data Exposure

## 1. What is Sensitive Data Exposure?

**Sensitive Data Exposure** occurs when an application fails to properly protect confidential data, making it accessible to unauthorized parties. In the context of the front end, this means that sensitive information is embedded directly into the HTML, CSS, or JavaScript code that is sent to the user's browser.

*   **Core Idea:** The front-end source code of a webpage is **completely visible to every user**. Any information placed within it, even if it's hidden from the rendered view, can be easily discovered.
*   **How to View Page Source:**
    *   **Right-click** on a webpage and select **"View Page Source"**.
    *   Use the keyboard shortcut **`Ctrl + U`**.
    *   Use the **Developer Tools (`F12`)**.
    *   Intercept the response with a web proxy like **Burp Suite**.

---

## 2. Common Types of Exposed Data

Reviewing the page source is one of the first and most basic steps in any web application penetration test. It's a hunt for "low-hanging fruit."

### Information Found in HTML Comments
Developers often leave comments in the code as reminders or for debugging purposes. Sometimes, they forget to remove these comments before deploying to production.
*   **Syntax:** HTML comments are enclosed in `<!-- ... -->`.
*   **Example:** A developer might leave a comment with test credentials.
    ```html
    <!-- TODO: remove test credentials before go-live. admin:password123 -->
    ```
    While finding cleartext passwords is rare, it's not impossible. More commonly, you might find:
    *   Usernames
    *   Internal IP addresses or server names
    *   Paths to hidden directories or API endpoints
    *   Notes about disabled or upcoming features

### Information in JavaScript Files
JavaScript code can also be a source of sensitive information.
*   **API Keys:** Keys for third-party services (like Google Maps or a payment gateway) might be hardcoded in the JS.
*   **API Endpoints:** The JavaScript will contain the URLs for the backend API endpoints the application communicates with. This is crucial for mapping the application's attack surface.
*   **Business Logic:** Sometimes, developers mistakenly place sensitive business logic (like pricing calculations or access control checks) in the client-side JavaScript. An attacker can easily read and manipulate this logic to their advantage.

---

## 3. The Security Impact

While front-end vulnerabilities primarily affect the end-user, exposing sensitive data can have a direct impact on the back end.
*   **Credential Theft:** Leaked credentials can be used to log in and gain unauthorized access.
*   **Information Gathering:** Exposed server names, internal paths, and API endpoints provide an attacker with a detailed map of the application's infrastructure, which is invaluable for planning further attacks.
*   **Bypassing Controls:** Discovering hidden functionality or debugging parameters can allow an attacker to bypass security measures.

---

## 4. Prevention

*   **Code Reviews:** All code should be reviewed before deployment to ensure no sensitive information, developer comments, or debugging code is left in.
*   **Data Classification:** Establish clear policies on what data is considered sensitive and ensure it is never sent to the client-side unless absolutely necessary.
*   **Secrets Management:** Never hardcode credentials, API keys, or other secrets in the front-end code. Use a secure secrets management system on the back end.
*   **JavaScript Obfuscation/Minification:** While not a true security control (as it can be reversed), obfuscating or minifying JavaScript code can make it much harder for casual attackers and automated tools to read and understand, which can help deter some attacks.
