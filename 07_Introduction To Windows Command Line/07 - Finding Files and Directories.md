# Finding Files and Directories


## 1. Searching for Files and executables

### `where`
The `where` command is used to locate the path of executable files. It automatically searches the current directory and the directories listed in the system's `PATH` environment variable.

*   **Syntax:** `where <filename>`
*   **Example (Find `calc.exe`):**
    ```powershell
    C:\> where calc.exe
    C:\Windows\System32\calc.exe
    ```
*   **Recursive Search (`/R` flag):** To search for any type of file within a specific directory tree, you must use the `/R` flag to perform a recursive search.
    ```powershell
    # Search the entire C:\Users\student directory for bio.txt
    C:\> where /R C:\Users\student\ bio.txt
    C:\Users\student\Downloads\bio.txt
    ```
*   **Using Wildcards:** `where` supports wildcards (`*`, `?`) for pattern matching.
    ```powershell
    # Find all .csv files under the C:\Users\student directory
    C:\> where /R C:\Users\student\ *.csv
    ```

---

## 2. Searching for Text within Files

### `find`
The `find` command searches for a specific text string within one or more files. It is simple but less powerful than `findstr`.

*   **Syntax:** `find "string_to_find" <filename>`
*   **Key Options:**
    *   `/v`: **Invert** the search; displays lines that **do not** contain the string.
    *   `/n`: Displays the **line number** for each match.
    *   `/i`: Ignores **case** sensitivity in the search.
*   **Example:**
    ```powershell
    # Search for lines in example.txt that do not contain "IP Address",
    # ignoring case, and show their line numbers.
    C:\> find /n /i /v "IP Address" example.txt
    ```

### `findstr`
The `findstr` command is a more powerful version of `find`. It can search for patterns using **regular expressions** and offers more advanced search capabilities.

*   **Core Idea:** Think of `findstr` as the Windows CMD equivalent of the Linux `grep` command. It is the preferred tool for searching text patterns within files.
*   **Example (Basic search):**
    ```powershell
    # Search for the string "password" in all .txt files in the current directory
    C:\> findstr "password" *.txt
    ```

---

## 3. Comparing and Sorting Files

These tools are useful for comparing file integrity and organizing data.

### `comp` and `fc` (File Compare)
*   **`comp`:** Performs a byte-by-byte comparison of two files and reports the first difference it finds. It is very basic.
*   **`fc`:** A more advanced file comparison tool. It compares files line-by-line and attempts to resynchronize after a mismatch to find further differences. It is much more useful for comparing text files.
    *   `/n`: Displays line numbers in the output.
    *   `/c`: Disregards the case of letters.
    *   `/b`: Performs a binary comparison.
    ```powershell
    C:\> fc passwords.txt modded.txt /n
    ```

### `sort`
The `sort` command reads input from a file or another command, sorts it alphabetically or numerically, and prints the result.

*   **Syntax:** `sort [options] [filename]`
*   **Key Options:**
    *   `/o <output_file>`: Specifies an **o**utput file to save the sorted results to.
    *   `/unique`: Returns only the **unique** lines from the input, discarding duplicates.
*   **Example (Sorting a file and saving the output):**
    ```powershell
    # Sort file-1.md and save the sorted content to sort-1.md
    C:\> sort file-1.md /o sort-1.md
    ```
*   **Example (with piping):**
    ```powershell
    # List directory contents, pipe to findstr to filter for ".txt", then pipe to sort
    C:\> dir | findstr ".txt" | sort
    ```
