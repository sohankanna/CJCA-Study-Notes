# Linux Structure 

**Linux** is an open-source, Unix-like operating system kernel. An **operating system (OS)** is the core software that manages all computer hardware and provides a platform for applications to run.

*   **Kernel:** The central component of the OS. The Linux kernel was created by Linus Torvalds in 1991.
*   **Distribution (Distro):** A complete operating system built around the Linux kernel, bundled with supporting software, libraries, and a package manager.
    *   **Examples:** Debian (which Parrot OS is based on), Ubuntu, Fedora, Red Hat, Arch.
*   **Key Strengths:** Renowned for its stability, flexibility, security, and open-source nature, making it a cornerstone of servers, embedded systems, and cybersecurity work.

---

## The Linux Philosophy

The design of Linux and its ecosystem is guided by a set of core principles that emphasize simplicity and modularity.

| Principle | Description |
| :--- | :--- |
| **1. Everything is a File** | In Linux, nearly every component—including hardware devices, directories, and processes—is represented as a file in the filesystem, allowing them to be manipulated with standard tools. |
| **2. Small, Single-Purpose Programs** | The philosophy encourages creating small, simple tools that do one thing and do it well (e.g., `grep` for searching, `sort` for sorting). |
| **3. Ability to Chain Programs Together** | Complex tasks are achieved by combining these small programs using pipes (`|`) and redirection (`>`, `<`). The output of one program becomes the input for the next. |
| **4. Avoid Captive User Interfaces** | The primary interface is the powerful command-line shell, which provides greater control and automation capabilities than a GUI. |
| **5. Configuration Data Stored in Text Files**| System and application settings are stored in human-readable plain text files, making them easy to view, edit, and manage. |

---

## Linux Architecture

The Linux OS is structured in several distinct layers.

| Layer | Description |
| :--- | :--- |
| **Hardware** | The physical components of the computer (CPU, RAM, disks, etc.). |
| **Kernel** | The **core of the OS**. It directly manages the hardware, acting as a bridge between the hardware and the software applications. |
| **Shell** | The **Command-Line Interface (CLI)**. It is the program that takes commands from the user and passes them to the kernel for execution. (e.g., Bash, Zsh). |
| **System Utilities & Applications**| All the programs and applications that the user interacts with (e.g., file managers, web browsers, and the small, single-purpose tools). |

---

## Key Components of a Linux System

*   **Bootloader:** The first piece of software that runs when the computer starts. Its job is to load the kernel into memory (e.g., **GRUB**).
*   **Kernel:** The core, as described above.
*   **Daemons:** Background services that run automatically to handle system tasks (e.g., networking, scheduling, logging).
*   **Shell:** The command-line interpreter.
*   **Graphical Server (X Server):** The underlying system that draws and manages graphical windows on the screen.
*   **Desktop Environment / Window Manager:** The Graphical User Interface (GUI) that the user sees (e.g., GNOME, KDE, XFCE).

---

## The Filesystem Hierarchy Standard (FHS)

Linux organizes its files in a standardized, tree-like directory structure. The top-level directory is the **root directory (`/`)**.

| Directory | Purpose |
| :--- | :--- |
| **`/`** | **Root** - The top-level directory of the entire filesystem. |
| **`/bin`** | **Essential User Binaries** - Contains fundamental commands needed by all users (e.g., `ls`, `cp`, `mv`). |
| **`/sbin`** | **System Binaries** - Contains essential commands for system administration (e.g., `ifconfig`, `reboot`). |
| **`/etc`** | **Configuration Files** - Contains all system-wide configuration files (e.g., `/etc/passwd`). |
| **`/home`** | **User Home Directories** - Contains a personal directory for each standard user (e.g., `/home/sohan`). |
| **`/root`** | **Root User's Home Directory** - The personal directory for the superuser, `root`. |
| **`/var`** | **Variable Files** - For files whose content is expected to grow, like logs (`/var/log`), mail, and web server content. |
| **`/tmp`** | **Temporary Files** - A world-writable directory for temporary files. Often cleared on reboot. |
| **`/usr`** | **User Programs** - Contains the majority of user-level applications and files (e.g., `/usr/bin`, `/usr/lib`). |
| **`/boot`** | **Bootloader Files** - Contains the files needed to boot the system, including the Linux kernel itself. |
| **`/dev`** | **Device Files** - Contains special files that represent hardware devices (e.g., `/dev/sda` for a hard drive). |
| **`/lib`** | **Essential Shared Libraries** - Contains library files needed by the binaries in `/bin` and `/sbin`. |
| **`/opt`** | **Optional Software** - Often used for installing third-party, self-contained applications. |
| **`/mnt`, `/media`** | **Mount Points** - Temporary mount points for removable media (`/media`) or other filesystems (`/mnt`). |
