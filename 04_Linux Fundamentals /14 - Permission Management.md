# Permission Management

 1. The Three Basic Permissions

Every file and directory in Linux has a set of three basic permissions.

| Permission | Character | For a File | For a Directory |
| :--- | :--- | :--- | :--- |
| **Read** | `r` | Allows the contents of the file to be viewed. | Allows the contents of the directory (i.e., the list of filenames) to be viewed. |
| **Write** | `w` | Allows the contents of the file to be modified. | Allows items within the directory to be created, deleted, or renamed. |
| **Execute** | `x` | Allows the file to be run as a program or script. | Allows the user to **enter** (or "traverse") the directory. **This is critical.** Without `x`, you cannot `cd` into a directory, even if you can read its contents. |

---

## 2. Permission Groups

These permissions are assigned to three distinct categories of users.

| Category | Description |
| :--- | :--- |
| **User (Owner)** | The specific user who owns the file. |
| **Group** | The group that is associated with the file. Any user who is a member of this group gets these permissions. |
| **Others (World)**| Everyone else on the system who is not the owner and not in the group. |

### Reading `ls -l` Output
The `ls -l` command displays these permissions in a 10-character string.

`-rwxr-xr--`

| Position | Meaning |
| :--- | :--- |
| **1** | **File Type:** `-` for a regular file, `d` for a directory, `l` for a symbolic link. |
| **2-4** | **User (Owner) Permissions:** `rwx` (Read, Write, Execute). |
| **5-7** | **Group Permissions:** `r-x` (Read, no Write, Execute). |
| **8-10** | **Others Permissions:** `r--` (Read, no Write, no Execute). |

---

## 3. Changing Permissions (`chmod`)

The `chmod` (change mode) command is used to modify file and directory permissions. There are two ways to use it: symbolic and octal.

### Symbolic Method
Uses letters (`u, g, o, a`) and symbols (`+, -, =`) to modify permissions.
*   **Users:** `u` (user/owner), `g` (group), `o` (others), `a` (all).
*   **Operators:** `+` (add permission), `-` (remove permission), `=` (set permission exactly).
*   **Example:** Give all users read permission.
    ```shell
    chmod a+r shell
    ```

### Octal (Numeric) Method
This is the more common and faster method. It uses a 3-digit octal number to represent the permissions for the user, group, and others, respectively.

Each permission has a numeric value:
*   **Read (r) = 4**
*   **Write (w) = 2**
*   **Execute (x) = 1**

You add the values together for each category (user, group, others) to get the final octal number.

| Permissions | Octal Value | Calculation |
| :--- | :--- | :--- |
| `rwx` | **7** | 4 + 2 + 1 |
| `rw-` | **6** | 4 + 2 + 0 |
| `r-x` | **5** | 4 + 0 + 1 |
| `r--` | **4** | 4 + 0 + 0 |

*   **Example:** Set permissions to `rwxr-xr--` (`754`).
    ```shell
    chmod 754 shell
    ```

---

## 4. Changing Ownership (`chown`)

The `chown` (change owner) command is used to change the user and/or group ownership of a file or directory.

*   **Syntax:** `chown <user>:<group> <file/directory>`
*   **Example:** Change the owner of the `shell` file to `root` and the group to `root`.
    ```shell
    sudo chown root:root shell
    ```

---

## 5. Special Permissions

These are advanced permissions that grant temporary elevated privileges.

### SUID (Set User ID)
*   **Permission:** `s` in the user's execute permission slot (e.g., `-rwsr-xr-x`).
*   **What it does:** When an executable file with the SUID bit is run, it executes with the permissions of the **file's owner**, not the user who ran it.
*   **Security Risk:** This is a major security concern. If a file owned by `root` has the SUID bit, any user who can execute it will run it **as root**. If that program has a vulnerability (e.g., a function to spawn a shell), it can lead to full system compromise.
*   **Resource:** **GTFOBins** is a curated list of Unix binaries that can be abused to bypass local security restrictions.

### SGID (Set Group ID)
*   **Permission:** `s` in the group's execute permission slot (e.g., `-rwxr-sr-x`).
*   **What it does:**
    *   **On a file:** The program executes with the permissions of the **file's group**.
    *   **On a directory:** Any new file created inside that directory will automatically inherit the group ownership of the directory itself, not the primary group of the user who created it. This is useful for shared project folders.

### Sticky Bit
*   **Permission:** `t` in the others' execute permission slot (e.g., `drwxrwxrwt`).
*   **What it does:** When set on a directory, it restricts file deletion. A user can create and modify files in the directory, but they can only delete or rename files that **they themselves own**.
*   **Use Case:** The `/tmp` directory. This allows all users to create temporary files, but prevents one user from deleting another user's files.
*   **`t` vs `T`:** A lowercase `t` means the sticky bit and execute permissions are set. An uppercase `T` means the sticky bit is set, but execute permissions are **not** set for "others."
