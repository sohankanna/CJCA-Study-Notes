# Command Prompt Basics

## 1. What is `cmd.exe`?

The **Command Prompt** (or **CMD**) is the default, legacy command-line interpreter for the Windows operating system. It provides a text-based interface for users to execute commands and interact directly with the OS.

*   **Core Idea:** It is a simple, direct way to control the system without a graphical user interface (GUI), which can be faster and more resource-efficient for many tasks.
*   **Security Relevance:** Attackers often use CMD for their operations. Even on a modern, PowerShell-hardened system, an attacker may be able to fall back to using `cmd.exe` and its built-in commands ("living off the land") to perform reconnaissance and lateral movement.

---

## 2. Accessing the Command Prompt

You can open a Command Prompt session through both local and remote access methods.

### Local Access
This refers to having direct physical (or virtual, in a VM) access to the machine.
*   **Run Dialog:** Press `Windows Key + R`, type `cmd`, and press Enter.
*   **Start Menu:** Search for "Command Prompt" or "cmd".
*   **Direct Path:** Execute the binary directly from `C:\Windows\System32\cmd.exe`.

### Remote Access
This refers to accessing the machine over a network. Common methods to gain a remote command shell include:
*   **Secure Shell (SSH):** If an SSH server is running on the Windows host.
*   **PsExec:** A Sysinternals tool that allows command execution on remote systems via SMB.
*   **WinRM (PowerShell Remoting):** The modern standard for Windows remote management.

---

## 3. Basic Usage and Navigation

The Command Prompt operates on a simple request-response model: you type a command, press Enter, and the system provides the output.

### The Command Prompt Interface
```
Microsoft Windows [Version 10.0.19044.2006]
(c) Microsoft Corporation. All rights reserved.

C:\Users\htb>
```
*   `C:\Users\htb>`: This is the **prompt**. It shows your current working directory.
*   The blinking cursor indicates that the shell is ready to accept a command.

### The `dir` Command
The `dir` command is the fundamental tool for listing the contents of a directory.

```powershell
C:\Users\htb\Desktop> dir
  
 Volume in drive C has no label.
 Volume Serial Number is DAE9-5896

 Directory of C:\Users\htb\Desktop

06/11/2021  11:59 PM    <DIR>          .
06/11/2021  11:59 PM    <DIR>          ..
06/11/2021  11:57 PM                 0 file1.txt
...
```
The output provides information such as the timestamp of the last modification, whether an item is a file or a directory (`<DIR>`), and the item's name.

---

## 4. Security Case Study: The "Sticky Keys" Bypass

The power of having command-line access, even in a limited environment, can lead to a full system compromise. The "Sticky Keys" attack is a classic example of physical access leading to privilege escalation.

*   **The Scenario:** An attacker has physical access to a locked machine but cannot log in.
*   **The Method:**
    1.  The attacker boots the machine from a **Windows installation or recovery disk**.
    2.  From the recovery environment, they open a Command Prompt.
    3.  They use `cmd.exe` to navigate the filesystem and **replace the "Sticky Keys" accessibility executable** (`C:\Windows\System32\sethc.exe`) with a **copy of `cmd.exe`**.
*   **The Result:**
    1.  The attacker reboots the machine back to the normal login screen.
    2.  They press the `Shift` key five times.
    3.  Instead of the normal Sticky Keys prompt, a **Command Prompt window opens**.
    4.  Crucially, this command prompt is running with the highest privileges: **`NT AUTHORITY\SYSTEM`**. The attacker has now completely bypassed authentication and has full control over the machine.
