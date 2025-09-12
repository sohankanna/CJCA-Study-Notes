# 02 - Web Application Layout

## 1. Web Application Infrastructure Models

This describes the physical or virtual layout of the servers and databases that host the application.

### One Server
*   **Description:** The entire application—web server, application logic, and database—is hosted on a single machine.
*   **Analogy:** "All eggs in one basket."
*   **Pros:** Simple and cheap to set up.
*   **Cons:** **Highly insecure.** A single vulnerability can lead to the compromise of the entire system and all its data. It's also a single point of failure; if the server goes down, everything is offline.

### Many Servers - One Database
*   **Description:** The web application is hosted on one or more web servers, which all connect to a single, separate database server.
*   **Analogy:** A restaurant with multiple kitchens (web servers) all pulling ingredients from one central pantry (database).
*   **Pros:** Better **segmentation**. A compromise of a web server does not immediately mean the database server is compromised (though it is the next logical target).
*   **Cons:** The database remains a single point of failure and a high-value central target.

### Many Servers - Many Databases
*   **Description:** The most resilient and secure model. Multiple web servers connect to multiple database servers. Each application may have its own dedicated database, or databases may be replicated for redundancy.
*   **Analogy:** A restaurant chain with multiple kitchens, each with its own local pantry, and a central warehouse for shared supplies.
*   **Pros:**
    *   **High Security:** Strong segmentation and access control.
    *   **High Availability & Redundancy:** The failure of a single server or database does not take the entire application offline.
*   **Cons:** Complex and expensive to implement and manage. Often requires **load balancers** to distribute traffic.

---

## 2. Web Application Architecture

This describes the logical layering of the software components. The **Three-Tier Architecture** is the most common model.

| Tier | Description | Key Components |
| :--- | :--- | :--- |
| **1. Presentation Layer** | The **Front End**. This is what the user interacts with in their browser. It's responsible for the user interface (UI) and user experience (UX). | **HTML, CSS, JavaScript** |
| **2. Application Layer** | The **Back End** or **Business Logic Layer**. This layer runs on the server and processes client requests, enforces business rules, handles user authentication, and interacts with the data layer. | **Web Server** (Apache, Nginx), **Application Logic** (PHP, Python, Java) |
| **3. Data Layer** | The **Database Layer**. This tier is responsible for storing, retrieving, and managing the application's data. | **Database Server** (MySQL, PostgreSQL, Microsoft SQL Server) |

---

## 3. Modern Architectural Concepts

### Microservices
*   **What it is:** An architectural style where a large, monolithic application is broken down into a collection of smaller, independent, and loosely coupled services.
*   **Analogy:** Instead of one giant application that handles everything for an online store, you have separate "microservices" for user registration, product search, payment processing, and reviews.
*   **How they Communicate:** These services communicate with each other over a network, typically using lightweight APIs.
*   **Benefits:** Agility (teams can work on services independently), flexible scaling, and resilience (the failure of one small service doesn't bring down the entire application).

### Serverless
*   **What it is:** A cloud computing model where the cloud provider dynamically manages the allocation and provisioning of servers. The developer writes and deploys code in the form of **functions** without worrying about the underlying infrastructure.
*   **Analogy:** You provide the recipe (code), and the cloud provider automatically provides the kitchen, ingredients, and staff (servers and resources) only for the exact amount of time it takes to cook the meal.
*   **Benefits:** No server management, pay-per-use cost model, and automatic scaling.

---

## 4. The Security Perspective

Understanding an application's architecture is critical for a penetration tester.
*   **Architectural Flaws:** A vulnerability may not be in a single line of code but in the overall design. For example, a lack of proper access control between different user roles (**Broken Access Control**) is an architectural flaw.
*   **Mapping the Target:** Identifying the architecture helps you understand the scope of a potential compromise. If you exploit a web server, knowing whether the database is on the same machine or a separate, firewalled server is crucial for planning your next steps (lateral movement).
*   **Security at Every Layer:** Security must be considered at every stage of development and in every layer of the architecture. A flaw in any component can potentially compromise the entire system.
