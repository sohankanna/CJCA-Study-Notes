# Bourne Again Shell (BASH)

## What is Bash Scripting?

**Bash scripting** is the process of writing a series of commands in a plain text file that the Bash interpreter can execute sequentially.

*   **Scripting vs. Programming:** The key difference is that scripting languages (like Bash, Python, PowerShell) are **interpreted**, meaning they are read and executed line-by-line by an interpreter program. Programming languages (like C++ or Java) are **compiled**, meaning the source code is first converted into a machine-readable executable file.
*   **Why it's important:** Scripting allows us to automate repetitive or complex tasks. For a penetration tester, this means automating enumeration, processing large amounts of data from scans, or creating custom tools on the fly.

### Core Scripting Concepts
Like a programming language, a scripting language includes fundamental building blocks:
*   Input & Output
*   Variables & Arrays
*   Conditional Execution (`if`/`else`)
*   Loops (`for`, `while`)
*   Arithmetic
*   Comparison Operators
*   Functions

---

## Executing a Bash Script

A Bash script is simply a text file containing commands. There are several ways to execute it.

1.  **Explicitly with the Interpreter:**
    You can directly tell the `bash` (or `sh`) interpreter to run your script. This method does **not** require the script file to have execute permissions.
    ```shell
    bash script.sh
    # OR
    sh script.sh
    ```

2.  **Making the Script Executable:**
    This is the more common method. It involves two steps:
    *   **Add a "shebang" line:** The very first line of your script should be `#!/bin/bash`. This special line, called a shebang, tells the operating system which interpreter to use to run the script.
    *   **Set execute permissions:** Use the `chmod` command to make the file executable.
        ```shell
        chmod +x script.sh
        ```
    *   Now you can run the script directly by its path:
        ```shell
        ./script.sh
        ```

---

## Anatomy of a Sample Script (`CIDR.sh`)

The provided `CIDR.sh` script is a great example of how different Bash concepts are combined to create a useful tool. Let's break down its structure.

*   **Script Goal:** Take a domain name as input, find its IP address(es), and then offer options to find the network range (CIDR block) and ping the hosts.

### The Five Main Parts of the Script

1.  **Check for Arguments (`if [ $# -eq 0 ]`)**
    *   **Purpose:** This is input validation. It checks if the user provided a domain name when running the script. `$#` is a special variable that holds the number of arguments given.
    *   **Logic:** If no arguments are given (`$#` is equal to `0`), it prints a usage message and exits. Otherwise, it assigns the first argument (`$1`) to a variable named `domain`.

2.  **Identify IP Address (`host $domain ...`)**
    *   **Purpose:** This is the initial reconnaissance step.
    *   **Logic:** It uses the `host` command to perform a DNS lookup, `grep` to find the line with the IP, `cut` to extract only the IP address, and `tee` to save the discovered IPs to a file.

3.  **Define Functions (`function network_range { ... }`)**
    *   **Purpose:** The script uses functions to organize reusable blocks of code.
    *   **`network_range` function:** Takes an IP address, uses the `whois` command to look up its registration details, and extracts the `NetRange` and `CIDR` information.
    *   **`ping_host` function:** Takes a list of IPs, loops through them, and uses the `ping` command to check if each host is online.

4.  **Present Available Options (`case $opt in ... esac`)**
    *   **Purpose:** Provides a user-friendly menu to the user.
    *   **Logic:** It uses the `read` command to prompt the user for input and a `case` statement (similar to a `switch` statement in other languages) to execute the correct function(s) based on the user's choice.

5.  **Putting It All Together:** The script first gets the IP, then shows the menu, and finally calls the appropriate functions based on user input. This demonstrates how a simple idea can be built into a structured, interactive, and useful tool through scripting.
