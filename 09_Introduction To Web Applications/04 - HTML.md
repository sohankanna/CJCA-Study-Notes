# 04 - HTML

## 1. What is HTML?

**HTML** is a markup language that uses **tags** to define the elements of a web page. A web browser reads an HTML document, interprets these tags, and renders the content for the user to see.

*   **Core Idea:** HTML provides the **skeleton** of a webpage. It defines what each piece of content *is* (e.g., this is a heading, this is a paragraph, this is an image).
*   **Tags and Elements:**
    *   An **element** is a component of a webpage.
    *   Most elements are defined by a starting **tag** (e.g., `<p>`) and a corresponding closing tag (e.g., `</p>`).
    *   The content of the element is placed between these tags.
    *   The entire construct—start tag, content, and end tag—makes up the HTML element.

### Basic HTML Page Structure
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Page Title</title>
        <!-- Metadata like CSS and scripts go here -->
    </head>
    <body>
        <h1>A Heading</h1>
        <p>A Paragraph</p>
        <!-- Visible page content goes here -->
    </body>
</html>
```
*   **`<!DOCTYPE html>`**: Declares the document type.
*   **`<html>`**: The root element that wraps the entire page.
*   **`<head>`**: Contains meta-information about the page that is not displayed directly, such as the `<title>`, links to CSS stylesheets, and `<script>` tags.
*   **`<body>`**: Contains all the visible content of the webpage, such as headings, paragraphs, images, and links.

---

## 2. The Document Object Model (DOM)

The **DOM (Document Object Model)** is the browser's internal, tree-like representation of an HTML document. When a browser loads a webpage, it parses the HTML and creates a logical tree of objects (nodes).

*   **Core Idea:** The DOM provides a structured interface that allows programming languages (primarily JavaScript) to access and dynamically manipulate the content, structure, and style of a document.
*   **Structure:** The `document` object is the root of the tree. Each HTML element becomes a node in this tree.
    *   `document`
        *   `html`
            *   `head`
                *   `title`
            *   `body`
                *   `h1`
                *   `p`
*   **Security Relevance:** Front-end vulnerabilities like **Cross-Site Scripting (XSS)** often work by injecting malicious JavaScript that manipulates the DOM to steal information or perform unauthorized actions on behalf of the user.

---

## 3. URL Encoding (Percent-Encoding)

URLs can only contain a limited set of characters from the ASCII character set. Any character outside of this safe set (like spaces, quotes, or other special symbols) must be **URL encoded** to be transmitted correctly.

*   **How it Works:** URL encoding replaces an unsafe character with a **percent sign (`%`)** followed by its two-digit hexadecimal ASCII value.
*   **Purpose:** To ensure that data sent within a URL is not misinterpreted by web servers or browsers. This is a fundamental concept for understanding and crafting web attack payloads.

### Common URL Encoded Characters

| Character | Encoding |
| :--- | :--- |
| **(space)** | `%20` or `+` |
| **`!`** | `%21` |
| **`"`** | `%22` |
| **`#`** | `%23` |
| **`$`** | `%24` |
| **`&`** | `%26` |
| **`'`** | `%27` |
| **`/`** | `%2F` |
| **`:`** | `%3A` |
| **`?`** | `%3F` |

*   **Tools:** Web proxies like **Burp Suite** have built-in decoders/encoders that are essential for analyzing and manipulating this type of data during a penetration test.
