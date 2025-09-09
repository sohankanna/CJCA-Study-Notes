# Comparison Operators

## 1. String Operators

These operators are used for comparing strings. When comparing a variable that might contain spaces, it is a crucial best practice to **enclose it in double quotes** (e.g., `"$var"`) to prevent errors.

| Operator | Within `[ ]` | Description | Example |
| :--- | :--- | :--- | :--- |
| **Is Equal To** | `==` or `=` | Checks if two strings are identical. | `if [ "$name" == "root" ]` |
| **Is Not Equal To**| `!=` | Checks if two strings are different. | `if [ "$user" != "guest" ]` |
| **Is Null/Empty**| `-z` | Returns true if the string is empty (has zero length). | `if [ -z "$input" ]` |
| **Is Not Null** | `-n` | Returns true if the string is not empty (has a non-zero length). | `if [ -n "$password" ]` |
| **Less/Greater Than**| `<` / `>` | Compares strings based on ASCII alphabetical order. **Must be used inside double brackets `[[ ]]`**. | `if [[ "$a" < "$b" ]]` |

---

## 2. Integer Operators

These operators are specifically for comparing numerical values.

| Operator | Description | Example |
| :--- | :--- | :--- |
| **`-eq`** | Is **eq**ual to | `if [ $count -eq 0 ]` |
| **`-ne`** | Is **n**ot **e**qual to | `if [ $lines -ne 10 ]` |
| **`-gt`** | Is **g**reater **t**han | `if [ $age -gt 18 ]` |
| **`-ge`** | Is **g**reater than or **e**qual to | `if [ $score -ge 90 ]` |
| **`-lt`** | Is **l**ess **t**han | `if [ $# -lt 1 ]` |
| **`-le`** | Is **l**ess than or **e**qual to | `if [ $attempts -le 3 ]` |

---

## 3. File Operators

These operators are used to check the status or attributes of a file or directory. They are extremely useful for checking if a file exists before trying to read it, or if you have the correct permissions.

| Operator | Description | Example |
| :--- | :--- | :--- |
| **`-e`** | Returns true if the file **e**xists (can be a file, directory, or link). | `if [ -e "/etc/passwd" ]` |
| **`-f`** | Returns true if the path is a regular **f**ile. | `if [ -f "script.sh" ]` |
| **`-d`** | Returns true if the path is a **d**irectory. | `if [ -d "/home/hacker" ]` |
| **`-r`** | Returns true if the file exists and has **r**ead permission for the current user. | `if [ -r "$config_file" ]` |
| **`-w`** | Returns true if the file exists and has **w**rite permission for the current user. | `if [ -w "output.log" ]` |
| **`-x`** | Returns true if the file exists and has e**x**ecute permission for the current user. | `if [ -x "./run.sh" ]` |
| **`-s`** | Returns true if the file exists and has a **s**ize greater than zero (is not empty). | `if [ -s "results.txt" ]` |
| **`-L`** | Returns true if the path is a symbolic **L**ink. | `if [ -L "/usr/bin/python" ]` |

---

## 4. Logical Operators

Logical operators are used to combine multiple conditions within a single `if` statement. They are typically used inside the more modern and flexible double square brackets `[[ ]]`.

| Operator | Description | Example |
| :--- | :--- | :--- |
| **`&&`** | **Logical AND:** The entire expression is true only if **both** conditions are true. | `if [[ -f "$file" && -r "$file" ]]` <br> (If the file exists AND it is readable). |
| **`\|\|`** | **Logical OR:** The entire expression is true if **either** of the conditions is true. | `if [[ $user == "root" \|\| $user == "admin" ]]` <br> (If the user is "root" OR "admin"). |
| **`!`** | **Logical NOT:** Inverts the result of the condition that follows it. | `if [[ ! -f "$file" ]]` <br> (If the file does NOT exist). |
