# Backup and Restores
1. Key Backup Tools in Linux

While many backup solutions exist, they often build upon a few core, powerful command-line utilities.

| Tool | Description | Key Feature |
| :--- | :--- | :--- |
| **`rsync`** | An open-source utility for fast, incremental file transfers. | **Efficiency.** It only transfers the parts of files that have actually changed (delta transfer), making it extremely fast for synchronizing large directories, especially over a network. |
| **`duplicity`**| A command-line backup tool that builds upon `rsync`. | **Encryption.** It adds a layer of GnuPG encryption to the backups, making it ideal for storing sensitive data on untrusted, remote servers or in the cloud. |
| **`Deja Dup`**| A user-friendly, graphical backup tool. | **Simplicity.** It provides an easy-to-use interface for desktop users while using the power of `duplicity` (and therefore `rsync`) in the background. |

**Analogy:**
*   `rsync` is a high-speed transport for your valuables.
*   `duplicity` is that same transport, but it puts your valuables inside an encrypted, armored safe first.
*   `Deja Dup` is the simple, one-button control panel for the armored safe transport.

---

## 2. Using `rsync`

`rsync` is the foundational tool for most advanced backup and synchronization tasks on Linux.

### Basic Syntax and Options
*   `-a` (archive): A meta-flag that preserves permissions, timestamps, ownership, and symbolic links. **Almost always use this.**
*   `-v` (verbose): Shows detailed output of the files being transferred.
*   `-z` (compress): Compresses the file data during the transfer, which can speed up transfers over slow networks.
*   `--delete`: Deletes files on the destination if they have been removed from the source, keeping the two locations in perfect sync.
*   `-e ssh`: Tells `rsync` to use **SSH** as its transport protocol, encrypting the entire transfer.

### Common `rsync` Commands

*   **Install `rsync`:**
    ```shell
    sudo apt install rsync -y
    ```

*   **Backup a Local Directory to a Remote Server:**
    ```shell
    # The trailing slash on the source directory is important!
    # It means "copy the contents of mydirectory", not the directory itself.
    rsync -avz /path/to/mydirectory/ user@backup_server:/path/to/backup/
    ```

*   **Restore a Directory from the Backup Server:**
    ```shell
    rsync -avz user@backup_server:/path/to/backup/ /path/to/restored_directory/
    ```

*   **Secure Transfer using SSH:**
    ```shell
    rsync -avz -e ssh /path/to/mydirectory/ user@backup_server:/path/to/backup/
    ```

---

## 3. Automating Backups with `cron` and SSH Keys

To automate `rsync` backups without needing to manually enter a password each time, you can combine a `cron` job with SSH key-based authentication.

### Step 1: Set Up Passwordless SSH Login
This only needs to be done once.

1.  **Generate an SSH key pair on your local machine:**
    ```shell
    ssh-keygen -t rsa -b 4096
    ```
    *(Press Enter through the prompts to accept the defaults and create a key without a passphrase for automation).*

2.  **Copy your public key to the remote backup server:**
    ```shell
    ssh-copy-id user@backup_server
    ```
    You can now `ssh user@backup_server` without being prompted for a password.

### Step 2: Create a Backup Script
Create a simple shell script that contains your `rsync` command.

*   **File:** `~/scripts/rsync_backup.sh`
*   **Content:**
    ```bash
    #!/bin/bash
    rsync -avz -e ssh /path/to/mydirectory/ user@backup_server:/path/to/backup/
    ```
*   **Make the script executable:**
    ```shell
    chmod +x ~/scripts/rsync_backup.sh
    ```

### Step 3: Schedule the Script with `cron`
Edit your user's crontab to run the script on a schedule.

1.  **Open the crontab editor:**
    ```shell
    crontab -e
    ```
2.  **Add the schedule line:**
    This example will run the backup script at the top of every hour.
    ```cron
    0 * * * * /home/hacker/scripts/rsync_backup.sh
    ```
3.  **Save and exit.** The backup process is now fully automated.
