# 07 - The POST Method

## 1. Why Use `POST` instead of `GET`?

`POST` is preferred over `GET` for sending data for several key reasons:

*   **Security & Privacy:** Data sent in the `POST` body is not visible in the URL, browser history, or server access logs, making it suitable for sensitive information like passwords.
*   **Data Size:** URLs have a practical length limit (around 2000 characters). The `POST` body can handle much larger amounts of data, making it necessary for things like file uploads.
*   **Data Type:** The `POST` body can handle various data types, including binary data, whereas URLs are restricted to a limited character set.

---

## 2. Common Use Case: Login Forms

A classic example of a `POST` request is submitting a login form.

1.  The user fills in their username and password and clicks "Login".
2.  The browser packages these credentials into the **body** of an HTTP `POST` request.
3.  The request is sent to a server-side script (e.g., `/login.php`).
4.  The server processes the credentials in the request body.

### Example `POST` Request Body
The data is typically sent as key-value pairs, separated by an ampersand (`&`).
```
username=admin&password=admin
```

### Making `POST` Requests with `cURL`
*   **`-X POST`**: Specifies that the request method should be `POST`.
*   **`-d 'data'`**: Specifies the **d**ata to be sent in the request body.

```shell
curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/login.php
```
*   **`-L`**: (Follow redirects). Many login forms redirect you to a dashboard upon successful login. The `-L` flag tells `cURL` to automatically follow this redirection.

---

## 3. Maintaining State with Cookies

After a successful login, a server needs a way to remember that you are authenticated for subsequent requests. This is typically done with **cookies**.

1.  **Server Sets the Cookie:** After a successful `POST` login, the server's response will include a `Set-Cookie` header.
    *   **Example:** `Set-Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1; path=/`
2.  **Client Sends the Cookie:** The browser automatically stores this cookie and includes it in a `Cookie` header on **all future requests** to that same domain. This is how the server recognizes your session.

### Using Cookies with `cURL`
*   **`-b 'cookie'`**: Specifies the **c**ookie to send with the request.

```shell
# Authenticate once with credentials to get a valid session cookie
# Then, use that cookie for all future requests to access protected pages
curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/dashboard.php
```

---

## 4. Sending `JSON` Data

Modern web applications and APIs often send and receive data in **JSON (JavaScript Object Notation)** format instead of the traditional URL-encoded format.

*   **Key Difference:** When sending JSON, you must tell the server what kind of data you're sending by setting the `Content-Type` header to `application/json`.

### `POST` Request with `JSON`
*   **JSON Body:** `{"search":"london"}`
*   **`cURL` Command:**
    ```shell
    curl -X POST \
      -d '{"search":"london"}' \
      -b 'PHPSESSID=...' \
      -H 'Content-Type: application/json' \
      http://<SERVER_IP>:<PORT>/search.php
    ```
    *   `-d`: The data is now a JSON string.
    *   `-H 'Header: Value'`: Adds a custom **H**eader to the request. Here, we set the `Content-Type`.

This ability to manually craft and modify requests with `cURL` is a fundamental skill for testing web application security.
