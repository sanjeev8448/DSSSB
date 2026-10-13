## 1. Introduction to XML

XML stands for eXtensible Markup Language. It is a markup language designed to store, describe, and transport structured data.

Unlike HTML, which uses predefined tags for displaying and structuring web content, XML allows users to define their own element names.

Example:

```
<?xml version="1.0" encoding="UTF-8"?>
<student>
    <name>Rahul</name>
    <rollno>101</rollno>
    <course>CSE</course>
</student>
```

Here, `student`, `name`, `rollno`, and `course` are user-defined element names.

### XML vs HTML

|Feature|XML|HTML|
|---|---|---|
|Main purpose|Store and transport structured data|Structure web content|
|Tags|User-defined|Standard predefined tags|
|Case sensitivity|Case-sensitive|HTML tag names are generally case-insensitive|
|Closing tags|Required for non-empty elements|Some HTML elements are void|
|Error handling|Requires well-formed syntax|Browsers often recover from markup errors|
|Data meaning|Element names can describe data|Tags describe document structure and semantics|
|Display|Does not inherently define visual styling|Browsers provide default rendering for HTML|

Exam trap: XML is case-sensitive. `<Name>` and `<name>` are different elements.

## 2. XML structure

A basic XML document may contain an XML declaration, a root element, child elements, attributes, and text content.

```
<?xml version="1.0" encoding="UTF-8"?>
<library>
    <book id="B101">
        <title>Computer Networks</title>
        <author>Andrew</author>
        <price>450</price>
    </book>
</library>
```

### Explanation

|Component|Example|Purpose|
|---|---|---|
|XML declaration|`<?xml version="1.0"?>`|Declares XML version and optional encoding|
|Root element|`<library>`|Contains the document's other elements|
|Child element|`<book>`|Nested within the root|
|Attribute|`id="B101"`|Supplies information about an element|
|Text content|`Computer Networks`|Data stored inside an element|
|Closing tag|`</book>`|Ends the element|

### Important structural rules

- An XML document must have exactly one document element (root element).
    
- Every non-empty element must have a matching closing tag.
    
- Elements must be properly nested.
    
- Attribute values must be enclosed in quotes.
    
- Element names are case-sensitive.
    

Correct nesting:

```
<student>
    <name>Rahul</name>
</student>
```

Incorrect nesting:

```
<student>
    <name>Rahul</student>
</name>
```

The second example is not well-formed XML because the tags overlap incorrectly.

## 3. XML elements

An XML element consists of a start tag, its content, and an end tag, or it can be an empty element.

### A. Element with text content

```
<name>Rahul</name>
```

### B. Nested elements

```
<student>
    <name>Rahul</name>
    <course>CSE</course>
</student>
```

Here, `name` and `course` are child elements of `student`.

### C. Empty element

```
<photo/>
```

This is equivalent to:

```
<photo></photo>
```

### D. Mixed content

An element may contain both text and child elements.

```
<message>Hello <bold>Rahul</bold>, welcome!</message>
```

This is an example of mixed content.

Exam point: XML allows nested elements and user-defined tags. A single document element is required, but that root can contain many child elements.

## 4. XML attributes

An attribute provides additional information about an element. It appears in the start tag as a name-value pair.

```
<student id="101" course="CSE">
    <name>Rahul</name>
</student>
```

Here, `id` and `course` are attributes of `student`.

### Attributes vs elements

|Attribute|Element|
|---|---|
|Appears inside a start tag|Uses tags|
|Example: `id="101"`|Example: `<id>101</id>`|
|Value must be quoted|Text content is placed between tags|
|Suitable for metadata or properties|Often suitable for structured data|

Both are valid ways to represent information, depending on the design.

### Important attribute rules

- Attribute values must be enclosed in single or double quotes.
    
- An element cannot have two attributes with the same name.
    
- Attribute names are case-sensitive in XML.
    
- Attribute order does not change the meaning of the element.
    

Valid:

```
<student id="101" course="CSE"/>
```

Invalid:

```
<student id=101/>
```

The attribute value is not quoted in the invalid example.

Exam trap: XML does not require every piece of data to be an attribute. Repeated, hierarchical, or complex information is often better represented using elements.

## 5. XML naming rules

XML names must follow specific naming rules.

|Rule|Example|
|---|---|
|A name may begin with a letter or underscore|`<student>` or `<_student>`|
|Names may contain letters and digits after the first character|`<student1>`|
|Hyphens and periods can appear in names|`<first-name>` and `<section.one>`|
|Names cannot begin with a digit|`<1student>` is invalid|
|Names cannot contain spaces|`<student name>` is invalid|
|Names cannot begin with `xml` in any capitalization|Avoid names such as `<xmlData>`|
|Names are case-sensitive|`<Name>` differs from `<name>`|

The colon is permitted in XML names, commonly for namespace-qualified names, but namespace use has additional rules.

### XML reserved characters

Some characters need special treatment when used as text.

|Character|XML entity|
|---|---|
|`&`|`&amp;`|
|`<`|`&lt;`|
|`>`|`&gt;`|
|`"`|`&quot;`|
|`'`|`&apos;`|

Example:

```
<message>Tom &amp; Jerry</message>
```

This represents the text `Tom & Jerry`.

Exam trap: The `<` character cannot normally appear literally in ordinary XML character data because it begins markup. Use `&lt;` instead.

## 6. DTD — Document Type Definition

A DTD defines the permitted structure of an XML document. It can specify which elements and attributes are allowed and how elements may be arranged.

DTD declarations can be written internally inside an XML document or referenced externally.

### A. Internal DTD

```
<?xml version="1.0"?>
<!DOCTYPE student [
    <!ELEMENT student (name, course)>
    <!ELEMENT name (#PCDATA)>
    <!ELEMENT course (#PCDATA)>
]>
<student>
    <name>Rahul</name>
    <course>CSE</course>
</student>
```

Explanation:

- `<!DOCTYPE student [...]>` declares the document type.
    
- `<!ELEMENT student (name, course)>` requires `name` followed by `course`.
    
- `<!ELEMENT name (#PCDATA)>` allows parsed character data inside `name`.
    
- `#PCDATA` means parsed character data.
    

### B. External DTD

XML document:

```
<?xml version="1.0"?>
<!DOCTYPE student SYSTEM "student.dtd">
<student>
    <name>Rahul</name>
    <course>CSE</course>
</student>
```

External file `student.dtd`:

```
<!ELEMENT student (name, course)>
<!ELEMENT name (#PCDATA)>
<!ELEMENT course (#PCDATA)>
```

The `SYSTEM` identifier references an external DTD file. A DTD can also be referenced using a `PUBLIC` identifier.

### Important DTD declarations

|Declaration|Purpose|
|---|---|
|`<!DOCTYPE ...>`|Declares the document type|
|`<!ELEMENT ...>`|Defines an element and its content model|
|`<!ATTLIST ...>`|Defines permitted attributes|
|`<!ENTITY ...>`|Defines an entity|
|`#PCDATA`|Parsed character data|

### Defining attributes using `ATTLIST`

```
<!ATTLIST student id CDATA #REQUIRED>
```

This declaration says that `student` has an attribute named `id`, of type `CDATA`, and that it is required.

Common attribute defaults:

- `#REQUIRED` — the attribute must be provided.
    
- `#IMPLIED` — the attribute is optional.
    
- `#FIXED "value"` — the attribute has a fixed declared value.
    
- A quoted default value — used when the attribute is omitted.
    

### DTD vs XML Schema (XSD)

|Feature|DTD|XML Schema (XSD)|
|---|---|---|
|Main purpose|Define XML structure|Define structure and data constraints|
|Syntax|DTD-specific syntax|XML syntax|
|Data types|Limited|Rich built-in and user-defined types|
|Namespaces|Limited namespace support|Designed to support XML namespaces|
|Numeric constraints|Limited|Supports more detailed constraints|

Exam point: DTD validates document structure but has much more limited data typing than XSD.

## 7. XML content models

A content model specifies what content an XML element is allowed to contain. In DTD, an element declaration defines its permitted content.

### A. Element-only content

```
<!ELEMENT student (name, course)>
```

The `student` element must contain `name` followed by `course`.

Valid:

```
<student>
    <name>Rahul</name>
    <course>CSE</course>
</student>
```

The order matters. Reversing the two children would violate this content model.

### B. Character data content

```
<!ELEMENT name (#PCDATA)>
```

The `name` element contains parsed character data.

```
<name>Rahul</name>
```

### C. Empty content

```
<!ELEMENT photo EMPTY>
```

The element must be empty:

```
<photo/>
```

### D. Any content

```
<!ELEMENT item ANY>
```

`ANY` permits any declared element content and character data according to DTD rules. It does not mean arbitrary malformed XML is permitted.

### E. Mixed content

```
<!ELEMENT message (#PCDATA | bold | italic)*>
```

The element may contain text and the declared `bold` and `italic` child elements in a mixture and in varying order.

Example:

```
<message>Hello <bold>Rahul</bold>!</message>
```

### Content model revision

|Model|Meaning|
|---|---|
|`(name, course)`|Both children, in the specified order|
|`(name \\| course)`|Either `name` or `course`|
|`(#PCDATA)`|Parsed character data|
|`EMPTY`|No content|
|`ANY`|Broadly permits declared element content and text|
|`(#PCDATA \\| bold)*`|Text and `bold` elements in mixed content|

Exam trap: A comma means sequence, while `|` means choice in DTD content models.

## 8. Occurrence indicators in DTD

Occurrence indicators specify how many times an element or group can occur.

There are three major symbols:

|Symbol|Meaning|Example|
|---|---|---|
|`?`|Zero or one occurrence|`(middle?)`|
|`*`|Zero or more occurrences|`(phone*)`|
|`+`|One or more occurrences|`(subject+)`|

### A. Question mark `?`

```
<!ELEMENT student (name, middle?, surname)>
```

The `middle` element is optional and can appear at most once.

Valid:

```
<student>
    <name>Rahul</name>
    <surname>Kumar</surname>
</student>
```

Also valid:

```
<student>
    <name>Rahul</name>
    <middle>Raj</middle>
    <surname>Kumar</surname>
</student>
```

### B. Asterisk `*`

```
<!ELEMENT student (name, phone*)>
```

The student must have a `name` and may have zero, one, or many `phone` elements.

### C. Plus sign `+`

```
<!ELEMENT course (subject+)>
```

The course must contain at least one `subject` element.

### Worked MCQ example

Given:

```
<!ELEMENT student (name, phone+, email?)>
```

The correct interpretation is:

- Exactly one `name` element, in that position.
    
- One or more `phone` elements.
    
- Zero or one `email` element, after the phone elements.
    

Memory trick:

- `?` = optional
    
- `*` = optional and repeatable
    
- `+` = required and repeatable
    

## 9. XML parser

An XML parser is software that reads XML documents and processes their structure and content. Depending on the parser and its configuration, it may also validate the document against a DTD or schema.

### Types of XML parsers

1. DOM parser

- Loads the XML document into a tree-like object structure.
    
- Allows access to different parts of the document.
    
- Convenient when the application needs to navigate or modify the document.
    
- Can consume substantial memory for large documents.
    

2. SAX parser

- Uses event-driven, sequential processing.
    
- Reports events such as the beginning of an element, character data, and the end of an element.
    
- Typically does not require loading the entire document tree into memory.
    
- Is useful for processing large documents sequentially.
    

3. Pull parser

- The application requests the next parsing event when needed.
    
- Provides more control over the parsing process than a push-based event interface.
    

### DOM vs SAX

|Feature|DOM parser|SAX parser|
|---|---|---|
|Processing|Builds a document tree|Processes sequentially through events|
|Access|Can navigate the tree|Normally forward-only|
|Memory|Often higher|Often lower|
|Modification|Convenient for tree manipulation|No full document tree by default|
|Suitable for|Documents requiring repeated navigation|Large documents processed sequentially|

### Well-formed vs valid XML

This is an important exam distinction.

- Well-formed XML: Follows XML syntax rules, including correct nesting, quoted attribute values, and a single root element.
    
- Valid XML: Is well-formed and also conforms to its associated DTD or schema.
    

A document can be well-formed but invalid if its structure violates the DTD.

For example, if a DTD requires:

```
<!ELEMENT student (name, course)>
```

this XML is well-formed but invalid against that declaration:

```
<student>
    <course>CSE</course>
    <name>Rahul</name>
</student>
```

The child elements are in the wrong order.

Exam trap: Not every XML parser performs validation. A non-validating parser can check basic well-formedness without checking conformance to a DTD.

## 10. XML final revision sheet

| Topic            | Key fact                                    |        |
| ---------------- | ------------------------------------------- | ------ |
| XML              | Extensible Markup Language                  |        |
| Root element     | Exactly one document element                |        |
| Case sensitivity | XML names are case-sensitive                |        |
| Empty element    | `<item/>`                                   |        |
| Attribute value  | Must be quoted                              |        |
| Naming rule      | A name cannot start with a digit            |        |
| `#PCDATA`        | Parsed character data                       |        |
| DTD              | Defines allowed document structure          |        |
| `<!ELEMENT>`     | Declares an element                         |        |
| `<!ATTLIST>`     | Declares attributes                         |        |
| `<!ENTITY>`      | Declares entities                           |        |
| `,` in DTD       | Sequence                                    |        |
| `\\              | ` in DTD                                    | Choice |
| `?`              | Zero or one                                 |        |
| `*`              | Zero or more                                |        |
| `+`              | One or more                                 |        |
| DOM parser       | Builds a document tree                      |        |
| SAX parser       | Event-driven sequential processing          |        |
| Well-formed XML  | Follows XML syntax rules                    |        |
| Valid XML        | Well-formed and conforms to a DTD or schema |        |