# System Information
## Logging in with SSH

**Secure Shell (SSH)** is the standard protocol for secure remote command-line access to Linux and Unix-like systems. It provides an encrypted connection to execute commands on a remote machine.

*   **Syntax:**
    ```shell
    ssh <username>@<ip_address>
    ```
*   **Example:**
    ```shell
    ssh htb-student@10.129.10.2
    ```

---

## Core System Information Commands

The following commands are fundamental for understanding the context of the system you are currently operating on.

| Command | Description | Example Usage & Output |
| :--- | :--- | :--- |
| **`whoami`** | **"Who am I?"** <br> Displays the username of the currently logged-in user. This is often the very first command run on a new shell. | `cry0l1t3@htb[/htb]$ whoami`<br>`cry0l1t3` |
| **`id`** | **"Identity"** <br> Provides detailed information about the current user, including their **User ID (uid)**, **Group ID (gid)**, and all the **groups** they are a member of. | `cry0l1t3@htb[/htb]$ id`<br>`uid=1000(cry0l1t3) gid=1000(cry0l1t3) groups=1000(cry0l1t3),27(sudo),...` |
| **`hostname`**| **"Host Name"** <br> Displays the name of the computer (the network node name). | `cry0l1t3@htb[/htb]$ hostname`<br>`nixfund` |
| **`uname`** | **"Unix Name"** <br> Prints basic information about the operating system and hardware. Use `uname -a` for all details. | `cry0l1t3@htb[/htb]$ uname -a`<br>`Linux box 4.15.0-99-generic ... GNU/Linux` |
| **`pwd`** | **"Print Working Directory"**<br> Shows the full path of the directory you are currently in. | `cry0l1t3@htb[/htb]$ pwd`<br>`/home/cry0l1t3` |
| **`ifconfig`**| **"Interface Configuration"** <br> A classic tool used to view and configure network interface parameters, including IP addresses, netmasks, and MAC addresses. | `cry0l1t3@htb[/htb]$ ifconfig` |
| **`ip`** | **"IP"** <br> A more modern and powerful tool that has largely replaced `ifconfig`. It is used to show and manipulate routing, network devices, and interfaces. | `cry0l1t3@htb[/htb]$ ip address show` |
| **`ps`** | **"Process Status"** <br> Displays information about the currently running processes. | `cry0l1t3@htb[/htb]$ ps aux` |
| **`ss`** | **"Socket Statistics"** <br> A modern utility for investigating network sockets. It is faster than and has largely replaced the older `netstat` command. | `cry0l1t3@htb[/htb]$ ss -tulpn` |
| **`who`** | **"Who is logged on"** <br> Shows a list of all users who are currently logged into the system. | `cry0l1t3@htb[/htb]$ who` |
| **`env`** | **"Environment"** <br> Prints a list of all environment variables for the current session. | `cry0l1t3@htb[/htb]$ env` |
| **`lsblk`** | **"List Block Devices"** <br> Lists all available block devices, such as hard drives and partitions. | `cry0l1t3@htb[/htb]$ lsblk` |
| **`lsof`** | **"List Open Files"** <br> Lists all files that are currently open by processes on the system. | `cry0l1t3@htb[/htb]$ lsof` |

---

## Practical Application for Security

Gathering this information is critical for both offensive and defensive security.

### From a Penetration Tester's Perspective:
*   **`whoami` & `id`:** The `id` command is especially important. If a user is a member of a privileged group like `sudo`, `docker`, or `adm`, it can be a direct path to **privilege escalation**. The `adm` group, for example, allows a user to read sensitive log files in `/var/log`.
*   **`uname -a`:** The kernel version (`4.15.0-99-generic`) is one of the most important pieces of information. You can search for this specific version online (e.g., on Exploit-DB) to find known, public **kernel exploits** that could grant you root access.
*   **`ip address show`:** Shows you the machine's IP address(es), which helps you understand the network topology and identify other potential targets on the same subnet.
*   **`ps aux`:** Reveals what services and applications are running on the system, which could be misconfigured or vulnerable.

### From a System Administrator's (Blue Team) Perspective:
*   **`id`:** Used to audit user permissions and ensure the **Principle of Least Privilege** is being followed. Does a user really need to be in the `sudo` group?
*   **`who`:** Used to see who is currently logged into a system, which can help identify unauthorized access.
*   **`ss -tulpn`:** Shows which services are listening for network connections, which is essential for understanding the system's attack surface and for firewall configuration.
