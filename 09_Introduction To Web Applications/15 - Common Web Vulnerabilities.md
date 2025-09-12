# 15 - Common Web Vulnerabilities

## 1. Broken Authentication & Access Control

These are two related but distinct categories of vulnerabilities that deal with how an application manages user identity and permissions. They are consistently among the most critical flaws.

### Broken Authentication
*   **What it is:** Flaws in the login, session management, or identity management functions of an application.
*   **Impact:** Allows an attacker to bypass the login process entirely or to impersonate other users.
*   **Example (Auth Bypass):** A classic SQL Injection payload like `' OR '1'='1' --` entered into a username field might trick a poorly coded login form into authenticating the attacker without a valid password.

### Broken Access Control
*   **What it is:** Occurs when an authenticated user is able to access data or perform actions that they are not authorized to.
*   **Impact:** A standard user might be able to access administrative pages, view another user's private data, or perform privileged actions.
*   **Example (Insecure Direct Object Reference - IDOR):** An application uses a predictable URL to access a resource, like `/view-profile?id=123`. If the application does not check that the logged-in user is actually user `123`, an attacker can simply change the ID in the URL to `124` to view another user's profile.

---

## 2. Injection Flaws

Injection flaws occur when untrusted, user-supplied data is sent to an interpreter as part of a command or query.

### Command Injection
*   **What it is:** Occurs when an application takes user input and includes it in a command that is executed on the underlying **operating system**.
*   **How it works:** If the input is not properly sanitized, an attacker can inject shell metacharacters (like `;`, `|`, `&&`) to append their own malicious commands to the original one.
*   **Example:** A webpage has a feature to `ping` an IP address supplied by the user.
    *   **Intended Command:** `ping 127.0.0.1`
    *   **Attacker's Input:** `127.0.0.1 ; whoami`
    *   **Executed Command:** `ping 127.0.0.1 ; whoami`
*   **Impact:** Can lead to full **Remote Code Execution (RCE)** on the web server.

### SQL Injection (SQLi)
*   **What it is:** Occurs when an application takes user input and includes it in a query that is sent to a **SQL database**.
*   **How it works:** Similar to command injection, an attacker provides specially crafted input that breaks the original query's syntax and injects new SQL commands.
*   **Impact:** Can allow an attacker to bypass authentication, read all data from the database, modify or delete data, and sometimes gain RCE on the database server.
*   **Example (Vulnerable PHP):**
    ```php
    // User input is directly inserted into the query - HIGHLY VULNERABLE
    $query = "SELECT * FROM users WHERE name LIKE '%$searchInput%'";
    ```

---

## 3. Malicious File Upload (Unrestricted File Upload)

*   **What it is:** A vulnerability that occurs when a web application allows a user to upload a file but fails to properly validate the file's type, size, or content.
*   **How it works:** An attacker uploads a file that is not what the application expects, such as a **web shell** (a script written in PHP, ASP.NET, etc.) disguised as an image file (e.g., `shell.php.jpg`).
*   **Impact:** If the attacker can get the server to execute their uploaded script, they gain **Remote Code Execution (RCE)** and can take full control of the web server. This is one of the most direct paths to a full server compromise.
