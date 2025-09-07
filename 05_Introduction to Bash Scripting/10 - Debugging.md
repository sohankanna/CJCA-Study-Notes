# Debugging

## What is Debugging in Bash?

In the context of Bash scripting, debugging involves running your script in a special mode that provides detailed, step-by-step information about its execution. This helps you trace the flow of your script, see the values of variables at different points, and identify the exact line where an error is occurring.

For a penetration tester, understanding debugging is also a foundational concept for exploit development, where you might intentionally cause a program to crash to analyze its behavior and find vulnerabilities.

---

## Using Bash's Built-in Debugging Options

You can enable Bash's debugging modes by passing options to the `bash` interpreter when you run your script.

### 1. The `-x` Option (xtrace)
The `-x` option enables **trace mode**. This is the **most useful and common** debugging option.

*   **What it does:** Before executing each command, Bash will print the command to the terminal, with all variables and command substitutions expanded.
*   **The Output:** Each traced command is prefixed with a plus sign (`+`).
*   **Why it's useful:** It lets you see the *exact* command that is being run after all the variables have been replaced with their values. This is perfect for spotting typos, incorrect variable assignments, or logic errors.

*   **Syntax:**
    ```shell
    bash -x script.sh
    ```
*   **Example Output:**
    ```shell
    hacker@htb[~]$ bash -x CIDR.sh
    + '[' 0 -eq 0 ']'
    + echo -e 'You need to specify the target domain.\n'
    You need to specify the target domain.

    + echo -e 'Usage:'
    Usage:
    + echo -e '\t./CIDR.sh <domain>'
    	./CIDR.sh <domain>
    + exit 1
    ```
    *(Here you can clearly see the `if` condition `[ 0 -eq 0 ]` being evaluated as true, leading to the execution of the `echo` commands inside the `then` block).*

### 2. The `-v` Option (verbose)
The `-v` option enables **verbose mode**.

*   **What it does:** Bash will print each line from the script to the terminal *before* it is read and executed.
*   **Why it's useful:** It shows you the raw lines from your script as they are being processed. This can be helpful for finding syntax errors.

### 3. Combining `-x` and `-v` for Maximum Detail
You can combine both options for the most detailed debugging output possible.

*   **What it does:** It will first print the raw line from the script (due to `-v`) and then print the expanded, ready-to-execute command (due to `-x`).

*   **Syntax:**
    ```shell
    bash -x -v script.sh
    ```
*   **Example Output:**
    ```shell
    #!/bin/bash
    
    # Check for given argument
    if [ $# -eq 0 ]
    then
        echo -e "You need to specify the target domain.\n"
        echo -e "Usage:"
        echo -e "\t$0 <domain>"
        exit 1
    else
        domain=$1
    fi
    + '[' 0 -eq 0 ']'
    + echo -e 'You need to specify the target domain.\n'
    You need to specify the target domain.
    ...
    ```

---

## In-Script Debugging with `set`

You can also turn debugging on and off for specific sections *within* your script using the `set` command. This is useful for focusing on a problematic part of a very large script.

```bash
#!/bin/bash

echo "Debugging is currently off."

# Turn on trace mode
set -x

# This part of the script will be traced
my_var="test"
if [ "$my_var" == "test" ]; then
    echo "Variable matches."
fi

# Turn off trace mode
set +x

echo "Debugging is off again."

```
