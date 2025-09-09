# Service Permissions


## 1. The Importance of Service Accounts

Windows services run in the background under the security context of a specific user account. The choice of this account is a critical security decision.

*   **The Problem:** By default, a service installed by an administrator might be configured to run as that administrator. If that admin's account is later disabled (e.g., they leave the company), the service will fail to start, causing a service outage.
*   **The Solution (Best Practice):** Critical services should be configured to run using a dedicated **service account**. This is a user account created for the sole purpose of running a specific application or service. This decouples the service's operation from any individual human user.

### Built-in Service Accounts
Windows provides several built-in, low-privilege accounts for running services securely.
*   **`LocalService`:** Has minimum privileges on the local computer and presents anonymous credentials on the network.
*   **`NetworkService`:** Has minimum privileges on the local computer but presents the computer's own credentials on the network.
*   **`LocalSystem`:** **The most privileged account on a local Windows system.** It has extensive privileges, equivalent to or even exceeding a local administrator. Running a service as `LocalSystem` should be done with extreme caution, following the **Principle of Least Privilege**.

---

## 2. Common Service-Related Vulnerabilities

Attackers specifically target services because they often run with high privileges and can be configured to start automatically.

| Vulnerability Vector | Description |
| :--- | :--- |
| **Weak Executable Permissions**| The `BINARY_PATH_NAME` points to an executable file. If a standard user has **write or modify permissions** on that `.exe` file, they can replace it with a malicious executable. The next time the service starts, the malicious code will run with the privileges of the service account (often `LocalSystem`). |
| **Unquoted Service Paths** | If a service path contains spaces and is not enclosed in quotes (e.g., `C:\Program Files\Some App\service.exe`), Windows may try to execute `C:\Program.exe` first. An attacker can place a malicious file at that location to achieve privilege escalation. |
| **Weak Service Permissions**| If a standard user has permissions to modify the configuration of a service (e.g., change the `BINARY_PATH_NAME`), they can reconfigure the service to run a malicious executable. |
| **Insecure Recovery Options**| The "Recovery" tab in a service's properties allows an administrator to configure an action to take if the service fails, including running a program. If an attacker can repeatedly crash the service, they can trigger their malicious program to be executed with the service's privileges. |

---

## 3. Managing Services from the Command Line

While `services.msc` is the graphical tool, command-line utilities are essential for scripting and automation.

### `sc.exe` (Service Control)
`sc.exe` is the traditional command-line tool for interacting with the Service Control Manager.

*   **Query Service Configuration (`qc`):** Displays detailed information about a service, including its `BINARY_PATH_NAME`.
    ```powershell
    sc qc wuauserv
    ```
*   **Modify Service Configuration (`config`):** Allows an administrator to change a service's properties.
    ```powershell
    sc config wuauserv binPath=C:\Path\To\malicious.exe
    ```
*   **View Service Permissions (`sdshow`):** Displays the service's security descriptor.
    ```powershell
    sc sdshow wuauserv
    ```

### In-Depth: Deconstructing SDDL (The "Garbage Output")
The output of `sc sdshow` is in a format called **Security Descriptor Definition Language (SDDL)**. While it looks like random characters, it's a highly structured language that precisely defines an object's access control list.

**Example SDDL String:**
`D:(A;;CCLCSWRPLORC;;;AU)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)`

Let's break down the **first Access Control Entry (ACE)**: `(A;;CCLCSWRPLORC;;;AU)`

*   **`( ... )`**: Encloses a single Access Control Entry (ACE).
*   **`A`**: The **ACE Type**. `A` stands for **Allow**. `D` would mean **Deny**.
*   **`;;`**: Two empty fields for ACE flags and Object GUID (not used here).
*   **`CCLCSWRPLORC`**: This is the most important part—the **Permissions Mask**. Each two-letter code represents a specific permission.
    *   `CC`: `SERVICE_QUERY_CONFIG` - Permission to query the service's configuration.
    *   `LC`: `SERVICE_QUERY_STATUS` - Permission to query the service's status.
    *   `SW`: `SERVICE_ENUMERATE_DEPENDENTS` - Permission to list dependent services.
    *   `RP`: `SERVICE_START` - Permission to start the service.
    *   `LO`: `SERVICE_INTERROGATE` - Permission to query the service for its current status.
    *   `RC`: `READ_CONTROL` - Permission to read the security descriptor.
*   **`;;;`**: Three more empty fields for Object Type, Inherited Object Type, and Application-specific data.
*   **`AU`**: The **Security Principal (Trustee)**. This is a shorthand for who this rule applies to.
    *   `AU`: **A**uthenticated **U**sers
    *   `BA`: **B**uilt-in **A**dministrators
    *   `SY`: Local **Sy**stem

**Translation of the First ACE:** `(A;;CCLCSWRPLORC;;;AU)` means:
> "**Allow** *Authenticated Users* to **query config**, **query status**, **enumerate dependents**, **start the service**, **interrogate status**, and **read the security descriptor**."

This level of detail is how Windows enforces granular control, and understanding how to read SDDL is an advanced skill for identifying subtle permission misconfigurations.

### PowerShell (`Get-Acl`)
PowerShell provides a more modern and readable way to view object permissions, including services. Since services are represented in the registry, you can use `Get-Acl` on their registry key.

*   **View Service Permissions:**
    ```powershell
    Get-Acl -Path HKLM:\System\CurrentControlSet\Services\wuauserv | Format-List
    ```
    This command returns the permissions in a much more human-readable format than `sc sdshow`, but also includes the full SDDL string for advanced analysis.
