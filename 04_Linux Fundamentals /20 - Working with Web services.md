# Working with Web services

## 1. The Apache Web Server

**Apache** is a powerful, modular, and one of the most widely used open-source web servers in the world.

*   **Analogy:** Think of Apache as the foundational framework of a house. Its core function is to serve content, but its real power comes from its modularity—you can add "rooms" (modules) to extend its functionality.
*   **Modules:**
    *   `mod_ssl`: Adds HTTPS capability to encrypt traffic.
    *   `mod_proxy`: Allows Apache to act as a reverse proxy.
    *   `mod_rewrite`: Enables powerful URL manipulation and redirection.
*   **Default Web Root:** `/var/www/html` - Files placed in this directory are served to visitors by default.
*   **Main Configuration File:** `/etc/apache2/apache2.conf`
*   **Port Configuration:** `/etc/apache2/ports.conf` - This file is where you change the default listening port (e.g., from 80 to 8080).

### Managing the Apache Service
```shell
# Install Apache on Debian/Ubuntu
sudo apt install apache2 -y

# Start the Apache service
sudo systemctl start apache2

# Check the status of the service
sudo systemctl status apache2

# Restart the service (after making configuration changes)
sudo systemctl restart apache2

```

## 2. Command-Line Web Clients

While web browsers are used to render and interact with websites, command-line tools are essential for scripting, automation, and detailed analysis of web traffic.

### curl (Client for URL)

- **What it is:** A versatile command-line tool for transferring data with URLs. It can speak dozens of protocols, but it is most commonly used for making HTTP/S requests.
    
- **Core Function:** curl displays the **raw response body** (e.g., the HTML source code) of a URL directly to your standard output (STDOUT).
    
- **Basic Usage (Get a webpage):**

```
curl http://localhost
```

**View Only Headers (-I flag):**

```
curl -I http://localhost:8080
```

- This is useful for quickly checking the server's status code and response headers without downloading the entire page.
    

### wget

- **What it is:** A command-line utility for **downloading files** from the web.
    
- **Core Function:** Unlike curl, which prints to STDOUT, wget's primary purpose is to save the content of a URL to a local file.
    
- **Basic Usage:**
```
wget http://localhost
```

This command will download the webpage and save it as index.html in the current directory.

## 3. Python's Simple HTTP Server

Python includes a built-in, simple web server module that is an **invaluable tool for penetration testers**. It is perfect for quickly sharing files from your machine to a target machine over the network.

- **Important:** This is **not** a production-grade web server. It's for temporary, ad-hoc file sharing and development purposes only.
    

### How to Use It

The command starts a web server in the directory where you run it.

- **Start the server on the default port (8000):**

```
python3 -m http.server
```

**Start the server on a different port:**

```
python3 -m http.server 4444
```

```
python3 -m http.server --directory /path/to/share
```

- **Accessing Files:** From another machine on the same network, you can now browse to http://<your_ip>:<port> and click to download any file in the directory where the server is running. The server will print a log of all incoming GET requests to your terminal.
