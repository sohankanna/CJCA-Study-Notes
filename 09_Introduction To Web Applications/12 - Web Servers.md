# 12 - Web Servers

## 1. What is a Web Server?

A **web server** is an application that runs on a back-end server and acts as the "front door" for a web application. Its primary job is to listen for incoming HTTP requests on specific ports (typically port 80 for HTTP and port 443 for HTTPS) and deliver the requested web resources (like HTML pages, images, etc.) back to the client.

### The Web Server Workflow
1.  A client (web browser) sends an HTTP request to the server's IP address and port.
2.  The web server software receives the request.
3.  It parses the request to understand the method (`GET`, `POST`, etc.) and the requested path (`/index.html`).
4.  It locates the requested resource on the server's filesystem.
5.  If the request is for a static file (like an image), it sends the file back directly.
6.  If the request is for a dynamic page (like a PHP script), it passes the request to the appropriate application engine (e.g., the PHP interpreter) to process.
7.  It receives the output from the application engine.
8.  It constructs an HTTP response, including a **status code**, headers, and the response body (the final HTML).
9.  It sends the response back to the client's browser.

---

## 2. The Three Most Common Web Servers

While many web server applications exist, the market is dominated by three main players.

### Apache HTTP Server (`httpd`)
*   **Market Share:** Historically the most popular web server.
*   **Key Characteristics:**
    *   **Modular:** Its functionality can be massively extended with a wide variety of modules (e.g., `mod_php` for PHP, `mod_ssl` for HTTPS).
    *   **Flexible Configuration:** Uses `.htaccess` files to allow for powerful, directory-level configuration changes.
    *   **Platform:** Runs on nearly all operating systems, but is most common in a **LAMP** (Linux, Apache, MySQL, PHP) stack.
*   **Used By:** Startups, small businesses, and many large companies like Adobe and Apple.

### Nginx (`engine-x`)
*   **Market Share:** The second most popular, and the most dominant among high-traffic websites.
*   **Key Characteristics:**
    *   **High Performance:** Designed with an asynchronous, event-driven architecture that is extremely efficient at handling a large number of concurrent connections with low memory usage.
    *   **Versatile:** Often used not just as a web server, but also as a **reverse proxy**, **load balancer**, and **caching** server.
*   **Used By:** The majority of the world's busiest websites, including Google, Netflix, and Hack The Box.

### Microsoft Internet Information Services (IIS)
*   **Market Share:** The third most popular web server.
*   **Key Characteristics:**
    *   **Platform:** Developed by Microsoft and runs exclusively on **Windows Server**.
    *   **Integration:** Tightly integrated with the Microsoft ecosystem, including the **.NET framework** and **Active Directory** (e.g., for Windows Integrated Authentication).
*   **Used By:** Organizations that are heavily invested in the Microsoft stack, such as Microsoft itself, Stack Overflow, and many large enterprises.

---

## 3. Other Notable Web Servers

*   **Apache Tomcat:** Not a full HTTP server, but a "servlet container" specifically designed to run web applications written in **Java**.
*   **Node.js:** While it's a JavaScript runtime, it includes a built-in HTTP server module, allowing developers to create entire web servers purely in JavaScript.
*   **Lighttpd ("lighty"):** A lightweight web server optimized for speed and low resource usage.

**Key Takeaway for Pentesters:** Identifying the web server software and version (often revealed in the `Server` response header) is a critical first step in reconnaissance. It allows an attacker to search for known vulnerabilities, misconfigurations, and default credentials specific to that server software.
