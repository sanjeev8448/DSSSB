# CSS (CASCADING STYLE SHEETS)

## 1. Introduction to CSS

CSS controls how HTML elements appear, including their colors, fonts, spacing, borders, and positioning.

- **HTML:** Defines the structure of a webpage.
    
- **CSS:** Defines the presentation and styling of a webpage.
    

### CSS syntax

```
selector {
    property: value;
}
```

Example:

```
p {
    color: blue;
    font-size: 18px;
}
```

|Part|Meaning|
|---|---|
|`p`|Selector|
|`color`|Property|
|`blue`|Value|
|`font-size`|Property|
|`18px`|Value|

A group of property-value declarations enclosed in curly braces is called a **declaration block**.

## 2. Three Ways to Apply CSS

### A. Inline CSS

Uses the `style` attribute directly inside an HTML element.

```
<p style="color: red;">Hello World</p>
```

### B. Internal CSS

Uses the `<style>` element, usually inside the `<head>` section.

```
<head>
    <style>
        p {
            color: blue;
        }
    </style>
</head>
```

### C. External CSS

Stores styles in a separate `.css` file.

HTML:

```
<link rel="stylesheet" href="style.css">
```

`style.css`:

```
p {
    color: green;
}
```

|Type|Location|Typical use|
|---|---|---|
|Inline|Inside an HTML element|Styling a specific element|
|Internal|Inside a `<style>` element|Styling one HTML document|
|External|Separate `.css` file|Reusing styles across multiple pages|

**Exam points:**

- External CSS is generally preferred for maintainability and reuse.
    
- The `<link>` element connects an external stylesheet.
    
- The `<style>` element contains internal CSS.
    
- The `style` attribute applies inline CSS.
    

## 3. CSS Selectors

A selector determines which HTML elements receive CSS declarations.

### A. Element selector

Selects all elements of a particular type.

```
p {
    color: blue;
}
```

This selects every `<p>` element.

### B. ID selector

Uses `#` to select an element by its ID.

HTML:

```
<p id="intro">Introduction</p>
```

CSS:

```
#intro {
    color: red;
}
```

An ID should be unique within an HTML document.

### C. Class selector

Uses `.` to select elements belonging to a class.

HTML:

```
<p class="highlight">First paragraph</p>
<p class="highlight">Second paragraph</p>
```

CSS:

```
.highlight {
    background-color: yellow;
}
```

A class can be applied to multiple elements.

### D. Universal selector

Selects all elements.

```
* {
    box-sizing: border-box;
}
```

### E. Grouping selector

Applies the same declarations to multiple selectors.

```
h1, h2, p {
    font-family: Arial, sans-serif;
}
```

### F. Descendant selector

Selects matching elements anywhere inside another element.

```
div p {
    color: purple;
}
```

This selects paragraphs inside a `<div>`, including nested descendants.

### G. Child selector

Selects only direct children.

```
div > p {
    color: green;
}
```

### H. Attribute selector

Selects elements based on their attributes.

```
input[type="text"] {
    border: 1px solid gray;
}
```

### I. Pseudo-classes

Select elements in a particular state or condition.

```
a:hover {
    color: red;
}

input:focus {
    border-color: blue;
}
```

Other examples:

- `:first-child`
    
- `:last-child`
    
- `:checked`
    

### J. Pseudo-elements

Style a specific part of an element.

```
p::first-letter {
    font-size: 30px;
}
```

Another common example is `::before`.

### Selector revision table

|Selector|Syntax|Example|
|---|---|---|
|Element|Tag name|`p`|
|ID|`#`|`#header`|
|Class|`.`|`.box`|
|Universal|`*`|`*`|
|Grouping|Comma|`h1, p`|
|Descendant|Space|`div p`|
|Child|`>`|`div > p`|
|Adjacent sibling|`+`|`h1 + p`|
|General sibling|`~`|`h1 ~ p`|
|Attribute|`[attribute]`|`input[type="text"]`|
|Pseudo-class|`:`|`a:hover`|
|Pseudo-element|`::`|`p::first-letter`|

**Important exam distinction:**

- `div p` selects descendant paragraphs at any depth.
    
- `div > p` selects only direct child paragraphs.
    
- `h1 + p` selects the paragraph immediately following an `h1`, when both share the same parent.
    
- `h1 ~ p` selects subsequent sibling paragraphs sharing the same parent.
    

## 4. Common CSS Properties

|Property|Purpose|Example|
|---|---|---|
|`color`|Text color|`color: red;`|
|`background-color`|Background color|`background-color: yellow;`|
|`font-size`|Text size|`font-size: 16px;`|
|`font-family`|Typeface|`font-family: Arial, sans-serif;`|
|`font-weight`|Text thickness|`font-weight: bold;`|
|`font-style`|Text style|`font-style: italic;`|
|`text-align`|Horizontal text alignment|`text-align: center;`|
|`text-decoration`|Text decoration|`text-decoration: underline;`|
|`text-transform`|Changes text casing|`text-transform: uppercase;`|
|`line-height`|Line spacing|`line-height: 1.5;`|

Example:

```
h1 {
    color: navy;
    font-family: Arial, sans-serif;
    font-size: 32px;
    text-align: center;
}

p {
    color: #333333;
    font-size: 16px;
    line-height: 1.5;
}
```

## 5. Units in CSS

|Unit|Meaning|Example|
|---|---|---|
|`px`|CSS pixel|`font-size: 16px;`|
|`%`|Percentage relative to the relevant reference|`width: 50%;`|
|`em`|Relative to the relevant font-size context|`font-size: 1.5em;`|
|`rem`|Relative to the root element's font size|`font-size: 2rem;`|
|`vw`|1% of viewport width|`width: 50vw;`|
|`vh`|1% of viewport height|`height: 50vh;`|

**Exam trap:** `**em**` **vs** `**rem**`

- `em` depends on the relevant element's font-size context.
    
- `rem` is based on the root element's font size.
    
- If the root font size is 16px, then `2rem = 32px`.
    

## 6. Margins

A **margin** is the space outside an element's border. It separates the element from neighboring elements.

```
.box {
    margin-top: 10px;
    margin-right: 20px;
    margin-bottom: 15px;
    margin-left: 5px;
}
```

### Margin shorthand

When four values are specified, the order is **Top, Right, Bottom, Left (TRBL)**.

```
.box {
    margin: 10px 20px 15px 5px;
}
```

|Number of values|Meaning|
|---|---|
|One: `margin: 10px`|All four sides are 10px|
|Two: `margin: 10px 20px`|Top/bottom 10px; left/right 20px|
|Three: `margin: 10px 20px 30px`|Top 10px; left/right 20px; bottom 30px|
|Four: `margin: 10px 20px 30px 40px`|Top 10px; right 20px; bottom 30px; left 40px|

### Centering an element

```
.container {
    width: 400px;
    margin: 0 auto;
}
```

For a block element with a specified width, `margin: 0 auto` can center it horizontally when the layout permits.

**Exam point:** Vertical margins between ordinary block elements can collapse under certain conditions. Padding does not collapse in the same way.

## 7. Padding

**Padding** is the space between an element's content and its border.

```
.box {
    padding-top: 10px;
    padding-right: 20px;
    padding-bottom: 10px;
    padding-left: 20px;
}
```

Shorthand:

```
.box {
    padding: 10px 20px;
}
```

This sets 10px padding at the top and bottom and 20px at the left and right.

### Margin vs Padding

|Feature|Margin|Padding|
|---|---|---|
|Position|Outside the border|Inside the border|
|Main purpose|Space between elements|Space around content|
|Background|Does not paint the element's background|Background extends through the padding area|
|Negative values|Allowed|Not allowed|
|`auto` value|Can be used for centering|Not a valid padding value|

### CSS box model

The box model consists of:

1. Content
    
2. Padding
    
3. Border
    
4. Margin
    

```
+--------------------------------+
|             Margin             |
|  +--------------------------+  |
|  |          Border          |  |
|  |  +--------------------+  |  |
|  |  |      Padding       |  |  |
|  |  |  +--------------+  |  |  |
|  |  |  |   Content    |  |  |  |
|  |  |  +--------------+  |  |  |
|  |  +--------------------+  |  |
|  +--------------------------+  |
+--------------------------------+
```

### Worked example

```
.box {
    width: 200px;
    padding: 10px;
    border: 5px solid black;
    margin: 20px;
}
```

With the default `box-sizing: content-box`:

- Content width = 200px
    
- Left and right padding = 20px total
    
- Left and right borders = 10px total
    
- Total border-box width = 200 + 20 + 10 = **230px**
    
- Adding left and right margins gives 230 + 40 = **270px** of occupied horizontal space in a simple layout.
    

**Exam trap:** Under `content-box`, the specified `width` normally excludes padding and borders.

## 8. Borders

A border surrounds an element's padding and content.

### Basic border properties

```
.box {
    border-width: 2px;
    border-style: solid;
    border-color: blue;
}
```

Shorthand:

```
.box {
    border: 2px solid blue;
}
```

The shorthand combines border width, style, and color.

### Common border styles

|Value|Appearance|
|---|---|
|`solid`|Continuous line|
|`dashed`|Dashed line|
|`dotted`|Dotted line|
|`double`|Double line|
|`none`|No border|
|`hidden`|Hidden border, particularly relevant to table border conflict rules|
|`groove`|Three-dimensional groove effect|
|`ridge`|Three-dimensional ridge effect|
|`inset`|Inset effect|
|`outset`|Outset effect|

### Border radius

The `border-radius` property rounds corners.

```
.card {
    border: 1px solid gray;
    border-radius: 10px;
}
```

A square element can appear circular when its width and height are equal and it has:

```
border-radius: 50%;
```

## 9. Box-sizing

```
* {
    box-sizing: border-box;
}
```

Two important values:

- `**content-box**` **(default):** Specified width applies to the content only.
    
- `**border-box**`**:** Specified width includes content, padding, and border.
    

For an element with `width: 200px`, 10px padding on each side, and a 5px border on each side:

|Box sizing|Total border-box width|
|---|---|
|`content-box`|230px|
|`border-box`|200px|

**Remember:** Margin is outside the border and is not included in the `border-box` width.

## 10. Complete CSS Example

This example combines selectors, colors, fonts, margins, padding, borders, and border radius.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS Example</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f1f5f9;
        }

        h1 {
            color: #1d4ed8;
            text-align: center;
        }

        .card {
            background-color: white;
            width: 300px;
            margin: 30px auto;
            padding: 20px;
            border: 1px solid #cbd5e1;
            border-radius: 10px;
        }

        .highlight {
            color: #0f766e;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="card">
        <h1>Learn CSS</h1>
        <p class="highlight">CSS styles web pages.</p>
        <p>Practise selectors and properties.</p>
    </div>
</body>
</html>
```

## 11. CSS Specificity and the Cascade

When multiple CSS rules apply to the same element, the browser considers importance, origin, cascade layers, selector specificity, and source order.

For basic exam questions, remember:

- An ID selector normally has higher specificity than a class selector.
    
- A class selector normally has higher specificity than an element selector.
    
- If competing declarations have the same importance and specificity, the later declaration generally wins.
    
- Inline styles generally override ordinary stylesheet declarations for the same property, but `!important` and the cascade can affect the result.
    

Example:

```
p {
    color: blue;
}

.note {
    color: green;
}

#intro {
    color: red;
}
```

For an element matching all three selectors, `#intro` normally wins for `color` because the ID selector has higher specificity than the class and element selectors.

### Basic specificity order

From lower to higher specificity in these common cases:

1. Element selector: `p`
    
2. Class selector: `.note`
    
3. ID selector: `#intro`
    

**Exam caution:** This is a simplified comparison. Specificity is determined by the selectors involved, and `!important`, cascade layers, and other cascade rules can affect the final result.

## 12. Quick Revision Sheet

|Topic|Remember|
|---|---|
|CSS full form|Cascading Style Sheets|
|CSS syntax|`selector { property: value; }`|
|ID selector|`#id`|
|Class selector|`.class`|
|Element selector|`p`, `h1`, etc.|
|Universal selector|`*`|
|External CSS|`<link rel="stylesheet" href="style.css">`|
|Margin|Outside the border|
|Padding|Between content and border|
|Border shorthand|Width, style, color|
|Four-value spacing order|Top, right, bottom, left|
|`content-box`|Width excludes padding and border|
|`border-box`|Width includes padding and border|
|Pseudo-class|`:hover`|
|Pseudo-element|`::before`|
|Horizontal centering|Often `margin: 0 auto` with a suitable block width|

## 13. Important MCQ Traps

1. Which selector selects an element by ID? `**#id**`
    
2. Which selector selects elements by class? `**.class**`
    
3. Which selector selects all elements? `*****`
    
4. Which selector selects direct children? `**>**`
    
5. Which selector selects descendants at any depth? **A space, as in** `**div p**`
    
6. Which property controls text color? `**color**`
    
7. Which property controls background color? `**background-color**`
    
8. What is the default value of `box-sizing`? `**content-box**`
    
9. Which CSS property rounds corners? `**border-radius**`
    
10. Which spacing is outside the border? **Margin**
    
11. Which spacing is between content and border? **Padding**
    
12. What is the four-value margin order? **Top, Right, Bottom, Left**
    
13. Which unit is relative to the root font size? `**rem**`
    
14. Which pseudo-class applies when a pointer hovers over a link? `**:hover**`
    
15. Which generally has higher specificity: `#intro` or `.note`? `**#intro**`