# DOM, ELEMENTS, NODES AND DYNAMIC HTML (DHTML)

## 1. DOM Concept

**DOM stands for Document Object Model.**

The DOM is a programming interface that represents an HTML document as a structured tree of objects. JavaScript uses this representation to access, modify, add, or remove page content and respond to user interactions.

### Example HTML

```
<html>
    <body>
        <h1 id="heading">Hello</h1>
        <p>Welcome to HTML.</p>
    </body>
</html>
```

### DOM tree representation

```
document
└── html
    └── body
        ├── h1
        │   └── "Hello"
        └── p
            └── "Welcome to HTML."
```

- `document` is the document object.
    
- `html` is the root HTML element.
    
- `body` is a child of `html`.
    
- `h1` and `p` are children of `body`.
    
- Their text content is represented by text nodes.
    

### Why is DOM important?

JavaScript can use the DOM to:

- Change text and HTML content.
    
- Change CSS styles.
    
- Add or remove elements.
    
- Read or modify attributes.
    
- Respond to clicks, keyboard input, and other events.
    

**Exam point:** HTML provides the document structure, the DOM represents it as objects, and JavaScript can manipulate those objects.

## 2. Elements

An element represents an HTML element such as `<h1>`, `<p>`, `<div>`, or `<button>` in the DOM.

Example:

```
<h1 id="title">Hello World</h1>
```

JavaScript can select this element using its ID:

```
const heading = document.getElementById("title");
```

Here, `heading` refers to the DOM object representing the `<h1>` element.

### Important DOM selection methods

|Method|Purpose|
|---|---|
|`getElementById("id")`|Selects an element by ID|
|`getElementsByClassName("name")`|Returns a live `HTMLCollection` of elements with a class|
|`getElementsByTagName("p")`|Returns a live `HTMLCollection` of elements with a tag name|
|`querySelector("selector")`|Returns the first matching element|
|`querySelectorAll("selector")`|Returns a static `NodeList` of matching elements|

Example:

```
<p class="info">First paragraph</p>
<p class="info">Second paragraph</p>

<script>
    const first = document.querySelector(".info");
    const all = document.querySelectorAll(".info");
</script>
```

- `first` refers to the first matching paragraph.
    
- `all` contains references to both matching paragraphs.
    

**Exam trap:**

- `querySelector()` returns the first match.
    
- `querySelectorAll()` returns all matches in a static `NodeList`.
    
- `getElementsByClassName()` and `getElementsByTagName()` return live `HTMLCollection` objects.
    

## 3. Nodes

A **node** is a fundamental object in the DOM tree. Elements are one type of node, but not every node is an element.

### Types of DOM nodes

|Node type|Example|Purpose|
|---|---|---|
|Document node|`document`|Represents the document|
|Element node|`<p>`, `<div>`|Represents an HTML element|
|Text node|`Hello World`|Represents text content|
|Comment node|`<!-- note -->`|Represents an HTML comment|
|Attribute|`id="title"`|Attribute information associated with an element|

Attributes have their own DOM objects, but they are not ordinary child nodes of an element.

Example:

```
<body>
    <h1 id="title">Hello</h1>
    <!-- Page comment -->
</body>
```

This contains a document node, element nodes, a text node, and a comment node. The `id` attribute belongs to the heading element.

### Element vs Node

|Element|Node|
|---|---|
|Specifically represents an HTML element|General term for objects in the DOM tree|
|Is a type of node|Includes elements, text, comments, and the document|
|Example: `<h1>`|Examples: `<h1>`, its text, and a comment|

**Remember:** Every HTML element is a node, but not every node is an HTML element.

### Parent, child and sibling nodes

Consider:

```
<div id="parent">
    <p>First</p>
    <p>Second</p>
</div>
```

- `div` is the parent element of both paragraphs.
    
- Each `p` is a child element of `div`.
    
- The two paragraphs are sibling elements.
    
- Their text is represented by text nodes.
    

Useful DOM properties:

```
element.parentElement;
element.children;
element.firstElementChild;
element.nextElementSibling;
element.textContent;
```

### `children` vs `childNodes`

- `children` returns child **elements only**.
    
- `childNodes` returns all child nodes, including text and comment nodes.
    

Whitespace between HTML tags can create text nodes, so `childNodes.length` may be greater than `children.length`.

## 4. Dynamic HTML (DHTML)

**DHTML stands for Dynamic HTML.**

DHTML refers to using technologies such as HTML, CSS, JavaScript, and the DOM together to change a webpage after it has loaded, often in response to user actions.

DHTML is not a separate programming language. It describes the technique of making web pages interactive and dynamically changeable.

### A. Change text using JavaScript

```
<h1 id="title">Old Heading</h1>

<script>
    document.getElementById("title").textContent =
        "New Heading";
</script>
```

The heading changes from “Old Heading” to “New Heading”.

### B. Change HTML content

```
<div id="box"></div>

<script>
    document.getElementById("box").innerHTML =
        "<p>Hello from JavaScript</p>";
</script>
```

`innerHTML` interprets the supplied string as HTML markup.

**Security point:** Avoid inserting untrusted input using `innerHTML`, as it can create cross-site scripting (XSS) vulnerabilities. Use `textContent` when you want to insert plain text.

### C. Change CSS styles

```
<p id="message">Welcome</p>

<script>
    const msg = document.getElementById("message");

    msg.style.color = "blue";
    msg.style.fontSize = "24px";
</script>
```

JavaScript changes the paragraph's text color and font size.

### D. Add an element dynamically

```
<div id="container"></div>

<script>
    const paragraph = document.createElement("p");
    paragraph.textContent = "New paragraph";

    document.getElementById("container")
        .appendChild(paragraph);
</script>
```

What happens?

1. `createElement("p")` creates a paragraph element.
    
2. `textContent` assigns its text.
    
3. `appendChild()` inserts it into the container.
    

### E. Remove an element

```
<p id="removeMe">This will be removed.</p>

<script>
    document.getElementById("removeMe").remove();
</script>
```

The paragraph is removed from the DOM.

### F. Respond to a button click

```
<p id="output">Original text</p>
<button id="changeBtn">Change Text</button>

<script>
    document.getElementById("changeBtn")
        .addEventListener("click", function () {
            document.getElementById("output").textContent =
                "Text changed!";
        });
</script>
```

When the button is clicked, the paragraph's text changes.

**Exam point:** `addEventListener()` attaches an event handler. The `"click"` event occurs when the user clicks the button.

## 5. Important DOM Properties and Methods

|Property or method|Use|
|---|---|
|`document.title`|Reads or changes the document title|
|`textContent`|Gets or sets text content|
|`innerHTML`|Gets or sets HTML markup inside an element|
|`innerText`|Gets or sets rendered text|
|`getAttribute()`|Reads an attribute value|
|`setAttribute()`|Sets an attribute value|
|`createElement()`|Creates an element|
|`appendChild()`|Appends a node as a child|
|`remove()`|Removes an element|
|`classList.add()`|Adds a CSS class|
|`classList.remove()`|Removes a CSS class|
|`classList.toggle()`|Adds or removes a class depending on its current state|
|`addEventListener()`|Registers an event handler|

### `textContent` vs `innerHTML` vs `innerText`

|Feature|`textContent`|`innerHTML`|`innerText`|
|---|---|---|---|
|Reads text|Yes|Returns markup as a string|Returns rendered text|
|Parses HTML when setting|No|Yes|No|
|Includes hidden descendant text when reading|Generally yes|Returns markup, including hidden elements represented in markup|Generally excludes non-rendered text|
|Common use|Safely set plain text|Insert trusted HTML markup|Work with rendered text|

Example:

```
const box = document.getElementById("box");

box.textContent = "<b>Hello</b>";
```

This displays the literal text `<b>Hello</b>` rather than making it bold.

However:

```
box.innerHTML = "<b>Hello</b>";
```

This interprets the markup and displays **Hello** in bold.

## 6. Quick Revision Sheet

|Topic|Key fact|
|---|---|
|DOM full form|Document Object Model|
|DHTML full form|Dynamic HTML|
|DOM representation|Tree of objects|
|JavaScript selection by ID|`getElementById()`|
|First matching element|`querySelector()`|
|All matching elements|`querySelectorAll()`|
|Live collection by class|`getElementsByClassName()`|
|Create an element|`createElement()`|
|Insert a child|`appendChild()`|
|Remove an element|`remove()`|
|Read or set plain text|`textContent`|
|Read or set HTML markup|`innerHTML`|
|Read rendered text|`innerText`|
|Add an event handler|`addEventListener()`|
|Add a CSS class|`classList.add()`|
|Remove a CSS class|`classList.remove()`|
|Toggle a CSS class|`classList.toggle()`|
|Child elements only|`children`|
|All child nodes|`childNodes`|

## 7. Important MCQ Traps

1. **What is the full form of DOM?** Document Object Model.
    
2. **Is DHTML a separate programming language?** No.
    
3. **Which method selects an element by ID?** `getElementById()`.
    
4. **Which method returns the first matching element?** `querySelector()`.
    
5. **Which method returns all matching elements in a static collection?** `querySelectorAll()`.
    
6. **Which returns a live** `**HTMLCollection**` **by class name?** `getElementsByClassName()`.
    
7. **Are all DOM nodes HTML elements?** No.
    
8. **Which property sets plain text?** `textContent`.
    
9. **Which property interprets supplied HTML markup?** `innerHTML`.
    
10. **Which method creates an element?** `createElement()`.
    
11. **Which method appends a child node?** `appendChild()`.
    
12. **Which method registers an event handler?** `addEventListener()`.
    
13. **Which property returns child elements only?** `children`.
    
14. **Which property returns text and comment nodes as well as elements?** `childNodes`.
    
15. **Which method removes an element?** `remove()`.