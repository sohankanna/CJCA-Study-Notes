# Arithmetic

## 1. Arithmetic Expansion: `$(( ))`

The primary method for performing arithmetic in Bash is with the **arithmetic expansion** syntax: `$((expression))`. The shell will evaluate the mathematical expression inside the double parentheses and replace the entire construct with the result.

*   **Key Idea:** This is the standard and most portable way to perform calculations directly within a command like `echo`.

### Basic Arithmetic Operators

| Operator | Description | Example |
| :--- | :--- | :--- |
| **`+`** | Addition | `echo $((10 + 10))` -> `20` |
| **`-`** | Subtraction | `echo $((10 - 5))` -> `5` |
| **`*`** | Multiplication | `echo $((10 * 10))` -> `100` |
| **`/`** | Division (Integer)| `echo $((10 / 3))` -> `3` (Note: Bash only performs integer division; remainders are discarded). |
| **`%`** | Modulus | `echo $((10 % 3))` -> `1` (Returns the remainder of a division). |

---

## 2. Arithmetic Context: `(( ))`

For performing assignments, increments, and decrements, Bash provides the **arithmetic context** syntax using double parentheses: `((expression))`. This is often used for modifying variables within loops and conditional statements.

*   **Key Idea:** This form is used when you want to *change* a variable's value, not just print the result of a calculation.

### Increment and Decrement Operators

| Operator | Description | Example |
| :--- | :--- | :--- |
| **`variable++`** | **Post-increment:** Increase the value of `variable` by 1. | `((count++))` |
| **`variable--`** | **Post-decrement:** Decrease the value of `variable` by 1. | `((stat--))` |
| **`++variable`** | **Pre-increment:** (Also increases by 1). | `((++count))` |
| **`--variable`** | **Pre-decrement:** (Also decreases by 1). | `((--stat))` |
| **`+=`, `-=`, `*=`** | Compound assignment. | `((total += 5))` (Same as `total = total + 5`). |

### Example Script
This script demonstrates the use of both arithmetic constructs.
```bash
#!/bin/bash

# Arithmetic Expansion to print results
echo "Addition: $((10 + 5))"
echo "Modulus: $((10 % 4))"

# Arithmetic Context to modify variables
count=1
echo "Initial value: $count"

((count++))
echo "Value after increment: $count"

((count--))
echo "Value after decrement: $count"
```

## 3. Getting String Length

While not a direct arithmetic operation, finding the length of a string is a common numerical task in scripting.

- **Syntax:** ${#variable_name}
    
- This syntax expands to the number of characters in the string stored in the variable.

```bash
#!/bin/bash

htb="HackTheBox"
echo "The length of the string '$htb' is ${#htb} characters."
```

**Output:**

```
The length of the string 'HackTheBox' is 10 characters.
```

