# Working with Services


## 1. What are Services?

**Services** are background applications that run without direct user interaction. They are a core component of Windows, responsible for everything from networking and printing to system updates.

*   **Processes vs. Services:** A service is a long-running application. A **process** is a temporary container for an application to perform its tasks. A single service can manage multiple processes.
*   **Security Context:** Services run under a specific user account (e.g., `LocalSystem`, `NetworkService`, or a dedicated service account), and their permissions are a critical aspect of system security.

---

## 2. The Core Service Management Cmdlets

PowerShell's `Microsoft.PowerShell.Management` module contains a suite of cmdlets with a consistent `Verb-Service` naming convention for managing services.

| Action | Cmdlet |
| :--- | :--- |
| **Get Service Info** | `Get-Service` |
| **Start a Service** | `Start-Service` |
| **Stop a Service** | `Stop-Service` |
| **Restart a Service** | `Restart-Service`|
| **Suspend a Service** | `Suspend-Service`|
| **Resume a Service** | `Resume-Service` |
| **Modify a Service** | `Set-Service` |
| **Create a New Service**| `New-Service` |
| **Remove a Service** | `Remove-Service`|

To see all available service-related cmdlets, you can run: `Get-Help *-Service`

---

## 3. Practical Service Management Examples

**(Note: Starting, stopping, or modifying services typically requires administrative privileges.)**

### Querying Services (`Get-Service`)
*   **List all services and format the output:**
    ```powershell
    Get-Service | Format-Table DisplayName, Status
    ```
*   **Filter for specific services using the pipeline:** This is the primary strength of PowerShell. The `Where-Object` cmdlet (alias: `where`) is used to filter the objects returned by `Get-Service`.
    ```powershell
    # Find all services with "Defender" in their display name
    Get-Service | where DisplayName -like '*Defender*'
    ```
*   **Query a specific service by name:**
    ```powershell
    Get-Service -Name WinDefend
    ```
    *(Note: You must use the actual `ServiceName`, not the `DisplayName`)*.

### Starting and Stopping Services
*   **Start a service:**
    ```powershell
    Start-Service -Name WinDefend
    ```
*   **Stop a service:**
    ```powershell
    Stop-Service -Name Spooler
    ```

### Modifying Services (`Set-Service`)
The `Set-Service` cmdlet is used to modify the properties of an existing service, such as its startup type.

*   **Example: Disabling the Print Spooler service:**
    ```powershell
    # Set the startup type of the Spooler service to Disabled
    Set-Service -Name Spooler -StartupType Disabled
    
    # Verify the change
    Get-Service -Name Spooler | Select-Object Name, StartType
    ```

---

## 4. Remote Service Management

PowerShell makes it easy to manage services on remote computers, provided you have the necessary permissions and WinRM (Windows Remote Management) is enabled.

### Using the `-ComputerName` Parameter
Many cmdlets, including `Get-Service`, have a built-in `-ComputerName` parameter.

```powershell
# Get all running services from a remote Domain Controller
Get-Service -ComputerName ACADEMY-ICL-DC | Where-Object {$_.Status -eq "Running"}
```

### Using `Invoke-Command`
For more complex operations or for running commands on multiple machines at once, the `Invoke-Command` cmdlet is used.

*   **Syntax:** `Invoke-Command -ComputerName <hosts> -ScriptBlock { <commands_to_run> }`
*   **Example: Checking the status of the `windefend` service on two machines:**
    ```powershell
    Invoke-Command -ComputerName ACADEMY-ICL-DC,LOCALHOST -ScriptBlock { Get-Service -Name 'windefend' }
    ```
**Key Takeaway:** PowerShell's object-oriented nature and powerful remoting capabilities make it an incredibly efficient tool for managing and enumerating services at scale across an entire network.
