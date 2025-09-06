# Service and Process Management

1. Services (Daemons)

A **service** (or **daemon**) is a program that runs in the background, without direct user interaction, to perform essential system tasks. Daemons are often identifiable by a `d` at the end of their name (e.g., `sshd`, `httpd`).

*   **System Services:** Core services required for the OS to function (e.g., managing hardware).
*   **User-Installed Services:** Services added by the user or administrator (e.g., a web server or database).

### `systemd` and `systemctl`
Most modern Linux distributions use **`systemd`** as their init system—the first process (PID 1) that starts at boot and manages all other services and processes. The primary tool for interacting with `systemd` is **`systemctl`**.

#### Common `systemctl` Commands for Service Management
(These commands usually require `sudo` privileges).

| Action | Command | Description |
| :--- | :--- | :--- |
| **Start a Service** | `systemctl start <service_name>` | Starts a service immediately. |
| **Stop a Service** | `systemctl stop <service_name>` | Stops a running service. |
| **Restart a Service** | `systemctl restart <service_name>` | Stops and then starts a service. Useful for applying configuration changes. |
| **Check Status** | `systemctl status <service_name>` | Shows the current status of a service (active/inactive), its PID, and recent log entries. **This is your primary troubleshooting command.** |
| **Enable a Service** | `systemctl enable <service_name>` | Configures the service to **start automatically at boot**. |
| **Disable a Service**| `systemctl disable <service_name>`| Prevents the service from starting automatically at boot. |
| **List Services** | `systemctl list-units --type=service`| Lists all active service units. |

### Viewing Service Logs (`journalctl`)
The `journalctl` command is used to query and view the logs collected by `systemd`. This is essential for diagnosing why a service failed to start.

*   **Syntax:** `journalctl -u <service_name>`
*   **Example:** To view the logs specifically for the SSH service:
    ```shell
    journalctl -u ssh.service --no-pager
    ```

---

## 2. Process Management

A **process** is any program that is currently running on the system. Each process is assigned a unique **Process ID (PID)**.

### Viewing Processes (`ps`)
The `ps` command provides a snapshot of the current processes.

*   **Command:** `ps aux`
    *   `a`: Show processes for all users.
    *   `u`: Display user-oriented format.
    *   `x`: Show processes not attached to a terminal (like daemons).
*   **Usage:** It's often piped to `grep` to find a specific process.
    ```shell
    ps aux | grep ssh
    ```

### Terminating Processes (`kill`)
The `kill` command is used to send a **signal** to a process, most often to terminate it.

*   **Syntax:** `kill [signal] <PID>`
*   To see all available signals: `kill -l`

#### The Most Common Signals

| Signal # | Name | Description |
| :--- | :--- | :--- |
| **15** | **`SIGTERM`** (Terminate) | The **default** and "polite" way to kill a process. It asks the process to shut down cleanly. `kill <PID>` |
| **9** | **`SIGKILL`** (Kill) | The "forceful" way to kill a process. It terminates the process immediately without any cleanup. Use this when a process is unresponsive. `kill -9 <PID>` |
| **2** | **`SIGINT`** (Interrupt) | The signal sent when you press `Ctrl + C` in the terminal to stop a running command. |
| **20** | **`SIGTSTP`** (Terminal Stop) | The signal sent when you press `Ctrl + Z`. It **suspends** (pauses) the process. |

---

## 3. Job Control (Background & Foreground)

Job control allows you to manage processes within your current shell session.

### Suspending and Backgrounding a Process
*   **Suspend (`Ctrl + Z`):** Press `Ctrl + Z` while a command is running to **suspend** it. The process is paused but not terminated.
*   **View Jobs:** The `jobs` command lists all suspended or backgrounded processes in the current session.
*   **Send to Background (`bg`):** After suspending a job, type `bg` to let it continue running in the **background**.
*   **Start in Background (`&`):** Add an ampersand (`&`) to the end of a command to start it directly in the background.
    ```shell
    ping -c 10 www.hackthebox.eu &
    ```

### Foregrounding a Process
*   **Bring to Foreground (`fg`):** Use the `fg` command with the job number (from the `jobs` command) to bring a background process back to the foreground, allowing you to interact with it again.
    ```shell
    fg 1
    ```

---

## 4. Executing Multiple Commands

There are several ways to run multiple commands on a single line.

| Separator | Name | Behavior | Example |
| :--- | :--- | :--- | :--- |
| **`;`** | **Semicolon** | **Command Separator.** Executes the commands sequentially, regardless of whether the previous command succeeded or failed. | `echo '1'; ls FAKE_FILE; echo '3'` (will print 1, an error, and 3) |
| **`&&`** | **AND** | **Logical AND.** Executes the next command **only if** the previous command completed successfully (exited with code 0). | `echo '1' && ls FAKE_FILE && echo '3'` (will print 1 and an error, but will **not** print 3) |
| **`\|`** | **Pipe** | **Pipeline.** Takes the **STDOUT** of the command on the left and uses it as the **STDIN** for the command on the right. | `ps aux \| grep ssh` |
