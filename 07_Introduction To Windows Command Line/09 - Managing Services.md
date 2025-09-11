# Managing Services


## 1. Why Service Management is Critical for Security

Services are a primary target for attackers because they often:
*   Run with high privileges (e.g., `NT AUTHORITY\SYSTEM`).
*   Start automatically at boot, making them an ideal mechanism for **persistence**.
*   Can be misconfigured (e.g., weak file permissions on the service executable), creating a vector for **privilege escalation**.

An attacker's goals when interacting with services often include:
*   Determining what services are running to understand the host's role and potential vulnerabilities.
*   Attempting to disable security services like antivirus (e.g., Windows Defender).
*   Modifying a legitimate service to execute a malicious payload.

---

## 2. The `sc.exe` (Service Controller) Utility

`sc` is the primary, built-in command-line tool for communicating with the Service Control Manager (SCM).

### Querying Services (`sc query`)
This is the fundamental command for enumerating services.

*   **Query all active services:**
    ```powershell
    sc query type= service state= all
    ```
    *(Note the required space after `type=` and `state=`).*

*   **Query a specific service:**
    ```powershell
    sc query windefend
    ```
    The output shows the service's `STATE` (e.g., RUNNING, STOPPED) and its permissions (e.g., `NOT_STOPPABLE`).

*   **Query service configuration (`sc qc`):** This is extremely useful as it shows the `BINARY_PATH_NAME` (the executable the service runs) and the `SERVICE_START_NAME` (the account it runs as).
    ```powershell
    sc qc wuauserv
    ```

### Starting and Stopping Services
These actions typically require administrative privileges.

*   **Stop a service:**
    ```powershell
    sc stop Spooler
    ```
*   **Start a service:**
    ```powershell
    sc start Spooler
    ```

**Security Note:** Certain critical system services (like Windows Defender, `windefend`) are protected and cannot be stopped even by a local administrator. This is a security feature to prevent tampering. Attempting to stop them will generate log entries and can alert a Blue Team to your presence.

### Modifying Services (`sc config`)
This powerful command allows an administrator to change a service's configuration. Changes made with `sc config` are written to the registry and are **persistent** across reboots.

*   **Change the startup type:**
    ```powershell
    # Disable the Windows Update service from starting automatically
    sc config wuauserv start= disabled
    ```
    *Startup types: `auto`, `demand` (manual), `disabled`.*

*   **Change the binary path (Privilege Escalation Vector):**
    If an attacker has permissions to modify a service, they can change its binary path to point to a malicious executable.
    ```powershell
    sc config VulnSvc binPath= "C:\path\to\evil.exe"
    ```
    When the service is next started, `evil.exe` will run with the permissions of the service account.

---

## 3. Alternative Tools for Service Enumeration

While `sc` is the primary tool for *management*, other commands are excellent for quick enumeration.

| Command | Description | Example |
| :--- | :--- | :--- |
| **`tasklist /svc`** | Lists all running processes and shows which services are hosted within each process. Very useful for seeing which `svchost.exe` instance is running which service. | `tasklist /svc` |
| **`net start`** | A simple command that provides a clean list of all currently **running** services by their display name. | `net start` |
| **`wmic service`**| The WMI command-line utility can list services with specific properties in a clean, table-based format. (Note: WMIC is deprecated). | `wmic service list brief` |
