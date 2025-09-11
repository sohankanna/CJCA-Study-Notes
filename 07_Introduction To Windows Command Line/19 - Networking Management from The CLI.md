# Networking Management from The CLI


## 1. Common Windows Networking Protocols

Windows networking relies on a suite of standard and proprietary protocols.

| Protocol     | Description                                                                                                                        |
| :----------- | :--------------------------------------------------------------------------------------------------------------------------------- |
| **SMB**      | **(Server Message Block)**. The core protocol for file and printer sharing in Windows environments.                                |
| **NetBIOS**  | A legacy naming and session service, often used for name resolution on a LAN when DNS fails.                                       |
| **LDAP**     | **(Lightweight Directory Access Protocol)**. An open protocol for querying and modifying directory services like Active Directory. |
| **LLMNR**    | **(Link-Local Multicast Name Resolution)**. A multicast-based name resolution protocol used as a fallback when DNS is unavailable. |
| **Kerberos** | The primary authentication protocol used in Active Directory environments.                                                         |
| **WinRM**    | **(Windows Remote Management)**. The modern, standard protocol for remote management and PowerShell Remoting.                      |
| **RDP**      | **(Remote Desktop Protocol)**. The standard protocol for graphical remote access.                                                  |
| **SSH**      | **(Secure Shell)**. Now natively supported in Windows for secure, command-line remote access.                                      |

---

## 2. Querying Local Network Settings

### Legacy CMD Tools (also work in PowerShell)
These are quick and universally available tools for basic network enumeration.

| Command | Description |
| :--- | :--- |
| **`ipconfig`** | Displays basic TCP/IP configuration for all network adapters (IP address, subnet mask, default gateway). |
| **`ipconfig /all`** | Provides a much more detailed output, including MAC addresses, DHCP status, and DNS server addresses. |
| **`arp -a`** | Displays the system's ARP cache, revealing other hosts on the local network that the machine has recently communicated with. |
| **`nslookup`** | A utility to query DNS servers to resolve hostnames to IP addresses and vice versa. |
| **`netstat -an`** | Displays all active network connections and listening ports in numerical format. |

### Modern PowerShell Net-Cmdlets
PowerShell provides a suite of `Net` cmdlets that return structured objects, making them ideal for filtering and scripting.

| Cmdlet | Description |
| :--- | :--- |
| **`Get-NetIPInterface`** | Retrieves properties for all network adapters. |
| **`Get-NetIPAddress`** | Retrieves detailed IP address configuration, similar to `ipconfig /all`. |
| **`Get-NetNeighbor`** | Retrieves the neighbor cache (equivalent to the ARP cache). |
| **`Get-NetRoute`** | Displays the IP routing table. |
| **`Test-NetConnection`**| A powerful diagnostic tool that can perform a ping test, a TCP port test, and a traceroute. |

---

## 3. Configuring Network Settings with PowerShell

PowerShell cmdlets are the standard way to programmatically configure network interfaces.

| Cmdlet | Purpose | Example |
| :--- | :--- | :--- |
| **`Set-NetIPInterface`**| Modifies general interface properties. | `Set-NetIPInterface -InterfaceIndex 25 -Dhcp Disabled` |
| **`Set-NetIPAddress`**| Modifies the IP address configuration. | `Set-NetIPAddress -InterfaceIndex 25 -IPAddress 10.10.100.54 -PrefixLength 24` |
| **`Enable-NetAdapter`** | Enables a network adapter. | `Enable-NetAdapter -Name 'Ethernet 3'` |
| **`Disable-NetAdapter`**| Disables a network adapter. | `Disable-NetAdapter -Name 'Ethernet 3'` |
| **`Restart-NetAdapter`**| Restarts a network adapter. | `Restart-NetAdapter -Name 'Ethernet 3'` |

---

## 4. Enabling and Using Remote Access

### SSH (Secure Shell)
Modern Windows includes a native OpenSSH client and server.

1.  **Install the SSH Server (if not present):**
    ```powershell
    Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
    ```
2.  **Start and Enable the Service:**
    ```powershell
    Start-Service sshd
    Set-Service -Name sshd -StartupType 'Automatic'
    ```
3.  **Connect from a Client:**
    ```powershell
    ssh username@remote_ip
    ```
    *(By default, this will drop you into a `cmd.exe` shell. You can type `powershell` to switch).*

### WinRM (Windows Remote Management) / PowerShell Remoting
WinRM is the standard for modern Windows remote administration and is enabled by default on Windows Server.

1.  **Enable and Configure WinRM on a Client OS:**
    ```powershell
    winrm quickconfig
    ```
    This command starts the WinRM service, sets it to start automatically, and creates a firewall exception.

2.  **Test the Connection:**
    ```powershell
    # Unauthenticated test to see if the service is listening
    Test-WSMan -ComputerName <remote_ip>
    ```

3.  **Establish an Interactive Remote Session:**
    The `Enter-PSSession` cmdlet is used to start an interactive PowerShell session on a remote machine.
    ```powershell
    Enter-PSSession -ComputerName <remote_ip> -Credential <username>
    ```

4.  **Run a Single Command Remotely:**
    The `Invoke-Command` cmdlet is used to run a command or script block on one or more remote computers.
    ```powershell
    Invoke-Command -ComputerName <host1>,<host2> -ScriptBlock { Get-Service -Name 'WinDefend' }
    ```

