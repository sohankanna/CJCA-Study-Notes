# 02 - Introduction to Nmap

## 1. What is Nmap?

**Nmap** is a powerful command-line tool used to scan IP networks to discover hosts and services. It uses raw IP packets to determine what hosts are available, what services (application name and version) those hosts are offering, what operating systems they are running, what type of packet filters/firewalls are in use, and dozens of other characteristics.

### Common Use Cases
*   **Network Mapping:** Discovering live hosts on a network.
*   **Port Scanning:** Identifying open TCP and UDP ports on a target.
*   **Service & Version Enumeration:** Determining the specific software and version running on an open port.
*   **OS Detection:** Attempting to identify the operating system of the target host.
*   **Security Auditing:** Using the **Nmap Scripting Engine (NSE)** to scan for common vulnerabilities and misconfigurations.

---

## 2. The Nmap Architecture (Scanning Phases)

A typical Nmap scan can be broken down into a series of logical phases:

1.  **Host Discovery:** Determines which hosts within the target range are online and responsive.
2.  **Port Scanning:** Probes the identified live hosts to determine which ports are open, closed, or filtered.
3.  **Service & Version Detection:** Interrogates the open ports to identify the running service and its version number.
4.  **OS Detection:** Analyzes the target's responses to a series of probes to make an educated guess about its operating system.
5.  **Script Scanning (NSE):** Runs scripts against the discovered services to perform more advanced enumeration or vulnerability checks.

---

## 3. Basic Nmap Syntax

The structure of an Nmap command is straightforward.

*   **Syntax:**
    ```shell
    nmap <scan_type(s)> <options> <target(s)>
    ```
    *   **`<scan_type(s)>`:** Specifies the technique Nmap will use to scan ports (e.g., `-sS`, `-sT`, `-sU`).
    *   **`<options>`:** Modifies the scan's behavior (e.g., `-p-` for all ports, `-sV` for version detection).
    *   **`<target(s)>`:** The IP address, hostname, or network range to be scanned.

---

## 4. Understanding the TCP SYN Scan (`-sS`)

The **TCP SYN Scan** is the default scan type for a privileged user (one who can create raw packets, like `root` or a user with `sudo`) and is the most popular scan method.

*   **Also Known As:** A "half-open" scan or a "stealth" scan.
*   **How it Works:**
    1.  Nmap sends a TCP packet with only the **SYN** (Synchronize) flag set to the target port.
    2.  It then analyzes the response to determine the port's state.
*   **Interpreting the Responses:**
    *   **`SYN/ACK` Response:** If the target responds with a packet containing both the **SYN** and **ACK** (Acknowledge) flags, the port is **OPEN**. Nmap then sends an `RST` (Reset) packet to tear down the connection before the three-way handshake is completed.
    *   **`RST` Response:** If the target responds with an **RST** packet, the port is **CLOSED**.
    *   **No Response:** If Nmap receives no response, the port is marked as **FILTERED**, which means a firewall or other filtering device is likely dropping the packet.

### Example `nmap` Scan
```shell
# Run a TCP SYN scan against the local machine
sudo nmap -sS localhost
```
**Example Output:**
```
Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-11 22:50 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000010s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
5432/tcp open  postgresql
5901/tcp open  vnc-1

Nmap done: 1 IP address (1 host up) scanned in 0.18 seconds
```
This output clearly shows four open TCP ports, their state, and the common service associated with each port.
