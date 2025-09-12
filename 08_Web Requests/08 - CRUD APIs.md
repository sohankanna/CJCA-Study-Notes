# 08 - CRUD APIs

## 1. What is a CRUD API?

A CRUD API exposes endpoints that allow a client to manage data in a database. It typically maps the four CRUD operations directly to standard HTTP request methods.

### The CRUD Operations and HTTP Methods

| Operation | HTTP Method | Description |
| :--- | :--- | :--- |
| **C**reate | `POST` | Adds a new entry or resource to the database. |
| **R**ead | `GET` | Retrieves an existing resource or a list of resources. |
| **U**pdate | `PUT` / `PATCH` | Modifies an existing resource. `PUT` typically replaces the entire resource, while `PATCH` applies a partial update. |
| **D**elete | `DELETE` | Removes an existing resource from the database. |

### API Endpoint Structure
A common way to structure these API endpoints is to use the URL path to identify the resource.
*   **Endpoint:** `/api.php/table/identifier`
*   **Example:** `http://<SERVER_IP>/api.php/city/london`
    *   `city`: The database table.
    *   `london`: The specific row/entry to act upon.

---

## 2. Interacting with the API using `cURL`

### Read (`GET`)
The `GET` method is used to retrieve data.

*   **Get a specific entry:**
    ```shell
    curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq
    ```
    *(The output is piped to `jq` to pretty-print the JSON response).*

*   **Search for entries:**
    ```shell
    curl -s http://<SERVER_IP>:<PORT>/api.php/city/le | jq
    ```

*   **Get all entries:**
    ```shell
    curl -s http://<SERVER_IP>:<PORT>/api.php/city/ | jq
    ```

### Create (`POST`)
The `POST` method is used to add a new entry. The data for the new entry is sent in the request body, often in JSON format.

*   **Syntax:**
    ```shell
    curl -X POST -d '<JSON_data>' -H 'Content-Type: application/json' <URL>
    ```
*   **Example:**
    ```shell
    curl -X POST \
      -d '{"city_name":"HTB_City", "country_name":"HTB"}' \
      -H 'Content-Type: application/json' \
      http://<SERVER_IP>:<PORT>/api.php/city/
    ```

### Update (`PUT`)
The `PUT` method is used to modify an existing entry. You must specify which entry to update in the URL.

*   **Syntax:**
    ```shell
    curl -X PUT -d '<JSON_data>' -H 'Content-Type: application/json' <URL/with/identifier>
    ```
*   **Example:**
    ```shell
    # This command finds the 'london' entry and updates its data
    curl -X PUT \
      -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' \
      -H 'Content-Type: application/json' \
      http://<SERVER_IP>:<PORT>/api.php/city/london
    ```

### Delete (`DELETE`)
The `DELETE` method is used to remove an entry. You simply specify the entry to delete in the URL.

*   **Syntax:**
    ```shell
    curl -X DELETE <URL/with/identifier>
    ```
*   **Example:**
    ```shell
    curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City
    ```

---

## Security Considerations

In a real-world application, these API endpoints would be protected by authentication and authorization mechanisms.
*   **Authentication:** A user would need to provide a valid **cookie** or an **`Authorization` header** (e.g., with a Bearer Token) to prove their identity.
*   **Authorization:** Even if authenticated, a user's privileges would be checked. A standard user might only be able to `GET` (read) data, while an administrator would have privileges to `POST`, `PUT`, and `DELETE` as well.

Discovering an API endpoint that lacks proper authorization controls (allowing any user to delete or modify data) is a critical security vulnerability.
