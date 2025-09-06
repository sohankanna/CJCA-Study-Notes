# Package Management

## What is a Package Manager?

A **package manager** is a collection of tools that automates the entire lifecycle of software on an operating system. It handles tasks like:
*   Downloading software from trusted online sources called **repositories**.
*   **Dependency resolution:** Automatically identifying and installing any other required software (libraries, etc.) that a package needs to function.
*   Keeping track of all installed files for clean updates and removals.
*   Ensuring system integrity and quality control.

### Common Package Managers by Distro Family

| Distro Family | Package Manager Tools | Package File Format |
| :--- | :--- | :--- |
| **Debian / Ubuntu / Parrot** | `apt`, `apt-get`, `dpkg` | `.deb` |
| **Red Hat / Fedora / CentOS**| `dnf`, `yum`, `rpm` | `.rpm` |

### Language-Specific Package Managers
Many programming languages have their own package managers for installing libraries and modules.
*   **Python:** `pip`
*   **Ruby:** `gem`
*   **Node.js:** `npm`

---

## `apt` - The Advanced Package Tool (Debian/Ubuntu)

**APT** is the high-level, user-friendly command-line interface for managing packages on Debian-based systems. It is the primary tool you will use.

### 1. Updating the Package List
Before installing or upgrading, you must always update your local list of available packages from the repositories.

```shell
sudo apt update
```

### 2. Upgrading Installed Packages

To upgrade all installed packages on your system to their latest versions:

```shell
    sudo apt upgrade -y
```

### 3. Searching for Packages

The apt-cache search command allows you to search the package database for a specific keyword.

```shell
 apt-cache search impacket
```

The apt-cache show command gives detailed information about a specific package.

```shell
apt-cache show impacket-scripts
```

### 4. Installing a Package

The apt install command downloads and installs a package and all of its dependencies.

```shell
sudo apt install impacket-scripts -y
```

- The -y flag automatically answers "yes" to any confirmation prompts.

### Removing a Package

| Command                   | Description                                                                                                  |
| ------------------------- | ------------------------------------------------------------------------------------------------------------ |
| sudo apt remove <package> | Removes the package but leaves its configuration files behind.                                               |
| sudo apt purge <package>  | Removes the package **and** all of its configuration files.                                                  |
| sudo apt autoremove       | Removes any packages that were installed as dependencies but are no longer needed by any installed software. |



## dpkg - Debian Package Manager (Low-Level)

**dpkg** is the underlying, lower-level tool that apt uses to handle the actual installation and removal of .deb files. You typically use dpkg to install a .deb file that you have downloaded manually.

- **Key Difference:** dpkg **does not** handle dependency resolution. If you try to install a .deb file with dpkg and it has missing dependencies, the installation will fail. apt is almost always the better choice.
    
- **Installation Syntax:**
```shell
wget http://example.com/package.deb
sudo dpkg -i package.deb
```


## git - Version Control System

While not a traditional package manager, git is an essential tool for obtaining software, especially security tools, directly from their source code repositories (most commonly on GitHub).

- **Cloning a Repository:** The git clone command downloads a copy of a remote repository to your local machine.

```shell
mkdir ~/nishang
git clone https://github.com/samratashok/nishang.git ~/nishang
```
