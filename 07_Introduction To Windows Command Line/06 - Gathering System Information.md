# Gathering System Information


## 1. The "Why": The Goal of Enumeration

The purpose of enumeration is to build **situational awareness**. Before taking any action on a system, you must understand its configuration, its role in the network, and the permissions of your current user account. This helps you answer key questions like:
*   What is this machine? (OS version, hostname)
*   Where is it on the network? (IP address, domain)
*   What can I do as this user? (Privileges, group memberships)
*   What other systems can it talk to? (Network resources, ARP cache)

For a penetration tester, thorough enumeration is more important than blindly trying exploits. Misconfigurations discovered during this phase are often the easiest path to privilege escalation.

---

## 2. General System Information

These commands provide a high-level overview of the host machine.

| Command | Description |
| :--- | :--- |
| **`systeminfo`** | A comprehensive, one-stop command that provides a wealth of information, including **hostname, OS version, build number, domain, and installed hotfixes (patches)**. This is an excellent starting point. |
| **`hostname`** | A simple command that displays only the computer's name. |
| **`ver`** | Displays the Windows version number. |

---

## 3. Networking Information

These commands help you understand the host's place on the network.

| Command | Description |
| :--- | :--- |
| **`ipconfig`** | Displays basic TCP/IP configuration for all network adapters, including IP address, subnet mask, and default gateway. |
| **`ipconfig /all`**| Provides a much more detailed output, including MAC addresses, DHCP status, and configured **DNS servers**. |
| **`arp -a`** | Displays the host's **ARP cache**, which is a table of recently resolved IP addresses and their corresponding MAC addresses on the local network. This is an excellent way to discover other active hosts on the same subnet. |
| **`net share`** | Lists all the shared folders on the local machine, including hidden administrative shares like `C$` and `ADMIN$`. |
| **`net view`** | Displays a list of computers and shared resources on the current domain or network. |

---

## 4. User and Group Information

These commands are critical for understanding the privileges and access level of your current user account.

### `whoami`
The `whoami` command is used to display information about the currently logged-on user.

| Command | Output |
| :--- | :--- |
| **`whoami`** | Displays the current user's name in the format `DOMAIN\username` or `HOSTNAME\username`. |
| **`whoami /priv`**| Displays the user's security **privileges**. This is crucial for identifying if a user has powerful rights like `SeBackupPrivilege` or `SeDebugPrivilege` that can be abused for privilege escalation. |
| **`whoami /groups`**| Displays all the groups the current user is a member of. Membership in groups like `Administrators`, `Remote Desktop Users`, or other custom-privileged groups is a key finding. |
| **`whoami /all`** | Combines the output of the above commands, showing the username, SID, groups, and privileges. |

### `net` Command
The `net` command is a versatile utility for managing users, groups, and network resources.

| Command | Description |
| :--- | :--- |
| **`net user`** | Lists all **local** user accounts on the machine. |
| **`net user <username>`** | Displays detailed information about a specific local user account. |
| **`net localgroup`** | Lists all **local** groups on the machine. |
| **`net localgroup <groupname>`**| Displays the members of a specific local group. |
| **`net group`** | (Domain Only) Can be used to query for **domain groups**, but must be run on a Domain Controller. |

---

## 5. A Note on Operational Security (OpSec)

While these commands are built-in ("living off the land"), their usage is often anomalous for a standard user.
*   Running commands like `whoami`, `ipconfig`, and especially `net user` is not typical behavior for an average employee.
*   In a well-monitored environment, this activity can generate alerts for a Security Operations Center (SOC) or Blue Team, indicating a potential compromise. As a penetration tester, it's a trade-off between gathering necessary information and remaining stealthy.

