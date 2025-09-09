# Introduction To Windows 


Microsoft Windows is a family of graphical operating systems that has dominated the desktop and enterprise server market for decades. Understanding its history and version differences is crucial, as many organizations still run older, unsupported "legacy" systems.

### A Brief History
*   **Early Days:** Started as a graphical shell for MS-DOS in 1985. Windows 95 was the first version to fully integrate the OS and offer built-in internet support.
*   **Desktop Evolution:** Progressed through major versions like Windows XP, Vista, 7, 8, and now Windows 11.
*   **Server Evolution:** Started with Windows NT Server. The release of **Windows 2000 Server** was a landmark event, introducing **Active Directory**, a directory service that became the backbone of nearly all corporate networks. Subsequent versions (2003, 2008, 2012, 2016, 2019, 2022) added features like built-in firewalls, Hyper-V virtualization, and container support.

### Windows Versions and End-of-Life
*   As new versions are released, older ones reach their "end-of-life" (EOL) and no longer receive security updates from Microsoft, making them highly vulnerable.
*   It is very common to find legacy systems (e.g., Windows 7, Server 2008) in corporate environments, often running critical applications. These are high-value targets for penetration testers.

| Common OS Names | Internal Version Number |
| :--- | :--- |
| Windows 7 / Server 2008 R2 | 6.1 |
| Windows 8 / Server 2012 | 6.2 |
| Windows 8.1 / Server 2012 R2 | 6.3 |
| Windows 10 / Server 2016 / 2019 / 2022| 10.0 |

*   **Getting Version Info:** You can retrieve the OS version and build number in PowerShell with the following command:
    ```powershell
    Get-WmiObject -Class Win32_OperatingSystem | Select-Object Version, BuildNumber
    ```
    *   **WMI (Windows Management Instrumentation)** is a powerful interface for managing and querying information about a Windows system.

---

## 2. Accessing Windows Systems

### Local vs. Remote Access
*   **Local Access:** Interacting with a computer directly via its own keyboard, mouse, and monitor.
*   **Remote Access:** Accessing and controlling a computer over a network. This is the primary method used by system administrators and penetration testers.

### Common Remote Access Protocols
While many protocols exist (VPN, SSH, FTP), the most common protocol for *graphical* remote access to Windows is **RDP**.

---

## 3. Remote Desktop Protocol (RDP)

**RDP** is a proprietary Microsoft protocol that allows a user to connect to and interact with the graphical desktop of a remote Windows machine.

*   **Default Port:** TCP/3389
*   **Architecture:** It uses a client/server model.
    *   **Server:** The target Windows machine with "Remote Desktop" enabled.
    *   **Client:** The application used to connect to the server.

### RDP Clients
*   **On Windows:** The built-in client is the **Remote Desktop Connection** (`mstsc.exe`).
    *   **Security Note:** Be aware that `mstsc.exe` allows users to save connection profiles, including credentials, in `.rdp` files. Finding these files on a compromised machine can be a source of valuable credentials.
*   **On Linux:** **`xfreerdp`** is a powerful and popular command-line RDP client.

### Using `xfreerdp`
The `xfreerdp` command provides a wide range of options for connecting to a Windows target.

*   **Basic Connection Syntax:**
    ```shell
    xfreerdp /v:<target_ip> /u:<username> /p:<password>
    ```
    *   `/v`: Specifies the target server (victim).
    *   `/u`: Specifies the username.
    *   `/p`: Specifies the password.

**Key Takeaway:** RDP is a critical service to look for during a penetration test. If port `3389` is open, it's a primary entry point for attackers who have valid credentials.
