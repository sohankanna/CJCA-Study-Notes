# Finding & Filtering Content


## 1. The PowerShell Philosophy: Everything is an Object

Unlike traditional shells that deal with plain text, in PowerShell, **everything is an object**.

*   **Object:** An instance of a class, containing data (**properties**) and actions that can be performed (**methods**).
*   **Analogy:** Think of a "user" object. Its *properties* are things like `Name`, `Enabled`, `SID`, and `PasswordLastSet`. Its *methods* are actions you can perform, like `Clone()` or `ToString()`.
*   **Why it Matters:** Because the output of a command is a structured object, you can access its properties by name and pipe (`|`) the entire object to another command for precise filtering, sorting, and manipulation.

### Exploring Objects (`Get-Member`)
The `Get-Member` cmdlet (alias: `gm`) is an introspection tool that shows you all the properties and methods of a given object. It's how you discover what you can do with an object.
```powershell
# Get the 'administrator' user object and pipe it to Get-Member
Get-LocalUser administrator | Get-Member
```

---

## 2. Filtering and Formatting Objects

Once you have a collection of objects (e.g., from `Get-Service` or `Get-Process`), you can use several key cmdlets to refine and display the output.

### `Select-Object` (alias: `select`)
*   **Purpose:** To select specific **properties** from an object. This is how you trim down a large, verbose output to show only the information you care about.
    ```powershell
    # Get all local users but only show their Name and PasswordLastSet properties
    Get-LocalUser * | Select-Object -Property Name,PasswordLastSet
    ```

### `Sort-Object` (alias: `sort`)
*   **Purpose:** To sort a collection of objects based on the value of one or more of their properties.
    ```powershell
    # Get all services, sort them alphabetically by their DisplayName
    Get-Service | Sort-Object -Property DisplayName
    ```

### `Group-Object` (alias: `group`)
*   **Purpose:** To group objects that have the same value for a specific property.
    ```powershell
    # Get all users and group them by whether their account is enabled or not
    Get-LocalUser * | Group-Object -Property Enabled
    ```

### `Where-Object` (alias: `where` or `?`)
*   **Purpose:** This is the primary cmdlet for **filtering** a collection of objects. It keeps only the objects where a specified condition is true.
*   **Syntax:** `... | where { $_.PropertyName -operator "Value" }`
    *   `$_`: The automatic variable representing the **current object** in the pipeline.
*   **Comparison Operators:**
    *   `-like`: Wildcard matching (`*` matches any character).
    *   `-contains`: The collection contains a specific value.
    *   `-eq`: Is **eq**ual to (case-insensitive by default).
    *   `-ne`: Is **n**ot **e**qual to.
    *   `-gt` / `-ge`: **G**reater **t**han / **G**reater than or **e**qual to.
    *   `-lt` / `-le`: **L**ess **t**han / **L**ess than or **e**qual to.
    *   `-match`: Regular expression matching.

*   **Example: Finding Defender Services**
    ```powershell
    Get-Service | where DisplayName -like '*Defender*'
    ```

---

## 3. Searching for Text within Files (`Select-String`)

The **`Select-String`** cmdlet (alias: `sls`) is the PowerShell equivalent of `grep` or `findstr`. It searches for text patterns within files or string input.

*   **Syntax:** `Select-String -Pattern "pattern" -Path <path>`
*   **Example (with piping):**
    ```powershell
    # Get all .txt files recursively and pipe them to Select-String
    # Search for lines containing "Password", "credential", or "key"
    Get-ChildItem -Path C:\Users\MTanaka\ -Filter "*.txt" -Recurse | Select-String "Password","credential","key"
    ```

---

## 4. The PowerShell Pipeline (`|`)

The **pipeline** is the mechanism that allows you to chain commands together, passing the object output of one cmdlet as the input to the next.

*   **How it Works:** The pipeline executes commands from left to right.
*   **Example (a complex chain):**
    ```powershell
    # Get all running processes, sort them by CPU usage (descending), select the top 5,
    # and display their Name and CPU properties in a formatted table.
    Get-Process | Sort-Object CPU -Descending | Select-Object -First 5 | Format-Table Name, CPU
    ```

### Pipeline Chain Operators (`&&` and `||`)
**(Note: Requires PowerShell 7 or newer)**
*   **`&&` (AND):** Executes the next command in the pipeline **only if** the previous command succeeded.
*   **`||` (OR):** Executes the next command in the pipeline **only if** the previous command failed.

---

## 5. Interesting Locations for File Hunting

When enumerating a host, focus your searches on these high-value locations:
*   **User AppData:** `%APPDATA%` and `%LOCALAPPDATA%` (often contain config files, saved credentials).
*   **User Home Folder:** `%USERPROFILE%` (check for SSH keys, VPN configs, scripts).
*   **PowerShell History:** The persistent history file contains a record of commands run by the user. A goldmine.
    *   `Get-Content (Get-PSReadlineOption).HistorySavePath`
*   **User's Clipboard:** `Get-Clipboard` can sometimes reveal recently copied sensitive information.
*   **Scheduled Tasks:** Check for scripts or executables run by scheduled tasks.
