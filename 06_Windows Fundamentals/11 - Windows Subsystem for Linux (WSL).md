# Windows Subsystem for Linux (WSL)


## What is WSL?

**WSL** is a feature of modern Windows (Windows 10 and later) that enables users, primarily developers and system administrators, to run a genuine GNU/Linux environment directly on their Windows machine.

*   **Core Idea:** It provides the power and flexibility of the Linux command line and its vast ecosystem of tools (`grep`, `sed`, `awk`, `ssh`, etc.) seamlessly integrated into a Windows workflow.
*   **Key Distinction from a VM:**
    *   **WSL 1:** A translation layer that converted Linux system calls into Windows system calls. It did *not* use a real Linux kernel.
    *   **WSL 2:** The modern version. It runs a **real, full Linux kernel** inside a lightweight, highly optimized virtual machine that is tightly integrated with the host Windows OS. This provides much better performance and full system call compatibility.

---

## Installation and Usage

### Enabling WSL
WSL is an optional Windows feature that must be enabled first. This is typically done with a single command in an **administrative PowerShell** prompt.

```powershell
wsl --install
```
*(On older systems, the command was `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`)*

After enabling the feature and rebooting, you can install a Linux distribution.

### Installing a Linux Distribution
*   **Microsoft Store:** The easiest method. You can go to the Microsoft Store and search for distributions like "Ubuntu," "Debian," or "Kali Linux" and install them like any other app.
*   **Manual Installation:** You can also download distro packages and install them from the command line.

### Launching WSL
Once a distro is installed, you can launch its shell in several ways:
*   From the Start Menu, by clicking on the installed distro's icon (e.g., "Ubuntu").
*   By opening a Command Prompt or PowerShell and simply typing `wsl` or `bash`.

---

## Interacting with WSL

Once you are in a WSL shell, you are in a genuine Linux environment.

*   **Linux Filesystem:** You will see the standard Linux filesystem hierarchy (`/`, `/bin`, `/etc`, `/home`, etc.).
    ```shell
    hacker@WSL:~$ ls /
    bin  boot  dev  etc  home  lib  ...
    ```
*   **Linux Kernel:** The `uname -a` command will show that you are running a real Linux kernel, often one specifically compiled by Microsoft for WSL.
    ```shell
    hacker@WSL:~$ uname -a
    Linux WS01 5.10.16.3-microsoft-standard-WSL2 ...
    ```

### Bridging Windows and Linux
A key feature of WSL is the seamless integration between the two filesystems.

*   **Accessing Windows Drives from Linux:** Your local Windows drives (like `C:`) are automatically mounted inside the WSL environment under the `/mnt` directory.
    ```shell
    # List the contents of the Windows C: drive from within WSL
    ls /mnt/c
    ```
*   **Accessing Linux Files from Windows:** The WSL filesystem can be accessed from Windows File Explorer by navigating to the special path `\\wsl$`.

This tight integration allows you to use powerful Linux tools to process files that are stored on your Windows system, combining the strengths of both operating systems.
