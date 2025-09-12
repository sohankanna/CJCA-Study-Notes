# 05 - Cascading Style Sheets

## 1. What is CSS?

If HTML provides the **structure and content** (the skeleton) of a webpage, **CSS** provides the **style and visual presentation** (the clothes, hair, and makeup). It controls everything from colors and fonts to layout and animations.

*   **Core Idea:** CSS separates the content of a document from its presentation. This allows developers to change the entire look and feel of a website by editing a single CSS file, without having to alter the underlying HTML structure of each page.

---

## 2. CSS Syntax

CSS works by creating **rules** that select specific HTML elements and apply stylistic properties to them.

### A Basic CSS Rule
```css
selector {
  property: value;
}
```
*   **Selector:** The pattern used to select the HTML element(s) you want to style.
*   **Declaration Block `{}`:** Contains one or more declarations.
*   **Declaration:** A combination of a `property` and its `value`, ending with a semicolon.

### Example CSS
```css
/* Selects the <body> element */
body {
  background-color: black;
}

/* Selects all <h1> elements */
h1 {
  color: white;
  text-align: center;
}

/* Selects all <p> elements */
p {
  font-family: helvetica;
  font-size: 10px;
}
```

### How CSS Selects Elements
*   **By Tag Name:** As seen above (`body`, `h1`, `p`).
*   **By Class Name:** Selects all elements with a specific `class` attribute. The selector starts with a dot (`.`).
    *   **HTML:** `<p class="error-message">Warning!</p>`
    *   **CSS:** `.error-message { color: red; }`
*   **By ID:** Selects a single, unique element with a specific `id` attribute. The selector starts with a hash (`#`).
    *   **HTML:** `<div id="main-content">...</div>`
    *   **CSS:** `#main-content { border: 1px solid black; }`

---

## 3. How CSS is Applied to a Webpage

There are three ways to include CSS in an HTML document:

1.  **External Stylesheet (Best Practice):** The CSS rules are placed in a separate `.css` file, which is then linked in the HTML `<head>` section. This is the most efficient and maintainable method.
    ```html
    <head>
      <link rel="stylesheet" href="styles.css">
    </head>
    ```
2.  **Internal Stylesheet:** The CSS rules are placed inside a `<style>` tag directly within the HTML `<head>`.
3.  **Inline Styles:** CSS rules are applied directly to a single HTML element using the `style` attribute. This is generally discouraged as it mixes content and presentation.

---

## 4. CSS Frameworks

To speed up development and ensure consistency, developers often use **CSS frameworks**. These are pre-written libraries of CSS code that provide ready-to-use components for grids, buttons, forms, navigation, and more.

### Popular CSS Frameworks
*   **Bootstrap:** The most popular and widely used CSS framework.
*   **SASS (Syntactically Awesome Style Sheets):** A CSS preprocessor that adds advanced features like variables, nesting, and functions to CSS.
*   **Foundation**
*   **Bulma**

---

## 5. Security Relevance

While CSS itself is not a programming language and is generally considered safe, it can be a vector in certain types of attacks:

*   **UI Redressing (Clickjacking):** Attackers can use CSS (specifically opacity and positioning) to create transparent, invisible elements over legitimate buttons. A user thinks they are clicking "Play Video" but are actually clicking an invisible "Delete Account" button on a different, hidden website loaded in an iframe.
*   **Data Exfiltration:** Advanced and creative CSS techniques can sometimes be used to slowly exfiltrate sensitive data (like CSRF tokens) from a page by making conditional style changes based on the data's value, which can then be monitored by an attacker.
*   **Keylogging:** CSS attribute selectors can be abused in some niche scenarios to infer what a user is typing into a form, character by character.
