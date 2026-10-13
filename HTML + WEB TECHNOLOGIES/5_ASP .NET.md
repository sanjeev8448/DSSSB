
## 1. Basic ASP Concepts

**ASP stands for Active Server Pages.**

Classic ASP is Microsoft's server-side web technology for generating dynamic web pages.

The server executes the ASP code and sends the resulting output, usually HTML, to the browser.

### How ASP works

1. **Client / Browser:** Requests an ASP page.
    
2. **Web Server:** Executes the server-side ASP code.
    
3. **Generated HTML:** The server sends the response to the browser.
    

### Example of Classic ASP

A Classic ASP file usually has the `.asp` extension.

```
<%
Response.Write "Hello World"
%>
```

- `<%` begins a server-side script block.
    
- `%>` ends the script block.
    
- `Response.Write` writes output into the HTTP response.
    

The browser receives the generated output, not the server-side script itself.

### Important ASP objects

|Object|Purpose|
|---|---|
|`Request`|Retrieves information sent by the client|
|`Response`|Sends output or responses to the client|
|`Server`|Provides server-related methods and utilities|
|`Session`|Stores information associated with a user's session|
|`Application`|Stores information shared across the application|

**Exam trap:** Classic ASP and ASP.NET are different technologies. Do not confuse Classic ASP's built-in objects with the ASP.NET application lifecycle.

## 2. ASP.NET

ASP.NET is Microsoft's web application framework for building dynamic websites, web applications, and web services. It supports server-side development using languages such as C# and VB.NET.

Traditional ASP.NET includes technologies such as Web Forms and ASP.NET MVC. Modern ASP.NET Core is a cross-platform successor with a different application architecture.

### Example of C# syntax

```
using System;

public class Example
{
    public static void Main()
    {
        string message = "Hello from ASP.NET concepts";
        Console.WriteLine(message);
    }
}
```

This example illustrates C# syntax; it is not a complete ASP.NET web page.

A traditional ASP.NET Web Forms page may combine an `.aspx` file with a C# code-behind file. ASP.NET Core commonly uses `.cshtml` Razor files, controllers, or other application components.

### Classic ASP vs ASP.NET

|Feature|Classic ASP|ASP.NET|
|---|---|---|
|Full form|Active Server Pages|ASP.NET is the successor web framework; it is not a separate acronym expansion|
|Common file extension|`.asp`|`.aspx` for Web Forms; other extensions are used by other technologies|
|Typical languages|VBScript, JScript|C#, VB.NET in traditional ASP.NET|
|Technology|Classic server-side scripting|Managed web application framework|
|Execution|Server executes scripts|Server executes application code|
|Common context|Legacy dynamic websites|Traditional and modern web applications|

**Exam point:** Classic ASP commonly uses VBScript, while traditional ASP.NET commonly uses C# or VB.NET.

## 3. Data Types

A data type defines the kind of value a variable can store and the operations that can be performed on it.

Because the syllabus mentions both ASP and ASP.NET, remember that Classic ASP with VBScript and ASP.NET with C# have different data type systems.

### A. Common C# data types in ASP.NET

|Data type|Example|Meaning|
|---|---|---|
|`int`|`int age = 25;`|Integer|
|`long`|`long count = 100000L;`|Large integer|
|`float`|`float price = 12.5f;`|Single-precision floating-point|
|`double`|`double pi = 3.14159;`|Double-precision floating-point|
|`decimal`|`decimal amount = 99.50m;`|Decimal arithmetic, useful for monetary values|
|`char`|`char grade = 'A';`|Single UTF-16 code unit|
|`string`|`string name = "Rahul";`|Text|
|`bool`|`bool isActive = true;`|Boolean value: `true` or `false`|

Example:

```
int age = 25;
string name = "Rahul";
bool isStudent = true;
double percentage = 87.2;
```

### B. Classic ASP with VBScript

VBScript is dynamically typed. Variables do not require declarations of C#-style types. Values are handled through the `Variant` type, which can represent different kinds of values.

```
<%
Dim age, name, percentage

age = 25
name = "Rahul"
percentage = 87.2

Response.Write name
%>
```

Here, `Dim` declares the variables, but it does not specify a C#-style data type.

**Exam trap:** Do not assume that Classic ASP uses C# declarations such as `int age = 25;`.

## 4. Variables

A variable is a named storage location used to hold a value that can change during program execution.

### A. Variables in C#

```
int age = 25;
age = 26;
```

The value of `age` changes from 25 to 26.

C# is statically typed. A variable declared as `int` cannot ordinarily be assigned a string value.

```
int age = "twenty"; // Compilation error
```

### B. Variables in Classic ASP / VBScript

```
<%
Dim name
name = "Rahul"

name = "Amit"
Response.Write name
%>
```

Output:

```
Amit
```

The output is `Amit` because the variable was reassigned.

### Scope of variables

Scope describes where a variable can be accessed.

In C#:

- **Local variable:** Declared inside a method or block.
    
- **Instance field:** Belongs to an object instance.
    
- **Static field:** Belongs to a type rather than a particular instance.
    
- **Parameter:** Receives a value passed to a method.
    

In Classic ASP, `Dim` variables can have procedure-level or script-level scope depending on where they are declared.

**Exam point:** A variable's scope and lifetime are related concepts, but they are not the same.

## 5. Constants

A constant represents a value that cannot be changed after it has been defined according to the language's constant rules.

### A. Constants in C#

Use `const` for compile-time constants.

```
const double PI = 3.14159;
const int MAX_MARKS = 100;
```

Attempting to assign a new value to a `const` variable causes a compilation error.

```
const int MAX_MARKS = 100;
// MAX_MARKS = 90; // Compilation error
```

C# also provides `readonly` fields. Unlike `const`, a `readonly` field can be assigned at declaration or in an appropriate constructor, and its value is not restricted to a compile-time constant in the same way.

### B. Constants in Classic ASP / VBScript

VBScript supports constants declared using `Const`.

```
<%
Const PI = 3.14159
Const MAX_MARKS = 100

Response.Write MAX_MARKS
%>
```

### Variables vs Constants

|Feature|Variable|Constant|
|---|---|---|
|Value|Can be reassigned, subject to language rules|Cannot be reassigned after declaration|
|C# declaration|`int age = 25;`|`const int MAX = 100;`|
|VBScript declaration|`Dim age`|`Const MAX = 100`|
|Typical use|User input, counters, changing state|Fixed limits, mathematical values|

**Exam trap:** In C#, `const` values must be available at compile time. `readonly` is not interchangeable with `const`.

## 6. `Global.asax`

`Global.asax` is an optional application-level file used in traditional ASP.NET applications, particularly Web Forms and MVC applications hosted on ASP.NET's classic application pipeline.

It can handle application-wide and session-related lifecycle events. Common uses include application initialization, session start/end handling, and certain application-level error events.

### Important events

|Event|Purpose|
|---|---|
|`Application_Start`|Runs when the application starts|
|`Application_End`|Runs when the application ends|
|`Session_Start`|Runs when a new user session starts|
|`Session_End`|Runs when a session ends, subject to hosting and session-mode limitations|
|`Application_Error`|Handles an unhandled application error|
|`Application_BeginRequest`|Runs at the beginning of an HTTP request|

### Example of `Global.asax`

```
<%@ Application Language="C#" %>

<script runat="server">

    void Application_Start(object sender, EventArgs e)
    {
        // Application initialization
    }

    void Session_Start(object sender, EventArgs e)
    {
        // New session begins
    }

    void Application_Error(object sender, EventArgs e)
    {
        // Handle an unhandled application error
    }

</script>
```

This is an example of a traditional ASP.NET application file, not a Classic ASP `.asp` script.

### Application vs Session

- **Application state:** Shared data for the application across users, subject to the application's process and hosting lifecycle.
    
- **Session state:** Data associated with a particular user session.
    

|Feature|Application|Session|
|---|---|---|
|Scope|Application-wide|Individual session|
|Shared between users|Generally yes|Generally no|
|Lifecycle event|`Application_Start`|`Session_Start`|
|Example use|Shared application configuration|User-specific temporary state|

### Important modern distinction

`Global.asax` belongs to the traditional ASP.NET application model. ASP.NET Core generally uses `Program.cs` and middleware for application startup, request processing, and error handling rather than `Global.asax`.

**Exam trap:** `Application_Start` is application-level; `Session_Start` is session-level. Do not confuse `Global.asax` with the `web.config` configuration file.

## 7. Last-Minute Revision Sheet

|Topic|Key fact|
|---|---|
|Classic ASP|Server-side scripting technology|
|ASP.NET|Microsoft's web application framework|
|Classic ASP extension|`.asp`|
|Web Forms extension|`.aspx`|
|C# integer type|`int`|
|C# text type|`string`|
|C# Boolean type|`bool`|
|C# constant|`const`|
|VBScript variable declaration|`Dim`|
|VBScript constant declaration|`Const`|
|`Request`|Receives client request information|
|`Response.Write`|Writes output in Classic ASP|
|`Global.asax`|Application-level lifecycle events in traditional ASP.NET|
|`Application_Start`|Application starts|
|`Session_Start`|New session starts|
|`Application_Error`|Handles an unhandled application error|
|ASP.NET Core startup|Commonly configured through `Program.cs`|

## 8. Important MCQ Traps

1. What is the full form of ASP? **Active Server Pages.**
    
2. Which file extension is commonly used by Classic ASP? `**.asp**`
    
3. Which file extension is used by ASP.NET Web Forms? `**.aspx**`
    
4. Which language is commonly used by Classic ASP? **VBScript.**
    
5. Which languages are commonly used in traditional ASP.NET? **C# and VB.NET.**
    
6. Which object retrieves client request information in Classic ASP? `**Request**`
    
7. Which statement writes output in Classic ASP? `**Response.Write**`
    
8. Which C# type stores Boolean values? `**bool**`
    
9. Which C# keyword declares a compile-time constant? `**const**`
    
10. Which VBScript keyword declares variables? `**Dim**`
    
11. Which VBScript keyword declares constants? `**Const**`
    
12. What does `Global.asax` handle in traditional ASP.NET? **Application-level lifecycle events.**
    
13. Which event occurs when a new session starts? `**Session_Start**`
    
14. Which event occurs when the application starts? `**Application_Start**`
    
15. What is commonly used for startup configuration in ASP.NET Core? `**Program.cs**`