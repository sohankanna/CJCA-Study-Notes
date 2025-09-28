# 06 - Service Enumeration

## 1. The Goal: Accurate Version Detection

The primary goal of service enumeration is to determine the **exact version** of the software listening on an open port.

*   **Why it's important:** Knowing the precise version (e.g., `OpenSSH 7.6p1` vs. `OpenSSH 8.9p1`) allows a penetration tester to search for version-specific public vulnerabilities and exploits (CVEs). A generic service name like "ssh" is not enough.

---

## 2. Nmap's Service Version Detection (`-sV`)

The `-sV` flag is the primary Nmap option for performing service and version detection.

*   **How it Works:** After Nmap identifies an open port, the `-sV` engine sends a series of intelligent probes to that port. It then analyzes the responses and compares them against a large database of known service signatures (`nmap-service-probes`) to identify the software and version.
*   **Banner Grabbing:** The simplest form of version detection is "banner grabbing." Many services announce who they are in a welcome message or "banner" as soon as a client connects. Nmap captures and parses these banners.

### Running a Version Scan
It is a best practice to combine a version scan (`-sV`) with a full port scan (`-p-`) to get a complete picture of the target's attack surface.

```shell
sudo nmap 10.129.2.28 -p- -sV
```
**Example Output:**
```
PORT      STATE    SERVICE      VERSION
22/tcp    open     ssh          OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
25/tcp    open     smtp         Postfix smtpd
80/tcp    open     http         Apache httpd 2.4.29 ((Ubuntu))
...
Service Info: Host:  inlane; OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
This output is highly valuable. We not only know that port 22 is open, but we know it's running a specific version of OpenSSH on an Ubuntu Linux system.

---

## 3. Monitoring Long Scans

Full port version scans can take a long time. Nmap provides several ways to monitor their progress.

| Method | Description |
| :--- | :--- |
| **Pressing the `Space Bar`** | While a scan is running, pressing the space bar will cause Nmap to print a one-time status update, including an estimated time of completion (ETC). |
| **`--stats-every=<time>`**| Tells Nmap to automatically print a status update at a regular interval (e.g., `--stats-every=10s` for every 10 seconds). |
| **Verbose Mode (`-v` / `-vv`)**| Increases the verbosity of the output. In verbose mode (`-v`), Nmap will print open ports to the screen as soon as they are discovered, providing real-time feedback. |

---

## 4. The Importance of Manual Verification

Automated tools like Nmap are powerful, but they are not perfect. Sometimes, they can misinterpret a service's response or miss subtle details in a banner. It is a critical skill for a penetration tester to know how to **manually verify** a tool's findings.

### Example: Manual Banner Grabbing
Nmap's `-sV` scan might report the service on port 25 as `Postfix smtpd`. To get more detail, we can connect to the port manually using a simple tool like `netcat` (`nc`).

*   **Command:**
    ```shell
    nc -nv 10.129.2.28 25
    ```
*   **Result:**
    ```
    Connection to 10.129.2.28 port 25 [tcp/*] succeeded!
    220 inlane ESMTP Postfix (Ubuntu)
    ```
*   **Analysis:** The manual connection reveals an extra, crucial piece of information that Nmap's summary might have missed: the mail server is running on **Ubuntu**. This detail helps us narrow down our search for potential vulnerabilities and exploits.

**Key Takeaway:** Always use automated tools to perform the initial broad scan, but be prepared to dive in manually to verify and gather more detailed information from interesting services.
