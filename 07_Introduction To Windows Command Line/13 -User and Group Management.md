# User and Group Management


## 1. Understanding User Accounts

Windows utilizes several types of user accounts, each with a different scope and purpose.

| Account Type          | Description                                                                                                                                                                                                    |
| :-------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Local Users**       | Accounts that exist only on a single, specific machine. They are stored in the local **SAM** database and are used to log in to that machine only.                                                             |
| **Domain Users**      | Accounts that exist within an **Active Directory (AD)** domain. These accounts are stored on a central server (a Domain Controller) and can be used to log in to *any* computer that is joined to that domain. |
| **Built-in Accounts** | Default accounts created during Windows installation, such as `Administrator` and `Guest`.                                                                                                                     |
| **Service Accounts**  | Special accounts (local or domain) used by services and applications to run in the background.                                                                                                                 |

---

## 2. Managing Local Users and Groups

These cmdlets are part of the `Microsoft.PowerShell.LocalAccounts` module and are used to manage accounts on a standalone machine or a member server.

### Local Users

| Action | Cmdlet | Example |
| :--- | :--- | :--- |
| **List Users** | `Get-LocalUser` | `Get-LocalUser` |
| **Create User** | `New-LocalUser` | `New-LocalUser -Name "JLawrence" -NoPassword` |
| **Modify User**| `Set-LocalUser` | `$Password = Read-Host -AsSecureString`<br>`Set-LocalUser -Name "JLawrence" -Password $Password` |
| **Remove User**| `Remove-LocalUser`| `Remove-LocalUser -Name "JLawrence"` |

### Local Groups

| Action | Cmdlet | Example |
| :--- | :--- | :--- |
| **List Groups**| `Get-LocalGroup` | `Get-LocalGroup` |
| **View Group Members**| `Get-LocalGroupMember`| `Get-LocalGroupMember -Name "Administrators"` |
| **Add Member to Group**| `Add-LocalGroupMember` | `Add-LocalGroupMember -Group "Remote Desktop Users" -Member "JLawrence"` |
| **Remove Member**| `Remove-LocalGroupMember`| `Remove-LocalGroupMember -Group "Remote Desktop Users" -Member "JLawrence"` |

---

## 3. Managing Domain Users and Groups (Active Directory)

To manage AD objects, you must use the `ActiveDirectory` PowerShell module. This module is typically installed as part of the **Remote Server Administration Tools (RSAT)**.

### Installing the Module
```powershell
# Installs the Active Directory RSAT tools
Get-WindowsCapability -Name RSAT.ActiveDirectory.DS-LDS.Tools* -Online | Add-WindowsCapability -Online
```

### Domain Users (`-ADUser`)

| Action | Cmdlet | Example |
| :--- | :--- | :--- |
| **Find Users** | `Get-ADUser` | `Get-ADUser -Filter *` (gets all users). <br> `Get-ADUser -Identity TSilver` (gets a specific user). <br> `Get-ADUser -Filter {EmailAddress -like '*greenhorn.corp'}` (filters on an attribute). |
| **Create User**| `New-ADUser` | `New-ADUser -Name "MTanaka" -AccountPassword (Read-Host -AsSecureString)` |
| **Modify User**| `Set-ADUser` | `Set-ADUser -Identity MTanaka -Description "New Description"` |
| **Remove User**| `Remove-ADUser`| `Remove-ADUser -Identity MTanaka` |

### Domain Groups (`-ADGroup`)

| Action | Cmdlet | Example |
| :--- | :--- | :--- |
| **Find Groups**| `Get-ADGroup` | `Get-ADGroup -Filter *` (gets all groups). |
| **View Group Members**| `Get-ADGroupMember`| `Get-ADGroupMember -Identity "Domain Admins"` |
| **Add Member to Group**| `Add-ADGroupMember` | `Add-ADGroupMember -Identity "Domain Admins" -Members "MTanaka"` |
| **Remove Member**| `Remove-ADGroupMember`| `Remove-ADGroupMember -Identity "Domain Admins" -Members "MTanaka"` |

---

## 4. Why Enumerating Users & Groups is Important for Pentesters

Enumerating users and groups is a critical reconnaissance step.
*   **Finding Weaknesses:** Attackers look for misconfigurations like weak passwords, disabled accounts that are still members of privileged groups, or excessive permissions.
*   **Discovering Privileged Users:** Identifying members of high-value groups like `Administrators`, `Domain Admins`, or `Enterprise Admins` provides a clear list of targets for credential theft.
*   **Understanding the Environment:** The structure of groups and user naming conventions can reveal information about the organization's departments, roles, and overall structure.
*   **Tools like BloodHound:** These tools automate the process of querying Active Directory for user and group information and visualize the relationships to find complex attack paths to privilege escalation.
