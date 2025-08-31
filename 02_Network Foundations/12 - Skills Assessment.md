# 12 - Skills Assessment

## Chapter 1: Investigating the Local Host (Pwnbox)

The first step is to analyze the network configuration of our own machine, the Pwnbox.

### 1. Viewing Network Interfaces
The `ifconfig -a` command is used to display all network interfaces, both active and inactive.

*   **Command:** `ifconfig -a`
*   **Result:** The command reveals three primary interfaces on the Pwnbox: `ens3` (public), `lo` (loopback), and `tun0` (VPN).

### 2. The Loopback Interface (`lo`)
The `lo` or **loopback** interface is a special virtual interface that a computer uses to send network traffic to itself, using the IP address `127.0.0.1` or the hostname `localhost`.

### 3. Viewing Listening Services
The `netstat` utility shows active network connections and listening ports.

*   **Command:** `netstat -tulnp4`
*   **Analysis:** The output shows services listening on:
    *   `127.0.0.1` (localhost): Accessible only locally (e.g., VNC on port 5901).
    *   `0.0.0.0`: Listening on **all** available network interfaces (e.g., SSH on port 22).
    *   A specific public IP: Listening only on that interface (e.g., HTTP on port 80).

---

## Chapter 2: Interacting with the Target

This chapter focuses on connecting to and enumerating a remote target machine on the lab network.

### 1. The Tunnel Interface (`tun0`)
*   **Purpose:** The `tun0` interface is a **VPN tunnel** connecting our Pwnbox to the private HTB lab network.
*   **Verification Command:** `ip route get <target_ip>` confirms traffic to the target is routed via `tun0`.

### 2. Testing Reachability (`ping`)
The `ping` utility uses **ICMP** to check if a remote host is online.

*   **Command:** `ping -c 4 <target_ip>`

### 3. Enumerating Open Ports (`nmap`)
**Nmap** is a powerful network scanner used to discover open ports and services.

*   **Initial Scan Command:** `nmap <target_ip>`
*   **Analysis:** The scan reveals open ports (21, 80, 135, 139, 445, 3389), strongly suggesting a **Windows host**.
*   **Service Version Scan Command:** `nmap -p21,80 -sC -sV <target_ip>`
    *   This more detailed scan on specific ports reveals that port 21 (FTP) allows **Anonymous FTP login**.

---

## Chapter 3: Interacting with Services (FTP & HTTP)

This optional chapter demonstrates how to manually "speak" protocols using `netcat`.

### 1. Interacting with FTP (Port 21)
FTP requires a Carriage Return and Line Feed (`\r\n`) at the end of commands. In the terminal, this is achieved with `[Ctrl+V][Enter]`.

1.  **Connect to the FTP Control Channel:**
    ```shell
    nc <target_ip> 21
    ```
2.  **Log in as an anonymous user:**
    ```ftp
    USER anonymous[Ctrl+V][Enter]
    PASS anything[Ctrl+V][Enter]
    ```
3.  **Enter Passive Mode:**
    ```ftp
    PASV[Ctrl+V][Enter]
    ```
    *   The server responds with an IP and two numbers for the data port calculation (e.g., `194, 40`).
    *   **Port Calculation:** `(first_number * 256) + second_number` (e.g., `194 * 256 + 40 = 49704`).

4.  **Connect to the Data Channel (in a new terminal):**
    ```shell
    nc <target_ip> <calculated_port>
    ```
5.  **List Files (in the first terminal):**
    ```ftp
    LIST[Ctrl+V][Enter]
    ```
    *   The file listing (`Note-From-IT.txt`) will appear in the second terminal (the data channel).

6.  **Retrieve the File:**
    *   First, establish a new data channel by sending `PASV` again in the control channel and calculating the new port.
    *   Connect to the new port with `nc` in a separate terminal.
    *   Send the retrieve command in the control channel:
    ```ftp
    RETR Note-From-IT.txt[Ctrl+V][Enter]
    ```
    *   The contents of the file will appear in the new data channel terminal.

### 2. Interacting with HTTP (Port 80)
The note from the FTP server reveals the web server requires a specific `User-Agent` header.

1.  **Connect to the Web Server:**
    ```shell
    nc -v <target_ip> 80
    ```
2.  **Craft and Send the Manual HTTP Request:**
    *   Type each line exactly as shown below, pressing `Enter` after each line.
    *   After the final header, press `Enter` **twice** to send the request.
    ```http
    GET / HTTP/1.1
    Host: <target_ip>
    User-Agent: Server Administrator

    ```
3.  **Analyze the Result:**
    *   The server responds with the full HTTP headers and the HTML source code of the webpage.
    *   A hidden flag is discovered within the HTML comments, which would not have been visible in a normal browser.
