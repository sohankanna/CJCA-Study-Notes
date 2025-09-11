# Working with Directories and Files - CMD


## 1. Managing Directories

### Viewing and Creating Directories

| Command         | Description                                                                   | Example            |
| :-------------- | :---------------------------------------------------------------------------- | :----------------- |
| `dir`           | Lists the files and subdirectories in the current or specified directory.     | `dir C:\Users`     |
| `tree`          | Graphically displays the folder structure of a path.                          | `tree C:\Users`    |
| `md` or `mkdir` | **M**ake **D**irectory. Creates a new directory. Both commands are identical. | `md new-directory` |

### Deleting Directories
The `rd` (or `rmdir`) command is used to remove directories.

*   **`rd <directory>`**: Removes an **empty** directory. If the directory contains files or subdirectories, the command will fail.
*   **`rd /s <directory>`**: Removes a directory and **all** of its contents, including subdirectories and files. It will prompt for confirmation.
    *   `rd /s /q <directory>`: The `/q` (quiet) switch will suppress the confirmation prompt. **Use with caution.**

### Modifying and Moving Directories

| Command | Description |
| :--- | :--- |
| `move` | Moves a directory and all its contents from a source to a destination. The original is deleted. |
| `xcopy`| A powerful command for copying files and directory trees. Can copy subdirectories, including empty ones (`/E`). **Deprecated, but still available.** |
| `robocopy`| **(Robust File Copy)**. The modern and highly recommended successor to `xcopy`. It is designed for reliable directory mirroring and syncing, and can preserve all file attributes, timestamps, and permissions. |

**Robocopy Example:**
```powershell
# Copy the entire contents of the Desktop to the Documents folder
robocopy C:\Users\htb\Desktop C:\Users\htb\Documents
```

---

## 2. Managing Files

### Viewing File Contents

| Command | Description |
| :--- | :--- |
| `type` | Displays the contents of a text file directly to the console. It's the CMD equivalent of the Linux `cat` command. |
| `more` | A "pager" that displays the contents of a file one screen at a time. Useful for very long files. |

### Creating and Modifying Files

| Command | Description | Example |
| :--- | :--- | :--- |
| `echo` | Used with redirection (`>`) to create a new file with text or append (`>>`) text to an existing file. | `echo This is a new file > demo.txt` <br> `echo More text >> demo.txt` |
| `fsutil`| A powerful utility for filesystem tasks. `fsutil file createNew <name> <size>` can create a new, pre-sized empty file. | `fsutil file createNew bigfile.txt 1024` |
| `ren` or `rename`| **Ren**ames a file. Both commands are identical. | `ren demo.txt superdemo.txt` |
| `copy` | Copies one or more files to another location. | `copy secrets.txt C:\Temp\` |
| `move` | Moves a file from a source to a destination. The original is deleted. | `move secrets.txt C:\Temp\` |

### Deleting Files
The `del` (or `erase`) command is used to delete one or more files.

*   **`del <filename>`**: Deletes a single file.
*   **`del /f <filename>`**: **F**orces the deletion of a read-only file.
*   **`del /a:<attribute>`**: Deletes files based on their attributes (e.g., `del /a:h *` deletes all hidden files in the current directory). Use `dir /a` to see file attributes.

---

## 3. Input/Output (I/O) Redirection and Piping

These special characters give you powerful control over the flow of data in the Command Prompt.

| Operator | Name | Description | Example |
| :--- | :--- | :--- | :--- |
| **`>`** | **Redirect Output** | Sends the output of a command to a file, **overwriting** the file if it exists. | `ipconfig /all > details.txt` |
| **`>>`** | **Append Output** | Sends the output of a command to a file, **appending** it to the end of the file if it exists. | `echo New log entry >> logfile.txt` |
| **`<`** | **Redirect Input** | Takes the contents of a file and uses it as the input for a command. | `find /i "error" < logfile.txt` |
| **`|`** | **Pipe** | Takes the output of the command on the left and uses it as the input for the command on the right. | `ipconfig /all \| find /i "IPV4"` |
| **`&`** | **Command Separator**| Executes command A, then executes command B, regardless of whether A succeeded or failed. | `ping 8.8.8.8 & type test.txt` |
| **`&&`** | **Conditional AND**| Executes command B **only if** command A completes successfully. | `cd C:\Temp && echo Success > file.txt` |
| **`\|\|`** | **Conditional OR** | Executes command B **only if** command A fails. | `dir C:\FakeFolder \|\| echo Folder not found` |
