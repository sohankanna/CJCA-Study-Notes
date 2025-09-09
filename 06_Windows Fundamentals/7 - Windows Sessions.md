# Windows Sessions


## 1. Logon Session Types

A **logon session** begins when a user is authenticated and ends when the user logs off. There are two primary types of sessions.

### Interactive Sessions
An **interactive session** is one where a user is actively and directly interacting with the system's desktop environment. This is initiated when a user provides credentials to log on.

*   **Methods for creating an interactive session:**
    1.  **Local Logon:** Physically logging into the computer with a keyboard and mouse.
    2.  **Remote Desktop (RDP):** Logging in graphically over the network. This creates a full interactive session on the remote machine.
    3.  **Secondary Logon (`runas`):** Using the `runas` command to start a process as a different user (e.g., `runas /user:Administrator cmd.exe`). This creates a new, separate interactive logon session for that process.

### Non-Interactive Sessions
A **non-interactive session** is created for processes that run in the background without any direct user interface. These are typically used by Windows services and scheduled tasks.

---

## 2. Non-Interactive Service Accounts

Windows has several built-in, special accounts designed to run services without requiring a password or user intervention. These accounts are a core part of the OS and are used to enforce the principle of least privilege for background services.

| Account Name | Full Identifier | Privilege Level | Description & Use Case |
| :--- | :--- | :--- | :--- |
| **Local System** | `NT AUTHORITY\SYSTEM` | **Highest.** The most powerful account on a local Windows machine, even more privileged than a local Administrator. | Used for core operating system services that require complete control over the local system (e.g., the Service Control Manager itself). Gaining code execution as `SYSTEM` is the ultimate goal of local privilege escalation. |
| **Local Service** | `NT AUTHORITY\LocalService` | **Low.** Has the privileges of a standard, unprivileged user on the local machine. | Used for services that need minimal local access. It presents **anonymous** credentials on the network, so it cannot access network resources. |
| **Network Service**| `NT AUTHORITY\NetworkService`| **Low.** Has similar limited privileges to `LocalService` on the local machine. | The key difference is that it presents the **computer's own account** credentials (e.g., `WORKSTATION$`) on the network. This allows it to access network resources that the computer account has permission to access. |

**Key Takeaway:** Understanding which account a service runs as is critical for a penetration tester. A service running as `LocalSystem` is a high-value target for exploitation, as a vulnerability in that service could lead to a complete compromise of the host. Conversely, a service running as `LocalService` is much less of a risk.
