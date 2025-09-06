# Task Scheduling

Task scheduling is a critical feature in Linux that automates the execution of scripts and commands at specified times or intervals. This eliminates the need for manual intervention for routine tasks, ensuring they are performed consistently and reliably.

It is available in all major Linux distributions, including Ubuntu, Red Hat, and Debian (as well as other UNIX-like systems such as Solaris).

**Common Use Cases:**
*   Automatic software updates
*   Executing recurring scripts
*   Database maintenance and cleanup
*   System backups
*   Generating alerts and notifications

> **Analogy:** Think of task scheduling like programming a coffee maker. You set it once to brew at 7 AM every morning. After that, it works automatically without any further action, ensuring your coffee is ready when you wake up.

### Why is this important for Cybersecurity?

As cybersecurity specialists and penetration testers, understanding task scheduling is vital. It's a double-edged sword:
*   **Defense (Blue Team):** You can audit scheduled tasks to find unauthorized or malicious jobs (e.g., a cron job maintaining a backdoor) that attackers use to establish persistence on a compromised system.
*   **Offense (Red Team):** You can use schedulers to maintain persistence, escalate privileges, or execute payloads at specific times to evade detection during a penetration test.

---

## 2. Using `systemd` Timers

`systemd` is a modern system and service manager for Linux. Beyond managing services, it includes **timers** that provide a powerful and flexible alternative to `cron`.

The process involves three main steps:
1.  Create a **service** file that defines the task to be executed.
2.  Create a **timer** file that defines when the service should be run.
3.  Activate the timer.

### Step 1: Create a Service File

The `.service` file specifies *what* to run. It contains the command or the path to the script you want to execute.

First, create the service file using a text editor like `vim` or `nano`:
```bash
sudo vim /etc/systemd/system/mytimer.service
```

Add the following content. The `ExecStart` directive is the most important part, as it points to your script.

```ini
[Unit]
Description=My Custom Service for a Scheduled Task

[Service]
Type=oneshot
ExecStart=/full/path/to/my/script.sh

[Install]
WantedBy=multi-user.target
```
*   **`[Unit]`**: Contains metadata. `Description` is a human-readable summary of the service.
*   **`[Service]`**:
    *   `Type=oneshot`: Indicates that this is a short-lived process that does its job and exits.
    *   `ExecStart`: The full path to the command or script to be executed. **This is the core of your task.**
*   **`[Install]`**:
    *   `WantedBy`: Defines the target to which this service should be linked when enabled. `multi-user.target` is standard for services that should run in a normal multi-user environment.

### Step 2: Create a Timer File

The `.timer` file specifies *when* to run the corresponding `.service` file. The timer file **must have the same name as the service file**, but with a `.timer` extension.

Create the timer file:
```bash
sudo vim /etc/systemd/system/mytimer.timer
```

Add the scheduling logic.

```ini
[Unit]
Description=Runs my custom service on a schedule

[Timer]
# Run 3 minutes after boot
OnBootSec=3min

# Run every 1 hour after the service was last activated
OnUnitActiveSec=1h

# You can also use OnCalendar for cron-like scheduling
# OnCalendar=daily
# OnCalendar=*-*-* 02:00:00

[Install]
WantedBy=timers.target
```
*   **`[Timer]`**: This is the scheduling section.
    *   `OnBootSec`: Triggers the timer a specified duration *after the system boots up*.
    *   `OnUnitActiveSec`: Triggers the timer a specified duration *after the service was last run*. This is ideal for recurring tasks.
    *   `OnCalendar`: A highly flexible option that allows for cron-like, calendar-based scheduling (e.g., daily, weekly, or at a specific time like `02:00`).
*   **`[Install]`**:
    *   `WantedBy=timers.target`: Ensures the timer is activated at boot when enabled.

### Step 3: Activate the Timer

After creating your files, you need to tell `systemd` to recognize them and then start and enable the timer.

1.  **Reload the systemd daemon** to read the new unit files.
    ```bash
    sudo systemctl daemon-reload
    ```

2.  **Start and enable the timer**.
    *   `start` activates the timer immediately in the current session.
    *   `enable` ensures the timer will start automatically on future system boots.
    ```bash
    # Start the timer now
    sudo systemctl start mytimer.timer

    # Enable the timer to start on boot
    sudo systemctl enable mytimer.timer
    ```
> **Note:** You enable the `.timer`, not the `.service`. The timer is responsible for triggering the service.

You can check the status of your timers with:
```bash
systemctl list-timers --all
```

---

## 3. Using `cron` and `crontab`

`cron` is the classic, time-tested utility for running scheduled tasks in Linux. It runs a daemon (`crond`) that wakes up every minute to check for jobs defined in a file called a `crontab`.

### The `crontab` Syntax

Each line in a `crontab` file represents a single job and follows this structure:

```
.---------------- minute (0 - 59)
|  .------------- hour (0 - 23)
|  |  .---------- day of month (1 - 31)
|  |  |  .------- month (1 - 12) OR jan,feb,mar,apr...
|  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
|  |  |  |  |
*  *  *  *  *  /path/to/command_or_script
```

**Special Characters:**
*   `*` (Asterisk): Represents "every". An asterisk in the `hour` field means "every hour".
*   `/` (Slash): Represents a "step" value. `*/15` in the `minute` field means "every 15 minutes".
*   `,` (Comma): Specifies a list of values. `1,15` in the `day of month` field means "on the 1st and 15th of the month".
*   `-` (Hyphen): Specifies a range of values. `1-5` in the `day of week` field means "from Monday to Friday".

### Editing the Crontab

To edit the `crontab` for the current user, use the following command. It will open the file in your default text editor.
```bash
crontab -e
```
To list the current user's scheduled cron jobs:
```bash
crontab -l
```
System-wide cron jobs are typically located in `/etc/crontab` or in directories like `/etc/cron.d/`, `/etc/cron.hourly/`, etc.

### `crontab` Examples

Here is an example `crontab` file with several common tasks:

```crontab
# ------------------ EXAMPLES ------------------

# Run a system update check every 6 hours
0 */6 * * * /path/to/update_software.sh

# Execute a script at midnight on the first day of every month
0 0 1 * * /path/to/scripts/run_scripts.sh

# Run a database cleanup script every Sunday at midnight
0 0 * * 0 /path/to/scripts/clean_database.sh

# Create a full backup every Saturday at 1 AM
0 1 * * 6 /path/to/scripts/backup.sh
```

**Breakdown of Examples:**
1.  **System Update (`0 */6 * * *`):**
    *   `0`: At minute 0.
    *   `*/6`: Every 6th hour (00:00, 06:00, 12:00, 18:00).
    *   `* * *`: Every day of every month.

2.  **Execute Scripts (`0 0 1 * *`):**
    *   `0 0`: At 00:00 (midnight).
    *   `1`: On the 1st day of the month.
    *   `* *`: Every month, any day of the week.

3.  **Cleanup DB (`0 0 * * 0`):**
    *   `0 0`: At 00:00 (midnight).
    *   `* *`: Every day of every month.
    *   `0`: On the 0th day of the week (Sunday).

4.  **Backups (`0 1 * * 6`):**
    *   `0 1`: At 01:00 AM.
    *   `* *`: Every day of every month.
    *   `6`: On the 6th day of the week (Saturday).

---

## 4. `systemd` vs. `cron`: A Comparison

Both tools are excellent for scheduling tasks, but they have different strengths.

| Feature                 | `systemd` Timers                                                                         | `cron` / `crontab`                                                                 |
| ----------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| **Configuration**       | Two separate files (`.service`, `.timer`). More verbose but very explicit and structured. | Single line in a `crontab` file. Simple and concise for basic tasks.               |
| **Logging & Monitoring**| Integrated with `journalctl`. Provides detailed logs, status, and failure reports.       | Traditionally relies on `syslog` or sending an email. Less detailed by default.      |
| **Flexibility**         | Extremely high. Can trigger on events, not just time (e.g., hardware changes, path modifications). | Strictly time-based. Cannot trigger on non-time-related events.                    |
| **Resource Management** | Can use cgroups to precisely control CPU, memory, and I/O for the scheduled task.        | No built-in resource control.                                                      |
| **Environment**         | Runs in a clean, predictable, and configurable environment.                              | Inherits a minimal environment, which can sometimes cause "it works in my shell but not in cron" issues. |
| **Dependencies**        | Can define complex dependencies (e.g., "run this task only after the network is up").      | No built-in dependency management.                                                 |
| **Ease of Use**         | Steeper learning curve, but more powerful.                                               | Very easy to learn for simple time-based scheduling.                               |

### Which Should You Use?

*   **For simple, time-based tasks:** `cron` is quick, easy, and universally available.
*   **For complex scheduling, better logging, and system integration:** `systemd` timers are the more powerful and robust modern choice.
