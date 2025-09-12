# 02 -Hypertext Transfer Protocol Secure (HTTPS)

## 1. The Problem with HTTP: Cleartext Transmission

The primary drawback of the original HTTP protocol is that all data, including sensitive information like usernames, passwords, and credit card numbers, is sent in **cleartext**.

*   **Security Risk:** Anyone on the network between the client and the server (e.g., on a public Wi-Fi network) can perform a **Man-in-the-Middle (MITM)** attack to intercept, read, and even modify the traffic.
*   **Example:** A captured HTTP login request would show the username and password in plain, readable text.

---

## 2. What is HTTPS?

**HTTPS (HTTP Secure)** is the solution to HTTP's lack of security. It is not a separate protocol but rather HTTP communication layered on top of a secure, encrypted channel provided by **SSL (Secure Sockets Layer)** or, more commonly today, its modern successor, **TLS (Transport Layer Security)**.

*   **Core Idea:** HTTPS wraps all HTTP communication in a layer of encryption.
*   **Default Port:** TCP/443
*   **Result:** An attacker intercepting HTTPS traffic will only see an encrypted stream of data, making it impossible to read the sensitive information within.

### Identifying an HTTPS Website
*   The URL will start with `https://`.
*   A **lock icon** will appear in the browser's address bar. Clicking this icon provides details about the site's security certificate.

---

## 3. The HTTPS Flow and TLS Handshake

This is the high-level process of establishing a secure connection.

1.  **Redirection (if necessary):** If a user tries to visit `http://example.com` and the site enforces HTTPS, the server on port 80 will respond with a **`301 Moved Permanently`** status code, redirecting the browser to `https://example.com` on port 443.

2.  **The TLS Handshake:** This is the critical negotiation process that happens before any application data is sent.
    *   **Client Hello:** The client (browser) sends a message to the server, announcing the TLS versions and cipher suites it supports.
    *   **Server Hello & Certificate:** The server responds, agreeing on a TLS version and cipher suite. Crucially, it sends its **SSL/TLS certificate** to the client. This certificate contains the server's public key and is digitally signed by a trusted **Certificate Authority (CA)**.
    *   **Certificate Verification:** The client verifies the server's certificate to ensure it is valid and was issued by a trusted CA. This authenticates the server and prevents MITM attacks.
    *   **Key Exchange:** The client and server use the server's public key to securely exchange information needed to generate a **shared, symmetric session key**.
    *   **Finished:** Both sides send an encrypted "Finished" message, confirming that the handshake was successful.

3.  **Encrypted Communication:** Once the handshake is complete, all subsequent HTTP request and response data is encrypted using the newly created symmetric session key.

**DNS Privacy Note:** While HTTPS encrypts your traffic to the web server, the initial DNS query to find the server's IP address may still be sent in cleartext, revealing which websites you are visiting. Using **DNS over HTTPS (DoH)** or a VPN can encrypt this DNS traffic as well.

---

## 4. Using `cURL` with HTTPS

`cURL` automatically handles the TLS handshake and encryption for HTTPS requests. However, it is strict about certificate validity.

### Dealing with Invalid Certificates
When testing development servers or lab environments, you may encounter self-signed or invalid SSL/TLS certificates. By default, `cURL` will refuse to connect, displaying an "SSL certificate problem" error. This is a security feature to protect against MITM attacks.

*   **The `-k` (or `--insecure`) flag:** This option tells `cURL` to **ignore certificate validation** and proceed with the connection.
    ```shell
    # This will fail due to the invalid certificate
    curl https://self-signed.badssl.com
    
    # This will succeed by skipping the certificate check
    curl -k https://self-signed.badssl.com
    ```
**Warning:** Only use the `-k` flag when you are in a trusted environment and you fully expect the certificate to be invalid (e.g., in a lab). Never use it for sensitive, real-world transactions.
