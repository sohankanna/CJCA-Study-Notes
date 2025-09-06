# User Management

## 1. Executing Commands as Another User

Often, a standard user needs to perform an administrative task that requires elevated privileges. Linux provides two primary commands for this.

### `sudo` (Superuser Do)
*   **What it is:** The `sudo` command allows a permitted user to execute a single command with the security privileges of another user, which by default is the **root** (superuser).
*   **Why it's used:** This is the **preferred method** for administrative tasks. It allows users to perform specific privileged actions without needing to log in as the `root` user directly, which is a major security best practice. It also creates a log of which user ran which command.
*   **Configuration:** Which users can use `sudo` and what commands they are allowed to run is configured in the `/etc/sudoers` file.
*   **Example:** A standard user cannot read the sensitive `/etc/shadow` file. Using `sudo` allows them to do so (if they have permission).
    ```shell
    hacker@htb[~]$ cat /etc/shadow
    cat: /etc/shadow: Permission denied

    hacker@htb[~]$ sudo cat /etc/shadow
    [sudo] password for hacker:
    root:$6$....:18395:0:99999:7:::
    ...
    ```

### `su` (Switch User)
*   **What it is:** The `su` command is used to switch to another user account and start a **new interactive shell session** as that user.
*   **Usage:**
    *   `su - <username>`: Switches to the specified user's account, requiring their password. The `-` simulates a full login, loading that user's environment.
    *   `su` (with no username): Attempts to switch to the `root` user, requiring the `root` password.
*   **`sudo` vs. `su`:** Use `sudo` to run a single command as root. Use `su` to become the root user for an entire shell session. For most tasks, `sudo` is safer and more auditable.

---

## 2. Managing Users

These commands are used to create, modify, and delete user accounts. They typically require `sudo` privileges to run.

| Command | Description | Example |
| :--- | :--- | :--- |
| **`useradd`** | Creates a new user account. | `sudo useradd -m -s /bin/bash newuser` <br> (`-m` creates a home directory, `-s` sets the default shell). |
| **`usermod`** | Modifies an existing user account. Very useful for adding a user to a group. | `sudo usermod -aG sudo newuser` <br> (`-aG` appends the user to the `sudo` group). |
| **`userdel`** | Deletes a user account. | `sudo userdel -r newuser` <br> (`-r` removes the user's home directory as well). |
| **`passwd`** | Used to set or change a user's password. | `sudo passwd newuser` (to set a password for `newuser`). <br> `passwd` (by itself, to change your own password). |

---

## 3. Managing Groups

These commands are used to create and delete groups.

| Command | Description | Example |
| :--- | :--- | :--- |
| **`addgroup`**| Creates a new group on the system. | `sudo addgroup developers` |
| **`delgroup`**| Removes a group from the system. | `sudo delgroup developers` |

**Key Takeaway:** Effective user management relies on the **Principle of Least Privilege**. Users and groups should only be given the absolute minimum permissions required for them to perform their job functions. Regularly auditing user accounts and group memberships is a critical security task.
