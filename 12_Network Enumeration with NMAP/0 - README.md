# Module: Network Enumeration with Nmap

This module provides a comprehensive, in-depth exploration of **Nmap (Network Mapper)**, the single most essential tool for network discovery and security auditing. The notes progress from the fundamental concepts of enumeration to advanced techniques for port scanning, service identification, and firewall evasion.

Mastering Nmap is a non-negotiable skill for any cybersecurity professional. It is the foundational tool used in nearly every penetration test to map the attack surface, identify potential vulnerabilities, and plan the subsequent phases of an engagement. This module covers the core features and practical applications of Nmap.

---

## Module Sections (Notes)

Below is a list of the topics covered in this module, organized to build a strong, practical foundation in network enumeration with Nmap.

1.  **Enumeration:** Introduces the core concept of enumeration, emphasizing its critical importance in a penetration test and contrasting the roles of automated tools versus manual, knowledge-driven investigation.

2.  **Introduction to Nmap:** A high-level overview of the Nmap tool, its primary use cases, architecture, and a look at the foundational TCP SYN Scan (`-sS`).

3.  **Host Discovery:** Covers the first phase of an Nmap scan, detailing the techniques (ARP vs. ICMP) and options (`-sn`) used to identify which hosts are online within a target network range.

4.  **Host and Port Scanning:** A deep dive into the core port scanning functionality of Nmap. This section explains the different port states (open, closed, filtered) and covers the key TCP (`-sS`, `-sT`) and UDP (`-sU`) scanning techniques.

5.  **Saving the Results:** Emphasizes the critical importance of documenting scans. It details Nmap's three main output formats (`-oN`, `-oG`, `-oX`) and how to convert the versatile XML output into a user-friendly HTML report.

6.  **Service Enumeration:** Covers the use of the `-sV` flag for service and version detection. Explains how Nmap performs "banner grabbing" and uses probes to accurately identify the software running on open ports, a crucial step for finding public exploits.

7.  **Nmap Scripting Engine (NSE):** Explores the powerful NSE, which extends Nmap's capabilities with Lua scripts. This section covers the different script categories (`default`, `vuln`, `brute`, etc.) and how to run them to automate advanced enumeration and vulnerability discovery.

8.  **Performance:** Discusses the trade-off between scan speed and accuracy. It details Nmap's timing templates (`-T0` through `-T5`) and the manual options for controlling scan rates and timeouts.

9.  **Firewall and IDS/IPS Evasion:** Covers advanced techniques used to bypass or evade network security devices. This includes the ACK scan (`-sA`), using decoys (`-D`), fragmenting packets (`-f`), and manipulating the source port (`--source-port`).
