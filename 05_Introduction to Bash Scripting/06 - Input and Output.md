# Input and Output

## 1. Controlling Input (`read`)

The `read` command is a Bash built-in that is used to get input from the user and store it in a variable. It causes the script to pause and wait for the user to type something and press Enter.

*   **Syntax:**
    ```shell
    read [options] variable_name
    ```
*   **Key Option:**
    *   `-p`: **(prompt)** Displays a prompt string on the same line, without a trailing newline. This is the standard way to ask a user for input.

### Example: The Menu from `CIDR.sh`
This code block demonstrates how to create a simple, interactive menu.

```bash
# Display the menu options
echo "Additional options available:"
echo -e "\t1) Identify network range."
echo -e "\t2) Ping discovered hosts."
echo -e "\t*) Exit.\n"

# Prompt the user for their choice and store it in the 'opt' variable
read -p "Select your option: " opt

# Use a 'case' statement to act on the user's input
case $opt in
    "1") network_range ;;
    "2") ping_host ;;
    "*") exit 0 ;;
esac

```

**Breakdown:**

1. echo commands are used to print the menu to the screen.
    
2. read -p "..." opt displays the prompt "Select your option: " and waits. Whatever the user types is stored in the opt variable.
    
3. The case statement then checks the value of $opt and executes the corresponding function.
    

---

## 2. Controlling Output (tee)

Standard output redirection (>) is useful for saving the output of a command to a file, but you don't see the output on your screen in real-time. The tee command solves this problem.

The **tee** command reads from standard input and writes it to **both** standard output (your screen) and one or more files simultaneously.

- **Analogy:** tee acts like a "T-splitter" in a plumbing pipe. It takes one stream of water (data) and splits it into two identical streams, one going to the screen and one going to a file.
    

### tee Syntax and Usage

tee is almost always used with a pipe (|).

- **Syntax:** command | tee [options] filename
    
- **Key Option:**
    
    - -a: **(append)** Appends the output to the file instead of overwriting it.
        

### Example from CIDR.sh

This command gets the IP address of a domain, displays it on the screen, AND saves it to a file at the same time.

```bash
hosts=$(host $domain | grep "has address" | cut -d" " -f4 | tee discovered_hosts.txt)
```

**Breakdown:**

1. host ... | cut ...: This part of the command pipeline produces the IP address as its standard output.
    
2. | tee discovered_hosts.txt: This output is piped to tee.
    
3. tee does two things:
    
    - It prints the IP address to the screen.
        
    - It writes the IP address to the file discovered_hosts.txt.
        
4. The output that tee printed to the screen is then captured by the command substitution $(...) and stored in the hosts variable.
