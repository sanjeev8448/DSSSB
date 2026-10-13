
HTML (HyperText Markup Language) is the standard markup language used to structure content on web pages. It defines elements such as headings, paragraphs, links, images, tables, and forms.

**Important:** HTML is a markup language, not a programming language. It describes the structure of content rather than providing general-purpose programming logic.

## 1. Basic Structure of HTML

### Basic HTML document

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My First Web Page</title>
</head>
<body>
    <h1>Welcome</h1>
    <p>This is my first web page.</p>
</body>
</html>
```

### Explanation of each part

|Element|Purpose|
|---|---|
|`<!DOCTYPE html>`|Declares an HTML5 document|
|`<html>`|Root element of the page|
|`<head>`|Contains metadata and resource references|
|`<meta charset="UTF-8">`|Specifies character encoding|
|`<title>`|Sets the browser tab's title|
|`<body>`|Contains the visible page content|
|`<h1>`|Defines a top-level heading|
|`<p>`|Defines a paragraph|

**Important exam point:** `<!DOCTYPE html>` is a declaration, not an ordinary HTML element. It tells the browser to render the document using standards mode.

---

## 2. HTML Tags and Elements

A **tag** is the markup notation enclosed in angle brackets. An **element** generally consists of the opening tag, its content, and the closing tag.

Example:

```
<p>Hello World</p>
```

- `<p>` — opening tag
    
- `Hello World` — content
    
- `</p>` — closing tag
    
- The complete markup is a paragraph element.
    

### Types of elements

**A. Paired elements**

They typically have opening and closing tags.

```
<h1>Heading</h1>
<p>Paragraph text</p>
```

**B. Void elements**

These do not have closing tags in HTML.

```
<br>
<img src="photo.jpg" alt="A photograph">
```

Other common void elements include `<hr>`, `<input>`, `<meta>`, and `<link>`.

**C. Nested elements**

Elements can be placed inside other elements.

```
<p>This is <strong>important</strong> text.</p>
```

Nesting should be valid. For example, close the `<strong>` element before closing the `<p>` element.

---

## 3. Headings: `<h1>` to `<h6>`

HTML provides six heading levels, from `<h1>` (highest level) to `<h6>` (lowest level).

```
<h1>Main Heading</h1>
<h2>Section Heading</h2>
<h3>Subsection Heading</h3>
<h4>Heading Level 4</h4>
<h5>Heading Level 5</h5>
<h6>Heading Level 6</h6>
```

- `<h1>` represents the main heading.
    
- `<h2>` represents a section beneath it.
    
- `<h3>` can represent a subsection under `<h2>`.
    
- `<h6>` is the lowest heading level.
    

**Exam trap:** HTML has six heading levels, not seven. Heading levels represent document structure; CSS controls their visual appearance.

---

## 4. Paragraph: `<p>`

The `<p>` element defines a paragraph.

```
<p>HTML is used to structure web pages.</p>
<p>CSS controls presentation.</p>
```

Browsers generally display paragraphs as separate blocks with default spacing.

### Line break: `<br>`

The `<br>` element inserts a line break without starting a new paragraph.

```
<p>
    First line<br>
    Second line
</p>
```

### Difference between `<p>` and `<br>`

|`<p>`|`<br>`|
|---|---|
|Defines a paragraph|Inserts a line break|
|A semantic block element|A void element|
|Usually has default paragraph spacing|Does not create a new paragraph|

Use CSS for visual spacing rather than inserting many `<br>` elements.

---

## 5. Links: `<a>`

The anchor element `<a>` creates a hyperlink. The `href` attribute specifies its destination.

```
<a href="https://www.example.com">Visit Example</a>
```

### Common types of links

```
<!-- External website -->
<a href="https://www.example.com">Example</a>

<!-- Another page on the same website -->
<a href="about.html">About Us</a>

<!-- Email link -->
<a href="mailto:test@example.com">Send Email</a>

<!-- Link to an element on the current page -->
<a href="#contact">Go to Contact</a>

<h2 id="contact">Contact</h2>
```

### Important attributes

- `href` — destination URL or fragment.
    
- `target="_blank"` — typically opens the destination in a new tab or window.
    
- `title` — provides advisory information, often displayed on hover.
    
- `download` — suggests downloading a linked resource.
    

For links using `target="_blank"`, modern browsers generally provide implicit protection against access to the originating page through `window.opener`; explicitly using `rel="noopener"` can still make the intention clear.

---

## 6. Images: `<img>`

The `<img>` element embeds an image in a web page.

```
<img src="flower.jpg" alt="A red flower">
```

### Important attributes

|Attribute|Meaning|
|---|---|
|`src`|Image source or path|
|`alt`|Text alternative describing the image|
|`width`|Display width|
|`height`|Display height|
|`title`|Optional advisory information|

Example:

```
<img src="logo.png"
     alt="Company logo"
     width="200"
     height="100">
```

### Exam traps

- `<img>` is a void element.
    
- `src` identifies the image resource.
    
- `alt` provides a text alternative, especially important when the image cannot be seen or loaded.
    
- HTML attributes generally appear in the opening tag.
    

---

## 7. Tables in HTML

HTML tables display information arranged in rows and columns.

### Important table tags

|Tag|Purpose|
|---|---|
|`<table>`|Creates a table|
|`<tr>`|Defines a table row|
|`<th>`|Defines a header cell|
|`<td>`|Defines a data cell|
|`<caption>`|Adds a table caption|
|`<thead>`|Groups header rows|
|`<tbody>`|Groups body rows|
|`<tfoot>`|Groups footer rows|

### Example

```
<table border="1">
    <caption>Student Marks</caption>
    <thead>
        <tr>
            <th>Name</th>
            <th>Marks</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Rahul</td>
            <td>85</td>
        </tr>
        <tr>
            <td>Priya</td>
            <td>92</td>
        </tr>
    </tbody>
</table>
```

**Expected table structure:**

|Name|Marks|
|---|---|
|Rahul|85|
|Priya|92|

### `colspan` and `rowspan`

- `colspan` makes a cell span multiple columns.
    
- `rowspan` makes a cell span multiple rows.
    

```
<table border="1">
    <tr>
        <th colspan="2">Student Details</th>
    </tr>
    <tr>
        <td>Name</td>
        <td>Rahul</td>
    </tr>
</table>
```

**Exam trap:** `<th>` is normally used for header cells, while `<td>` is used for ordinary data cells. The `border` attribute is an older presentation technique; CSS is preferred for styling modern HTML tables.

---

## 8. Forms in HTML

An HTML form collects user input and can submit it to a server.

### Important form tags

|Tag|Purpose|
|---|---|
|`<form>`|Defines a form|
|`<input>`|Accepts different types of input|
|`<label>`|Provides a label for a control|
|`<textarea>`|Accepts multiline text|
|`<select>`|Creates a selection menu|
|`<option>`|Defines a menu option|
|`<button>`|Creates a button|
|`<fieldset>`|Groups related controls|
|`<legend>`|Provides a caption for a fieldset|

### Example

```
<form action="/submit" method="post">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>

    <br><br>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email">

    <br><br>

    <label for="course">Course:</label>
    <select id="course" name="course">
        <option value="cse">CSE</option>
        <option value="it">IT</option>
    </select>

    <br><br>

    <button type="submit">Submit</button>
</form>
```

### Common input types

|Type|Use|
|---|---|
|`text`|Single-line text|
|`password`|Password entry, visually masked by default|
|`email`|Email input with built-in format validation|
|`number`|Numeric input|
|`radio`|Select one option from a group|
|`checkbox`|Select zero or more options|
|`date`|Date selection|
|`file`|File selection|
|`submit`|Submit the form|
|`reset`|Reset controls to their initial values|
|`hidden`|A form control not normally displayed|

Example:

```
<input type="radio" name="gender" value="male"> Male
<input type="radio" name="gender" value="female"> Female

<input type="checkbox" name="skill" value="html"> HTML
<input type="checkbox" name="skill" value="css"> CSS
```

Radio buttons with the same `name` are generally grouped so that only one can be selected in that group. Checkboxes can be selected independently.

### Important form attributes

- `action` — URL that receives the submitted form data.
    
- `method` — HTTP method, commonly `get` or `post`.
    
- `name` — identifies the control's data in form submission.
    
- `required` — requires a value before submission.
    
- `placeholder` — displays a hint inside an input.
    
- `value` — specifies a control's value.
    
- `id` — uniquely identifies an element within the document.
    

### GET vs. POST

|GET|POST|
|---|---|
|Commonly used to retrieve resources|Commonly used to submit data or request changes|
|Form data is commonly included in the URL query string|Form data is commonly sent in the request body|
|Often suitable for searches and filters|Often suitable for submitting forms|
|URLs can be bookmarked with query parameters|Request body is not normally shown in the URL|

**Exam trap:** POST does not automatically encrypt data. HTTPS provides transport encryption. Also, form controls generally need a `name` attribute to contribute their values to ordinary form submission.

---

## 9. HTML Attributes

Attributes provide additional information or configuration for an HTML element. They are normally written in the opening tag.

```
<a href="https://www.example.com"
   target="_blank"
   title="Visit Example">
    Open Website
</a>
```

### Global attributes

These can be used on many HTML elements.

|Attribute|Purpose|
|---|---|
|`id`|Unique identifier within the document|
|`class`|Groups elements for CSS or JavaScript|
|`style`|Adds inline CSS|
|`title`|Advisory information|
|`lang`|Declares the language|
|`hidden`|Indicates that an element is not currently relevant for display|
|`data-*`|Stores custom data on elements|

Example:

```
<p id="intro" class="highlight" style="color: blue;">
    Welcome to HTML.
</p>
```

Here, `id`, `class`, and `style` are attributes.

### Attribute vs. element

|Element|Attribute|
|---|---|
|`<a>`|`href`|
|`<img>`|`src`, `alt`|
|`<input>`|`type`, `name`, `required`|
|`<form>`|`action`, `method`|

**Remember:** `href` is not an HTML tag; it is an attribute of an element such as `<a>`.

---

## 10. Lists in HTML

HTML provides three main list types.

### A. Ordered list: `<ol>`

Displays items in a sequence, commonly numbered.

```
<ol>
    <li>Wake up</li>
    <li>Study HTML</li>
    <li>Practise MCQs</li>
</ol>
```

### B. Unordered list: `<ul>`

Displays items with bullets by default.

```
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ul>
```

### C. Description list: `<dl>`

Used for terms and their descriptions.

```
<dl>
    <dt>HTML</dt>
    <dd>Structures web content.</dd>

    <dt>CSS</dt>
    <dd>Styles web content.</dd>
</dl>
```

|Tag|Meaning|
|---|---|
|`<ol>`|Ordered list|
|`<ul>`|Unordered list|
|`<li>`|List item|
|`<dl>`|Description list|
|`<dt>`|Term or name|
|`<dd>`|Description or details|

**Exam trap:** `<li>` is used for list items in ordered and unordered lists. `<dt>` and `<dd>` belong to description lists.

---

## 11. The `<head>` Element

The `<head>` contains document metadata and references to resources. Its contents are generally not displayed as ordinary page content.

```
<head>
    <title>My Website</title>
    <meta charset="UTF-8">
    <meta name="description" content="Learning HTML">
    <link rel="stylesheet" href="style.css">
    <script src="app.js" defer></script>
</head>
```

|Element|Purpose|
|---|---|
|`<title>`|Sets the document title shown in the browser tab|
|`<meta>`|Supplies metadata|
|`<link>`|Links external resources, commonly CSS files|
|`<style>`|Contains embedded CSS|
|`<script>`|Embeds or references JavaScript|
|`<base>`|Sets the base URL or default target for relative URLs|

**Exam trap:** `<head>` and `<header>` are different. The `<head>` contains metadata; `<header>` is a semantic element for introductory content within a page or section.

---

## 12. The `<body>` Element

The `<body>` contains the document's main content, such as headings, paragraphs, images, links, tables, and forms.

```
<!DOCTYPE html>
<html>
<head>
    <title>Student Portal</title>
</head>
<body>
    <h1>Student Portal</h1>
    <p>Welcome to the portal.</p>
    <a href="courses.html">View Courses</a>
</body>
</html>
```

A standard HTML document has one `<head>` and one `<body>` element.

---

## 13. HTML Comments

Comments are notes in the HTML source that browsers do not display as ordinary page content.

### Syntax

```
<!-- This is an HTML comment -->

<h1>Welcome</h1>

<!--
This is a
multiline comment.
-->
```

### Important facts

- Comments begin with `<!--` and end with `-->`.
    
- They are useful for documenting code and temporarily annotating markup.
    
- HTML comments cannot be nested reliably.
    
- Comments are still visible to anyone who can inspect the page source, so never store passwords or secrets in them.
    

**Exam trap:** HTML comments are different from CSS comments (`/* ... */`) and JavaScript comments (`// ...` or `/* ... */`).

---

## 14. Complete HTML Example

This combines the major topics in the syllabus.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Student Information</title>
</head>
<body>
    <!-- Main heading -->
    <h1>Student Information</h1>

    <p>Welcome to the student portal.</p>
    <p>Learn <strong>HTML</strong> step by step.</p>

    <h2>Useful Website</h2>
    <a href="https://www.example.com">Visit Example</a>

    <h2>Course Image</h2>
    <img src="course.jpg" alt="Computer course">

    <h2>Subjects</h2>
    <ul>
        <li>HTML</li>
        <li>CSS</li>
    </ul>

    <h2>Marks</h2>
    <table border="1">
        <tr>
            <th>Subject</th>
            <th>Marks</th>
        </tr>
        <tr>
            <td>Computer Science</td>
            <td>90</td>
        </tr>
    </table>

    <h2>Contact Form</h2>
    <form action="/submit" method="post">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
        <br><br>
        <button type="submit">Submit</button>
    </form>
</body>
</html>
```

---

## 15. Last-Minute Revision Sheet

|Question concept|Correct fact|
|---|---|
|HTML full form|HyperText Markup Language|
|HTML5 doctype|`<!DOCTYPE html>`|
|Largest heading level|`<h1>`|
|Smallest heading level|`<h6>`|
|Paragraph|`<p>`|
|Line break|`<br>`|
|Hyperlink|`<a>`|
|Image|`<img>`|
|Table row|`<tr>`|
|Table header cell|`<th>`|
|Table data cell|`<td>`|
|Ordered list|`<ol>`|
|Unordered list|`<ul>`|
|List item|`<li>`|
|Form|`<form>`|
|Input control|`<input>`|
|Metadata section|`<head>`|
|Main document content|`<body>`|
|Comment|`<!-- ... -->`|
|Link destination attribute|`href`|
|Image source attribute|`src`|
|Image text alternative|`alt`|
|Unique element identifier|`id`|

## Highest-Priority DSSSB Exam Traps

1. **HTML is a markup language**, not a programming language.
    
2. `**<!DOCTYPE html>**` is a declaration, not an ordinary element.
    
3. **Six heading levels:** `<h1>` through `<h6>`.
    
4. **Void elements:** `<br>`, `<img>`, `<hr>`, `<input>`, `<meta>`, and `<link>`.
    
5. `**<head>**` **vs.** `**<header>**`**:** Metadata section vs. semantic introductory content.
    
6. `**href**` **vs.** `**src**`**:** `href` specifies a link destination; `src` identifies a resource such as an image.
    
7. `**<th>**` **vs.** `**<td>**`**:** Header cell vs. ordinary data cell.
    
8. `**<ol>**` **vs.** `**<ul>**`**:** Ordered vs. unordered list.
    
9. **Radio buttons vs. checkboxes:** Radio buttons with the same name form a single-choice group; checkboxes can be selected independently.
    
10. **GET vs. POST:** GET commonly places form parameters in the URL; POST commonly sends them in the request body. POST alone does not provide encryption.
    
11. `**id**` **vs.** `**class**`**:** `id` identifies an element uniquely within the document; `class` groups elements.
    
12. **HTML comments:** They are visible in the page source and must not contain secrets.