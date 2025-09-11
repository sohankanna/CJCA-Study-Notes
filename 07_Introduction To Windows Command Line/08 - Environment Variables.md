# Environment Variables


## 1. What is an Environment Variable?

An **environment variable** is a dynamic, named object that stores a string value. This value can be used by the operating system and various applications to determine key settings, such as file paths, the system root, or temporary directories.

*   **Referencing a Variable:** In CMD, you reference a variable by enclosing its name in percent signs (`%`).
    ```powershell
    C:\> echo %SYSTEMROOT%
    C:\Windows
    ```
*   **Case Insensitivity:** Unlike in Linux, Windows environment variables are not case-sensitive (`%path%` is the same as `%PATH%`).

---

## 2. Variable Scope

The "scope" of a variable determines where and by whom it can be accessed. Windows has three main scopes for environment variables.

| Scope | Description | Permissions to Modify | Persistence | Registry Location |
| :--- | :--- | :--- | :--- | :--- |
| **System (Machine)** | **Global.** These variables are set for the entire machine and are inherited by **all users and all processes**. They are essential for the OS to function correctly. | Administrator | **Permanent.** Stored in the registry. | `HKLM\SYSTEM\...\Environment` |
| **User** | **Local to a user.** These variables are specific to a user account and are loaded when that user logs in. They are only visible to that user. | The specific user or an Administrator. | **Permanent.** Stored in the registry. | `HKCU\Environment` |
| **Process** | **Temporary.** These variables exist only for the lifetime of the current process (e.g., your current `cmd.exe` window). They are inherited from the System and User scopes but any changes made are lost when the process ends. | The current user. | **Volatile.** Stored only in the process's memory. | N/A |

---

## 3. Managing Environment Variables

You can view, create, edit, and delete environment variables from the command line using two primary commands.

### `set` vs. `setx`
This is a critical distinction.
*   **`set`:** Works with **temporary, process-scoped** variables. Any changes made with `set` are **lost** when you close your current Command Prompt window.
*   **`setx`:** Works with **permanent, user or system-scoped** variables. Changes made with `setx` are written to the **Registry** and will persist across reboots and new sessions.

### Common Commands

| Action | `set` (Temporary) | `setx` (Permanent) |
| :--- | :--- | :--- |
| **View All Variables** | `set` | N/A (use `set` or view registry) |
| **View a Specific Variable**| `echo %VARNAME%` | `echo %VARNAME%` (in a *new* CMD session) |
| **Create/Edit a Variable** | `set VARNAME=value` | `setx VARNAME "value"` |
| **Delete a Variable** | `set VARNAME=` (Set it to an empty value) | `setx VARNAME ""` (Set it to an empty string) |

**Example Workflow:**
```powershell
# Create a temporary variable for the current session
C:\> set DCIP=172.16.5.2

# View it
C:\> echo %DCIP%
172.16.5.2

# Create a permanent variable (for the current user)
C:\> setx PERMANENT_VAR "This will survive a reboot"
SUCCESS: Specified value was saved.

# To see the new permanent variable, you must open a NEW Command Prompt.

# Delete the permanent variable
C:\> setx PERMANENT_VAR ""
SUCCESS: Specified value was saved.
```

---

## 4. Important Environment Variables for Enumeration

Enumerating environment variables is a key reconnaissance step for a penetration tester, as they can reveal a wealth of information about the system and its configuration.

| Variable | Expands to (Example) | What it Tells You |
| :--- | :--- | :--- |
| **`%PATH%`** | `C:\Windows\system32;C:\Python39\...` | A list of directories that Windows searches to find executable files. An attacker may look for writable directories in the PATH for DLL hijacking attacks. |
| **`%SYSTEMROOT%`**| `C:\Windows` | The location of the core Windows OS files. |
| **`%WINDIR%`** | `C:\Windows` | An alias for `%SYSTEMROOT%`. |
| **`%USERPROFILE%`**| `C:\Users\hacker` | The path to the current user's profile directory. A key location for user-specific data. |
| **`%APPDATA%`** | `C:\Users\hacker\AppData\Roaming` | The location of the current user's Roaming application data. Often contains sensitive configuration files. |
| **`%LOCALAPPDATA%`**| `C:\Users\hacker\AppData\Local` | The location for local, non-roaming application data. |
| **`%LOGONSERVER%`**| `\\DC01` | **Crucial for reconnaissance.** This variable shows the name of the server that authenticated the current user. It's a quick way to identify if a machine is domain-joined and find the name of a Domain Controller. |
| **`%ProgramFiles%`**| `C:\Program Files` | The default location for 64-bit applications. |
| **`%ProgramFiles(x86)%`**| `C:\Program Files (x86)` | The default location for 32-bit applications on a 64-bit system. The presence of this variable confirms you are on a 64-bit OS. |
