# Flow Control - Loops

## 1. `for` Loops

A **`for` loop** is used to iterate over a given list of items. It executes a block of code **once for each item** in the list.

*   **Core Idea:** Use a `for` loop when you have a known, finite set of items you need to process one by one.

### `for` Loop Syntax and Examples

*   **Basic Syntax:**
    ```bash
    for variable_name in item1 item2 item3
    do
        # Commands to execute, using $variable_name
        echo "Processing item: $variable_name"
    done
    ```

*   **Iterating over a list of IP addresses:**
    ```bash
    for ip in 10.10.10.1 10.10.10.2
    do
        ping -c 1 $ip
    done
    ```

*   **Iterating over a variable containing a list:**
    In the `CIDR.sh` script, a variable `ipaddr` holds a space-separated list of IPs. The `for` loop processes each one.
    ```bash
    ipaddr="192.168.1.1 192.168.1.2"
    for ip in $ipaddr
    do
        whois $ip
    done
    ```

*   **One-Liner Syntax:**
    You can write a `for` loop on a single line using semicolons.
    ```shell
    for i in 1 2 3; do echo $i; done
    ```

---

## 2. `while` Loops

A **`while` loop** executes a block of code **as long as a specified condition is true**.

*   **Core Idea:** Use a `while` loop when you want to repeat an action an unknown number of times, until a condition is no longer met.
*   **Important:** The condition must eventually become false, otherwise you will create an **infinite loop**. This usually involves a counter variable that is incremented or decremented inside the loop.

### `while` Loop Syntax and Example

*   **Basic Syntax:**
    ```bash
    while [ <condition> ]
    do
        # Commands to execute
    done
    ```

*   **Example (a simple counter):**
    ```bash
    #!/bin/bash
    
    counter=0
    
    while [ $counter -lt 5 ]
    do
        echo "Counter is now: $counter"
        ((counter++))  # Increment the counter to prevent an infinite loop
    done
    ```

---

## 3. `until` Loops

An **`until` loop** is the logical opposite of a `while` loop. It executes a block of code **as long as a specified condition is false**.

*   **Core Idea:** The loop continues to run *until* the condition becomes true.
*   **Usage:** It is less common than `while` loops, but can sometimes make the logic of a script clearer.

### `until` Loop Syntax and Example
*   **Basic Syntax:**
    ```bash
    until [ <condition> ]
    do
        # Commands to execute
    done
    ```

*   **Example (counting up to 10):**
    ```bash
    #!/bin/bash

    counter=0
    
    # Loop UNTIL the counter is equal to 10
    until [ $counter -eq 10 ]
    do
        ((counter++))
        echo "Counter: $counter"
    done
    ```

---

## 4. Controlling Loops: `break` and `continue`

You can alter the flow of a loop from within the loop's body.

*   **`break`:** **Immediately terminates** the entire loop and execution continues with the next command after the `done` keyword.
*   **`continue`:** **Skips the rest of the current iteration** and immediately starts the next iteration of the loop.

### Example
```bash
#!/bin/bash

counter=0

while [ $counter -lt 10 ]
do
    ((counter++))
    
    if [ $counter == 2 ]
    then
        continue # Skip the echo for '2' and start the next loop
    fi
    
    if [ $counter == 5 ]
    then
        break # Exit the loop entirely when counter hits 5
    fi

    echo "Counter: $counter"
done

echo "Loop finished."
```

```
Counter: 1
Counter: 3
Counter: 4
Loop finished.
```

