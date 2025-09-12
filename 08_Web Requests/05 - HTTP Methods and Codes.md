# 05 - HTTP Methods and Codes

## 1. HTTP Request Methods

The HTTP method, or "verb," indicates the desired action to be performed on a resource. While there are many methods, a few are used in the vast majority of web communications.

| Method | Description | Safe? | Key Use Case |
| :--- | :--- | :--- | :--- |
| **`GET`** | Requests a representation of the specified resource. Data can be passed in the URL's query string. | **Yes** | The most common method. Used for retrieving web pages, images, and data. |
| **`POST`** | Submits an entity to the specified resource, often causing a change in state or side effects on the server. Data is sent in the request body. | **No** | Submitting login forms, uploading files, creating a new user. |
| **`HEAD`** | Identical to a `GET` request, but the server **does not** send the response body. | **Yes** | A very fast way to check a resource's metadata (like its `Content-Length` or `Last-Modified` date) without downloading the entire file. |
| **`PUT`** | Replaces all current representations of the target resource with the request payload. | **No** | Uploading a file to a specific path, completely overwriting it if it already exists. |
| **`DELETE`**| Deletes the specified resource. | **No** | Deleting a file, a user account, or another resource from the server. |
| **`OPTIONS`**| Describes the communication options (i.e., the allowed HTTP methods) for the target resource. | **Yes** | A key method for reconnaissance, as it can tell an attacker which methods are enabled on a server endpoint. |
| **`PATCH`** | Applies partial modifications to a resource. | **No** | Updating a single field of a user's profile without resubmitting the entire profile. |

*   **Safe Methods (`GET`, `HEAD`, `OPTIONS`)** are those that are not intended to have any side effects on the server.

---

## 2. HTTP Status Codes

The status code is a three-digit number included in the first line of the server's response that indicates the result of the client's request. They are grouped into five classes.

### Status Code Classes

| Class | Name | Meaning |
| :--- | :--- | :--- |
| **`1xx`** | **Informational**| The request was received and the process is continuing. |
| **`2xx`** | **Success** | The request was successfully received, understood, and accepted. |
| **`3xx`** | **Redirection** | Further action must be taken by the client to complete the request. |
| **`4xx`** | **Client Error** | The client seems to have made an error (e.g., a malformed request or requesting a non-existent page). |
| **`5xx`** | **Server Error** | The server failed to fulfill a seemingly valid request. |

### "Must-Know" Status Codes
While there are many status codes, these are the ones you will encounter most frequently.

| Code | Status Message | Meaning |
| :--- | :--- | :--- |
| **`200 OK`** | **OK** | The request has succeeded. The standard response for a successful `GET`. |
| **`301 Moved Permanently`**| **Moved Permanently**| The requested resource has been assigned a new, permanent URL. |
| **`302 Found`**| **Found (Temporary Redirect)**| The server is redirecting the client to a different URL for the time being. Common after a successful login. |
| **`400 Bad Request`**| **Bad Request** | The server cannot process the request due to a client-side syntax error. |
| **`401 Unauthorized`**| **Unauthorized** | The client must authenticate itself to get the requested response. |
| **`403 Forbidden`**| **Forbidden** | The client does not have access rights to the content. The server understands the request but refuses to authorize it. |
| **`404 Not Found`**| **Not Found** | The server cannot find the requested resource. This is a key code used when enumerating for hidden files and directories. |
| **`500 Internal Server Error`**| **Internal Server Error**| A generic server-side error, indicating that something went wrong on the server and it could not be more specific. Often indicates a bug in the application code. |
