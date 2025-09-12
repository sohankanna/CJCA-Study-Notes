# 12 - Web Application Testing

## 1. The Foundation: Understanding Web Applications

To effectively test a web application, a penetration tester must have a solid understanding of how they are built and how they function. This includes the standard **three-tier architecture**.

1.  **Presentation Tier (Front End):** The user interface that runs in the client's browser.
    *   **Technologies:** HTML, CSS, JavaScript.
2.  **Application Tier (Back End):** The server-side logic that processes requests and handles business rules.
    *   **Technologies:** Server-side languages (PHP, Python, Java, Node.js) running on web servers (Apache, Nginx).
3.  **Database Tier:** The back-end database that stores and retrieves application data.
    *   **Technologies:** SQL (MySQL, PostgreSQL) and NoSQL (MongoDB) databases.

A tester must be familiar with how these tiers interact via the **HTTP/HTTPS protocol**.

---

## 2. Common Web Application Vulnerabilities

A significant portion of web application testing involves looking for well-known, common vulnerability classes, many of which are outlined in the **OWASP Top 10**.

### a) Injection Vulnerabilities
These occur when an application fails to properly sanitize untrusted user input before passing it to a back-end interpreter.
*   **SQL Injection (SQLi):** Injecting malicious SQL code into database queries. This is often the most critical type of injection flaw.
*   **Command Injection:** Injecting operating system commands that are then executed on the web server.

### b) Broken Authentication & Session Management
These are flaws in how the application handles user identity.
*   **Weak Password Policies:** Allowing simple or easily guessable passwords.
*   **Session Hijacking:** Stealing a user's session cookie to impersonate them.
*   **Authentication Bypass:** Finding a logic flaw that allows an attacker to access protected functionality without logging in.

### c) Cross-Site Scripting (XSS)
This vulnerability occurs when an application includes unsanitized user input in a page that is then displayed to other users.
*   **Impact:** An attacker can inject malicious JavaScript code that will execute in the victim's browser. This can be used to steal session cookies, perform actions on behalf of the user, or redirect them to malicious websites.

---

## 3. Essential Tools and Skills

### a) Core Tools
*   **Intercepting Proxy (Essential):** This is the most important tool for a web pentester. It sits between the browser and the web server, allowing the tester to intercept, inspect, and modify all HTTP/S requests and responses in real-time.
    *   **Examples:** **Burp Suite Professional** (the industry standard), **OWASP ZAP** (a powerful, free, and open-source alternative).
*   **Browser Developer Tools (`F12`):** Crucial for inspecting the front-end code (HTML, CSS, JS), analyzing network traffic, and manipulating the DOM.

### b) Key Skills
*   **Technical Knowledge:** Deep understanding of the web technologies and common vulnerabilities listed above.
*   **Scripting:** Proficiency in a scripting language like **Python** is invaluable for automating repetitive tasks, fuzzing inputs, and writing custom exploits.
*   **Analytical Mindset:** The ability to understand application logic, think like an attacker, and creatively chain together minor flaws to create a significant impact.

---

## 4. Legal and Ethical Considerations

*   **Authorization:** Always have **explicit, written permission** before conducting any tests.
*   **Scope:** Strictly adhere to the defined scope of the engagement. Do not test systems or applications that are not on the approved list.
*   **Responsible Disclosure:** If a vulnerability is found, it must be reported privately to the organization so they can fix it.
*   **"Do No Harm":** The goal is to identify vulnerabilities, not to cause damage or disrupt business operations.

**Key Takeaway:** Professional web application penetration testing is not just about "breaking things." It is a systematic process of identifying weaknesses and providing clear, actionable recommendations to help organizations improve their security posture.
