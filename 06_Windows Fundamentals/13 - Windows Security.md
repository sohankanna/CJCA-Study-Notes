# Windows Security


## 1. Core Security Principles

Windows security is built on a model of authenticating "security principals" and authorizing their access to resources.

### Security Identifier (SID)
*   **What it is:** A **Security Identifier (SID)** is a unique, immutable string value that identifies a security principal (a user, group, or computer).
*   **Purpose:** Windows uses SIDs, not usernames, to track permissions internally. Even if you rename a user account, its underlying SID remains the same.
*   **Structure:** `S-R-I-S-S...-R`
    *   `S`: Indicates it's a SID.
    *   `R`: Revision level (always `1`).
    *   `I`: Identifier Authority (e.g., `5` for `NT AUTHORITY`).
    *   `S...`: Subauthorities, which include a unique domain/machine identifier.
    *   `R`: The **Relative ID (RID)**. This is the last part of the SID and is what uniquely identifies the account within its domain or local machine. Standard user accounts typically start with a RID of 1000 or higher.
*   **Command:** `whoami /user`

### Access Control Model
*   **SAM (Security Accounts Manager):** The database on a local Windows machine (stored in the file `C:\Windows\System32\config\SAM`) that stores local user accounts and their password hashes.
*   **ACL (Access Control List):** A list of permissions attached to an object (like a file or a service).
*   **ACE (Access Control Entry):** A single entry in an ACL that specifies a permission (e.g., "Allow Read") for a specific SID.
*   **DACL vs. SACL:**
    *   **DACL (Discretionary ACL):** Controls who is allowed or denied access to an object.
    *   **SACL (System ACL):** Controls which access attempts are logged in the Security Event Log.
*   **LSA (Local Security Authority):** The process (`lsass.exe`) responsible for authenticating users and creating their **access tokens**, which contain the user's SID and the SIDs of all the groups they belong to.

---

## 2. Key Security Features

### User Account Control (UAC)
*   **What it is:** A security feature that helps prevent unauthorized changes to the system.
*   **How it Works:** Even when you are logged in as an administrator, your processes run with standard user privileges by default. When an action requires administrative rights, UAC displays a **consent prompt** that you must approve.
*   **Purpose:** Prevents malware from silently performing administrative actions in the background. It forces an interactive confirmation for elevated tasks.

### The Windows Registry
*   **What it is:** A hierarchical database that stores low-level configuration settings for the operating system and for applications.
*   **Structure:** Organized into root keys (e.g., `HKEY_LOCAL_MACHINE` or `HKLM`, `HKEY_CURRENT_USER` or `HKCU`), subkeys, and values.
*   **Registry Hives:** The actual data for the registry is stored in files called "hives," primarily located in `C:\Windows\System32\config`. The user-specific hive is `NTUSER.DAT` in their profile folder.
*   **Security Relevance (Run Keys):** The `Run` and `RunOnce` registry keys are a common **persistence mechanism**. Programs listed in these keys will automatically start at boot or user logon. Attackers frequently add malicious entries here.
    *   `HKLM\Software\Microsoft\Windows\CurrentVersion\Run`
    *   `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`

---

## 3. Application Whitelisting

Application whitelisting is a "zero trust" security model where, by default, all applications are blocked from running except for those that are explicitly on an approved list.

*   **Whitelisting vs. Blacklisting:**
    *   **Blacklisting:** Blocks a known list of bad applications (like an antivirus). This is less effective as new malware is created constantly.
    *   **Whitelisting:** Allows only a known list of good applications. Much more secure but can be more challenging to manage.
*   **AppLocker:** Microsoft's built-in application whitelisting solution. It allows administrators to create granular rules to control which executables, scripts, DLLs, and installers users are allowed to run. Rules can be based on file path, hash, or digital signature.

---

## 4. Group Policy
*   **What it is:** A feature that provides centralized management and configuration of operating systems, applications, and user settings in an Active Directory environment.
*   **Local Group Policy (`gpedit.msc`):** A version that can be used to configure settings on a single, standalone machine. It can be used to enforce strong password policies, configure auditing, and manage AppLocker rules locally.

---

## 5. Windows Defender Antivirus
*   **What it is:** The built-in, free antivirus and anti-malware solution that ships with modern Windows operating systems.
*   **Key Features:**
    *   **Real-time Protection:** Scans files as they are accessed to block known threats.
    *   **Cloud-delivered Protection:** Uses Microsoft's cloud intelligence to identify new and emerging threats.
    *   **Tamper Protection:** Prevents users and malware from disabling security settings.
    *   **Controlled Folder Access:** A feature designed to protect specific folders from unauthorized changes, providing a layer of defense against ransomware.
*   **PowerShell Cmdlet:** `Get-MpComputerStatus` can be used to check the status of Defender's various protection features.
