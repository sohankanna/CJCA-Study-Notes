# Working with Files and Directories 
## The Linux Approach to File Management

While graphical file managers (like Windows Explorer) are available, the command-line shell provides a faster, more powerful, and scriptable way to manage files and directories. This is the preferred method for most system administrators and security professionals.

---

## 1. Creating Files and Directories

### Creating an Empty File (`touch`)
The `touch` command is primarily used to create a new, empty file. (It can also be used to update the timestamp of an existing file).

*   **Syntax:** `touch <filename>`
*   **Example:**
    ```shell
    hacker@htb[~]$ touch info.txt
    ```

### Creating a Directory (`mkdir`)
The `mkdir` command is used to create a new directory.

*   **Syntax:** `mkdir <directory_name>`
*   **Example:**
    ```shell
    hacker@htb[~]$ mkdir Storage
    ```

*   **Creating Parent Directories (`-p` flag):**
    To create a nested directory structure in a single command, use the `-p` (parents) flag. This will create any necessary parent directories that don't already exist.
    ```shell
    hacker@htb[~]$ mkdir -p Storage/local/user/documents
    ```

---

## 2. Viewing Directory Structures (`tree`)

The `tree` command is a useful utility for visualizing the contents of a directory and its subdirectories in a tree-like format.

*   **Syntax:** `tree [path]`
*   **Example (to view the current directory):**
    ```shell
    hacker@htb[~]$ tree .
    .
    ├── info.txt
    └── Storage
        └── local
            └── user
                └── documents

    4 directories, 1 file
    ```

---

## 3. Moving and Renaming (`mv`)

The `mv` (move) command is used for two distinct purposes: moving files/directories to a new location, and renaming them.

### Renaming a File or Directory
To rename something, you "move" it from its old name to a new name within the same directory.

*   **Syntax:** `mv <old_name> <new_name>`
*   **Example:**
    ```shell
    hacker@htb[~]$ mv info.txt information.txt
    ```

### Moving Files or Directories
To move one or more items into a different directory.

*   **Syntax:** `mv <item_to_move> <destination_directory>`
*   **Example (moving a single file):**
    ```shell
    hacker@htb[~]$ mv information.txt Storage/
    ```
*   **Example (moving multiple files):**
    ```shell
    hacker@htb[~]$ mv information.txt readme.txt Storage/
    ```

---

## 4. Copying Files and Directories (`cp`)

The `cp` (copy) command is used to create a duplicate of a file or directory.

### Copying a File
*   **Syntax:** `cp <source_file> <destination>`
*   **Example:**
    ```shell
    hacker@htb[~]$ cp Storage/readme.txt Storage/local/
    ```

### Copying a Directory
To copy an entire directory and its contents, you must use the `-r` (recursive) flag.

*   **Syntax:** `cp -r <source_directory> <destination>`
*   **Example:**
    ```shell
    hacker@htb[~]$ cp -r Storage/local/ NewBackup/
    ```
