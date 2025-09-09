# Interacting with the Windows Operating System


## 1. Graphical User Interface (GUI)

The GUI is the point-and-click, visual interface that most Windows users are familiar with. It was designed to make computers accessible and user-friendly without requiring knowledge of specific commands.

*   **Remote Access via GUI:** The **Remote Desktop Protocol (RDP)** is the primary method for accessing a full graphical desktop environment on a remote Windows machine. It operates on **TCP port 3389** and is a key service for remote administration.

---

## 2. Windows Command Line

The command line provides a more powerful, scriptable, and efficient way to control the operating system. Windows has two main command-line shells.

### Command Prompt (`cmd.exe`)
*   **What it is:** The legacy, traditional command-line interpreter for Windows.
*   **Getting Help:**
    *   `help`: Lists many of the built-in commands.
    *   `help <command_name>`: Provides information about a specific command.
    *   `<command_name> /?`: Many commands have their own built-in help menu, accessed with the `/?` switch (e.g., `ipconfig /?`).

### PowerShell (`powershell.exe`)
*   **What it is:** A modern, powerful, object-oriented command shell and scripting language. It is built on the .NET Framework and is the preferred shell for system administration and automation on Windows.
*   **Key Features:**
    *   Can run most standard `cmd.exe` commands.
    *   Provides a much richer scripting environment than CMD's batch files.

#### PowerShell Cmdlets
*   **What they are:** "Cmdlets" (pronounced "command-lets") are the native commands in PowerShell. They are small, single-function tools.
*   **Verb-Noun Naming Convention:** Cmdlets follow a consistent `Verb-Noun` format, which makes them easy to discover and understand.
    *   `Get-Process`: Retrieves a list of running processes.
    *   `Stop-Service`: Stops a running service.
    *   `Get-ChildItem`: Lists the items in a directory (similar to `ls` or `dir`).

#### PowerShell Aliases
*   **What they are:** Nicknames or shortcuts for longer cmdlet names. This makes PowerShell more familiar for users coming from other shells.
*   **Examples:**
    *   `ls` and `dir` are aliases for `Get-ChildItem`.
    *   `cd` is an alias for `Set-Location`.
    *   `cat` is an alias for `Get-Content`.
*   **Viewing Aliases:** Use the `Get-Alias` cmdlet to see all available aliases.

#### PowerShell Help System
*   **Updating Help:** PowerShell's help files are not installed by default. You must first run `Update-Help` (in an administrative shell) to download them.
*   **Getting Help:** Use the `Get-Help` cmdlet.
    ```powershell
    # Get help for a specific cmdlet
    Get-Help Get-Service
    
    # Open the online version of the help page in a browser
    Get-Help Get-Service -Online
    ```

#### Running PowerShell Scripts (`.ps1`)
*   **Execution:** You can run a script from the current directory using `.\ScriptName.ps1`.
*   **Modules:** You can load a script as a module to make its functions available in your current session using `Import-Module .\ScriptName.ps1`.

#### PowerShell Execution Policy
*   **What it is:** A safety feature in PowerShell that controls whether scripts can be run. It is **not** a security boundary, as it can be easily bypassed.
*   **Viewing the Policy:**
    ```powershell
    Get-ExecutionPolicy -List
    ```
*   **Common Policies:**
    *   **`Restricted`:** The default on client machines. No scripts are allowed.
    *   **`RemoteSigned`:** The default on servers. You can run local scripts, but scripts downloaded from the internet must be digitally signed.
    *   **`Bypass`:** Nothing is blocked, and no warnings are given.
*   **Bypassing the Policy:** A user can often bypass the policy for their current session, even without admin rights.
    ```powershell
    # This sets the policy to Bypass only for the current PowerShell window
    Set-ExecutionPolicy Bypass -Scope Process
    ```
