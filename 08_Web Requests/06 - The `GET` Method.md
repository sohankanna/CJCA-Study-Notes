# 06 - The `GET` Method

## 1. What is a `GET` Request?

When you type a URL into your browser, click a link, or view an image on a webpage, your browser is sending a `GET` request to a server.

*   **Purpose:** To request and retrieve data from a specified resource.
*   **Data Transmission:** `GET` requests should only retrieve data. Any data sent *to* the server must be appended to the URL as **query string parameters**.
    *   **Example:** `https://example.com/search.php?query=dogs&page=2`
    *   This is not suitable for sending sensitive information like passwords, as the parameters are visible in the URL, browser history, and server logs.
*   **Safety:** `GET` is considered a "safe" method, meaning it is not intended to change the state of the server.

---

## 2. Handling `GET` Requests with Authentication

Web servers can protect resources and require authentication even for `GET` requests. A common (though older) method for this is **HTTP Basic Authentication**.

### HTTP Basic Authentication
*   **How it Works:** The server first responds to an unauthenticated request with a `401 Unauthorized` status code and a `WWW-Authenticate: Basic realm="..."` header. This prompts the browser to display a native login pop-up.
*   **The `Authorization` Header:** When the user enters their credentials, the browser retries the request, this time adding an `Authorization` header.
    *   **Format:** `Authorization: Basic <base64_encoded_credentials>`
    *   The value is the string `username:password` encoded in Base64.
    *   **Example:** `admin:admin` becomes `YWRtaW46YWRtaW4=`.

### Making Authenticated `GET` Requests with `cURL`
There are several ways to provide Basic Auth credentials with `cURL`.

1.  **Using the `-u` flag (Recommended):**
    `cURL` handles the Base64 encoding for you.
    ```shell
    curl -u admin:admin http://<SERVER_IP>:<PORT>/
    ```

2.  **Embedding in the URL:**
    You can include the credentials directly in the URL.
    ```shell
    curl http://admin:admin@<SERVER_IP>:<PORT>/
    ```

3.  **Manually setting the `Authorization` header (`-H` flag):**
    This method requires you to manually Base64 encode the `username:password` string.
    ```shell
    curl -H "Authorization: Basic YWRtaW46YWRtaW4=" http://<SERVER_IP>:<PORT>/
    ```

---

## 3. Analyzing `GET` Requests with Browser DevTools

Browser Developer Tools (`F12` or `Ctrl+Shift+I`) are essential for analyzing how a web application works.

### The Network Tab
The Network tab records every request a webpage makes.
1.  Open the Network tab and clear any existing requests.
2.  Perform an action on the page (e.g., type in a search box and hit Enter).
3.  Observe the new request that appears in the list.

### Replicating Requests
DevTools make it incredibly easy to replicate a request for further testing.
*   **Right-click** on the request in the Network tab.
*   **Copy > Copy as cURL:** This copies the entire request, including all headers and cookies, as a `cURL` command that you can paste directly into your terminal. This is an extremely common and useful technique for penetration testers.
*   **Copy > Copy as Fetch:** This copies the request as a JavaScript `fetch()` command, which you can paste into the browser's **Console** tab to re-send the request from within the browser itself.
