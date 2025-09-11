# CMD vs PowerShell


## 1. Key Differences: PowerShell vs. CMD

While both are command-line interfaces, PowerShell is fundamentally more powerful and flexible than CMD.

| Feature | PowerShell | Command Prompt (CMD) |
| :--- | :--- | :--- |
| **Core Engine** | Built on the **.NET Framework**; object-oriented. | Legacy executable; text-based. |
| **Output** | **Objects.** The output of one command is a structured object that can be piped (`|`) to another command for sophisticated filtering and manipulation. | **Text.** The output is plain text, which is difficult to parse and cannot be piped as a structured object. |
| **Commands** | Uses **Cmdlets** (`Verb-Noun` format) and supports aliases. | Uses traditional executable commands. |
| **Scripting** | A powerful, modern scripting language (`.ps1`). | Simple, linear batch scripting (`.bat`). |
| **Execution** | Can run CMD commands, batch files, and its own cmdlets. | Can only run its own commands and batch files. |
| **Cross-Platform** | Yes, modern PowerShell runs on Windows, Linux, and macOS. | No, Windows-only. |

**Why it Matters:** For administrators, PowerShell enables complex automation that is impossible with CMD. For penetration testers, PowerShell provides a rich environment for "living off the land," but its extensive logging capabilities also make it a "noisier" choice than CMD if stealth is a primary concern.

---

## 2. Accessing PowerShell

You can launch PowerShell in several ways:
*   **Windows Search:** Search for "PowerShell".
*   **Windows Terminal:** The modern terminal application that can host multiple shell types, including PowerShell and CMD.
*   **PowerShell ISE:** The Integrated Scripting Environment, a built-in GUI for writing and debugging PowerShell scripts.
*   **From CMD:** Simply type `powershell` in a Command Prompt window to launch a PowerShell session within it.

---

## 3. PowerShell Fundamentals

### The `Get-Help` System
PowerShell has a comprehensive, built-in help system.
*   **Updating Help:** The help files are not included by default. You must run `Update-Help` in an administrative PowerShell session to download them.
*   **Getting Help:** Use the `Get-Help` cmdlet.
    ```powershell
    # Get detailed help for a specific cmdlet
    Get-Help Get-Service
    
    # Open the online Microsoft Docs page for a cmdlet
    Get-Help Get-Service -Online
    
    # See practical examples
    Get-Help Get-Service -Examples
    ```

### Basic Navigation Cmdlets
PowerShell uses `Verb-Noun` cmdlets for navigation, but provides familiar aliases for ease of use.

| Action | PowerShell Cmdlet | Common Aliases |
| :--- | :--- | :--- |
| **Print Working Directory** | `Get-Location` | `pwd`, `gl` |
| **List Directory Contents** | `Get-ChildItem` | `ls`, `dir`, `gci` |
| **Change Directory** | `Set-Location` | `cd`, `sl`, `chdir` |
| **View File Contents** | `Get-Content` | `cat`, `type`, `gc` |

---

## 4. Tips and Tricks for PowerShell

### Finding Commands (`Get-Command`)
The `Get-Command` cmdlet is a powerful tool for discovering commands.
```powershell
# List all available commands
Get-Command

# Find all commands that start with the verb "Get"
Get-Command -Verb Get

# Find all commands that act on the noun "Service" (using a wildcard)
Get-Command -Noun Service*
```

### Command History
PowerShell has a robust history feature.
*   **`Get-History`:** Displays the command history for the current session. An alias is `h`.
*   **`PSReadLine` Module:** By default, PowerShell saves a persistent history of all commands from all sessions to a file, making it easy to recall commands from previous days.
*   **`Ctrl+R`:** Activates a reverse-search of your command history.

### Aliases
Aliases are nicknames for cmdlets.
*   **`Get-Alias`:** Lists all defined aliases.
*   **`Set-Alias`:** Creates a new, custom alias for the current session.
    ```powershell
    Set-Alias -Name gh -Value Get-Help
    ```

### Hotkeys and Tab Completion
*   **Tab Completion:** PowerShell has excellent tab completion. Start typing a command, parameter, or path and press `Tab` to cycle through possible completions.
*   **`Ctrl+L`:** Clears the screen (alias for `Clear-Host`).
*   **`Escape`:** Clears the current line you are typing.
