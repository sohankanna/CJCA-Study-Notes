# Network Services

1. SSH (Secure Shell)

**SSH** is the standard protocol for secure remote command-line access. It provides an encrypted channel for logging in, executing commands, and transferring files.

*   **Default Port:** TCP/22
*   **Server Software:** The most common implementation is **OpenSSH Server** (`openssh-server`).
*   **Configuration File:** `/etc/ssh/sshd_config`
*   **Key Commands:**
    *   **Install:** `sudo apt install openssh-server -y`
    *   **Check Status:** `systemctl status ssh`
    *   **Connect as a Client:** `ssh <username>@<ip_address>`

**Security Implication:** SSH is a primary target for attackers. It must be properly secured by disabling root login, using strong passwords or, preferably, public key authentication, and potentially changing the default port.

---

## 2. NFS (Network File System)

**NFS** is a distributed file system protocol that allows a user on a client computer to access files over a network in a manner similar to how local storage is accessed.

*   **Default Ports:** TCP/UDP 111 (Portmapper), 2049 (NFS)
*   **Purpose:** To provide centralized, shared file storage for multiple Linux/Unix clients.
*   **Configuration File:** `/etc/exports`. This critical file defines which directories are shared and who can access them.

### Key `exports` Permissions
| Permission | Description | Security Note |
| :--- | :--- | :--- |
| `rw` | **Read/Write:** Allows clients to read and modify files in the share. | |
| `ro` | **Read-Only:** Clients can only read files. | |
| `root_squash`| **Default & Secure.** Any requests from the `root` user on a client machine are "squashed" down to the permissions of a low-privilege anonymous user (`nobody`). | Prevents a remote root user from having root access on the file share. |
| `no_root_squash`| **Highly Insecure.** Disables root squashing. A `root` user on a client machine will have `root` level permissions on the file share. | This is a classic misconfiguration that can lead to immediate privilege escalation if an attacker gains root on a client. |

*   **Client-Side Command:** To access an NFS share, you must "mount" it to a local directory.
    ```shell
    # Create a local mount point
    mkdir ~/target_nfs
    # Mount the remote share to the local directory
    sudo mount <server_ip>:/path/to/share ~/target_nfs
    ```

---

## 3. Web Servers

A **web server** is software that listens for HTTP/S requests from clients (browsers) and serves web content.

### Apache2
*   **Description:** One of the most popular, powerful, and widely used open-source web servers.
*   **Default Web Root:** `/var/www/html` (Files placed here are served by default).
*   **Main Configuration File:** `/etc/apache2/apache2.conf`
*   **Key Commands:**
    *   **Install:** `sudo apt install apache2 -y`
    *   **Check Status:** `systemctl status apache2`

### Python's Simple HTTP Server
*   **Description:** A simple, built-in web server module in Python. It is **not** for production use but is an **extremely useful tool** for penetration testers to quickly serve files (like exploits or tools) to a target machine.
*   **Key Commands:**
    *   **Start server in current directory (on port 8000):**
        ```shell
        python3 -m http.server
        ```
    *   **Start server on a different port:**
        ```shell
        python3 -m http.server 443
        ```
    *   **Serve files from a different directory:**
        ```shell
        python3 -m http.server --directory /path/to/files
        ```

---

## 4. VPN (Virtual Private Network)

A **VPN** creates a secure, encrypted "tunnel" over a public network, allowing a remote client to connect to a private network as if they were physically there.

*   **Purpose:** Secure remote access, anonymization, and site-to-site connectivity.

### OpenVPN
*   **Description:** A very popular, open-source, and highly configurable VPN solution. It is the VPN technology used by Hack The Box.
*   **Server Configuration:** `/etc/openvpn/server.conf`
*   **Client Configuration:** Clients connect using a `.ovpn` configuration file.
*   **Key Commands:**
    *   **Install:** `sudo apt install openvpn -y`
    *   **Connect as a client:** `sudo openvpn /path/to/config.ovpn`
