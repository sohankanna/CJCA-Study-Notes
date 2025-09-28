# 07 - Nmap Scripting Engine

## 1. What is the Nmap Scripting Engine?

The **NSE** is a feature that allows Nmap to use **scripts written in the Lua programming language** to interact with target services. It transforms Nmap from a simple scanner into a powerful framework for security auditing and vulnerability detection.

### NSE Script Categories
Nmap's vast library of scripts is organized into 14 main categories. Understanding these categories helps you select the right scripts for your goal.

| Category        | Description                                                                                                                                         |
| :-------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`default`**   | A safe, essential subset of scripts that run by default when you use the `-sC` or `-A` flags.                                                       |
| **`discovery`** | Scripts used to gather more information about the network, such as SNMP details, SMB shares, or DNS information.                                    |
| **`vuln`**      | **Very important.** Scripts that actively check for specific, known vulnerabilities.                                                                |
| **`exploit`**   | Scripts that go a step further and attempt to actively exploit a known vulnerability.                                                               |
| **`auth`**      | Scripts that try to discover authentication credentials, often by testing for anonymous access or default logins.                                   |
| **`brute`**     | Scripts designed to perform brute-force password guessing against services like SSH, FTP, or web forms.                                             |
| **`safe`**      | Scripts that are designed to be non-intrusive and are unlikely to crash a service.                                                                  |
| **`intrusive`** | Scripts that have a higher risk of crashing a service or being disruptive. Not recommended for production environments without explicit permission. |
| **`malware`**   | Scripts that check if the target system is infected with known malware or is part of a botnet.                                                      |
| **`version`**   | Scripts used to perform more in-depth version detection than the standard `-sV` flag.                                                               |

---

## 2. How to Use NSE Scripts

There are several ways to specify which scripts Nmap should run.

### a) Default Scripts (`-sC`)
This is the most common and easiest way to run a safe and useful set of discovery scripts.
```shell
sudo nmap <target> -sC
```

### b) The Aggressive Scan (`-A`)
The `-A` flag is a powerful shortcut that enables several options at once, including:
*   Service Version Detection (`-sV`)
*   OS Detection (`-O`)
*   Traceroute (`--traceroute`)
*   **Default NSE Scripts (`-sC`)**
```shell
sudo nmap <target> -A
```

### c) Running Scripts by Category
You can run all scripts from one or more specific categories.
```shell
# Run all scripts from the "vuln" category against the web server
sudo nmap <target> -p 80 --script vuln
```

### d) Running Specific Scripts by Name
You can run one or more specific scripts by their filenames.
```shell
# Run the 'banner' and 'smtp-commands' scripts against the SMTP port
sudo nmap <target> -p 25 --script banner,smtp-commands
```
---

## 3. Practical Examples

### Example 1: Deeper SMTP Enumeration
```shell
sudo nmap 10.129.2.28 -p 25 --script banner,smtp-commands
```
**Output Analysis:**
*   **`banner` script:** Grabs the service banner, revealing `220 inlane ESMTP Postfix (Ubuntu)`. This confirms the OS.
*   **`smtp-commands` script:** Interacts with the SMTP server to determine which commands it supports (e.g., `VRFY`), which can be useful for enumerating valid usernames.

### Example 2: WordPress Enumeration with an Aggressive Scan
```shell
sudo nmap 10.129.2.28 -p 80 -A
```
**Output Analysis:**
*   The default HTTP scripts (`_http-title`, `_http-generator`) run as part of the `-A` scan.
*   **Key Finding:** The `_http-generator` script identifies the web application as **WordPress 5.3.4**, a critical piece of information.

### Example 3: Vulnerability Scanning with the `vuln` Category
```shell
sudo nmap 10.129.2.28 -p 80 -sV --script vuln
```
**Output Analysis:**
*   **`http-enum` script:** Discovers common WordPress directories and files like `/wp-login.php` and `/readme.html`.
*   **`http-wordpress-users` script:** Attempts to enumerate valid usernames, successfully finding the `admin` user.
*   **`vulners` script:** Cross-references the discovered service version (`Apache httpd 2.4.29`) with the Vulners database and lists associated public vulnerabilities (**CVEs**).

**Key Takeaway:** The Nmap Scripting Engine transforms Nmap from a simple port scanner into a powerful, extensible framework for deep service enumeration and automated vulnerability discovery.
