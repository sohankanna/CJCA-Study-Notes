# Working with Files and Directories

## 1. Common File & Directory Management Cmdlets

PowerShell follows a consistent `Verb-Noun` pattern for its cmdlets, which makes them easy to remember. Many also have familiar aliases from CMD and Linux.

| Action | Cmdlet | Common Aliases |
| :--- | :--- | :--- |
| **Get an Item** | `Get-Item` | `gi` |
| **List Contents** | `Get-ChildItem`| `ls`, `dir`, `gci` |
| **Create New Item**| `New-Item` | `ni`, `mkdir`, `md` |
| **Copy Item** | `Copy-Item` | `cp`, `copy`, `cpi` |
| **Move Item** | `Move-Item` | `mv`, `move`, `mi` |
| **Rename Item** | `Rename-Item` | `ren`, `rni` |
| **Remove Item** | `Remove-Item` | `rm`, `del`, `erase`, `rmdir`|
| **Get Content** | `Get-Content` | `cat`, `type`, `gc` |
| **Add Content** | `Add-Content` | `ac` |
| **Set Content** | `Set-Content` | `sc` |
| **Clear Content**| `Clear-Content`| `clc` |
| **Compare Objects**| `Compare-Object`| `diff`, `compare` |

---

## 2. Practical Examples

### Creating Directories
The `New-Item` cmdlet is used to create new items. You must specify the `-ItemType`.
```powershell
# Create a new directory named "SOPs"
PS C:\> New-Item -Name "SOPs" -ItemType Directory
```

### Creating Files and Adding Content
*   **Create an empty file:**
    ```powershell
    PS C:\SOPs> New-Item -Name "Readme.md" -ItemType File
    ```
*   **Add content to a file (`Add-Content`):** This cmdlet **appends** text to a file. Multi-line strings can be created using a "here-string" `@"..."@` or by simply pressing Enter within quotes.
    ```powershell
    # Add a multi-line header to the Readme.md file
    PS C:\SOPs> Add-Content .\Readme.md @"
    Title: Insert Document Title Here
    Date: x/x/202x
    Author: MTanaka
    Version: 0.1 (Draft)
    "@
    
```
*   **Overwrite content in a file (`Set-Content`):** This cmdlet **replaces** the entire content of a file with new content.
```powershell
    PS C:\SOPs> Set-Content .\Readme.md "This is the new and only content."
```

### Renaming and Moving Items
*   **Rename an item:** The `Rename-Item` cmdlet changes the name of a file or directory.
```powershell
    PS C:\SOPs> Rename-Item .\Cyber-Sec-draft.md -NewName Infosec-SOP-draft.md
```
*   **Move an item:** The `Move-Item` cmdlet moves a file or directory to a new location.
```powershell
    PS C:\SOPs> Move-Item .\Readme.md -Destination C:\Temp\
```

---

## 3. Bulk Operations with the Pipeline

The true power of PowerShell comes from its object-based pipeline. You can `Get` a collection of items and pipe (`|`) them to another cmdlet to perform an action on all of them at once.

**Example: Change the extension of all `.txt` files to `.md`**
```powershell
# 1. Get all items ending in .txt
# 2. Pipe them to the Rename-Item cmdlet
# 3. For each item ($_), create a new name by replacing ".txt" with ".md"
PS C:\> Get-ChildItem -Path *.txt | Rename-Item -NewName {$_.Name -replace ".txt",".md"}
```
*   `$_.Name`: In a pipeline script block `{}`, the `$_` automatic variable represents the **current object** being processed.

---

## 4. A Note on File & Directory Permissions (NTFS)

PowerShell provides a robust set of cmdlets for managing the granular NTFS permissions on files and folders.

*   `Get-Acl`: Retrieves the Access Control List (ACL) of an object.
*   `Set-Acl`: Applies a modified ACL to an object.

While a deep dive is covered in the Windows Fundamentals module, the core permission types are:
*   **Full Control:** Complete and unrestricted access.
*   **Modify:** Read, write, and delete files/folders.
*   **Read & Execute:** View contents and run programs.
*   **List Folder Contents:** View the names of items in a folder.
*   **Read:** View the contents of a file.
*   **Write:** Add or modify files and folders.
