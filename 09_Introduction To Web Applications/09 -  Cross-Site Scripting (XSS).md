# 09 -  Cross-Site Scripting (XSS)

## 1. What is Cross-Site Scripting (XSS)?

**XSS** is a client-side code injection vulnerability. It is an evolution of HTML Injection where the injected code is not just HTML, but executable **JavaScript**.

*   **Core Idea:** The vulnerability exists because the web application takes untrusted user input and includes it in a response page without proper validation or encoding. The victim's browser, seeing the malicious script as part of the legitimate page, executes it with the full permissions of that website.
*   **The Goal:** The ultimate goal of an XSS attack is to bypass the **Same-Origin Policy (SOP)**, a security mechanism that prevents websites from different origins from interfering with each other. By executing a script in the context of the vulnerable website, the attacker's script can access that site's data, such as the user's session cookies.

---

## 2. The Three Main Types of XSS

XSS attacks are categorized based on how the malicious payload is delivered to the victim's browser.

| Type | Description | Persistence |
| :--- | :--- | :--- |
| **Reflected XSS** | The malicious script is part of the victim's **request** to the server. The server then "reflects" this script back in its HTTP **response**, and the browser executes it. This is the most common type of XSS. | **Non-Persistent.** The attacker must trick the victim into clicking a specially crafted link that contains the payload (e.g., `http://example.com/search?query=<script>...</script>`). |
| **Stored XSS** | The malicious script is **permanently stored** on the target server, for example, in a database. It is then delivered to any user who views the page containing the stored content. | **Persistent.** The payload is served to every user who visits the affected page (e.g., a malicious script in a forum post or a product review). This is the most dangerous type of XSS. |
| **DOM-based XSS** | The vulnerability exists purely in the **client-side JavaScript code**. The user input is taken by the JavaScript and written back into the page's **DOM** without being properly sanitized, all without ever being sent to the server. | **Non-Persistent.** The payload is often delivered via a URL fragment (`#`). |

---

## 3. A Practical Example (DOM-based XSS)

Let's revisit the vulnerable code from the HTML Injection note.
```html
<script>
    function inputFunction() {
        var input = prompt("Please enter your name", "");
        if (input != null) {
            // VULNERABLE: Input is written directly to the DOM's innerHTML.
            document.getElementById("output").innerHTML = "Your name is " + input;
        }
    }
</script>
```
Because the input is written directly to `.innerHTML`, an attacker can inject a `<script>` tag or, more commonly, use an HTML tag with a JavaScript event handler.

### The Payload
This is a classic and effective XSS payload.
```html
"><img src=x onerror=alert(document.cookie)>
```
**Breakdown:**
*   `"`: Closes the previous HTML attribute.
*   `>`: Closes the previous HTML tag.
*   `<img src=x`: Tries to load an image from an invalid source `x`.
*   `onerror=alert(document.cookie)>`: This is the key part. Because the image source is invalid, the `onerror` event handler will trigger. The JavaScript code `alert(document.cookie)` is then executed, which displays the user's session cookie in an alert box.

### The Impact
When this payload is entered, the browser displays an alert box containing the user's session cookie. An attacker wouldn't just `alert()` the cookie; they would use JavaScript to silently send the `document.cookie` value to a server they control. With this stolen session cookie, the attacker can often impersonate the victim and take over their account.
