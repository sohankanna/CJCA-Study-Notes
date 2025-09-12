# 08 - HTML Injection

## 1. What is HTML Injection?

**HTML Injection** is a vulnerability that allows an attacker to inject arbitrary HTML code into a webpage, which is then rendered by the browser as part of the page's legitimate content.

*   **Core Idea:** The vulnerability exists because the application blindly trusts user input and directly includes it in the HTML response. The browser, unable to distinguish between the intended HTML and the attacker's injected HTML, renders both.
*   **The Root Cause:** **Improper input validation and sanitization.** The application should treat all user input as untrusted data, not as executable code.

---

## 2. The Impact of HTML Injection

While it may seem simple, HTML Injection can be used for a variety of malicious purposes.

| Attack Type | Description |
| :--- | :--- |
| **Web Page Defacement** | An attacker injects HTML and CSS to drastically alter the appearance of a webpage. This can be used to display malicious ads, post propaganda, or simply vandalize the site, leading to significant reputational damage. |
| **Phishing** | An attacker injects a fake HTML login form onto a trusted webpage. A user, believing the form is legitimate, enters their credentials, which are then sent to a server controlled by the attacker. |
| **Gateway to Cross-Site Scripting (XSS)**| This is the most significant impact. HTML Injection is often a direct pathway to XSS. If an attacker can inject HTML tags like `<h1>` or `<b>`, they can almost certainly inject a `<script>` tag as well, allowing them to execute malicious JavaScript in the victim's browser. |

---

## 3. A Practical Example

Consider a simple webpage that asks for a user's name and then displays it back to them.

### Vulnerable Code
The vulnerability lies in how the user's input is handled by the JavaScript.
```html
<!DOCTYPE html>
<html>
<body>
    <button onclick="inputFunction()">Click to enter your name</button>
    <p id="output"></p>

    <script>
        function inputFunction() {
            var input = prompt("Please enter your name", "");

            if (input != null) {
                // VULNERABLE: Input is directly inserted into the HTML
                document.getElementById("output").innerHTML = "Your name is " + input;
            }
        }
    </script>
</body>
</html>
```
The line `document.getElementById("output").innerHTML = ...` is dangerous because `.innerHTML` tells the browser to parse and render any HTML tags within the `input` string.

### Exploitation
Instead of entering a normal name like "Alex", an attacker can enter a string of HTML code.

*   **The Payload:**
    ```html
    <style> body { background-image: url('https://academy.hackthebox.com/images/logo.svg'); } </style>
    ```
*   **The Result:** When the JavaScript executes, it injects this `<style>` block into the page's DOM. The browser immediately applies the new CSS rule, changing the background image of the entire page. This demonstrates a successful defacement attack.

---

## 4. Prevention

The key to preventing HTML Injection (and by extension, many forms of XSS) is to **never trust user input**.

*   **Input Validation:** On the server-side, check that user input conforms to the expected format, type, and length.
*   **Output Encoding:** This is the most critical defense. Before displaying user-supplied input back on a page, you must **encode** it so that the browser treats it as literal text, not as HTML code. For example, the `<` character should be converted to its HTML entity `&lt;`.
    *   **Vulnerable:** `<p>Hello, <script>alert(1)</script></p>`
    *   **Secure (Encoded):** `<p>Hello, &lt;script&gt;alert(1)&lt;/script&gt;</p>` (The browser will display the literal text `<script>alert(1)</script>` instead of executing it).
*   **Sanitization:** Use trusted libraries to parse user-supplied HTML and strip out any potentially dangerous tags (like `<script>`, `<iframe>`) and attributes (like `onclick`), while allowing a safe subset of tags (like `<b>`, `<i>`).
