# 13 - Databases

## 1. Relational Databases (SQL)

**Relational databases** organize data into a structured format of **tables**, **rows**, and **columns**. They use **SQL (Structured Query Language)** to manage and query the data.

*   **Core Idea:** Data is highly structured. Relationships between different tables are defined using unique **keys**.
*   **Schema:** The formal definition of how the data is organized—the tables, the columns within them, their data types, and the relationships between tables—is called the **database schema**.
*   **Analogy:** A relational database is like a collection of perfectly organized spreadsheets (tables). Each spreadsheet has defined columns (e.g., `ID`, `Username`, `Email`), and each row is a unique record. You can link rows between different spreadsheets using a common ID.

### Common Relational Databases

| Database | Description |
| :--- | :--- |
| **MySQL / MariaDB**| The most widely used open-source relational database. A core component of the popular **LAMP** stack. (MariaDB is a community-driven fork of MySQL). |
| **PostgreSQL** | A powerful, open-source object-relational database known for its extensibility and standards compliance. |
| **Microsoft SQL Server (MSSQL)**| Microsoft's proprietary relational database, tightly integrated with the Windows Server and .NET ecosystem. |
| **Oracle Database** | A powerful, enterprise-grade relational database known for its reliability and advanced features, but often with high licensing costs. |
| **SQLite** | A self-contained, serverless, file-based SQL database engine. It's often embedded directly into applications (like web browsers and mobile apps) for local data storage. |

---

## 2. Non-Relational Databases (NoSQL)

**Non-relational databases** (often called **NoSQL**) do not use the rigid table-based structure of relational databases. They are designed for large-scale, unstructured or semi-structured data and offer greater flexibility and scalability.

*   **Core Idea:** Data is stored in a less structured format, without a predefined schema. This makes them highly flexible and horizontally scalable.

### Common NoSQL Storage Models

| Model | Description |
| :--- | :--- |
| **Key-Value** | The simplest model. Data is stored as a collection of key-value pairs, much like a dictionary or hash map. **Redis** is a popular example. |
| **Document-Based**| Data is stored in flexible, semi-structured documents, typically in a format like **JSON** or BSON. **MongoDB** is the most popular document-based database. |
| **Wide-Column**| Data is stored in tables, but the columns can be dynamic for each row. Optimized for queries over large datasets. **Apache Cassandra** is a key example. |
| **Graph** | Designed specifically to store and navigate relationships between data points. Uses nodes, edges, and properties. **Neo4j** is a popular example. |

---

## 3. How Web Applications Use Databases

Web applications communicate with databases to perform the four **CRUD** (**C**reate, **R**ead, **U**pdate, **D**elete) operations.

1.  **Connection:** The application's back-end code (e.g., in PHP, Python, Java) establishes a connection to the database server, usually with a username and password.
2.  **Query:** The application constructs a query (e.g., in SQL) to request data. This query often includes input provided by the user.
3.  **Execution:** The database engine executes the query.
4.  **Result:** The database returns the results of the query to the application.
5.  **Processing:** The application processes the results and incorporates them into the HTML response that is sent back to the user's browser.

### The Security Risk: SQL Injection
The most critical vulnerability related to databases is **SQL Injection (SQLi)**.

*   **The Vulnerability:** Occurs when an application takes user-supplied input and directly includes it in a database query without proper sanitization or the use of parameterized queries.
*   **The Attack:** An attacker can provide specially crafted input that breaks out of the intended data context and is interpreted as part of the SQL command itself.
*   **The Impact:** SQLi can allow an attacker to bypass authentication, read all data from the database (including other users' information), modify or delete data, and in some cases, even execute commands on the underlying operating system of the database server.

**Vulnerable PHP Code Example:**
```php
// User input is directly concatenated into the query string - HIGHLY VULNERABLE!
$searchInput = $_POST['findUser'];
$query = "SELECT * FROM users WHERE name LIKE '%$searchInput%'";
$result = $conn->query($query);
```

An attacker could provide input like ' OR '1'='1 to potentially dump all users from the table.
