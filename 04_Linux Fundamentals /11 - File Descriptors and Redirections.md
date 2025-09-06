# File Descriptors and Redirections

## 1. What are File Descriptors (FD)?

A **file descriptor** is a number that the operating system uses to keep track of an open file, socket, or other I/O resource. It's an abstract indicator or "handle" for a resource.

**Analogy:** A file descriptor is like the ticket number you get at a coat check. You give the attendant your coat (the file), and they give you a ticket (the file descriptor). To get your coat back, you just give them the ticket number.

### The Three Standard Streams
By default, every process in Linux starts with three standard file descriptors open:

| FD # | Name | Abbreviation | Description |
| :--- | :--- | :--- | :--- |
| **0** | Standard Input | **STDIN** | The default channel for a program to receive input (usually the keyboard). |
| **1** | Standard Output | **STDOUT** | The default channel for a program to send its normal output (usually the terminal screen). |
| **2** | Standard Error | **STDERR** | The default channel for a program to send its error messages (also usually the terminal screen). |

---

## 2. I/O Redirection

**Redirection** is a shell feature that allows you to change where the standard streams (STDIN, STDOUT, STDERR) go. Instead of the keyboard or screen, you can redirect them to or from a file.

### Redirecting Output (`>` and `>>`)

*   **`>` (Redirect and Overwrite):** Redirects the output of a command to a file. **If the file exists, it will be overwritten.** If it doesn't exist, it will be created.
    *   **Syntax:** `command [fd]> file` (If `fd` is omitted, it defaults to `1` for STDOUT).
    *   **Redirect STDOUT:**
        ```shell
        ls -l > file_listing.txt
        ```
    *   **Redirect STDERR to `/dev/null` (the "black hole"):** This is a very common technique to suppress error messages.
        ```shell
        find / -name "shadow" 2> /dev/null
        ```
    *   **Redirect STDOUT and STDERR to separate files:**
        ```shell
        find /etc/ -name "shadow" 1> stdout.txt 2> stderr.txt
        ```

*   **`>>` (Redirect and Append):** Redirects the output of a command to a file. **If the file exists, the new output will be added to the end.**
    *   **Syntax:** `command [fd]>> file`
    *   **Example:**
        ```shell
        echo "This is the second line." >> my_log.txt
        ```

### Redirecting Input (`<` and `<<`)

*   **`<` (Redirect Input):** Takes the content of a file and uses it as the STDIN for a command.
    *   **Syntax:** `command < file`
    *   **Example:**
        ```shell
        cat < file_listing.txt
        ```

*   **`<<` (Here Document):** Allows you to type multi-line input directly into the terminal, which is then fed as STDIN to a command. The input ends when a specific delimiter (often `EOF` for End-Of-File) is typed on a new line.
    *   **Syntax:** `command << DELIMITER`
    *   **Example:**


```
        cat << EOF > new_file.txt
        This is the first line.
        This is the second line.
        EOF
```

## 3. Pipes (`|`)

A **pipe** is a powerful shell feature used to send the **STDOUT** of one command directly into the **STDIN** of another command, without using an intermediate file. This allows you to chain commands together to perform complex tasks.

*   **Syntax:** `command1 | command2 | command3`

### Common Use Cases for Pipes

*   **Filtering Output with `grep`:** This is one of the most common uses. `grep` filters its input for lines containing a specific pattern.
    ```shell
    # Find all .conf files in /etc/ and then filter for lines containing "systemd"
    find /etc/ -name "*.conf" 2>/dev/null | grep systemd
    ```

*   **Counting Lines with `wc -l`:** `wc` (word count) with the `-l` flag counts the number of lines in its input.
    ```shell
    # Find all .conf files, filter for "systemd", and then count how many results there are
    find /etc/ -name "*.conf" 2>/dev/null | grep systemd | wc -l
    ```
