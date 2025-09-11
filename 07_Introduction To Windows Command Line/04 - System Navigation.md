# System Navigation


## 1. Listing Directory Contents (`dir`)

The `dir` command is used to list the files and subdirectories within a directory.

*   **Syntax:** `dir [path]`
*   **Purpose:** To see what's inside your current location or a specified folder.
*   **Example (listing the current directory):**
    ```powershell
    C:\Users\htb\Desktop> dir
    
     Directory of C:\Users\htb\Desktop
    
    06/11/2021  11:59 PM    <DIR>          .
    06/11/2021  11:59 PM    <DIR>          ..
    06/11/2021  11:57 PM                 0 file1.txt
    ...
    ```

---

## 2. Navigating the Filesystem (`cd` / `chdir`)

The `cd` (or `chdir`) command is used to change your current working directory. Before you can move, it's essential to know where you are.

### Finding Your Current Location
Running `cd` with no arguments will print your current directory path to the screen.
```powershell
C:\htb> cd
C:\htb
```

### Absolute vs. Relative Paths
*   **Absolute Path:** A path that starts from the **root directory** (e.g., `C:\`). It is a complete, unambiguous location.
    ```powershell
    C:\htb> cd C:\Users\htb\Pictures
    ```
*   **Relative Path:** A path that starts from your **current working directory**. It is relative to your current location.
    ```powershell
    C:\Users\htb> cd Pictures
    ```

### Special Directory Shortcuts

| Command | Destination |
| :--- | :--- |
| `cd .` | The current directory (often used in paths like `.\script.ps1`). |
| `cd ..` | The **parent directory** (moves you up one level). |
| `cd \` | The **root directory** of the current drive (e.g., `C:\`). |

You can chain `..` to move up multiple levels quickly.
```powershell
# Move up three directories from the current location
C:\Users\htb\Pictures> cd ..\..\..
C:\>
```

---

## 3. Visualizing Directory Structures (`tree`)

The `tree` command provides a graphical, tree-like representation of a directory's structure, which is excellent for quickly understanding a complex folder hierarchy.

*   **Syntax:** `tree [path] [options]`
*   **Key Option:**
    *   `/f`: Includes the **files** within each directory in the output. By default, `tree` only shows directories.
*   **Example (listing directories and files):**
    ```powershell
    C:\htb\student> tree /F
    C:.
    ├───Desktop
    │       passwords.txt
    │       secrets.txt
    │
    └───Documents
    ```

---

## 4. Interesting Directories for a Penetration Tester

When performing reconnaissance on a Windows host, certain directories are often prime targets because they are world-writable or contain sensitive user data.

| Environment Variable | Default Location | Description & Security Relevance |
| :--- | :--- | :--- |
| **`%SYSTEMROOT%\Temp`**| `C:\Windows\Temp`| A **global** temporary directory. It is often world-writable, meaning any user can write files here. This makes it a common location for attackers to drop malicious payloads. |
| **`%TEMP%`** | `C:\Users\<user>\AppData\Local\Temp`| A **user-specific** temporary directory. Useful for dropping files when you have compromised a specific user account. |
| **`%PUBLIC%`** | `C:\Users\Public` | A directory accessible to all interactive users on the system. Another good spot for dropping files, as it's often less monitored than `C:\Windows\Temp`. |
| **`%ProgramFiles%`** | `C:\Program Files` | Contains 64-bit applications. Useful for enumerating installed software to find potential vulnerabilities. |
| **`%ProgramFiles(x86)%`**| `C:\Program Files (x86)`| Contains 32-bit applications on a 64-bit system. Also used for software enumeration. |
