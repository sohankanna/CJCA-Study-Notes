# Arguments, Variables, and Arrays

 1. Arguments (Positional Parameters)

**Arguments** are the inputs you provide to a script on the command line when you run it. Bash automatically captures these arguments and assigns them to special, numbered variables.

*   **Syntax:**
    ```shell
    ./script.sh arg1 arg2 arg3
    ```
*   **Assignment:**
    *   `$0` = `./script.sh` (The name of the script itself)
    *   `$1` = `arg1` (The first argument)
    *   `$2` = `arg2` (The second argument)
    *   ...and so on up to `$9`.

### Special Variables for Arguments
Bash provides several special variables to work with arguments in a more general way.

| Variable | Description |
| :--- | :--- |
| **`$#`** | The **total number** of arguments passed to the script (not including the script name). |
| **`$@`** | All arguments, treated as a **list of separate, quoted strings**. This is the safest way to iterate over arguments. |
| **`$*`** | All arguments, treated as a **single string**. |
| **`$0`** | The name of the script itself. |
| **`$1`, `$2`...**| The individual positional arguments. |
| **`$$`** | The **Process ID (PID)** of the currently running script. |
| **`$?`** | The **exit status** of the most recently executed command. `0` means success, any non-zero value means failure. |

### Example from `CIDR.sh`
```bash
if [ $# -eq 0 ]
then
    echo "Usage: $0 <domain>"
    exit 1
else
    domain=$1
fi
```

*   **Assignment:**
    *   `$0` = `./script.sh` (The name of the script itself)
    *   `$1` = `arg1` (The first argument)
    *   `$2` = `arg2` (The second argument)
    *   ...and so on up to `$9`.

### Special Variables for Arguments
Bash provides several special variables to work with arguments in a more general way.

| Variable | Description |
| :--- | :--- |
| **`$#`** | The **total number** of arguments passed to the script (not including the script name). |
| **`$@`** | All arguments, treated as a **list of separate, quoted strings**. This is the safest way to iterate over arguments. |
| **`$*`** | All arguments, treated as a **single string**. |
| **`$0`** | The name of the script itself. |
| **`$1`, `$2`...**| The individual positional arguments. |
| **`$$`** | The **Process ID (PID)** of the currently running script. |
| **`$?`** | The **exit status** of the most recently executed command. `0` means success, any non-zero value means failure. |

### Example from `CIDR.sh`
```bash
if [ $# -eq 0 ]
then
    echo "Usage: $0 <domain>"
    exit 1
else
    domain=$1
fi
```
*   `$#` is used to check if the number of arguments is zero.
*   `$0` is used to print the script's name in the usage message.
*   `$1` is used to capture the first argument and assign it to the `domain` variable.

---

## 2. Variables

A **variable** is a named placeholder used to store data.

### Declaring and Using Variables
*   **Declaration/Assignment:** `variable_name=value`
    *   **CRITICAL:** There must be **NO spaces** around the equals (`=`) sign.
    *   **Correct:** `myvar="Hello World"`
    *   **Incorrect:** `myvar = "Hello World"` (This will result in a "command not found" error).
*   **Usage (Dereferencing):** To get the value stored in a variable, you must prefix its name with a dollar sign (`$`).
    ```shell
    hacker@htb[~]$ myvar="Hello HTB"
    hacker@htb[~]$ echo $myvar
    Hello HTB
    ```

### Variable Types in Bash
Unlike many other programming languages, Bash does not have strict variable types (like "integer" or "boolean"). By default, **all variables are treated as strings**. Bash can perform arithmetic on variables containing only numbers, but their underlying type is still a string.

---

## 3. Arrays

An **array** is a special type of variable that can hold a list of multiple values.

### Declaring an Array
*   **Syntax:** `array_name=(value1 value2 value3)`
*   The values are separated by spaces.
*   **Example:**
    ```bash
    domains=(www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com)
    ```

### Accessing Array Elements
Array elements are accessed using a numerical index, starting from `0`.

*   **Syntax:** `${array_name[index]}`
    *   The curly braces `{}` are important for clarity and to avoid ambiguity, especially when the variable is next to other characters.
*   **Access the first element (index 0):**
    ```bash
    echo ${domains[0]}
    # Output: www.inlanefreight.com
    ```
*   **Access all elements:**
    ```bash
    echo ${domains[@]}
    ```

**Important Quoting Note:** When declaring an array, values inside quotes (`"`) are treated as a single element, even if they contain spaces.
```bash
# This creates an array with TWO elements, not three.
domains=("www.inlanefreight.com ftp.inlanefreight.com" vpn.inlanefreight.com)

echo ${domains[0]}
# Output: www.inlanefreight.com ftp.inlanefreight.com
```



