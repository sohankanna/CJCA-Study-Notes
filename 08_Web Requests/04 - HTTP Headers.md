# 04 - HTTP Headers

## 1. Header Categories

HTTP headers can be grouped into several categories based on their function.

### General Headers
These headers are contextual and can be present in both requests and responses.
*   **`Date`**: The date and time the message was generated.
*   **`Connection`**: Controls whether the network connection stays open after the current transaction finishes (e.g., `keep-alive` or `close`).

### Entity Headers
These headers describe the content (the "entity" or "body") of the message.
*   **`Content-Type`**: Specifies the media type of the resource (e.g., `text/html`, `application/json`, `image/jpeg`).
*   **`Content-Length`**: The size of the message body in bytes.
*   **`Content-Encoding`**: Specifies any compression applied to the body (e.g., `gzip`).

---

## 2. Request Headers

These headers are sent by the client to the server to provide more context about the request.

| Header | Example | Description |
| :--- | :--- | :--- |
| **`Host`** | `Host: www.inlanefreight.com` | **Mandatory.** Specifies the domain name of the server being requested. Allows a single web server to host multiple websites. |
| **`User-Agent`**| `User-Agent: Mozilla/5.0 ...`| Identifies the client software (browser, OS, version) making the request. |
| **`Referer`** | `Referer: https://google.com`| The URL of the page that linked to the current resource. (Note the common misspelling of "Referrer"). |
| **`Accept`** | `Accept: text/html,*/*` | Tells the server what content types the client can understand. |
| **`Cookie`** | `Cookie: PHPSESSID=...` | Sends previously stored cookies from the client back to the server to maintain a session or state. |
| **`Authorization`**| `Authorization: Basic ...` | Contains the credentials for authenticating the client to the server (e.g., a username/password or an API token). |

---

## 3. Response Headers

These headers are sent by the server back to the client and provide information about the response.

| Header | Example | Description |
| :--- | :--- | :--- |
| **`Server`** | `Server: Apache/2.4.41` | Contains information about the web server software. A key piece of information for reconnaissance. |
| **`Set-Cookie`**| `Set-Cookie: PHPSESSID=...`| Instructs the client's browser to store a cookie for future requests. |
| **`WWW-Authenticate`**| `WWW-Authenticate: Basic realm=...`| Sent with a `401 Unauthorized` response to indicate what authentication scheme is required. |
| **`Location`** | `Location: /new-page.html`| Used in redirection responses (status codes 3xx) to tell the browser the new URL to visit. |

---

## 4. Security Headers

These are special **response headers** sent by the server to instruct the browser to enable certain security features, helping to protect the user from web-based attacks.

| Header | Example | Description |
| :--- | :--- | :--- |
| **`Content-Security-Policy`** | `script-src 'self'` | **(CSP)**. A powerful header that tells the browser which sources are allowed to load resources (scripts, images, etc.). Helps prevent Cross-Site Scripting (XSS) attacks. |
| **`Strict-Transport-Security`**| `max-age=31536000` | **(HSTS)**. Tells the browser that it should *only* ever communicate with this site using HTTPS, never HTTP. Prevents SSL stripping attacks. |
| **`Referrer-Policy`** | `origin` | Controls how much referrer information the browser should include in the `Referer` header when navigating away from the page. Helps prevent leaking sensitive URLs. |
| **`X-Frame-Options`** | `SAMEORIGIN` | Prevents the page from being displayed in an `<iframe>` on another site. Helps prevent Clickjacking attacks. |

---

## 5. Working with Headers

### `cURL`
*   **`-v` (Verbose):** Shows both request (`>`) and response (`<`) headers and connection details.
*   **`-i` (Include):** Includes the response headers in the output along with the response body.
*   **`-I` (Head):** Sends a `HEAD` request to the server, which asks for **only the headers** and not the body. This is a very fast way to inspect a server's response headers.
*   **`-H` (Header):** Adds a custom header to your request.
    ```shell
    curl -H "X-Custom-Header: MyValue" https://example.com
    ```
*   **`-A` (User-Agent):** A shortcut for setting the `User-Agent` header.
    ```shell
    curl -A "MyCustomBrowser/1.0" https://example.com
    ```

### Browser Developer Tools
*   Press `F12` or `Ctrl+Shift+I` to open DevTools.
*   Go to the **Network** tab and refresh the page.
*   Click on any request in the list to view its **Request** and **Response Headers** in a clean, organized format.
