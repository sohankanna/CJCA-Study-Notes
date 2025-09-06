# Filter Contents
1. Viewing Files (Pagers)

**Pagers** are tools that allow you to view the contents of a file one screen at a time. They are essential for reading large files.

| Command | Description | Key Feature |
| :--- | :--- | :--- |
| **`more`** | A basic, older pager. Allows you to scroll **forward** only. | Simple and universally available. |
| **`less`** | A more modern and powerful pager. Allows you to scroll **forward and backward**, search for text, and more. | The standard pager on most modern systems. It's "less" because it doesn't have to read the entire file into memory to start. |

**Key Takeaway:** Always use `less` over `more` if it is available. It is far more capable.

---

## 2. Viewing Parts of Files

Sometimes you don't need to see the whole file, just the beginning or the end.

| Command | Description |
| :--- | :--- |
| **`head`** | Displays the **first 10 lines** of a file by default. Use `-n <number>` to specify a different number of lines (e.g., `head -n 20 /var/log/syslog`). |
| **`tail`** | Displays the **last 10 lines** of a file by default. Use `-n <number>` for more/fewer lines. The `-f` (follow) flag is extremely useful for watching log files in real-time as new lines are added. |

---

## 3. Filtering and Manipulating Text

These are the core "filter" commands that you will chain together with pipes (`|`).

| Command | Description | Common Usage |
| :--- | :--- | :--- |
| **`sort`** | Sorts the lines of its input alphabetically or numerically. | `cat file.txt \| sort` |
| **`grep`** | **(Global Regular Expression Print)**. The most important filtering tool. It searches its input for lines that match a specified pattern. | `cat /etc/passwd \| grep "/bin/bash"` (Find all users with a bash shell). <br> `grep -v "pattern"` (Invert match - show lines that **do not** contain the pattern). |
| **`cut`** | Extracts specific columns or "fields" from each line of its input. | `cat /etc/passwd \| cut -d":" -f1` (Use `:` as the delimiter and print the first field - the username). |
| **`tr`** | **(Translate)**. Translates or deletes characters. | `cat file.txt \| tr ":" " "` (Replace all colons with spaces). |
| **`column`** | Formats its input into clean, aligned columns. | `cat file.txt \| column -t` (Format the input as a table). |
| **`awk`** | A powerful programming language for pattern scanning and text processing. Excellent for manipulating column-based data. | `awk '{print $1, $NF}'` (Print the first (`$1`) and the very last (`$NF`) fields of each line). |
| **`sed`** | **(Stream Editor)**. A powerful tool for performing text transformations on an input stream. Commonly used for find-and-replace operations. | `sed 's/old/new/g'` (Substitute all occurrences of "old" with "new"). |
| **`wc`** | **(Word Count)**. Counts lines, words, and characters in its input. | `cat file.txt \| wc -l` (Count the number of lines). |

---

## Example: A Powerful Command Chain

Let's combine these tools to extract a specific piece of information: a sorted list of usernames who have a valid shell.

```shell
cat /etc/passwd | grep -v "nologin\|false" | cut -d":" -f1 | sort
```


**Breaking it down:**

1. **cat /etc/passwd**: Dumps the content of the passwd file.
    
2. **|**: Pipes that output to the next command.
    
3. **grep -v "nologin\|false"**: Filters out any lines containing nologin or false, leaving only users with real shells.
    
4. **|**: Pipes the filtered list to the next command.
    
5. **cut -d":" -f1**: Cuts the output using : as a delimiter and keeps only the first field (the username).
    
6. **|**: Pipes the list of usernames to the final command.
    
7. **sort**: Sorts the final list of usernames alphabetically.

