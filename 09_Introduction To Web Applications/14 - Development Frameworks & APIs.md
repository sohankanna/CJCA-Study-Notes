# 14 - Development Frameworks & APIs

## 1. Web Development Frameworks

A **web development framework** is a pre-written, standardized set of tools, libraries, and best practices that provides a foundation for building web applications.

*   **Core Idea:** Instead of building a web application from scratch, developers use a framework to handle common, repetitive tasks (like routing, database interaction, and user authentication). This allows them to focus on the unique business logic of their application, leading to faster and more reliable development.

### Popular Back-End Frameworks by Language

| Language | Framework(s) | Used By |
| :--- | :--- | :--- |
| **PHP** | **Laravel**, Symfony | Startups and smaller companies, known for ease of use. |
| **Python**| **Django**, Flask | Google, YouTube, Instagram. Django is a full-featured framework, while Flask is more lightweight. |
| **Ruby** | **Ruby on Rails** | GitHub, Airbnb, Twitch. Known for its "convention over configuration" philosophy. |
| **JavaScript (Node.js)**| **Express.js**| PayPal, Uber, IBM. The most popular framework for building back ends with JavaScript. |
| **Java** | Spring | Common in large enterprise applications. |
| **C#** | ASP.NET | Core to the Microsoft development ecosystem. |

---

## 2. APIs (Application Programming Interfaces)

An **API** is a set of rules and definitions that allows one software application to communicate with another. In web development, APIs are the crucial link that enables the **front end** to interact with the **back end**.

*   **Core Idea:** The API defines the "contract" for communication. It specifies what requests the back end will accept, what data the front end needs to provide, and what the back end will return.

### Query Parameters
The simplest way to send data from the front end to the back end is through **query parameters** in an HTTP request.
*   **GET Request:** Parameters are appended to the URL.
    ```
    /search.php?item=apples&category=fruit
    ```
*   **POST Request:** Parameters are sent in the request body.
    ```http
    POST /search.php HTTP/1.1
    Host: example.com
    Content-Type: application/x-www-form-urlencoded

    item=apples&category=fruit
```
### Web API Architectural Styles
For more complex interactions, web applications use standardized API styles.

#### a) REST (Representational State Transfer)
**REST** is the most popular architectural style for designing web APIs. It is a set of principles, not a strict protocol.

*   **Core Principles:**
    *   **Client-Server:** The client and server are separate.
    *   **Stateless:** Each request from a client to a server must contain all the information needed to understand and complete the request. The server does not store any client state between requests.
    *   **Resource-Based:** Functionality is exposed through **resources**, which are identified by URLs (e.g., `/users/123`, `/posts/456`).
*   **HTTP Methods:** REST APIs make heavy use of standard HTTP methods to perform **CRUD** (Create, Read, Update, Delete) operations on resources.
    *   `GET /users/123`: **Read** the data for user 123.
    *   `POST /users`: **Create** a new user.
    *   `PUT /users/123`: **Update/Replace** the data for user 123.
    *   `DELETE /users/123`: **Delete** user 123.
*   **Data Format:** REST APIs most commonly use **JSON** for transmitting data, but can also use XML or other formats.

#### b) SOAP (Simple Object Access Protocol)
**SOAP** is an older, more rigid protocol-based standard for exchanging structured information.

*   **Core Principles:**
    *   **Strict Protocol:** Has a strict set of rules for message structure.
    *   **XML-Based:** All SOAP messages **must** be formatted as XML.
*   **Use Case:** Often used in legacy enterprise environments, especially for stateful operations or when complex transactions are required. It is generally considered more complex and less efficient than REST for most modern web use cases.
