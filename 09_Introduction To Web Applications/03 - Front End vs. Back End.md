# 03 - Front End vs. Back End

## 1. The Front End (Client-Side)

The **Front End** is everything the user directly experiences in their web browser. It is the user interface (UI) and user experience (UX) of the application. The browser downloads the front-end code from the web server and executes it locally on the user's machine.

### The "Front End Trinity"
The front end is built with three core technologies:
*   **HTML (Hypertext Markup Language):** Provides the fundamental **structure and content** of the webpage (headings, paragraphs, images, links).
*   **CSS (Cascading Style Sheets):** Provides the **styling and visual presentation** (colors, fonts, layout, animations).
*   **JavaScript (JS):** Provides the **interactivity and dynamic functionality** (handling clicks, validating forms, fetching data without reloading the page).

### Key Characteristics
*   **Platform-Independent:** Runs in any modern web browser, regardless of the underlying operating system.
*   **User-Centric:** Focuses on usability, accessibility, and responsive design (adapting to different screen sizes).
*   **Security Context:** The front-end code is fully visible to the user ("View Page Source"). Security vulnerabilities on the front end often involve manipulating how the browser processes this code, such as in **Cross-Site Scripting (XSS)**.

---

## 2. The Back End (Server-Side)

The **Back End** is the "engine room" of the web application. It runs on the web server and is responsible for all the core logic, data processing, and communication with other systems. The user never directly interacts with the back end; their browser sends requests to it.

### The Four Main Back End Components

| Component | Description | Examples |
| :--- | :--- | :--- |
| **Back End Servers** | The physical or virtual hardware and operating system that hosts the application. | Linux, Windows Server, Docker Containers |
| **Web Servers** | The software that receives HTTP requests from clients and serves responses. | Apache, Nginx, Microsoft IIS |
| **Databases** | The systems used to store, manage, and retrieve application data. | **Relational:** MySQL, PostgreSQL, MS SQL <br> **Non-Relational:** MongoDB (NoSQL) |
| **Development Frameworks**| The programming languages and frameworks used to write the application's core logic. | PHP (Laravel), Python (Django), Java (Spring), C# (ASP.NET), JavaScript (Node.js) |

### Key Responsibilities
*   Processing incoming HTTP requests.
*   Authenticating users and managing sessions.
*   Executing business logic.
*   Interacting with the database to read or write data.
*   Integrating with third-party services and APIs.

---

## 3. The Security Perspective

Security must be considered on both sides of the application, but the nature of the vulnerabilities differs.

### Penetration Testing Models
*   **Whitebox Testing:** The tester has **full access to the source code** (both front end and back end). This allows for a deep code review to find flaws.
*   **Blackbox Testing:** The tester has **no prior knowledge** of the internal workings or source code. They test the application from the outside, just like a real attacker would.

### Common Back End Vulnerabilities
Because the back end code is not visible, attackers probe it by sending malicious input and analyzing the server's response.
*   **Injection Attacks (e.g., SQL Injection, Command Injection):** The most critical back end vulnerability. Occurs when the application fails to properly sanitize user-supplied input before passing it to a backend component (like a database or the OS shell).
*   **Broken Access Control / IDOR:** The application's logic fails to correctly enforce permissions, allowing a user to access data or functionality they are not authorized for.
*   **Server-Side Request Forgery (SSRF):** An attacker tricks the server into making requests to internal or external resources on their behalf.

**Key Takeaway:** A secure web application requires a **defense-in-depth** strategy, with security measures implemented on both the front end (to protect users) and, most critically, on the back end (to protect the core logic and data).
