# Windows Services & Processes

## 1. Windows Services

A **Windows Service** is a long-running executable application that runs in its own session in the background. Services can be configured to start automatically when the computer boots and can continue to run even if no user is logged in.

*   **Purpose:** To handle core OS functions (like networking, printing, updates) and to run applications (like a database or web server) that need to be available 24/7 without direct user interaction.
*   **Management:**
    *   **GUI:** The **Services MMC Snap-in** (`services.msc`). This provides a graphical interface to view, start, stop, and configure services.
    *   **PowerShell:** The `Get-Service` cmdlet is the modern way to manage services from the command line.
    *   **Command Prompt:** The legacy `sc.exe` (Service Control) utility.

### Key Service Properties
*   **Status:** Running, Stopped, Paused.
*   **Startup Type:**
    *   **Automatic:** The service starts automatically at boot.
    *   **Automatic (Delayed Start):** Starts shortly after boot to improve boot performance.
    *   **Manual:** The service must be started manually by a user or another application.
    *   **Disabled:** The service cannot be started.
*   **Log On As:** The user account the service runs under (e.g., `Local System`, `Network Service`, `Local Service`). **Misconfigured service permissions are a very common privilege escalation vector.**

---

## 2. Processes

A **process** is an instance of a computer program that is being executed. Every application you run and every service that is active has one or more processes associated with it.

### Critical System Processes
Terminating these processes will likely cause system instability or a crash.

| Process Name | Description | Security Relevance |

| **`lsass.exe`** | **Local Security Authority Subsystem Service.** | **Extremely high-value target.** This process handles user authentication, enforces security policies, and creates access tokens. Attackers use tools like **Mimikatz** to dump credentials (passwords and hashes) directly from the memory of the `lsass.exe` process. |
| **`smss.exe`** | Session Manager SubSystem. | Responsible for creating user sessions. |
| **`csrss.exe`** | Client Server Runtime Process. | Manages the user-mode side of the Windows subsystem. |
| **`wininit.exe`**| Windows Initialization Process.| Manages startup of key background services. |
| **`services.exe`**| Service Control Manager. | Manages the starting and stopping of Windows services. |
| **`winlogon.exe`**| Windows Logon Application.| Handles the secure attention sequence (`Ctrl+Alt+Del`) and user logon. |
| **`svchost.exe`**| Service Host. | A generic host process for services that run from DLL files. You will see many instances of `svchost.exe` running, each hosting one or more services. |

---

## 3. Tools for Managing Processes and Services

### Task Manager (`taskmgr.exe`)
The built-in, primary tool for viewing and managing running applications and processes.
*   **Key Tabs:**
    *   **Processes:** Lists running apps and background processes with resource usage (CPU, Memory, Disk, Network).
    *   **Performance:** Real-time graphs of system resource utilization.
    *   **Startup:** Allows you to enable or disable programs that run automatically at boot.
    *   **Details:** A more detailed view of processes, including their Process ID (PID) and the user they are running as.
    *   **Services:** A simple interface for starting and stopping services.

### Sysinternals Suite
The **Sysinternals Suite** is a collection of advanced, free troubleshooting utilities for Windows, created by Mark Russinovich at Microsoft. They are essential tools for any serious administrator or security professional.

*   **How to Access:** They are portable (no installation needed) and can be downloaded or run directly from the live share: `\\live.sysinternals.com\tools\`
*   **Key Tools:**
    *   **Process Explorer (`procexp.exe`):** A supercharged version of Task Manager. It shows a hierarchical view of processes (parent-child relationships) and can inspect which handles and DLLs a process has loaded.
    *   **Process Monitor (`procmon.exe`):** A powerful real-time monitoring tool that shows all file system, Registry, and network activity on the system. Invaluable for seeing what a program is *actually* doing.
    *   **TCPView (`tcpview.exe`):** A simple utility that shows all active TCP and UDP connections on the system and the processes associated with them.
    *   **PSExec (`psexec.exe`):** A tool for executing processes on remote systems. It is a legitimate admin tool but is also heavily used by penetration testers for lateral movement.
    *   **Procdump (`procdump.exe`):** A command-line utility for creating crash dumps of running processes. It can be used, for example, to create a dump of the `lsass.exe` process memory for offline credential extraction.
