# 04- Host and Port Scanning

## 1. Understanding Port States

Nmap can report a port in one of six states. Understanding these is key to interpreting scan results.

| State | Description |
| :--- | :--- |
| **`open`** | The port is actively accepting TCP connections or UDP datagrams. A service is listening here. This is our primary interest. |
| **`closed`**| The port is accessible, but there is no application listening on it. For TCP, the host responded with an `RST` packet. |
| **`filtered`**| Nmap cannot determine if the port is open or closed because a firewall, filter, or other network device is blocking the probes. Nmap typically receives no response at all for these ports. |
| **`unfiltered`**| The port is accessible, but Nmap cannot determine if it is open or closed. This state is only seen in an ACK scan (`-sA`). |
| **`open|filtered`**| Nmap cannot determine if the port is open or filtered. This often happens with UDP scans where no response is received. |
| **`closed|filtered`**| Nmap cannot determine if the port is closed or filtered. This is a rare state seen only in the IP ID idle scan. |

---

## 2. Defining Port Scan Targets

You can tell Nmap exactly which ports to scan, which is more efficient than scanning all 65,535.

| Option | Description | Example |
| :--- | :--- | :--- |
| **`-p <ports>`** | Scans a specific list or range of ports. | `-p 22,80,443` <br> `-p 22-1000` |
| **`--top-ports <number>`**| Scans the `n` most common ports from Nmap's internal database. | `--top-ports=10` |
| **`-F` (Fast Scan)**| A shortcut for `--top-ports=100`. | `-F` |
| **`-p-`** | A shortcut to scan **all 65,535** TCP/UDP ports. | `-p-` |

---

## 3. Core TCP Port Scanning Techniques

### a) TCP SYN Scan (`-sS`)
*   **What it is:** The default scan for privileged users. It's a "half-open" or "stealth" scan.
*   **How it Works:** Sends a `SYN` packet. An `SYN/ACK` response means the port is **open**. An `RST` response means the port is **closed**.
*   **Pros:** Fast and relatively stealthy because it doesn't complete the full TCP three-way handshake, which is less likely to be logged by older systems.

### b) TCP Connect Scan (`-sT`)
*   **What it is:** The default scan for unprivileged users who cannot create raw packets.
*   **How it Works:** Uses the operating system's `connect()` system call to perform a **full TCP three-way handshake**.
*   **Pros:** Highly accurate and can sometimes bypass firewalls that filter `SYN` packets.
*   **Cons:** Slower and much "noisier" than a SYN scan. A full connection is almost always logged by the target system.

---

## 4. UDP Port Scanning (`-sU`)

Scanning for open UDP ports is fundamentally different and more challenging than scanning for TCP.

*   **How it Works:** Nmap sends an empty UDP datagram to the target port.
*   **Interpreting Results:**
    *   **Response Received:** If any UDP response is received, the port is marked **`open`**.
    *   **ICMP "Port Unreachable" Error:** If the target responds with this specific ICMP error (type 3, code 3), the port is definitively **`closed`**.
    *   **No Response:** If no response is received after multiple retransmissions, the port is marked **`open|filtered`**. This is a very common result, as open UDP ports are not required to respond to empty datagrams, and firewalls often drop them silently.
*   **Challenge:** UDP scanning is significantly **slower** than TCP scanning due to the need to wait for potential timeouts.

---

## 5. Service and Version Detection (`-sV`)

This is one of the most valuable options in Nmap.

*   **What it is:** After finding an open port, the `-sV` flag tells Nmap to send a series of probes to that port to try and determine the **exact software and version** of the service running there.
*   **How it Works:** Nmap has a large database of service-specific probes and response signatures. It sends probes and matches the responses against this database.
*   **Why it's Crucial:** Knowing the exact version (e.g., "Samba smbd 3.X - 4.X") is the key to finding specific, publicly known vulnerabilities (CVEs) and exploits for that service. This moves the test from simple port scanning to true vulnerability analysis.
