# Linux Security
1. Core System Hardening Principles

These are the foundational, non-negotiable steps for securing any Linux system.

### 1. Keep the System Updated
This is the single most important security measure. Regularly updating the operating system and all installed packages ensures that known vulnerabilities are patched.
```shell
sudo apt update && sudo apt dist-upgrade -y
```

### 2. Manage Services Securely

- **Principle of Least Functionality:** Remove or disable any services and software that are not absolutely necessary. The fewer running services, the smaller the attack surface.
    
- **Disable Insecure Protocols:** Remove services that use unencrypted authentication (e.g., Telnet, FTP). Always prefer secure alternatives (SSH, SFTP).
    

### 3. Implement a Host-Based Firewall

Even if there is a network firewall, a host-based firewall provides an additional layer of defense. Tools like **UFW (Uncomplicated Firewall)** or **iptables** can be used to restrict incoming and outgoing traffic to only what is required.

### 4. Secure SSH Configuration

SSH is a primary target for attackers. Harden its configuration in /etc/ssh/sshd_config.

- **Disable Root Login:** Set PermitRootLogin no.
    
- **Disable Password Authentication:** Set PasswordAuthentication no and enforce the use of more secure **SSH keys**.
    
- **Use Fail2Ban:** This tool monitors logs for failed login attempts and automatically blocks the offending IP addresses, protecting against brute-force attacks.
    

### 5. Enforce Strong Access Control

- **Principle of Least Privilege:** Users should only have the minimum permissions necessary to perform their jobs. Avoid giving out full sudo rights indiscriminately.
    
- **Use Individual Accounts:** Every user should have their own account. Do not use shared accounts.
    
- **Enforce Strong Password Policies:** Use tools like pam_cracklib to enforce password complexity, history, and aging.
    
- **Lock Accounts After Failed Logins:** Configure the system to temporarily lock a user account after a set number of failed login attempts.
    

---

## 2. System Auditing and Monitoring

Regularly auditing a system is crucial for finding misconfigurations and potential signs of compromise.

- **Audit for Risky Permissions:**
    
    - **SUID/SGID Binaries:** Find and review all files with SUID/SGID bits set (find / -type f -perm /6000 2>/dev/null). Unnecessary SUID binaries should have this permission removed.
        
    - **World-Writable Files:** Find and fix files and directories that can be written to by any user (find / -type f -perm -0002 2>/dev/null).
        
- **Check for Misconfigured cron jobs:** Review system and user crontabs for unusual or unauthorized scheduled tasks.
    
- **Enable Logging:** Ensure services like syslog or rsyslog are running to capture important system events.
    
- **Use Host-Based Intrusion Detection (HIDS):** Tools like chkrootkit and rkhunter can scan the system for signs of rootkits and malware.
    
- **Use Hardening Scanners:** Tools like Lynis can perform an in-depth security audit of the system and provide actionable hardening recommendations.
    

---

## 3. Mandatory Access Control (MAC)

MAC systems provide a deeper, more granular layer of security by enforcing a system-wide security policy that users cannot override.

- **SELinux (Security-Enhanced Linux):** A powerful MAC system integrated into the kernel. It assigns a security label (context) to every process and file and enforces rules about how they can interact. It is extremely secure but complex to manage.
    
- **AppArmor:** Another MAC system that uses application "profiles" to confine programs to a specific set of permissions. It is generally considered easier to configure than SELinux.
    

---

## 4. TCP Wrappers

**TCP Wrappers** are a simple, host-based access control mechanism that can restrict access to network services based on the client's IP address or hostname.

- **How it Works:** It uses two configuration files, which are checked in order:
    
    1. /etc/hosts.allow: If a connection matches a rule in this file, it is **allowed**, and the check stops.
        
    2. /etc/hosts.deny: If the connection did not match a rule in hosts.allow, this file is checked. If it matches a rule here, it is **denied**.
        
- **Example Rule (/etc/hosts.deny):**
```
# Deny all services to all hosts by default (a secure starting point)
ALL : ALL
```

**Example Rule (/etc/hosts.allow):**

```
# Allow SSH connections only from the local 10.129.14.0/24 network
sshd : 10.129.14.0/24
```

- **Limitation:** TCP Wrappers are an older technology and only work for applications that have been compiled with libwrap support. They are a good additional layer but are not a replacement for a proper firewall.

