# Getting Help


## 1. The `help` Command

The `help` command is the primary tool for discovering and learning about the commands that are built into the CMD shell.

### General Help
Running `help` with no arguments provides a list of all available built-in system commands and a brief, one-line description of each. This is the best place to start when you're unsure what commands are available.

*   **Command:**
    ```powershell
    C:\htb> help
    ```
*   **Output:**
    ```
    For more information on a specific command, type HELP command-name
    ASSOC          Displays or modifies file extension associations.
    ATTRIB         Displays or changes file attributes.
    ...
    ```

### Specific Help
To get detailed information about a particular command, including its syntax and available options, use `help` followed by the command name.

*   **Syntax:** `help <command_name>`
*   **Example:**
    ```powershell
    C:\htb> help time
    Displays or sets the system time.

    TIME [/T | time]

    Type TIME with no parameters to display the current time...
    ```

---

## 2. The `/?` Switch

Many commands, especially standalone executable programs that are not built directly into the shell (like `ipconfig.exe`), do not have a page in the `help` utility. For these commands, you can almost always get help by using the `/?` switch.

*   **Syntax:** `<command_name> /?`
*   **Example:** `help ipconfig` will fail, but `ipconfig /?` will succeed.
    ```powershell
    C:\htb> ipconfig /?
    USAGE:
        ipconfig [/? | /all | /release | ...]
    ...
    ```

**Key Takeaway:** If `help <command>` doesn't work, your next step should always be to try `<command> /?`.

---

## 3. Command History (`doskey`)

The Command Prompt keeps a history of the commands you've run within the current session. This is extremely useful for re-running commands without retyping them.

**Important:** Unlike modern shells like PowerShell or Bash, CMD's history is **not persistent**. When you close the Command Prompt window, the history for that session is lost.

### Interacting with History

| Method | Description |
| :--- | :--- |
| **Up/Down Arrow Keys** | The primary way to scroll through your command history one command at a time. |
| **`F7` Key** | Opens a pop-up, interactive list of your command history. You can use the arrow keys to select a command and press Enter to run it. |
| **`doskey /history`** | The command-line way to print the entire command history for the current session to the screen. |
| **Saving History:** | To save your history before closing a session, you can redirect the output of `doskey` to a file: `doskey /history > my_commands.txt` |

---

## 4. Other Essential Tips & Tricks

| Action | Command / Shortcut | Description |
| :--- | :--- | :--- |
| **Clear the Screen** | `cls` | Clears all the text from the terminal window, giving you a clean prompt. |
| **Stop a Running Process**| `Ctrl + C` | Interrupts and terminates the currently running command or process in the foreground. |

---

## 5. External Resources

When you do have internet access, these resources are excellent for deep-diving into Windows commands.
*   **Microsoft Command Reference:** The official, comprehensive A-Z documentation for all Windows commands.
*   **SS64.com:** An outstanding quick-reference site for command-line syntax for CMD, PowerShell, Bash, and more.
