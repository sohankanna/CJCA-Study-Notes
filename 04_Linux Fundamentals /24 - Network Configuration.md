# Network Configuration

 1. Configuring Network Interfaces

Linux provides two primary command-line tools for managing network interfaces.

| Tool | Description |
| :--- | :--- |
| **`ifconfig`** | The **legacy** tool for viewing and configuring network interfaces. While deprecated, it is still found on many systems and is useful for quick checks. |
| **`ip`** | The **modern** and more powerful replacement for `ifconfig`. It is the current standard for network configuration in Linux. |

### Viewing Interface Information
```shell
# Using the legacy tool
ifconfig

# Using the modern tool
ip addr show
# Or the shorter version:
ip a
```

### Common Configuration Tasks

| Task                     | ifconfig (Legacy)                                    | ip (Modern)                               |
| ------------------------ | ---------------------------------------------------- | ----------------------------------------- |
| **Activate Interface**   | sudo ifconfig eth0 up                                | sudo ip link set eth0 up                  |
| **Deactivate Interface** | sudo ifconfig eth0 down                              | sudo ip link set eth0 down                |
| **Assign IP & Netmask**  | sudo ifconfig eth0 192.168.1.2 netmask 255.255.255.0 | sudo ip addr add 192.168.1.2/24 dev eth0  |
| **Set Default Gateway**  | sudo route add default gw 192.168.1.1 eth0           | sudo ip route add default via 192.168.1.1 |

### Configuring DNS

The DNS servers a system uses are typically defined in the /etc/resolv.conf file.

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```


**Important:** On modern systems using services like NetworkManager or systemd-resolved, this file is often **auto-generated**. Manual edits will be overwritten. Permanent changes should be made through the appropriate network management tool or configuration file for your distribution.

### Making Configuration Persistent

To make network settings survive a reboot, they must be written to a configuration file.

- **Location (Debian/Ubuntu):** /etc/network/interfaces
    
- **Example Static Configuration:**

```ini
auto eth0
iface eth0 inet static
  address 192.168.1.2
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 8.8.8.8 8.8.4.4
```

**Applying Changes:** After editing the file, restart the networking service.

```shell
sudo systemctl restart networking
```

## 2. Network Access Control (NAC)

**NAC** refers to the security models and technologies used to restrict network access to authorized users and compliant devices.

### Access Control Models

|   |   |   |
|---|---|---|
|Model|Acronym|Description|
|**Discretionary Access Control**|**DAC**|The **owner** of a resource (e.g., a file) has the discretion to set permissions for other users. This is the standard Linux permission model (chmod, chown).|
|**Mandatory Access Control**|**MAC**|Access rules are **enforced by the operating system** based on a system-wide security policy. Users cannot override these policies, even for files they own. This is a much stricter model.|
|**Role-Based Access Control**|**RBAC**|Permissions are assigned to **roles** (e.g., "Database Admin," "HR Manager"), and users are then assigned to those roles. This simplifies permission management in large organizations.|

### NAC Technologies in Linux

- **SELinux (Security-Enhanced Linux):** A powerful and highly granular **MAC** system integrated into the Linux kernel. It is extremely secure but can be complex to manage.
    
- **AppArmor:** Another **MAC** system that uses application "profiles" to restrict what a program can do. It is generally considered easier to configure than SELinux.
    
- **TCP Wrappers:** A simple, host-based NAC tool that restricts access to network services based on the client's IP address. It uses two files: /etc/hosts.allow and /etc/hosts.deny.
    

---

## 3. Network Troubleshooting Tools

These are essential command-line tools for diagnosing network problems.

|   |   |
|---|---|
|Tool|Purpose|
|**ping**|Tests basic Layer 3 (IP) connectivity to a remote host by sending ICMP echo requests. The first tool to use to check if a host is reachable.|
|**traceroute**|Traces the network path (the sequence of routers or "hops") that packets take to reach a remote host.|
|**netstat / ss**|ss (Socket Statistics) is the modern replacement for netstat. It displays active network connections, listening ports, and socket information.|
|**tcpdump / wireshark**|Powerful packet sniffing tools used to capture and analyze network traffic in real-time for deep analysis.|
|**nmap**|A versatile network scanner used for host discovery, port scanning, and service enumeration.|


