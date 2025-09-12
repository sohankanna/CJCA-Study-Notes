# 01 - HyperText Transfer Protocol

## 1. What is HTTP?

**HTTP** is a client-server protocol used to request and transfer resources, such as HTML documents, images, and data, across the web.

*   **Client:** The party initiating the request (e.g., your web browser).
*   **Server:** The party that receives the request and returns the resource (e.g., the web server hosting `hackthebox.com`).
*   **Default Port:** HTTP operates on **TCP port 80**. Its secure counterpart, HTTPS, uses **TCP port 443**.

---

## 2. Anatomy of a URL

A **Uniform Resource Locator (URL)** is the address used to identify and access a specific resource on the web.

`scheme://user:pass@host:port/path?query#fragment`

| Component | Example | Description |
| :--- | :--- | :--- |
| **Scheme** | `http://` | The protocol used to access the resource. **This and the Host are mandatory.** |
| **User Info**| `admin:password@`| (Optional) Credentials for authentication, sent to the host. |
| **Host** | `inlanefreight.com`| The domain name or IP address of the server. **This and the Scheme are mandatory.** |
| **Port** | `:80` | (Optional) The specific port on the server to connect to. Defaults to 80 for HTTP and 443 for HTTPS. |
| **Path** | `/dashboard.php` | The specific resource (file or folder) being requested on the server. |
| **Query String**| `?login=true`| A set of key-value pairs, starting with `?`, used to send data to the server. Multiple pairs are separated by `&`. |
| **Fragment** | `#status` | An identifier, starting with `#`, that points to a specific section *within* the requested resource. It is handled client-side by the browser. |

---

## 3. The HTTP Flow

This is the high-level process of a user accessing a website.

1.  **DNS Resolution:** The user enters a URL (e.g., `inlanefreight.com`) into their browser.
    *   The browser first checks its local cache and the system's `hosts` file.
    *   If the IP is not found locally, it sends a query to a **DNS server** to translate the domain name into an IP address (e.g., `152.153.81.14`).
2.  **HTTP Request:** The browser establishes a TCP connection to the server's IP address on the appropriate port (e.g., 80) and sends an **HTTP Request** (e.g., `GET /`).
3.  **Server Processing:** The web server receives the request, processes it, and retrieves the requested resource (e.g., `index.html`).
4.  **HTTP Response:** The server sends back an **HTTP Response**, which includes:
    *   A **Status Code** (e.g., `200 OK` for success).
    *   **Headers** with metadata about the response.
    *   The **Response Body** containing the resource itself (the HTML content).
5.  **Rendering:** The browser receives the response, renders the HTML, CSS, and JavaScript, and displays the webpage to the user.

---

## 4. `cURL` - The Command-Line Web Client

**cURL (Client URL)** is an essential command-line tool for making web requests and transferring data. It allows you to interact with web services directly from the terminal, which is crucial for scripting, automation, and penetration testing.

### Basic `cURL` Usage

| Action | Command | Description |
| :--- | :--- | :--- |
| **Make a Request**| `curl inlanefreight.com`| Sends a GET request to the URL and prints the raw HTML response body to the terminal. |
| **Download a File**| `curl -O <URL>/file.zip`| Downloads the file and saves it using its **O**riginal remote name. |
| **Download to a Specific File**| `curl -o newfile.zip <URL>/file.zip`| Downloads the file and saves it with a specified **o**utput name. |
| **Silent Mode**| `curl -s -O <URL>/file.zip`| Downloads the file without showing the progress meter or status information. |
| **View Headers** | `curl -i <URL>` | **I**ncludes the HTTP response headers in the output. |
| **Verbose Mode** | `curl -v <URL>` | Makes the operation more "talkative," showing details about the connection and both the request and response headers. |
| **Get Help** | `curl -h` or `man curl`| Displays the help menu or the full manual page. |
