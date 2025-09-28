# 05 - Saving the Results

## 1. Nmap's Output Formats

Nmap offers several formats for saving scan results. The `-oA` flag is the most efficient way to save in all three primary formats simultaneously.

*   **Command:** `sudo nmap <target> -oA <basename>`
*   **Example:** `sudo nmap 10.129.2.28 -oA target`
*   **Result:** This will create three files: `target.nmap`, `target.gnmap`, and `target.xml`.

### a) Normal Output (`-oN`)
*   **File Extension:** `.nmap`
*   **Description:** This format is nearly identical to the interactive output you see on your screen during a scan. It is human-readable and well-suited for a quick review.
*   **Example:**
    ```
    # Nmap 7.80 scan initiated ...
    Nmap scan report for 10.129.2.28
    Host is up (0.053s latency).
    PORT   STATE SERVICE
    22/tcp open  ssh
    25/tcp open  smtp
    80/tcp open  http
    ...
    ```

### b) Grepable Output (`-oG`)
*   **File Extension:** `.gnmap`
*   **Description:** A condensed, single-line-per-host format designed to be easily parsed by command-line tools like `grep`, `awk`, and `cut`. It is excellent for scripting and quick data extraction.
*   **Example:**
    ```
    # Nmap 7.80 scan initiated ...
    Host: 10.129.2.28 ()	Status: Up
    Host: 10.129.2.28 ()	Ports: 22/open/tcp//ssh///, 25/open/tcp//smtp///, ...
    ...
    ```

### c) XML Output (`-oX`)
*   **File Extension:** `.xml`
*   **Description:** A structured, machine-readable format. This is the **most comprehensive and versatile** output format. It contains all the detailed information from the scan in a well-defined structure.
*   **Use Case:** This format is designed to be imported into other tools for further analysis or reporting. Many security tools and frameworks can directly parse Nmap's XML output.

---

## 2. Creating an HTML Report

The XML output can be easily converted into a user-friendly, interactive HTML report. This is an excellent way to present scan results to clients or team members who may not be comfortable with the command line.

*   **Tool:** `xsltproc` is a command-line tool used to apply XSL stylesheets to XML documents.
*   **Command:**
    ```shell
    xsltproc target.xml -o target.html
    ```
*   **Breakdown:**
    *   `xsltproc`: The command to run the tool.
    *   `target.xml`: The input Nmap XML file.
    *   `-o target.html`: The name of the output HTML file to be created.

Opening the resulting `target.html` file in a web browser will display a clean, organized, and sortable report of your Nmap scan findings.
