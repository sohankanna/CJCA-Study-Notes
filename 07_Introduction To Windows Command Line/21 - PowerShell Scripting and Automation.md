# PowerShell Scripting and Automation


## 1. Scripts vs. Modules

*   **Script (`.ps1`):** A text file containing a sequence of PowerShell commands. You typically execute a script directly (e.g., `.\MyScript.ps1`).
*   **Module (`.psm1`, `.psd1`):** A reusable, bundled package of PowerShell functionality. A module can contain multiple scripts, functions, cmdlets, and variables. You load a module into your session using `Import-Module`, making its functions and cmdlets available for you to call.

**Key Idea:** A script is a single recipe. A module is an entire cookbook.

---

## 2. Building a PowerShell Module

Creating a module follows a structured process to ensure it is reusable and easy to manage.

### Step 1: Create a Directory for the Module
A module should reside in its own directory. This directory must be placed in one of the paths listed in the `$env:PSModulePath` environment variable for PowerShell to find it automatically.
```powershell
# Create a new module directory in the user's default module path
mkdir ~\Documents\WindowsPowerShell\Modules\quick-recon
```

### Step 2: Create a Module Manifest (`.psd1`)
A **module manifest** is a data file that contains metadata about your module. While optional for simple modules, it is a best practice.
*   **Purpose:** Describes the module's version, author, dependencies, and explicitly controls which functions, cmdlets, and variables are "exported" (made public) when the module is imported.
*   **Create a Manifest:** The `New-ModuleManifest` cmdlet generates a template for you.
    ```powershell
    New-ModuleManifest -Path .\quick-recon.psd1
    ```

### Step 3: Create the Script Module File (`.psm1`)
This file contains the actual PowerShell code—your functions, variables, and logic.
```powershell
# Create an empty script module file
New-Item quick-recon.psm1 -ItemType File
```

---

## 3. Writing the Script (`.psm1` file)

### Functions
Functions are the core of a module. They are named blocks of reusable code.
```powershell
# A simple function to gather basic system info
function Get-Recon {
    # 1. Collect data and store it in variables
    $Hostname = $env:ComputerName
    $IP = ipconfig
    
    # 2. Format the output
    $Output = "--- Hostname ---", $Hostname, "--- IP Config ---", $IP
    
    # 3. Write the output to a file on the user's desktop
    Add-Content -Path ~\Desktop\recon.txt -Value $Output
}
```

### Comment-Based Help
PowerShell has a standardized way to write help documentation directly inside your script using special comment blocks. This allows `Get-Help` to work on your custom functions.
```powershell
<#
.SYNOPSIS
    A brief summary of what the function does.

.DESCRIPTION
    A more detailed description of the function.

.EXAMPLE
    Get-Recon
    This example runs the reconnaissance function and saves output to the desktop.
#>
function Get-Recon {
    # ... function code here ...
}
```

### Exporting Members
By default, all functions in a `.psm1` file are exported. To explicitly control what is made public, use the `Export-ModuleMember` cmdlet at the end of your script.
```powershell
# Only make the Get-Recon function and the Hostname variable public
Export-ModuleMember -Function Get-Recon -Variable Hostname
```

---

## 4. Using the Module

### Importing the Module
To use the functions within your module, you must first import it into your PowerShell session.
```powershell
# If the module is in a PSModulePath directory, you can just use the name
Import-Module quick-recon

# If it's located elsewhere, provide the full path to the .psm1 or .psd1 file
Import-Module C:\Path\To\quick-recon\quick-recon.psd1
```

### Verifying the Import
*   **Check loaded modules:** `Get-Module` will show `quick-recon` in the list.
*   **Check available commands:** `Get-Command -Module quick-recon` will show the exported functions (e.g., `Get-Recon`).
*   **Check the help:** `Get-Help Get-Recon` will display the comment-based help you wrote.

### Running the Function
Once imported, you can run the function just like any other cmdlet.
```powershell
Get-Recon
```
This will execute the code inside your function, creating the `recon.txt` file on your desktop.
