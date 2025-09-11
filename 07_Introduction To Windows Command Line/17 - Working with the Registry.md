# Working with the Registry


## 1. What is the Windows Registry?

The **Registry** is a central repository for configuration data. It's organized in a tree-like structure containing two main elements:
*   **Keys:** These are the "folders" or containers in the Registry. A key can contain other subkeys and values.
*   **Values:** These are the "files" within a key. A value consists of a name, a data type (e.g., string, binary, number), and the actual data.

**Security Relevance:** The Registry is a treasure trove of information. It can reveal installed software, system configurations, and user settings. It is also a primary target for attackers to establish **persistence** by creating entries that automatically run their malware at boot or logon.

### Registry Hives
The actual Registry data is stored in files called **hives**, located primarily in `C:\Windows\System32\config`. The user-specific hive (`HKEY_CURRENT_USER`) is stored in the `NTUSER.DAT` file within each user's profile.

### The Five Main Root Keys

| Abbreviation | Full Name | Description |
| :--- | :--- | :--- |
| **`HKLM`** | `HKEY_LOCAL_MACHINE` | Contains machine-specific configuration data that applies to the entire computer, regardless of who is logged in (e.g., hardware, system software). |
| **`HKCU`** | `HKEY_CURRENT_USER` | Contains configuration settings that are specific to the **currently logged-in user**. This is a link to the current user's subkey within `HKEY_USERS`. |
| **`HKCR`** | `HKEY_CLASSES_ROOT` | Contains information about file associations and COM object registrations. |
| **`HKU`** | `HKEY_USERS` | Contains the `NTUSER.DAT` hive for **all** user profiles on the machine, including a default profile. |
| **`HKCC`** | `HKEY_CURRENT_CONFIG` | Contains information about the hardware profile the system is using at startup. |

---

## 2. Interacting with the Registry

You can interact with the Registry from the command line using PowerShell cmdlets or the legacy `reg.exe` utility.

### Using PowerShell
PowerShell treats the Registry like a filesystem, allowing you to use familiar cmdlets to navigate and manage it. Registry paths are accessed via specific PowerShell drives (e.g., `HKLM:` and `HKCU:`).

*   **List Keys (`Get-ChildItem`):**
    ```powershell
    # List the subkeys in the Run key
    Get-ChildItem -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
    ```
*   **Read Values (`Get-ItemProperty`):**
    ```powershell
    # Read all the values (startup programs) within the Run key
    Get-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
    ```
*   **Create a New Key (`New-Item`):**
    ```powershell
    New-Item -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\ -Name TestKey
    ```
*   **Create/Set a New Value (`New-ItemProperty` / `Set-ItemProperty`):**
    ```powershell
    New-ItemProperty -Path HKCU:\...\RunOnce\TestKey -Name "MyPayload" -PropertyType String -Value "C:\path\to\evil.exe"
    ```
*   **Remove a Key/Value:**
    ```powershell
    # Remove the value named "MyPayload"
    Remove-ItemProperty -Path HKCU:\...\RunOnce\TestKey -Name "MyPayload"
    
    # Remove the entire "TestKey" key
    Remove-Item -Path HKCU:\...\RunOnce\TestKey
    ```

### Using `reg.exe`
`reg.exe` is the legacy command-line tool for managing the Registry. It is less flexible than PowerShell but is still widely used and available.

*   **Query a Key:**
    ```powershell
    reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
    ```
*   **Search the Registry:** The `/f` (find) and `/s` (recursive) flags make `reg query` a powerful search tool.
    ```powershell
    # Search the entire HKCU hive for any key or value containing the string "password"
    reg query HKCU /f "password" /s
    ```
*   **Add a Key/Value:**
    ```powershell
    reg add "HKCU\...\RunOnce\TestKey" /v MyPayload /t REG_SZ /d "C:\path\to\evil.exe"
    ```
    *   `/v`: Specifies the **v**alue name.
    *   `/t`: Specifies the data **t**ype.
    *   `/d`: Specifies the **d**ata.

---

## 3. The "Run" Keys: A Key Persistence Location

The `Run` and `RunOnce` keys are one of the most common and effective places for malware to establish persistence. Programs listed as values in these keys are automatically executed at startup or logon.

*   **Run (for all users):** `HKLM\Software\Microsoft\Windows\CurrentVersion\Run`
*   **Run (for the current user):** `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`
*   **RunOnce:** Same locations as `Run`, but the entry is deleted after it is executed once.

A key part of any host investigation is to carefully enumerate the contents of these registry keys to look for suspicious or unauthorized startup programs.
