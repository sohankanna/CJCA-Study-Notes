# Find Files and Directories

## 1. `which` - Finding Command Locations

The `which` command is a simple utility that tells you the full path of an executable command. It searches the directories listed in your system's `$PATH` environment variable.

*   **Purpose:** To determine if a specific command/program is installed and where its binary is located.
*   **Syntax:**
    ```shell
    which <command_name>
    ```
*   **Example:**
    ```shell
    hacker@htb[~]$ which python
    /usr/bin/python
    ```
    If the command is not found, `which` will produce no output.

---

## 2. `find` - The Powerful, Granular Search Tool

The `find` command is an extremely powerful and versatile tool for searching for files and directories based on a wide variety of criteria. It recursively searches through a directory tree.

*   **Syntax:**
    ```shell
    find <starting_directory> <expression>
    ```
*   **Key Idea:** `find` is slower than `locate` because it performs a real-time search of the filesystem, but it offers incredibly detailed filtering options.

### Common `find` Options (Expressions)

| Option | Description | Example |
| :--- | :--- | :--- |
| `-type` | Specifies the type of item to find. `f` for file, `d` for directory. | `find / -type f` (find all files) |
| `-name` | Searches for files by name. It is case-sensitive. Use wildcards (`*`) to match patterns. | `find . -name "*.conf"` (find all files in the current directory ending with `.conf`) |
| `-iname` | Same as `-name`, but the search is **case-insensitive**. | `find . -iname "notes.txt"` |
| `-user` | Finds files owned by a specific user. | `find /home -user hacker` |
| `-group`| Finds files owned by a specific group. | `find /var/www -group www-data` |
| `-size` | Finds files based on size. Use `+` for "greater than" and `-` for "less than". Units: `c` (bytes), `k` (KiB), `M` (MiB), `G` (GiB). | `find / -size +100M` (find files larger than 100 MiB) |
| `-perm` | Finds files with specific permissions. | `find / -type f -perm /4000` (find SUID files) |
| `-mtime`| Finds files based on last modification time (in days). | `find . -mtime -7` (find files modified in the last 7 days) |
| `-exec` | **Executes a command** on each file that is found. `{}` is a placeholder for the found file's name, and `\;` terminates the command. | `find . -name "*.log" -exec rm {} \;` (find and delete all `.log` files) |

### Suppressing Errors
When searching the entire filesystem, you will often encounter "Permission denied" errors. You can hide these errors by redirecting the Standard Error stream (`2`) to `/dev/null`.

*   **Example:**
    ```shell
    find / -name "secret.txt" 2>/dev/null
    ```

---

## 3. `locate` - The Fast Database Search Tool

The `locate` command searches for files using a pre-built database of the filesystem's contents.

*   **Key Idea:** `locate` is **extremely fast** because it's not searching the live filesystem; it's just looking up names in its database.
*   **The Catch:** The database is not always up-to-date. You may need to manually update it to find newly created files.

### Basic Usage
1.  **Update the database (requires `sudo`):**
    ```shell
    sudo updatedb
    ```
2.  **Search for a file:**
    ```shell
    locate <filename_pattern>
    ```
    *Example:* `locate *.conf`

### `find` vs. `locate`: When to Use Which?

| Use Case | Recommended Tool | Why? |
| :--- | :--- | :--- |
| I need to find a file by name and I need the result **instantly**. | `locate` | It searches a database, not the live filesystem. |
| I need to find a file that was **created just now**. | `find` | `locate`'s database may not have been updated yet. |
| I need to search for files based on **complex criteria** like size, permissions, or modification date. | `find` | `locate` can only search by name. |
