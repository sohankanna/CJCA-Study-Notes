# 03 - Host Discovery

## 1. The `-sn` Flag: The Ping Scan

The `-sn` flag is the primary option for performing a host discovery scan.

*   **What it does:** It tells Nmap to perform **only host discovery** and to **skip the port scanning** phase. This makes it much faster and stealthier than a full port scan.
*   **Also Known As:** A "Ping Scan."
*   **Analogy:** This is like knocking on every door in a neighborhood just to see who is home, without trying to open any of the doors.

---

## 2. Defining Scan Targets

Nmap is extremely flexible in how you can specify the targets for your scan.

### a) Scanning a Network Range (CIDR)
This is the most common way to scan an entire subnet.

```shell
# Scan the entire 10.129.2.0/24 network
sudo nmap -sn 10.129.2.0/24
```

### b) Scanning from a List of IPs (`-iL`)
If you have a file containing a list of target IP addresses, you can use the `-iL` flag.

*   **File (`hosts.lst`):**
    ```
    10.129.2.4
    10.129.2.10
    ...
    ```
*   **Command:**
    ```shell
    sudo nmap -sn -iL hosts.lst
    ```

### c) Scanning Multiple or Ranged IPs
You can specify multiple targets directly on the command line.
*   **Multiple individual IPs:**
    ```shell
    sudo nmap -sn 10.129.2.18 10.129.2.19
    ```
*   **A range of IPs:**
    ```shell
    sudo nmap -sn 10.129.2.18-20
    ```

### d) Scanning a Single IP
This is used to quickly check if a single host is online.
```shell
sudo nmap -sn 10.129.2.18
```

---

## 3. How Nmap Discovers Hosts (ARP vs. ICMP)

Nmap uses different techniques to discover hosts depending on the network context.

### The Default Behavior on a Local Network (LAN)
*   **ARP Ping:** If Nmap detects that you are scanning hosts on the **same local network** (like the same Ethernet or Wi-Fi network), it will **default to using ARP requests** for host discovery.
*   **Why?** ARP is much **faster and more reliable** on a LAN than ICMP (`ping`). Most hosts cannot block ARP requests without losing network connectivity, whereas many are configured to block ICMP.
*   **Detection:** Nmap sends an "ARP who-has" request. If it receives an "ARP reply," it knows the host is **UP**.

### Forcing an ICMP Scan on a LAN
If you want to force Nmap to use a traditional ICMP ping scan, even on a local network, you must explicitly disable ARP ping.

*   **Command:**
    ```shell
    # -PE: Use ICMP Echo Request
    # --disable-arp-ping: Do not use ARP for host discovery
    sudo nmap -sn -PE --disable-arp-ping 10.129.2.18
    ```

---

## 4. Useful Nmap Options for Host Discovery

| Option | Description |
| :--- | :--- |
| **`-oA <filename>`** | **O**utput in **A**ll formats. Saves the scan results to `.nmap`, `.gnmap`, and `.xml` files. **This is a critical best practice for documentation.** |
| **`--packet-trace`** | Shows every single packet Nmap sends and receives. Extremely useful for debugging and understanding exactly how a scan is working. |
| **`--reason`** | For each result (e.g., "Host is up"), this flag will tell you *why* Nmap came to that conclusion (e.g., "received arp-response"). |
| **`-PE`** | Explicitly tells Nmap to use an **ICMP Echo Request** for its ping scan. This is the default for remote (non-LAN) targets. |
