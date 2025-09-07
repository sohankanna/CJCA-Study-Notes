# Functions

## What are Functions?

A **function** is a named block of code that performs a specific task. Once defined, you can "call" the function by its name anywhere in your script to execute that block of code.

**Core Idea:** Functions help you avoid repeating code. If you have a task that needs to be performed multiple times, you write the code for it once inside a function and then simply call that function whenever you need it. This makes scripts shorter, easier to read, and easier to maintain.

### Defining a Function
There are two common syntaxes for defining a function in Bash. Both are functionally identical.

**Method 1 (with the `function` keyword):**
```bash
function function_name {
    # commands go here
    echo "Hello from the function!"
}
```

**Method 2 (without the `function` keyword):**
```bash
function_name() {
    # commands go here
    echo "Hello from the function!"
}
```

**Important:** A function must be **defined** in the script *before* it is called for the first time, as Bash reads and executes scripts from top to bottom.

### Calling a Function
To execute the code inside a function, you simply call it by its name.
```bash
# Calling the function defined above
function_name
```

---

## Passing Parameters to Functions

You can pass arguments to a function, just like you pass arguments to a script. Inside the function, these arguments are accessed using the same special positional variables (`$1`, `$2`, `$#`, etc.).

*   **Key Concept:** The positional parameters inside a function are **local** to that function. They are separate from the script's own positional parameters.

### Example: Passing Parameters
```bash
#!/bin/bash

# Define a function that accepts parameters
function print_greeting {
    echo "Hello, $1! Welcome to the $2 module."
}

# Call the function and pass two arguments to it
print_greeting "Hacker" "Bash Scripting"
```
**Execution Output:**
```
Hello, Hacker! Welcome to the Bash Scripting module.
```
*   Inside the `print_greeting` function, `$1` was "Hacker" and `$2` was "Bash Scripting".

---

## Returning Values from Functions

Unlike many programming languages, Bash functions do not have a straightforward way to return arbitrary values (like strings or numbers). Instead, there are two primary ways to get a result *out* of a function.

### 1. Using the `return` Status Code
The `return` command sets the **exit status** of the function. This is a number between 0 and 255.

*   **Convention:**
    *   `return 0`: The function succeeded.
    *   `return 1` (or any non-zero value): The function failed or encountered an error.
*   **Accessing the return code:** You can access the exit status of the most recently executed function using the special variable `$?`.

**Example:**
```bash
#!/bin/bash

function check_args {
    if [ $# -lt 1 ]; then
        return 1 # FAILED
    else
        return 0 # SUCCESS
    fi
}

check_args "one_argument"
echo "Status code: $?" # Will print 0

check_args
echo "Status code: $?" # Will print 1
```

### 2. Using `echo` and Command Substitution (The Standard Method)
This is the most common way to "return" a string or numerical value from a function. The function `echo`es its result to standard output, and you capture that output in a variable using command substitution `$(...)`.

**Example:**
```bash
#!/bin/bash

function get_full_name {
    local first_name=$1
    local last_name=$2
    
    # "Return" the result by printing it to STDOUT
    echo "$first_name $last_name"
}

# Capture the output of the function in a variable
full_name=$(get_full_name "Jane" "Doe")

echo "The full name is: $full_name"
```
**Execution Output:**
```
The full name is: Jane Doe
```
*   **`local` keyword:** Declaring a variable with `local` inside a function makes it accessible only within that function. This is a best practice to avoid accidentally overwriting global variables.
