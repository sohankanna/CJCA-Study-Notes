# The Windows File System


## 1. Windows File System Types

| File System | Full Name | Key Characteristics & Use Cases |
| :--- | :--- | :--- |
| **FAT32** | File Allocation Table 32-bit | An older, widely compatible file system. <br> **Pros:** Excellent cross-platform compatibility (Windows, macOS, Linux, cameras, consoles). <br> **Cons:** **4GB maximum file size limit**, no built-in security features like file permissions. <br> **Use Case:** USB flash drives, SD cards. |
| **exFAT** | Extensible File Allocation Table | A modern replacement for FAT32. <br> **Pros:** Excellent cross-platform compatibility, **no realistic file size limit**. <br> **Cons:** No advanced features like journaling or granular permissions. <br> **Use Case:** Large external hard drives and USB drives that need to be used on both Windows and macOS. |
| **NTFS** | **New Technology File System** | The **default, modern file system for all Windows operating systems**. <br> **Pros:** Highly reliable due to **journaling** (logging changes to prevent corruption), supports very large files and partitions, and has a robust, granular **permission system**. <br> **Cons:** Limited native support on non-Windows systems (macOS can read but not write to NTFS without third-party tools). <br> **Use Case:** Internal hard drives for Windows installations. |

---

## 2. NTFS Permissions

NTFS provides a powerful and granular permission system that controls access to files and folders. These permissions can be inherited from a parent folder or set explicitly on an object.

### Basic NTFS Permissions

| Permission | Description |
| :--- | :--- |
| **Full Control**| Allows a user to do anything: read, write, modify, delete, change permissions, and take ownership. |
| **Modify** | Allows reading, writing, and deleting files and folders. |
| **Read & Execute**| Allows viewing file/folder contents and running executable files. |
| **List Folder Contents**| Allows viewing the names of files and subfolders within a directory (applies to folders only). |
| **Read** | Allows viewing the contents of a file and listing the contents of a folder. |
| **Write** | Allows creating new files/folders and writing data to files. |

**Key Concept: Inheritance**
By default, a file or folder **inherits** its permissions from its parent folder. This simplifies administration, but an administrator can disable inheritance to set explicit, custom permissions on a specific object.

---

## 3. Managing NTFS Permissions (`icacls`)

While you can manage permissions through the graphical interface (File Explorer -> Properties -> Security), the `icacls` (Integrity Control Access Control List) command-line utility provides a powerful and scriptable way to manage them.

### Viewing Permissions
*   **Syntax:** `icacls <file_or_directory>`
*   **Example:**
    ```powershell
    C:\htb> icacls C:\Windows
    ```

### Understanding `icacls` Output
The output for each user or group is shown in the format: `Principal:(Inheritance)(Permissions)`

*   **Example Line:** `BUILTIN\Users:(OI)(CI)(RX)`

*   **Principal:** The user or group (e.g., `BUILTIN\Users`).
*   **Inheritance Flags:**
    *   `(OI)`: **O**bject **I**nherit - This permission will be inherited by files.
    *   `(CI)`: **C**ontainer **I**nherit - This permission will be inherited by subfolders.
    *   `(IO)`: **I**nherit **O**nly - The permission does not apply to the current object, only to its children.
    *   `(I)`: **I**nherited - Indicates this specific permission was inherited from a parent container.
*   **Permission Codes:**
    *   `(F)`: Full access
    *   `(M)`: Modify access
    *   `(RX)`: Read and execute access
    *   `(R)`: Read-only access
    *   `(W)`: Write-only access

### Modifying Permissions
You can use `icacls` to grant or remove permissions. This typically requires administrative privileges.

*   **Granting Permissions:**
    ```powershell
    # Grant the user 'joe' Full Control over the C:\Users folder
    icacls c:\users /grant joe:F
    ```
    *(Note: Without inheritance flags, this only applies to the folder itself, not its contents).*

*   **Removing Permissions:**
    ```powershell
    # Remove all permissions for the user 'joe' from the C:\Users folder
    icacls c:\users /remove joe
    ```
