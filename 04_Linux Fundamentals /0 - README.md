# Module: Linux Fundamentals

This module provides a comprehensive introduction to the Linux operating system, a cornerstone technology in the world of servers, cloud computing, and cybersecurity. The notes cover the foundational structure and philosophy of Linux, essential command-line skills, and key administrative concepts.

Mastering these fundamentals is non-negotiable for any aspiring cybersecurity professional, as the command line is the primary interface for system administration, security auditing, and penetration testing on the vast majority of servers.

---

## Module Sections (Notes)

Below is a list of the topics covered in this module, organized to build a strong, practical foundation in Linux.

### 1. The Core Concepts
*   **Linux Structure:** Explains the history, philosophy, core components, architecture, and the Filesystem Hierarchy Standard (FHS).
*   **Linux Distributions:** Describes what a "distro" is and highlights the key characteristics of popular and security-focused distributions like Debian, Ubuntu, and Parrot OS.

### 2. The Shell Environment
*   **Introduction to Shell:** Defines the relationship between the shell, the terminal, and the kernel.
*   **The Shell Prompt:** Breaks down the anatomy of the BASH prompt and how it's customized with the `PS1` variable.
*   **Getting Help:** Covers the essential commands for self-help in the terminal: `man`, `--help`, and `apropos`.

### 3. Essential Command-Line Skills
*   **System Information:** A tour of the first commands to run on any new system to gain situational awareness (`whoami`, `id`, `uname`, `ip`, `ps`, etc.).
*   **Navigation:** Covers the fundamental commands for moving around the filesystem (`pwd`, `ls`, `cd`).
*   **Working with Files & Directories:** Details the commands for basic file management (`touch`, `mkdir`, `mv`, `cp`, `tree`).
*   **Editing Files:** An introduction to the two most common command-line text editors: the beginner-friendly `nano` and the powerful `vim`.
*   **Find Files & Directories:** Explores the powerful search tools `which`, `find`, and the fast database-driven `locate`.
*   **File Descriptors & Redirections:** Explains the core concepts of STDIN, STDOUT, STDERR, and how to control I/O with redirection (`>`, `>>`, `<`) and pipes (`|`).
*   **Filter Content:** A deep dive into the text-processing toolkit (`less`, `head`, `tail`, `grep`, `sort`, `cut`, `awk`, `sed`, `wc`) to manipulate and filter command output.
*   **Regular Expressions:** An introduction to the powerful pattern-matching language used by tools like `grep` to perform advanced searches.

### 4. System Administration
*   **Permission Management:** Covers the Linux permission model (Read, Write, Execute), user/group/other categories, and the `chmod` command. Also explains special permissions like SUID, SGID, and the Sticky Bit.
*   **User Management:** Details the commands for creating, modifying, and deleting users and groups (`useradd`, `usermod`, `passwd`, etc.) and for escalating privileges (`sudo`, `su`).
*   **Package Management:** Explains how to install, update, and remove software using package managers like `apt` and `dpkg`, and how to clone source code with `git`.
*   **Service & Process Management:** Covers the management of background services (daemons) with `systemctl` and the control of running processes (`ps`, `kill`, job control).
*   **Task Scheduling:** Details how to automate tasks using the modern `systemd` timers and the classic `cron` utility.
*   **Network Services:** An overview of configuring and managing key network services like SSH, NFS, and web servers (Apache, Python).
*   **Working with Web Services:** A practical look at interacting with web servers from the command line using tools like `curl` and `wget`.
*   **Backup and Restore:** Explores the use of `rsync` for efficient, automated backups, secured with SSH and scheduled with `cron`.
*   **File System Management:** Covers Linux file system types (ext4, Btrfs), the role of inodes, and the management of physical disks with `fdisk` and `mount`.
*   **Containerization:** An introduction to the concepts of containers, comparing them to VMs, with a focus on Docker and LXC.
*   **Network Configuration:** Details the commands and files used to configure network interfaces, IP addresses, and DNS settings.
*   **Remote Desktop Protocols:** An overview of graphical remote access protocols relevant to Linux, including VNC and X11 Forwarding.
*   **Linux Security:** A summary of essential security hardening best practices, including system updates, access control, MAC systems (SELinux/AppArmor), and tools like TCP Wrappers.
*   **Firewall Setup:** A foundational look at the `iptables` framework, covering its tables, chains, rules, and targets for building a host-based firewall.
*   **System Logs:** Explains the importance of logs for security and troubleshooting, covering the key log files in `/var/log` (e.g., `syslog`, `auth.log`) and how to analyze them.
