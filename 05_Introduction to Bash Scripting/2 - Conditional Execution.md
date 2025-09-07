# Conditional Execution
 1. The Shebang

The **shebang** is the very first line in a script, and it is essential for making a script directly executable.

*   **Syntax:** `#!<path_to_interpreter>`
*   **Purpose:** It tells the operating system which program (interpreter) should be used to run the rest of the file.
*   **Bash Shebang:**
    ```bash
    #!/bin/bash
    ```
*   **Python Shebang:**
    ```python
    #!/usr/bin/env python3
    ```

---

## 2. The `if` Statement

The `if` statement is the primary structure for conditional execution. It allows a block of code to be executed *only if* a specific condition is true.

### The Structure of an `if` Statement
The basic structure is an `if`, `then`, `else`, and `fi` block. The `else` part is optional.

*   `if [ <condition> ]`: This is where the test is performed. The square brackets `[ ]` are a shorthand for the `test` command. **Note the required spaces inside the brackets.**
*   `then`: If the condition is true, the commands following `then` are executed.
*   `else`: (Optional) If the condition is false, the commands following `else` are executed.
*   `fi`: Marks the end of the `if` block (which is "if" spelled backward).

### `if-else` Example from `CIDR.sh`
This code checks if the user provided exactly one argument to the script.

```bash
#!/bin/bash

# Check for given arguments
if [ $# -eq 0 ]
then
    echo "You need to specify a target domain."
    exit 1
else
    domain=$1
fi
```

**Breakdown:**

- $#: A special shell variable that holds the **count of arguments** passed to the script.
    
- -eq 0: The condition. It checks if the number of arguments is **eq**ual to 0.
    
- if ... then: If the condition is true (no arguments were given), it prints an error message and exits.
    
- else: If the condition is false (at least one argument was given), it assigns the first argument ($1) to the domain variable.
    

### Adding More Conditions with elif

You can test for multiple, different conditions using elif (else if).

- if: The first condition to test.
    
- elif: An alternative condition to test if the first one was false. You can have multiple elif blocks.
    
- else: A final block that runs if **none** of the preceding if or elif conditions were true.

```bash
#!/bin/bash

value=$1

if [ $value -gt 10 ]
then
    echo "Argument is greater than 10."
elif [ $value -lt 10 ]
then
    echo "Argument is less than 10."
elif [ $value -eq 10 ]
then
    echo "Argument is exactly 10."
else
    echo "Argument is not an integer."
fi
```

(Note: -gt means "greater than", -lt means "less than", -eq means "equal to" for numerical comparisons).

---

## 3. Special Variables Used in Scripts

Bash provides several special variables that are extremely useful in scripting.

|   |   |
|---|---|
|Variable|Description|
|**$#**|The **number** of positional arguments passed to the script.|
|**$0**|The **name** of the script itself.|
|**$1, $2, $3 ...**|The positional arguments themselves. $1 is the first argument, $2 is the second, and so on.|
|**$?**|The **exit code** of the last command that was executed. An exit code of 0 means success, while any non-zero value indicates an error.|
|**$@**|All positional arguments, as a list of separate strings.|
|**$***|All positional arguments, as a single string.|
