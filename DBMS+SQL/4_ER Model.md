## 1. Understand the ER model with an example

Imagine you are designing a college database. You need to store information about students, courses, and which students enrol in which courses.

### STUDENT

StudentID, Name

ENROLLS

Many-to-many (M:N)

### COURSE

CourseID, Title

A student can enrol in multiple courses, and a course can have multiple students. `STUDENT` and `COURSE` are entity sets; `ENROLLS` is the relationship between them.

## 2. Entity

An entity is a distinguishable real-world object, person, place, or thing about which data is stored.

Examples:

- A particular student, such as student ID 101.
    
- A particular employee.
    
- A specific book in a library.
    
- A particular department.
    

Remember: An entity is one individual object.

### ER diagram notation

An entity is generally represented by a rectangle.

STUDENT

Rectangle = Entity type in a conventional ER diagram

## 3. Entity set

An entity set is a collection of entities of the same type that share the same attributes.

For example, a college might have these student entities:

|StudentID|Name|
|---|---|
|101|Amit|
|102|Neha|
|103|Ravi|

Each student record represents an individual entity; the collection of those students is the `STUDENT` entity set.

Entity vs entity set

|Entity|Entity set|
|---|---|
|One individual object|Collection of similar entities|
|Example: student 101|Example: all students|
|Represents one instance|Represents the group/type of instances|

Exam trap: An entity is not the same as an entity set. Individual student vs collection of students.

## 4. Attributes

An attribute is a property or characteristic of an entity.

For the `STUDENT` entity, attributes can include:

`StudentID`, `Name`, `DateOfBirth`, `PhoneNumber`.

Common attribute types are important for MCQs.

### A. Simple attribute

Cannot be meaningfully divided into smaller attributes for the database's intended use.

Example: `Salary`, `Gender` (if modelled as a single field).

### B. Composite attribute

Can be divided into smaller meaningful attributes.

Example:

`Name` → `FirstName`, `MiddleName`, `LastName`

`Address` → `Street`, `City`, `State`, `PIN`.

### C. Single-valued attribute

Has one value for each entity in the given database model.

Example: `DateOfBirth` for a student.

### D. Multivalued attribute

Can have multiple values for one entity.

Example: a student having multiple phone numbers.

In conventional ER notation, a multivalued attribute is shown using a double oval.

### E. Derived attribute

Its value can be calculated from another attribute.

Example: `Age` can be derived from `DateOfBirth` and the current date.

In conventional ER notation, a derived attribute is shown using a dashed oval.

### F. Key attribute

An attribute that uniquely identifies an entity within its entity set.

Example: `StudentID`.

In conventional ER notation, a key attribute is usually underlined.

### G. Stored attribute

An attribute whose value is stored directly rather than calculated from another attribute.

Example: `DateOfBirth`, from which age may be derived.

### Attribute notation summary

|Attribute type|Example|Conventional ER notation|
|---|---|---|
|Simple|Salary|Single oval|
|Composite|Name split into parts|Oval connected to component ovals|
|Single-valued|DateOfBirth|Single oval|
|Multivalued|PhoneNumbers|Double oval|
|Derived|Age from DateOfBirth|Dashed oval|
|Key|StudentID|Underlined name|
|Stored|DateOfBirth|Ordinary attribute oval|

## 5. Relationships

A relationship represents an association between entities.

Examples:

- Student enrols in Course.
    
- Employee works for Department.
    
- Person owns Vehicle.
    
- Teacher teaches Subject.
    

In conventional ER diagrams, a relationship is represented by a diamond.

STUDENT

ENROLLS

COURSE

Rectangles represent entity types; a diamond represents a relationship type.

### Degree of a relationship

The degree of a relationship refers to the number of entity types participating in it.

|Relationship degree|Meaning|Example|
|---|---|---|
|Unary (recursive)|One entity type participates|Employee supervises Employee|
|Binary|Two entity types participate|Student enrols in Course|
|Ternary|Three entity types participate|Supplier supplies Part to Project|

Exam trap: Relationship degree is not the same as relationship cardinality. Degree counts participating entity types; cardinality describes how many entities may be associated.

## 6. Cardinality in the ER model

In an ER model, cardinality describes the number of entities that can participate in a relationship. This differs from relational-table cardinality, which means the number of rows.

The main mapping cardinalities are:

### A. One-to-one (1:1)

One entity in A is associated with at most one entity in B, and vice versa.

Example: One person has one passport under a model where each person and each passport can be associated with only one another.

### B. One-to-many (1:N)

One entity in A can be associated with many entities in B, while each entity in B is associated with at most one entity in A.

Example: One department employs many employees, while each employee belongs to one department.

### C. Many-to-one (N:1)

Many entities in A can be associated with one entity in B.

Example: Many employees work for one department.

This is the reverse perspective of one-to-many.

### D. Many-to-many (M:N)

Many entities in A can be associated with many entities in B.

Example: Students enrol in multiple courses, and each course has multiple students.

### Comparison table

|Cardinality|Meaning|Example|
|---|---|---|
|1:1|One to one|Person ↔ Passport|
|1:N|One to many|Department → Employees|
|N:1|Many to one|Employees → Department|
|M:N|Many to many|Students ↔ Courses|

Exam tip: Cardinality constraints are often specified using maximum participation. Minimum participation is handled separately through participation constraints.

## 7. Participation constraints

Participation describes whether participation of entities in a relationship is mandatory or optional.

### A. Total participation

Every entity in the entity set must participate in at least one instance of the relationship.

Example: If every employee must belong to a department, every `EMPLOYEE` must participate in `WORKS_FOR`.

- Minimum participation: 1.
    
- Conventional ER notation: double line between the entity rectangle and relationship diamond.
    

### B. Partial participation

Some entities may exist without participating in the relationship.

Example: A department may exist even if it currently has no employees.

- Minimum participation: 0.
    
- Conventional ER notation: single line between the entity rectangle and relationship diamond.
    

### Total vs partial participation

|Feature|Total participation|Partial participation|
|---|---|---|
|Participation required?|Yes|No|
|Minimum participation|1|0|
|Diagram notation|Double line|Single line|
|Example|Every employee must belong to a department|A department may have no employees|

Important: Total participation does not mean that an entity must have many relationships. It means that every entity must participate at least once.

## 8. Weak entity

A weak entity is an entity type that cannot be uniquely identified by its own attributes alone and depends on an identifying relationship with an owner (strong entity).

Example: An employee can have multiple dependents. A dependent's name may not be unique across all employees.

Suppose:

EMPLOYEE

|EmployeeID|Name|
|---|---|
|501|Amit|
|502|Neha|

DEPENDENT

|EmployeeID|DependentName|
|---|---|
|501|Rahul|
|501|Priya|
|502|Rahul|

`DependentName` alone cannot uniquely identify all dependents. We can use the combination `(EmployeeID, DependentName)`.

Here:

- `EMPLOYEE` is the strong entity.
    
- `DEPENDENT` is the weak entity.
    
- `EmployeeID` is the owner's key.
    
- `DependentName` may act as a partial key (discriminator) within the owner's dependents.
    
- `(EmployeeID, DependentName)` identifies a dependent.
    

### Weak entity notation

EMPLOYEE

DEPENDENT

Strong entity: single rectangle. Weak entity: double rectangle.

Other common weak-entity symbols

Weak entity

Double rectangle

Identifies

Identifying relationship: double diamond

Partial key

Often shown using a dashed underline

A weak entity commonly has total participation in its identifying relationship because it cannot exist independently of the owner in the model.

Exam trap: A weak entity is not merely an entity with few attributes. Its key distinction is that it requires the owner's key, together with its partial key, for identification.

## 9. High-value revision table

|Concept|What to remember|
|---|---|
|Entity|One distinguishable real-world object|
|Entity set|Collection of entities of the same type|
|Attribute|Property of an entity|
|Composite attribute|Can be divided into meaningful components|
|Multivalued attribute|Can contain multiple values for one entity|
|Derived attribute|Calculated from other stored data|
|Relationship|Association between entities|
|Relationship degree|Number of participating entity types|
|Cardinality|Mapping constraint, such as 1:1 or M:N|
|Total participation|Every entity must participate at least once|
|Partial participation|Participation is optional for some entities|
|Weak entity|Needs an owner's key for unique identification|
|Partial key|Distinguishes weak entities belonging to the same owner|Last-minute revision: Rectangle = entity; oval = attribute; diamond = relationship; 1:1, 1:N, M:N = cardinality; double line = total participation; double rectangle = weak entity.

Last-minute revision: Rectangle = entity; oval = attribute; diamond = relationship; 1:1, 1:N, M:N = cardinality; double line = total participation; double rectangle = weak entity.