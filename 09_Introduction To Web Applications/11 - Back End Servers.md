# 11 - Back End Servers

## 1. What is a Back End Server?

A **back end server** is the physical or virtual machine that provides the computing resources for a web application to operate. It is the core of the **Data Access Layer** in the three-tier architecture.

*   **Core Idea:** The back end server is the "engine room" of a web application. While users interact with the front end in their browser, all the heavy lifting—processing logic, executing code, and managing data—happens on the back end server.

---

## 2. Software Components of a Back End Server

The back end server hosts the three other essential back end components:

1.  **Web Server Software:** The program that listens for and responds to HTTP requests (e.g., Apache, Nginx, IIS).
2.  **Application Logic / Development Framework:** The code that defines the application's functionality (e.g., written in PHP, Python, Java, C#).
3.  **Database:** The system used to store and retrieve the application's data (e.g., MySQL, PostgreSQL, Microsoft SQL Server).

Other software that may run on the back end server includes hypervisors (for virtualization), container runtimes (like Docker), and Web Application Firewalls (WAFs).

### Common "Stacks" (Software Bundles)
A "stack" is a popular combination of an operating system, web server, database, and programming language that are commonly used together to build a web application.

| Acronym | Components | Description |
| :--- | :--- | :--- |
| **LAMP** | **L**inux, **A**pache, **M**ySQL, **P**HP | The classic, foundational stack for open-source web development. |
| **LEMP** | **L**inux, **E**NGINX (Nginx), **M**ySQL, **P**HP | A popular, high-performance alternative to LAMP, using Nginx instead of Apache. |
| **WAMP** | **W**indows, **A**pache, **M**ySQL, **P**HP | The Windows-based equivalent of the LAMP stack. |
| **WINS** | **W**indows, **I**IS, **.NET**, **S**QL Server | A common stack for Microsoft-centric enterprise applications. |
| **XAMPP** | **X** (Cross-Platform), **A**pache, **M**ariaDB, **P**HP, **P**erl | A popular, cross-platform development environment that bundles the components of a LAMP stack. |
| **MEAN** | **M**ongoDB, **E**xpress.js, **A**ngular, **N**ode.js | A popular stack for building applications entirely with JavaScript. |

---

## 3. Hardware and Hosting

The hardware of the back end server (CPU, RAM, storage) directly impacts the performance, stability, and scalability of the web application.

### Hosting Models
*   **On-Premise:** The organization owns and manages its own physical servers in its own data center.
*   **Data Center / Co-location:** The organization rents space and network connectivity in a professional data center to house its servers.
*   **Cloud Hosting (IaaS - Infrastructure as a Service):** The most common modern approach. The organization rents virtual servers from a cloud provider like **Amazon Web Services (AWS)**, **Microsoft Azure**, or **Google Cloud Platform (GCP)**. The cloud provider manages the physical hardware, and the organization manages the virtual server (the operating system and all software on top of it).

**Key Takeaway:** The back end server is the ultimate target for a penetration tester. Gaining control of the back end server (e.g., through a web shell or remote code execution vulnerability) provides access to the application's source code, databases, and potentially the entire internal network.
