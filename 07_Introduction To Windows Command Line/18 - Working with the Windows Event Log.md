# Working with the Windows Event Log


## 1. What is the Windows Event Log?

The **Windows Event Log** is a standard, centralized system that allows the OS and applications to record significant events. It is a required service (`EventLog`) that starts at boot and runs within a `svchost.exe` process.

*   **Event:** Any action or occurrence that can be identified by the system (e.g., a user logging in, a service starting, an application crashing).
*   **Log Files:** By default, logs are stored as `.evtx` files in `C:\Windows\System32\winevt\logs`.

### Log Categories
Windows organizes events into several main logs.

| Log Name | Description |
| :--- | :--- |
| **Application** | Contains events logged by software applications. |
| **Security** | **Most important for security.** Records events based on the system's audit policy, such as successful and failed logon attempts, object access, and privilege changes. |
| **System** | Contains events logged by Windows system components, such as a driver failing to load or a service failing to start. |
| **Setup** | Contains events related to application and OS installation. |
| **Forwarded Events**| Contains events collected from other computers on the network. |

### Event Types and Levels

| Type (Security Log) | Level (Other Logs) | Level # | Description |
| :--- | :--- | :--- | :--- |
| **Success Audit** | **Information** | 4 | An event that describes the successful operation of a task (e.g., a successful user logon). |
| **Failure Audit** | **Warning** | 3 | An event that is not necessarily significant, but might indicate a future problem (e.g., low disk space). |
| | **Error** | 2 | A significant problem has occurred (e.g., a service failed to start). |
| | **Critical** | 1 | A severe problem that requires immediate attention. |
| | **Verbose** | 5 | Detailed progress or success messages, usually for debugging. |

### Elements of an Event
Each event log entry is a structured record containing key details:
*   **Event ID:** A unique number that identifies a specific type of event. **This is crucial for filtering and alerting.** (e.g., Event ID `4624` = Successful Logon, `4625` = Failed Logon).
*   **Source:** The program or component that logged the event (e.g., `Microsoft-Windows-Security-Auditing`).
*   **Date/Time:** When the event occurred.
*   **User:** The user account associated with the event.
*   **Computer:** The name of the machine where the event occurred.

---

## 2. Interacting with Event Logs

### `wevtutil.exe` (Command Prompt Utility)
`wevtutil` is the built-in command-line tool for managing and querying event logs.

| Action | Command |
| :--- | :--- |
| **Enumerate Logs (`el`)** | `wevtutil el` (Lists all available log names). |
| **Get Log Info (`gl` / `gli`)** | `wevtutil gl "Windows PowerShell"` (Gets configuration info). <br> `wevtutil gli "Windows PowerShell"` (Gets status info like record count). |
| **Query Events (`qe`)** | `wevtutil qe Security /c:5 /rd:true /f:text` <br> (`/c:5`: count of 5 events; `/rd:true`: reverse direction/newest first; `/f:text`: format as text). |
| **Export Log (`epl`)** | `wevtutil epl System C:\system_export.evtx` (Exports the entire System log). |

### `Get-WinEvent` (PowerShell Cmdlet)
`Get-WinEvent` is the modern, more powerful PowerShell cmdlet for querying event logs. It returns objects, which makes it excellent for filtering and automation.

*   **List all logs:**
    ```powershell
    Get-WinEvent -ListLog *
    ```
*   **Get the 5 most recent events from the Security log:**
    ```powershell
    Get-WinEvent -LogName Security -MaxEvents 5
    ```
*   **Filtering with `-FilterHashTable` (The Best Method):**
    This is the most efficient way to query for specific events. The filtering is done by the event log service itself, which is much faster than pulling all logs and filtering them in PowerShell.
    ```powershell
    # Find all failed logon events (Event ID 4625) in the Security log
    Get-WinEvent -FilterHashtable @{LogName='Security'; ID='4625'}
    
    # Find all Critical (Level 1) events in the System log
    Get-WinEvent -FilterHashtable @{LogName='System'; Level=1}
    ```

---

## 3. Security Relevance

*   **For Defenders (Blue Team):** Event logs are the primary source of data for detecting attacks. Logs are forwarded to a **SIEM** (Security Information and Event Management) system, where rules and alerts are configured to automatically flag suspicious activity (e.g., "Alert if there are 10 failed logons for the same user in 1 minute").
*   **For Attackers (Red Team):**
    *   **Reconnaissance:** Logs can reveal usernames, hostnames, network activity, and security software in use.
    *   **Credential Discovery:** In rare misconfigurations, credentials can sometimes be found in cleartext in application or system logs.
    *   **Stealth Assessment:** An attacker can check logs to see if their own activities have been detected. They may also attempt to **clear the event logs** to cover their tracks, although this action itself is a major indicator of compromise.
