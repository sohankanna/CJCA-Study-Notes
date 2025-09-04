# Navigation

## 1. Finding Your Location (`pwd`)

The `pwd` command tells you which directory you are currently in.

*   **Command:** `pwd` (Print Working Directory)
*   **Purpose:** To know your current location in the filesystem hierarchy.
*   **Example:**
    ```shell
    cry0l1t3@htb[~]$ pwd
    /home/cry0l1t3
    ```

---

## 2. Listing Directory Contents (`ls`)

The `ls` command is used to list the files and directories inside a specific location.

### Basic Usage
*   **Command:** `ls`
*   **Purpose:** Lists the contents of the current directory.
    ```shell
    cry0l1t3@htb[~]$ ls
    Desktop  Documents  Downloads  Music  Pictures
    ```

### Common `ls` Options (Flags)
Options are added to commands to modify their behavior.

| Option | Command | Description |
| :--- | :--- | :--- |
| `-l` | `ls -l` | **Long listing format.** Provides detailed information for each item. |
| `-a` | `ls -a` | **All files.** Shows hidden files and directories (those that start with a `.`). |
| `-la` | `ls -la`| A common combination of the two flags above. Shows a detailed list of **all** files, including hidden ones. |
| `-h` | `ls -lh`| **Human-readable.** Displays file sizes in an easy-to-read format (e.g., `4.0K`, `3.2M`) instead of just bytes. |

### Understanding the `ls -l` Output
The long listing format (`-l`) provides a wealth of information in columns.

`drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:37 Desktop`

| Column | Example | Description |
| :--- | :--- | :--- |
| **Permissions**| `drwxr-xr-x`| The file type (`d` for directory, `-` for file) and the access permissions for the owner, group, and others. |
| **Links** | `2` | The number of hard links to the file. |
| **Owner** | `cry0l1t3` | The user who owns the file. |
| **Group** | `htbacademy`| The group that owns the file. |
| **Size** | `4096` | The size of the file in bytes. |
| **Timestamp** | `Nov 13 17:37`| The date and time of the last modification. |
| **Name** | `Desktop` | The name of the file or directory. |

---

## 3. Changing Directories (`cd`)

The `cd` command is used to move from one directory to another.

*   **Command:** `cd` (Change Directory)

### Special Directory Shortcuts

| Command | Destination |
| :--- | :--- |
| `cd /path/to/directory` | Navigates to an **absolute path** (starts from the root `/`). |
| `cd directory_name` | Navigates to a **relative path** (a subdirectory within your current location). |
| `cd` (with no arguments)| Navigates back to your **home directory** (`~`). |
| `cd ..` | Navigates **up one level** to the parent directory. |
| `cd .` | Refers to the **current directory**. |
| `cd -` | Navigates to the **previous directory** you were in. |

---

## 4. Useful Shell Shortcuts & Tips

*   **Tab Completion (Tab Key):** This is the **most important shortcut**. Start typing a command or filename and press `Tab`. The shell will automatically complete it for you. If there are multiple possibilities, pressing `Tab` twice will show you all of them.

*   **Clearing the Screen:**
    *   **Command:** `clear`
    *   **Shortcut:** `Ctrl + L`

*   **Command History:**
    *   **Arrow Keys (`↑` / `↓`):** Scroll through your previously executed commands.
    *   **Reverse Search (`Ctrl + R`):** A powerful feature. Press `Ctrl + R` and start typing any part of a previous command to search your history for it.

*   **Command Chaining (`&&`):**
    *   You can run multiple commands on a single line by separating them with `&&`. The second command will only run if the first one succeeds.
    *   **Example:** `cd shm && clear` (changes to the `shm` directory AND THEN clears the screen).

