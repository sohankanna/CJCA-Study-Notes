# 09 - Firewall and IDS,IPS Evasion

## 1. Understanding Firewalls and IDS/IPS

*   **Firewall:** A network security device that acts as a gatekeeper. It inspects network traffic and decides whether to **allow** or **block** it based on a set of predefined rules.
*   **IDS (Intrusion Detection System):** A passive monitoring system that inspects network traffic for known attack signatures or anomalous behavior. When it detects a potential threat, it generates an **alert**.
*   **IPS (Intrusion Prevention System):** An active system that sits "in-line" with network traffic. Like an IDS, it detects threats, but it can also **actively block** the malicious traffic in real-time.

---

## 2. Determining Firewall Rules (`-sA` ACK Scan)

A standard SYN scan (`-sS`) can be easily blocked by a stateful firewall. An **ACK Scan (`-sA`)** is a more advanced technique used to map out firewall rule sets and determine if ports are `filtered` or `unfiltered`.

*   **How it Works:** The ACK scan sends a TCP packet with only the `ACK` flag set.
    *   If a host responds with an `RST` packet, the port is marked as **`unfiltered`**. This means the packet reached the host, indicating there is no firewall rule blocking it.
    *   If no response is received, or an ICMP "unreachable" error is returned, the port is marked as **`filtered`**. This means a firewall is likely blocking the ACK packet.
*   **Limitation:** The ACK scan **cannot determine if a port is `open`**. Its primary purpose is to probe firewall rules.

```shell
# An ACK scan can often get responses from ports that a SYN scan would show as filtered.
sudo nmap <target> -sA
```

---

## 3. Evading IDS/IPS

IDS/IPS systems look for suspicious patterns. Evasion techniques aim to make your scan traffic look less suspicious or to hide your true identity.

### a) Decoys (`-D`)
The `-D` flag is used to spoof the source IP address of scan packets to make it harder for an IDS to determine where the scan is actually coming from.

*   **How it Works:** Nmap sends scan packets that appear to be coming from multiple, random IP addresses (the "decoys"), with your real IP address hidden among them.
*   **Syntax:**
    ```shell
    # Send scan packets from 5 random decoy IPs plus your own
    sudo nmap <target> -D RND:5

    # You can also specify specific decoy IPs
    sudo nmap <target> -D decoy1,decoy2,ME
    ```
    *(`ME` tells Nmap where to place your real IP in the sequence).*
*   **Limitation:** The decoys must be online hosts for some scans to work properly. Many ISPs will also block packets with a spoofed source IP address.

### b) Source Port Manipulation (`--source-port`)
Some firewalls have poorly configured rules that trust traffic originating from a specific source port, most commonly **port 53 (DNS)**.

*   **How it Works:** The `--source-port` flag (or `-g`) tells Nmap to send all of its scan probes *from* the specified port.
*   **The Attack:** An attacker might find that a port is `filtered` with a standard scan. By changing their source port to `53`, the firewall might trust the packet and allow it through, revealing that the port is actually `open`.
*   **Syntax:**
    ```shell
    sudo nmap <target> -p 50000 --source-port 53
    ```

---

## 4. Other Key Evasion Techniques

| Option | Description | Technique |
| :--- | :--- | :--- |
| **`-f`** | **Fragment Packets.** Splits the scan packets into smaller, 8-byte fragments. | This can sometimes evade older, less sophisticated IDS/IPS that do not properly reassemble fragmented packets for inspection. |
| **`--data-length <num>`** | Appends a specified number of random bytes to most sent packets. | Can be used to make packets look like they contain legitimate data, potentially bypassing simple filters. |
| **`--scan-delay <time>`** | Adds a mandatory delay between each probe Nmap sends. | This is a simple but effective way to slow down a scan and make it "less noisy," reducing the chances of triggering rate-based alerts on an IDS/IPS. |
| **`-S <spoofed_ip>`** | **Spoof Source Address.** A more direct way to set a single fake source IP address. (Note: Often blocked by ISPs). | This is used when you need to test a specific firewall rule (e.g., "does the firewall allow traffic from this trusted IP?"). Requires the `-e` flag to specify the interface. |

**Key Takeaway:** Evading modern security systems is a complex cat-and-mouse game. These Nmap techniques are powerful tools for probing defenses, but a skilled defender with a well-configured firewall and IPS will likely still detect aggressive scanning activity.
