# Operating System Structure

## The Windows Root Directory

Unlike Linux, which has a single root (`/`), Windows uses a drive-letter system. The primary drive where the OS is installed is almost always the **`C:\`** drive. This is the **root directory** or **boot partition**.

### Essential System Directories
The `C:\` drive contains several critical folders that are standard across modern Windows versions.

| Directory | Purpose | Security Relevance |
| :--- | :--- | :--- |
| **`\Program Files`** | The default installation location for **64-bit** applications. | Contains application binaries and configuration files. Misconfigured permissions here could allow for tampering with application files. |
| **`\Program Files (x86)`**| On a 64-bit system, this is the default location for older **32-bit** applications. | Same as `Program Files`. |
| **`\ProgramData`** | A **hidden** directory containing application data and settings that are shared among **all users** on the system. | A great place to look for application configuration files, license keys, or other sensitive data that isn't user-specific. |
| **`\Users`** | Contains the profile folder for each user who has logged into the machine. | The central location for all user-specific data. |
| **`\Windows`** | The core of the operating system. Contains system files, drivers, and critical libraries. | Contains many high-value targets. |
| **`\PerfLogs`** | Intended to store Windows performance logs, but is often empty by default. | |

### Key Subdirectories

*   **`\Users\<username>\AppData`**:
    *   This is a **hidden** directory inside each user's profile that stores their personal application settings, cache, and configuration files.
    *   It's a goldmine for penetration testers, as it can contain saved browser sessions, application credentials, and other sensitive user data.
    *   It contains three subfolders: `Local`, `LocalLow`, and `Roaming`.

*   **`\Windows\System32`**:
    *   One of the most critical directories. It contains the core system executables (`.exe`) and Dynamic Link Libraries (`.dll`) required for the 64-bit version of Windows to function.

*   **`\Windows\SysWOW64`**:
    *   On a 64-bit system, this folder contains the 32-bit versions of system executables and DLLs, used for compatibility with older 32-bit applications.

*   **`\Windows\WinSxS`**:
    *   The "Windows Component Store." It holds multiple versions of system files and DLLs to ensure application compatibility and to facilitate system updates and repairs.

---

## Exploring Directories from the Command Line

While the graphical File Explorer is common, the command line is a faster and more powerful way to navigate the filesystem, especially during a security assessment.

### `dir` - Listing Directory Contents
The `dir` command is the Windows equivalent of the Linux `ls` command.

*   **Basic Usage:**
    ```powershell
    # List the contents of the current directory
    dir
    ```
*   **List Contents of a Specific Directory:**
    ```powershell
    dir C:\Users
    ```
*   **View Hidden Files (`/a` flag):**
    The `/a` flag displays files with specified attributes. To see hidden files, you would typically use `/a:h` or just `/a` to see all attributes.
    ```powershell
    dir C:\ /a
    ```

### `tree` - Visualizing Directory Structure
The `tree` command graphically displays the folder structure of a path in a tree-like format.

*   **Basic Usage:**
    ```powershell
    tree "C:\Program Files"
    ```
*   **Include Files in the Listing (`/f` flag):**
    By default, `tree` only shows directories. The `/f` flag tells it to also list the files within each directory.
    ```powershell
    tree C:\Users /f
    ```
*   **Paging Long Output:** The output of `tree` can be very long. You can pipe (`|`) its output to the `more` command to view it one screen at a time.
    ```powershell
    tree C:\ /f | more
    ```
