# All About Cmdlets and Modules


## 1. Cmdlets: The Building Blocks of PowerShell

A **cmdlet** (pronounced "command-let") is a single-function, native command in PowerShell.

*   **Structure:** Cmdlets follow a strict **`Verb-Noun`** naming convention, separated by a dash (e.g., `Get-Help`, `Set-ExecutionPolicy`). This makes them predictable and easy to understand.
*   **Implementation:** Unlike shell commands, cmdlets are not standalone executables. They are compiled classes, typically written in C#, that are part of the .NET framework.
*   **Object-Oriented:** The most significant feature of cmdlets is that their output is a structured **object**, not just plain text. This allows you to pipe (`|`) the output of one cmdlet directly to another for powerful, one-line operations.

---

## 2. PowerShell Modules

A **PowerShell module** is a reusable package that bundles together related PowerShell components, making them easy to share and manage.

*   **Contents:** A module can contain:
    *   Cmdlets
    *   Functions
    *   Scripts (`.ps1` files)
    *   Variables and aliases
    *   A **module manifest** (`.psd1` file), which is a data file containing metadata about the module (version, author, included commands, etc.).
    *   A **script module** (`.psm1` file), which contains the actual PowerShell code (functions, etc.).

**Key Idea:** Modules are the primary way that PowerShell's functionality is extended.

---

## 3. Working with Modules

### Finding and Loading Modules
*   **`Get-Module`:** Lists all modules that are currently **loaded** into your active PowerShell session.
*   **`Get-Module -ListAvailable`:** Lists all modules that are **installed** on the system, whether they are currently loaded or not.
*   **`Import-Module`:** Manually loads a module into your current session. This is necessary for custom scripts or modules that are not in a standard module path.
    ```powershell
    # Import the PowerSploit module from a local file
    Import-Module .\PowerSploit.psd1
    ```
*   **`$env:PSModulePath`:** This environment variable contains a list of directories where PowerShell automatically looks for modules. Placing a module in one of these directories allows for auto-loading.

### Discovering Commands within a Module
Once a module is loaded, you can see all the new commands it provides.
```powershell
Get-Command -Module PowerSploit
```

---

## 4. The PowerShell Gallery and `PowerShellGet`

The **PowerShell Gallery** is the official, public repository for sharing and acquiring PowerShell modules and scripts.

**`PowerShellGet`** is a built-in module that provides cmdlets for interacting with the PowerShell Gallery.
*   **`Find-Module`:** Searches the PowerShell Gallery for a specific module.
    ```powershell
    Find-Module -Name AdminToolbox
    ```
*   **`Install-Module`:** Downloads and installs a module from the PowerShell Gallery. This typically requires administrative privileges.
    ```powershell
    Install-Module -Name AdminToolbox
    ```
*   **`Update-Module`:** Updates an installed module to the latest version.
*   **`Uninstall-Module`:** Removes a module.

---

## 5. Bypassing the Execution Policy

As covered previously, PowerShell's **Execution Policy** can prevent scripts and modules from being loaded.
*   **The Problem:** Running `Import-Module` may fail with a "running scripts is disabled on this system" error.
*   **The Check:** `Get-ExecutionPolicy`
*   **The Fix (Temporary & Safe):** Change the policy only for the current process. This change will be lost when you close the PowerShell window and is the recommended way to bypass the policy during an engagement.
    ```powershell
    Set-ExecutionPolicy Bypass -Scope Process
    ```

---

## 6. Notable PowerShell Tools for Pentesters

*   **PowerSploit:** A classic, foundational collection of offensive PowerShell modules for reconnaissance, privilege escalation, and more.
*   **Empire:** A post-exploitation framework that heavily utilizes PowerShell for its agents and modules.
*   **Inveigh:** A powerful tool for network spoofing and Man-in-the-Middle attacks.
*   **BloodHound / SharpHound:** A tool for mapping Active Directory environments. The `SharpHound` data collector is often run via PowerShell.
