# 06 - JavaScript

## 1. What is JavaScript?

If HTML is the skeleton and CSS is the skin and clothes, then **JavaScript** is the **nervous system and muscles** of a webpage. It is a full-fledged programming language that is executed by the user's web browser (client-side).

*   **Core Idea:** JavaScript is responsible for making a webpage **interactive**. Without it, a page would be static and non-responsive to user actions.
*   **Primary Functions:**
    *   Manipulating the **DOM (Document Object Model)**: Dynamically changing the HTML and CSS of a page after it has loaded.
    *   Handling user events (e.g., clicks, mouse movements, keyboard input).
    *   Validating data in forms before it's sent to the server.
    *   Making asynchronous network requests (**Ajax**) to fetch or send data to the server without a full page reload.

---

## 2. How JavaScript is Included in a Webpage

JavaScript code can be included in an HTML document in two main ways, both using the `<script>` tag.

1.  **Inline Script:**
    The JavaScript code is written directly inside the `<script>` tags within the HTML file.
    ```html
    <script type_of="text/javascript">
        alert('Hello, World!');
    </script>
    ```

2.  **External Script (Best Practice):**
    The JavaScript code is placed in a separate `.js` file, which is then linked in the HTML file using the `src` attribute. This is the preferred method as it keeps the code organized and allows the browser to cache the script file.
    ```html
    <script src="./assets/main.js"></script>
    ```

---

## 3. The Power of JavaScript: DOM Manipulation

The primary way JavaScript makes a page dynamic is by interacting with the DOM. It can find, create, change, or delete any HTML element on the page.

*   **Example:** This line of JavaScript finds the HTML element with the `id` of "button1" and changes the text inside it.
    ```javascript
    document.getElementById("button1").innerHTML = "Text Changed!";
    ```

### Asynchronous JavaScript and XML (Ajax)
*   **What it is:** A set of web development techniques that allow a web page to make requests to a server in the background and update parts of the page with the response, **without requiring a full page refresh**.
*   **Why it's important:** Ajax is the technology that powers most modern, dynamic web applications, making them feel fast and responsive like a desktop application.

---

## 4. JavaScript Frameworks and Libraries

Writing a large, complex web application with "vanilla" (plain) JavaScript can be inefficient. To speed up development and provide standardized solutions to common problems, developers use **JavaScript frameworks and libraries**.

*   **What they are:** Pre-written collections of JavaScript code that provide reusable components, tools, and a structured way to build applications.

### Popular Front End Frameworks
*   **React:** Developed by Facebook. The most popular framework for building user interfaces.
*   **Angular:** A comprehensive framework developed by Google.
*   **Vue.js:** A progressive framework known for its simplicity and ease of integration.
*   **jQuery:** An older but still widely used library that simplifies DOM manipulation and Ajax requests.

### Back End JavaScript (Node.js)
*   **Node.js:** A runtime environment that allows JavaScript to be used on the **back end (server-side)**, outside of a web browser. This has made JavaScript a "full-stack" language, capable of powering both the front end and back end of a web application.

---

## 5. Security Relevance

JavaScript is at the heart of many of the most common web application vulnerabilities.

*   **Cross-Site Scripting (XSS):** This is the primary JavaScript-related vulnerability. It occurs when an attacker can inject malicious JavaScript code into a webpage, which is then executed by the browsers of other users. This can be used to steal session cookies, redirect users, or deface websites.
*   **Insecure Client-Side Logic:** If developers place sensitive logic (like pricing calculations or permission checks) in the front-end JavaScript, an attacker can simply view and manipulate this code in their browser to bypass the intended controls. **Security decisions should always be made on the back end.**
