#  Regular Expressions

## What is a Regular Expression?

A **Regular Expression (RegEx)** is a special sequence of characters that defines a search pattern. It's like a highly advanced "find and replace" tool that can match complex and variable patterns, not just fixed strings of text.

*   **Core Idea:** Instead of searching for the literal word "color", you can create a RegEx pattern that matches both "color" and "colour".
*   **Key Components:** A RegEx is made up of:
    *   **Literal Characters:** Normal characters that match themselves (e.g., `a`, `b`, `1`, `2`).
    *   **Metacharacters:** Special symbols that have a specific meaning and define the rules of the pattern (e.g., `*`, `+`, `?`).
*   **Usage:** RegEx is supported by a vast number of programming languages and command-line tools, most notably `grep`, `sed`, and `awk`.

---

## The Three Main Grouping Operators

These operators are the fundamental building blocks for creating complex patterns.

| Operator | Name | Description | Example |
| :--- | :--- | :--- | :--- |
| **`( )`** | **Group** | Groups multiple characters or sub-patterns together, allowing you to apply a quantifier or operator to the entire group. | `(very )?good` matches both "good" and "very good". |
| **`[ ]`** | **Character Class** | Defines a set of characters to match. It will match **any single character** from within the brackets. | `[abc]` matches `a`, `b`, or `c`. <br> `[a-z]` matches any lowercase letter. <br> `[0-9]` matches any digit. |
| **`{ }`** | **Quantifier** | Specifies exactly how many times the preceding character or group must occur. | `a{3}` matches `aaa`. <br> `[0-9]{1,3}` matches any number between 1 and 3 digits long. |

---

## Logical Operators in RegEx

To create more flexible patterns, you can use logical operators. When using these advanced operators with `grep`, you often need to use the **`-E` flag** for "extended regular expressions".

### The `|` (OR) Operator
The pipe character (`|`) within a group acts as a logical **OR**. The pattern will match if the text contains *either* of the expressions.

*   **Syntax:** `grep -E "(pattern1|pattern2)"`
*   **Example:** Find all lines in `/etc/passwd` that contain either the word `my` OR the word `false`.
    ```shell
    hacker@htb:~$ grep -E "(my|false)" /etc/passwd
    lxd:x:105:65534::/var/lib/lxd/:/bin/false
    pollinate:x:109:1::/var/cache/pollinate:/bin/false
    mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
    ```

### The `.*` (AND) Combination
While there is no explicit "AND" operator, you can achieve the same result by using the dot (`.`) and asterisk (`*`) metacharacters together between two patterns.
*   `.` : Matches **any single character**.
*   `*` : Matches the preceding character **zero or more times**.
*   `.*`: Together, this means "match any character, any number of times."

This combination effectively says, "Find `pattern1`, followed by anything, followed by `pattern2` on the same line."

*   **Syntax:** `grep -E "(pattern1.*pattern2)"`
*   **Example:** Find all lines in `/etc/passwd` that contain `my` AND `false` in that order.
    ```shell
    hacker@htb:~$ grep -E "(my.*false)" /etc/passwd
    mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
    ```

**Alternative "AND" Method:** You can also achieve an AND operation by piping two `grep` commands together. This is often simpler and easier to read.
```shell
hacker@htb:~$ grep "my" /etc/passwd | grep "false"
mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
