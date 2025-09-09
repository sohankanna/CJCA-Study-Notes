# NTFS vs. Share Permissions

## 1. The Two Layers of Permissions

When a user accesses a folder over the network via the **SMB (Server Message Block)** protocol, their access is determined by the combination of two separate sets of permissions.

### Share Permissions (The "Gatekeeper")
*   **Scope:** Applies **only** when accessing a folder *over the network*. They do not apply to a user who is logged in locally or via RDP.
*   **Simplicity:** They are very basic and offer three levels: **Read**, **Change**, and **Full Control**.
*   **Analogy:** The main security guard at the front gate of a corporate campus. They decide if you are allowed onto the campus at all.

| Share Permission | Description |
| :--- | :--- |
| **Read** | Allows viewing file and folder names, reading file contents, and running programs. |
| **Change** | Includes all "Read" permissions, plus the ability to create, modify, and delete files and folders. |
| **Full Control** | Includes all "Change" permissions, plus the ability to change the *Share Permissions* themselves. |

### NTFS Permissions (The "Room Keys")
*   **Scope:** Applies **at all times**, whether the user is accessing the file locally, via RDP, or over a network share.
*   **Granularity:** They are highly detailed and offer a wide range of permissions (Full Control, Modify, Read & Execute, List, Read, Write, and many more Special Permissions).
*   **Analogy:** The individual key cards that grant access to specific rooms and floors *inside* the corporate campus. Even if the front gate guard lets you in, you still need the right key card to get into the server room.

---

## 2. The Golden Rule: The Most Restrictive Permission Wins

When a user accesses a resource over the network, Windows calculates their "effective permissions" by combining both the Share and NTFS permissions. The rule is simple: **the most restrictive permission is the one that applies.**

*   **Scenario:**
    *   **Share Permission** for the `Everyone` group is set to **Read**.
    *   **NTFS Permission** for the `Everyone` group is set to **Full Control**.
*   **Result:** When a user accesses the folder over the network, they will only have **Read** permissions. Even though NTFS would allow them to do more, the more restrictive Share permission takes precedence.

**Best Practice:**
Because NTFS permissions are far more granular and apply in all situations, the modern best practice is to set Share Permissions to be very permissive (e.g., `Everyone` or `Authenticated Users` with **Full Control**) and then use the detailed **NTFS permissions** to enforce the actual, fine-grained security policies.

---

## 3. Creating and Accessing a Network Share

### Creating a Share (Windows GUI)
1.  Right-click a folder -> `Properties`.
2.  Go to the **Sharing** tab -> `Advanced Sharing...`.
3.  Check "Share this folder" and click the `Permissions` button to configure **Share Permissions**.
4.  Go to the **Security** tab to configure **NTFS Permissions**.

### Accessing a Share from Linux (`smbclient`)
`smbclient` is a powerful command-line tool for interacting with SMB shares from a Linux host.

*   **List Available Shares on a Host:**
    ```shell
    smbclient -L <SERVER_IP> -U <username>
    ```
*   **Connect to a Specific Share:**
    ```shell
    # The share name is case-sensitive and spaces must be quoted.
    smbclient '\\<SERVER_IP>\Company Data' -U <username>
    ```

### Mounting a Share from Linux (`mount.cifs`)
You can mount a remote SMB share to a local directory on your Linux machine, making it appear like a local folder.

*   **Install necessary tools (if needed):**
    ```shell
    sudo apt-get install cifs-utils
    ```
*   **Mount the share:**
    ```shell
    # Create a local mount point first
    mkdir ~/windows_share
    
    sudo mount -t cifs -o username=<user>,password=<pass> //<SERVER_IP>/"Company Data" ~/windows_share
    ```

---

## 4. Monitoring Shares on Windows

*   **`net share` command:** A command-line tool to quickly list all active shares on a Windows machine.
    *   **Note:** Default administrative shares like `C$`, `ADMIN$`, and `IPC$` are hidden from normal view but are always present.
*   **Computer Management (`compmgmt.msc`):** A graphical tool that allows you to see shared folders, active user sessions, and which files are currently open over the network.
*   **Event Viewer (`eventvwr.msc`):** The central logging utility for Windows. Security logs here will record events related to share access, including successful and failed authentication attempts.
