# 03 -  HTTP Requests and Responses

## 1. The HTTP Request

An **HTTP Request** is a message sent by a client (e.g., a web browser, `cURL`) to a server to ask for a resource or perform an action.

### Structure of an HTTP Request
An HTTP request consists of three main parts: the request line, headers, and an optional body.

#### a) Request Line
This is the very first line of the request and contains three essential components.
`GET /users/login.html HTTP/1.1`

| Component | Example | Description |
| :--- | :--- | :--- |
| **Method** | `GET` | The HTTP Verb that specifies the action to be performed (e.g., `GET`, `POST`). |
| **Path** | `/users/login.html`| The path to the specific resource being requested on the server. |
| **Version** | `HTTP/1.1` | The version of the HTTP protocol being used. |

#### b) Request Headers
These are key-value pairs that follow the request line, providing additional information or context about the request.

*   **`Host: inlanefreight.com`**: **Mandatory in HTTP/1.1.** Specifies the domain name of the server being requested.
*   **`User-Agent: Mozilla/5.0 ...`**: Identifies the client software making the request (e.g., the browser type and version).
*   **`Cookie: PHPSESSID=...`**: Sends any cookies the client has stored for this domain back to the server.
*   **`Accept: */*`**: Tells the server what kind of content types the client can understand.

#### c) Request Body
This is an **optional** part of the request that contains data to be sent to the server. It is primarily used with methods like `POST` to submit form data or upload files. `GET` requests do not have a body.

---

## 2. The HTTP Response

An **HTTP Response** is the message a server sends back to the client after receiving and processing its request.

### Structure of an HTTP Response
An HTTP response mirrors the structure of a request, with a status line, headers, and a body.

#### a) Status Line
The first line of the response, containing three components.
`HTTP/1.1 200 OK`

| Component | Example | Description |
| :--- | :--- | :--- |
| **Version** | `HTTP/1.1` | The version of the HTTP protocol being used. |
| **Status Code**| `200` | A 3-digit number indicating the result of the request. |
| **Status Message**| `OK` | A short, human-readable text description of the status code. |

#### b) Response Headers
Key-value pairs that provide metadata about the response.
*   **`Server: Apache/2.4.41`**: Identifies the web server software.
*   **`Content-Type: text/html`**: Specifies the media type of the resource in the response body.
*   **`Content-Length: 464`**: The size of the response body in bytes.
*   **`Set-Cookie: PHPSESSID=...`**: Instructs the client's browser to store a cookie.

#### c) Response Body
This is the main part of the response, containing the actual resource that was requested (e.g., the HTML source code of the webpage, a JSON object, an image file).

---

## 3. Tools for Viewing Requests and Responses

### `cURL` (Verbose Mode)
The `-v` (verbose) flag in `cURL` is extremely useful for seeing the full request and response, including all headers.

*   **Syntax:** `curl <URL> -v`
*   **Output Breakdown:**
    *   Lines prefixed with `>` are part of the **request** that `cURL` is sending.
    *   Lines prefixed with `<` are part of the **response** that the server is sending back.

### Browser Developer Tools
Modern web browsers have powerful, built-in Developer Tools that are essential for web penetration testing.

*   **How to Open:** Press `F12` or `Ctrl+Shift+I` in most browsers (Chrome, Firefox).
*   **The Network Tab:** This is the most important tab for our purposes.
    1.  Open the Network tab.
    2.  Refresh the webpage.
    3.  You will see a list of **every single request** the page made to load its resources (HTML, CSS, JavaScript, images, API calls).
    4.  Clicking on any individual request will show you its full request and response headers, body, cookies, and timing information in a clean, organized interface.
