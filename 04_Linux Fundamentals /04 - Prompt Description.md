# Prompt Description

## What is a Shell Prompt?

The **shell prompt** is a short line of text that the shell displays to inform the user that it is ready for a new command. The cursor will blink immediately after the prompt.

### Anatomy of a Default BASH Prompt
A standard BASH prompt is designed to provide useful, contextual information at a glance.

**Standard User Prompt:**
```bash
<username>@<hostname>:<current_directory>$
```

Example 

```bash
sohan@pwnbox:~$
```

- sohan: The current **username**.
    
- pwnbox: The **hostname** of the machine you are connected to.
    
- ~: The **current working directory**. The tilde (~) is a special character that is a shortcut for the current user's home directory (e.g., /home/sohan).
    
- $: The **prompt character**, which indicates that you are logged in as a **standard, unprivileged user**

### The Root User Prompt

When you are logged in as the root user (the superuser with full system privileges), the prompt character changes to a hash (#).

**Example:**
```bash
root@pwnbox:/var/www#
```

- #: The prompt character indicating you are the **root user**. This serves as a constant visual warning that the commands you run can have a major impact on the system.
    

### Minimal Prompts

Sometimes, especially on a compromised system or a very basic shell, you may only see the prompt character. It's crucial to recognize what this means.

- $ : A standard user shell.
    
- #: A root user shell.

## Customizing the Prompt (PS1 Variable)

The appearance of the prompt is controlled by a special environment variable called **PS1**. By changing the value of PS1, you can customize the information your prompt displays.

This is often done in the user's shell configuration file (e.g., ~/.bashrc) to make the changes permanent.

### Common PS1 Special Characters

You can use special backslash-escaped characters to add dynamic information to your prompt.

| Character | Description                                                |
| --------- | ---------------------------------------------------------- |
| \u        | The current **username**                                   |
| \h        | The **hostname** (short form)                              |
| \H        | The **full hostname**                                      |
| \w        | The **full path** of the current working directory         |
| \d        | The current date (e.g., Mon Feb 06)                        |
| \t        | The current time (24-hour HH:MM:SS)                        |
| \n        | A new line                                                 |
| \$        | Displays a $ for a standard user, or a # for the root user |

### Why Customize the Prompt?

For a penetration tester, customizing the prompt can be very useful for documentation and situational awareness. You can add things like:

- The IP address of the target machine.
    
- Timestamps for each command.
    
- The exit code of the last command (to see if it succeeded or failed).

