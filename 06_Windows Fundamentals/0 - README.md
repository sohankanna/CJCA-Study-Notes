# Module: Windows Fundamentals

This module provides a comprehensive introduction to the Microsoft Windows operating system, a dominant force in both desktop and enterprise environments. The notes cover the foundational structure of Windows, its core security principles, and the essential tools used for both graphical and command-line interaction.

A deep understanding of Windows is non-negotiable for a cybersecurity professional. The majority of corporate networks are built around Windows and Active Directory, making it a primary target in most penetration testing engagements. This module lays the groundwork for understanding how to navigate, manage, and ultimately assess the security of Windows systems.

---

## Module Sections (Notes)

Below is a list of the topics covered in this module, organized to build a solid, practical foundation in the Windows operating system.

### 1. The Core of the Operating System
*   **Introduction to Windows:** A high-level overview of the history of Windows desktop and server editions, the importance of legacy systems, and the common methods for remote access, with a focus on **RDP**.
*   **Operating System Structure:** A breakdown of the standard Windows filesystem hierarchy, detailing the purpose of key directories like `C:\Windows`, `C:\Users`, and `C:\Program Files`.
*   **File System:** An explanation of the Windows file systems, focusing on the features and granular permission model of **NTFS**.

### 2. Permissions and Access Control
*   **NTFS vs. Share Permissions:** A critical comparison of the two layers of permissions that govern access to network shares and the golden rule of how they interact.
*   **Service Permissions:** A deep dive into the security of Windows services, covering service accounts, common misconfigurations, and how they can be a vector for privilege escalation.
*   **Windows Sessions:** Explains the difference between interactive and non-interactive sessions and details the built-in, non-interactive accounts (`LocalSystem`, `NetworkService`, `LocalService`).

### 3. Interacting with and Managing Windows
*   **Interacting with the Windows Operating System:** Compares the GUI with the two primary command-line shells: the legacy **Command Prompt (CMD)** and the modern, powerful **PowerShell**.
*   **Windows Management Instrumentation (WMI):** Covers the WMI framework, a core technology for querying system information and performing administrative tasks on local and remote machines.
*   **Microsoft Management Console (MMC):** Explains the MMC framework and the concept of "snap-ins," the modular tools used for graphical administration (e.g., `services.msc`, `eventvwr.msc`).
*   **Windows Subsystem for Linux (WSL):** An introduction to the compatibility layer that allows for running native Linux tools and environments directly on Windows.

### 4. Security Concepts
*   **Desktop Experience vs. Server Core:** Compares the full GUI installation of Windows Server with the minimal, command-line-only Server Core, highlighting the security benefits of a smaller attack surface.
*   **Windows Security:** A summary of fundamental Windows security mechanisms, including **Security Identifiers (SIDs)**, the **Access Control Model (ACLs)**, **User Account Control (UAC)**, the **Registry**, **AppLocker**, and **Windows Defender**.
