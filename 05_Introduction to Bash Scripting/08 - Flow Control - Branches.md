# Flow Control - Branches

## 1. `case` Statements

A **`case` statement** simplifies complex `if-elif-else` chains when you need to compare a single variable against several specific, exact values. It is often referred to as a "switch-case" statement in other programming languages.

*   **Core Idea:** Use a `case` statement when you have a menu of options and want to perform a different action for each one. It makes the code much cleaner and more readable than a long series of `elif` statements.
*   **Key Difference from `if`:**
    *   `if` statements can evaluate any boolean expression (e.g., `greater than`, `file exists`, `string contains`).
    *   `case` statements can only check for an **exact match** of a variable against a pattern.

### `case` Statement Syntax
```bash
case $variable in
    pattern1)
        # Commands to execute if $variable matches pattern1
        ;;
    pattern2)
        # Commands to execute if $variable matches pattern2
        ;;
    pattern3|pattern4)
        # Commands to execute if $variable matches pattern3 OR pattern4
        ;;
    *)
        # Default case: Commands to execute if no other pattern matches
        ;;
esac
```

**Breakdown of the Syntax:**
*   `case $variable in`: Starts the statement, specifying the variable to be checked.
*   `pattern)`: Defines a specific value or pattern to match against. The parenthesis is required.
*   `;;`: The **double semicolon** is crucial. It marks the end of a block of statements for a specific pattern, similar to the `break` keyword in other languages.
*   `*)`: The asterisk acts as a **wildcard** or **default case**. This block will execute if the variable does not match any of the other patterns listed.
*   `esac`: Marks the end of the `case` statement (which is "case" spelled backward).

---

## Example: The Menu from `CIDR.sh`

The `case` statement is the perfect tool for handling the menu logic in our `CIDR.sh` script.

```bash
# Prompt the user for input and store it in the 'opt' variable
read -p "Select your option: " opt

# Evaluate the user's input
case $opt in
    "1")
        # If the user typed "1"
        network_range
        ;;
    "2")
        # If the user typed "2"
        ping_host
        ;;
    "3")
        # If the user typed "3"
        network_range && ping_host
        ;;
    *)
        # If the user typed anything else
        echo "Invalid option. Exiting."
        exit 0
        ;;
esac
```
This code is much cleaner and easier to read than an equivalent `if-elif-else` chain would be:
```bash
if [ "$opt" == "1" ]; then
    network_range
elif [ "$opt" == "2" ]; then
    ping_host
elif [ "$opt" == "3" ]; then
    network_range && ping_host
else
    echo "Invalid option. Exiting."
    exit 0
fi
```


