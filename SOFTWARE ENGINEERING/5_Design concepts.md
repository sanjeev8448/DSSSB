# COHESION AND COUPLING — SOFTWARE ENGINEERING

The golden rule of good software design is:

[  
High Cohesion + Low Coupling
]

- **High cohesion:** Each module has a focused responsibility.
    
- **Low coupling:** Modules have minimal dependence on one another.
    

## 1. Cohesion

**Definition:** Cohesion is the degree to which the elements within a single module are related to one another and work together to achieve a common purpose.

In simple words, cohesion measures how focused a module is on one responsibility.

### Example

Consider two modules in a college management system.

- **Module A — Student Records:** Adds student details, updates student details, and retrieves student records.
    
- **Module B — Mixed Utilities:** Calculates student marks, sends emails, prints reports, and manages unrelated database backups.
    

Module A has higher cohesion because its operations are closely related. Module B has lower cohesion because it combines unrelated responsibilities.

### Types of Cohesion

The following is the traditional classification, arranged from **weakest to strongest**.

**1. Coincidental cohesion — Lowest**

Unrelated tasks are grouped in the same module.

Example: A single module calculates tax, prints a report, and plays an audio file.

**2. Logical cohesion**

Tasks of the same general category are grouped together, and a control flag or selection determines which task runs.

Example: A single input module handles keyboard, mouse, and file input based on a selected option.

**3. Temporal cohesion**

Tasks are grouped because they occur at the same time.

Example: A startup module initializes configuration, opens a log, and initializes a cache.

**4. Procedural cohesion**

Elements are grouped because they must follow a particular sequence of execution, even if they operate on different data.

Example: A module validates a session and then displays a standard navigation menu.

**5. Communicational cohesion**

Operations are grouped because they use or operate on the same data.

Example: A module retrieves a student record and displays or updates that record.

**6. Sequential cohesion**

The output of one operation becomes the input of the next operation.

Example: Read marks → calculate total → calculate percentage.

**7. Functional cohesion — Highest**

Every element contributes to one clearly defined function.

Example: A module whose sole responsibility is calculating the factorial of a number.

### Cohesion Memory Trick

Coincidental → Logical → Temporal → Procedural → Communicational → Sequential → Functional

Remember: **Cohesion increases as you move toward functional cohesion.**

Some textbooks also include informational cohesion, particularly in object-oriented or abstract-data-type discussions. Follow the classification used in your study material if it differs.

## 2. Coupling

**Definition:** Coupling is the degree of interdependence between different software modules.

In simple words, coupling measures how strongly one module depends on another.

### Example

Imagine an online shopping application with three modules:

- Order module
    
- Payment module
    
- Notification module
    

If the order module depends on many internal details of the payment module, changing payment logic may require changes in the order module. This represents stronger coupling.

If the order module interacts with the payment module through a small, clearly defined interface, the modules can change more independently. This represents lower coupling.

### Types of Coupling

The following is a traditional classification arranged from **strongest to weakest**.

**1. Content coupling — Highest**

One module directly accesses or modifies another module's internal data or code.

Example: Module A directly changes an internal variable or logic belonging to Module B.

**2. Common coupling**

Multiple modules access the same shared global data.

Example: Several modules read and modify the same global variable.

**3. External coupling**

Modules depend on an externally imposed format, protocol, device interface, or communication standard.

Example: Two modules depend on the same fixed file format or external communication protocol.

**4. Control coupling**

One module passes a control flag that determines the internal behavior of another module.

Example: `generate_report(true)` selects a detailed report, while `generate_report(false)` selects a summary.

**5. Stamp coupling**

A module passes a composite data structure, such as a complete record, even though the receiving module uses only part of it.

Example: Passing an entire student object to a function that needs only the student's ID.

**6. Data coupling — Lowest in this classification**

Modules communicate by passing only the necessary data items.

Example:

```
def calculate_total(price, quantity):
    return price * quantity
```

The function receives only the price and quantity it needs.

### Coupling Memory Trick

Content → Common → External → Control → Stamp → Data

Remember: **Coupling decreases as you move toward data coupling.**

Some textbooks include message coupling as a particularly loose form of coupling, especially in object-oriented systems. It involves communication through messages or public interfaces without sharing internal implementation details.

## 3. Cohesion vs. Coupling

|Basis|Cohesion|Coupling|
|---|---|---|
|Measures|Relationship within a module|Dependency between modules|
|Scope|Internal to one module|Between modules|
|Desired level|High|Low|
|Good design example|One module focuses on payment processing|Payment and order modules interact through a clear interface|
|Benefit|Improves clarity and maintainability|Reduces the impact of changes across modules|
|Poor design|One module performs unrelated tasks|Modules rely heavily on each other's internals|

### Visual Memory Aid

**High cohesion — good**

Each module has a focused responsibility.

- Student Records
    
- Payments
    
- Notifications
    

**Low coupling — good**

Modules exchange only the information required through a defined interface.

- Order
    
- Payment
    

### Why Are High Cohesion and Low Coupling Preferred?

- Modules become easier to understand and test.
    
- Changes are less likely to affect unrelated components.
    
- Code reuse becomes easier.
    
- Maintenance and debugging become simpler.
    
- Development teams can work on separate modules more independently.
    

These are design goals, not absolute rules. A practical design must also meet performance, security, and other requirements.

## 4. Last-Minute Revision

- **Cohesion:** Relationship within a module — aim for high cohesion.
    
- **Coupling:** Dependency between modules — aim for low coupling.
    
- **Highest traditional cohesion:** Functional.
    
- **Lowest traditional cohesion:** Coincidental.
    
- **Highest traditional coupling:** Content.
    
- **Lowest coupling in the six-type classification:** Data.
    

### Quick Exam Recall

| Question                                                         | Answer                         |
| ---------------------------------------------------------------- | ------------------------------ |
| What is the golden rule of software design?                      | High cohesion and low coupling |
| Which cohesion groups unrelated tasks?                           | Coincidental                   |
| Which cohesion has a single, well-defined purpose?               | Functional                     |
| Which coupling accesses another module's internals?              | Content                        |
| Which coupling uses shared global data?                          | Common                         |
| Which coupling passes a control flag?                            | Control                        |
| Which coupling passes an entire record when only part is needed? | Stamp                          |
| Which coupling passes only required data?                        | Data                           |