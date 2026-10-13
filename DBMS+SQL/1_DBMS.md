# 1. Database

A database is an organized collection of related data that can be stored, accessed, managed, and updated.

For example, a college database may contain information about students, courses, teachers, and examination results.

### Example: College database

Students

Student ID, name, course

Courses

Course ID, title, credits

Results

Student ID, marks, grade

Teachers

Teacher ID, name, department

These related collections together can form a college database.

### Examples of databases

|Application|Example data stored|
|---|---|
|Banking|Accounts, balances, transactions|
|Hospital|Patients, appointments, medical records|
|College|Students, courses, marks|
|E-commerce|Products, customers, orders|
|Railway reservation|Trains, passengers, seats, bookings|

### Data vs information

- Data: Raw facts, such as `85`, `S101`, or `Amit`.
    
- Information: Meaningful results derived from data, such as “Amit scored 85 marks.”
    

Exam trap: A database is a collection of data. The software that manages that data is the DBMS; they are not the same thing.

# 2. DBMS (Database Management System)

A DBMS is software that enables users and applications to define, create, store, retrieve, update, and control access to databases.

Examples include MySQL, PostgreSQL, Oracle Database, Microsoft SQL Server, and SQLite.

## 2.1 Main functions of a DBMS

|Function|Meaning|
|---|---|
|Data storage and retrieval|Stores data and retrieves requested records|
|Data manipulation|Inserts, updates, and deletes data|
|Security|Controls who can access or modify data|
|Integrity enforcement|Enforces rules that keep data valid|
|Concurrency control|Coordinates simultaneous access by multiple transactions|
|Backup and recovery|Helps restore data after failures|
|Transaction management|Helps ensure reliable transaction execution|
|Data independence|Separates some aspects of data organization from application programs|

### Example

Suppose a banking application must transfer ₹1,000 from account A to account B. A properly designed DBMS can manage the two balance changes as one transaction so that a partial transfer does not leave the database in an inconsistent state.

This is related to transaction properties, which you can study further under ACID.

## 2.2 Advantages of a DBMS

1. Reduced data redundancy: Shared data can be stored centrally rather than copied into many independent files.

2. Improved consistency: Centralized updates and integrity rules can prevent conflicting copies of the same information.

3. Security: Access privileges can restrict who reads or changes data.

4. Data sharing: Multiple authorized users and applications can access the database.

5. Backup and recovery: Recovery facilities help manage failures.

6. Data independence: Application programs can be less dependent on the exact physical storage arrangement.

## 2.3 Limitations of a DBMS

A DBMS may require licensing or infrastructure costs, additional configuration, trained administrators, and more computing resources than a simple standalone file. A DBMS can also introduce complexity that is unnecessary for very small applications.

Exam trap: A DBMS improves control over data, but it does not automatically eliminate every form of redundancy, prevent every security breach, or guarantee correct application logic.

# 3. RDBMS (Relational Database Management System)

An RDBMS is a type of DBMS that organizes data using the relational model. Data is represented primarily through relations, commonly implemented as tables with rows and columns.

Examples include MySQL, PostgreSQL, Oracle Database, Microsoft SQL Server, and SQLite.

Consider a `Student` relation:

|StudentID|Name|Course|
|---|---|---|
|101|Amit|CSE|
|102|Neha|IT|
|103|Ravi|CSE|

Here:

- The table represents a relation in the relational-model introduction.
    
- Each row represents a record, or tuple.
    
- Each column represents an attribute.
    
- `StudentID` can be designated as the primary key because it uniquely identifies each student.
    

### 3.1 Important features of an RDBMS

- Organizes related data into tables.
    
- Uses relationships between tables.
    
- Typically supports SQL for querying and manipulating data.
    
- Supports constraints such as primary keys, foreign keys, `UNIQUE`, and `NOT NULL`.
    
- Commonly supports transactions and multi-user access.
    
- Can reduce duplication through appropriate relational schema design and normalization.
    

### 3.2 Example of relationships between tables

Suppose a college maintains two tables.

Student

|StudentID (PK)|Name|
|---|---|
|101|Amit|
|102|Neha|
|103|Ravi|

Enrollment

|EnrollmentID (PK)|StudentID (FK)|Course|
|---|---|---|
|1|101|CSE|
|2|102|IT|
|3|101|DBMS|

`StudentID` is the primary key in the `Student` table and a foreign key in `Enrollment`.

The foreign key establishes a relationship between the enrollment records and the students.

This design avoids repeating the student's name in every enrollment record.

## 3.3 DBMS vs RDBMS

|Feature|DBMS|RDBMS|
|---|---|---|
|Meaning|General software for managing databases|DBMS based on the relational model|
|Data organization|Depends on the database model|Primarily relations/tables|
|Relationships|Depends on the model|Commonly represented using keys and relational operations|
|Keys and constraints|Depends on the DBMS|Supports relational integrity constraints|
|SQL|May or may not use SQL, depending on the system|Commonly uses SQL|
|Examples|Relational and non-relational database systems|MySQL, PostgreSQL, Oracle Database, SQL Server, SQLite|

Important distinction: RDBMS is a type of DBMS, not an entirely separate category of software. Some traditional textbook comparisons state that DBMS lacks relationships or keys, but those are oversimplifications of the general DBMS category.

# 4. File system vs DBMS

Before database systems were widely used, applications often stored data in separate files managed by the operating system or application code.

For example, a college might keep separate files for student details, fees, and examination marks. If each file stores the same student's name independently, updates may become inconsistent.

A DBMS offers centralized management, querying, integrity enforcement, and transaction facilities.

## 4.1 Comparison table

|Feature|Traditional file system|DBMS|
|---|---|---|
|Data organization|Separate files and application-defined formats|Managed database structures|
|Redundancy|Can be high if information is copied across files|Can be reduced through schema design|
|Consistency|Updating multiple copies can be difficult|Integrity rules and transactions can help maintain consistency|
|Data sharing|Depends heavily on the applications and file access mechanisms|Database services support controlled multi-user access|
|Security|Often implemented using file permissions and application logic|Can provide database-specific users, roles, and privileges|
|Querying|Often requires custom code or external tools|Supports database query facilities|
|Integrity constraints|Commonly implemented by application code|Can be enforced centrally by the DBMS|
|Concurrency|Depends on file formats, locks, and application logic|DBMS can provide transaction and concurrency control|
|Backup and recovery|Depends on file/application tools|May provide integrated backup and recovery facilities|
|Data independence|Usually more tightly coupled to application file formats|Logical and physical data independence may be supported|

## 4.2 Understanding redundancy and inconsistency

Suppose the same student appears in two independent files.

`fees.txt`

```
101, Amit, 50000
```

`marks.txt`

```
101, Amit, 85
```

If the student's name changes to `Amit Kumar` and only one file is updated, the two files become inconsistent.

A database design can keep the student's name in one `Student` table and use `StudentID` to relate fee and marks records to that student.

### Key limitations of the file-system approach

- Redundant copies can lead to inconsistencies.
    
- Custom code may be required for each type of query.
    
- Shared updates and simultaneous access can be difficult to coordinate.
    
- Integrity rules may be scattered across applications.
    

### Are file systems always bad?

No. Ordinary files are perfectly suitable for simple storage needs, static documents, configuration files, logs, and data that does not require database-level queries or concurrent transactions.

The key is choosing the right tool for the application's needs.

Exam trap: A file system stores and organizes files. A DBMS provides specialized facilities for defining, querying, controlling, and recovering structured data. A DBMS also uses files internally in many implementations.

# 5. Data models

A data model is a collection of concepts used to describe how data is organized, related, constrained, and manipulated within a database.

Data models help database designers represent real-world information in a structured way.

## 5.1 Types of data models

|Model|Main idea|Example or use|
|---|---|---|
|Hierarchical model|Data is organized as a tree with parent-child relationships|A department structure with subordinate units|
|Network model|Records can have multiple links and relationship paths|Complex interconnected records|
|Relational model|Data is organized into relations, commonly implemented as tables|Student, course, and enrollment tables|
|Entity-Relationship (ER) model|Represents entities, attributes, and relationships|Designing a college database before implementation|
|Object-oriented model|Represents information as objects with attributes and behavior|Applications built around object-oriented structures|
|Document model|Stores data as documents, often JSON-like structures|Product documents with varying attributes|

For your basic DBMS syllabus, focus particularly on the hierarchical, network, relational, and ER models.

## 5.2 Hierarchical data model

The hierarchical model organizes records in a tree-like structure. A parent can have multiple children, but each child ordinarily has one parent within the hierarchy.

Example:

```
University
   |
 Faculties
   |
Departments
   |
Students
```

This model is suitable for naturally hierarchical data, but representing many-to-many relationships is less direct than in a relational model.

## 5.3 Network data model

The network model represents records connected through links. A record can participate in multiple relationships, allowing more complex structures than a simple parent-child hierarchy.

Conceptual example:

```
Student A ───── Course X
    |               |
 Course Y ───── Student B
```

This is just an illustration of interconnected relationships, not a strict network-model schema.

## 5.4 Relational data model

The relational model organizes data into relations. A relation is mathematically a set of tuples over defined attributes.

Example:

|StudentID|Name|Department|
|---|---|---|
|101|Amit|CSE|
|102|Neha|IT|
|103|Ravi|CSE|

It supports operations such as selection, projection, and joining relations.

## 5.5 ER model

The Entity-Relationship model is commonly used to design a database at the conceptual level.

Its principal concepts are:

- Entity: An object or concept, such as a Student.
    
- Attribute: A property, such as StudentID or Name.
    
- Relationship: An association, such as a Student enrolling in a Course.
    

Example:

```
STUDENT ─── ENROLLS IN ─── COURSE
```

The ER design can later be translated into relational tables.

### Conceptual vs logical vs physical models

These three levels can appear in database-theory questions.

|Level|Focus|
|---|---|
|Conceptual|What entities, relationships, and rules are needed?|
|Logical|How is data organized in a logical model such as relational tables?|
|Physical|How and where is data actually stored, indexed, and accessed?|

Exam trap: The ER model is primarily a conceptual design tool. The relational model defines data using relations and is used at the logical level.

# 6. Relational model — detailed study

The relational model, proposed by E. F. Codd, organizes data into relations. In an RDBMS, relations are commonly represented as tables.

Consider this `Student` relation:

|StudentID|Name|Age|Department|
|---|---|---|---|
|101|Amit|22|CSE|
|102|Neha|21|IT|
|103|Ravi|23|CSE|

Let's understand the formal terminology.

## 6.1 Relation

A relation is a set of tuples defined over a set of attributes.

In the example, `Student` is the relation.

In the mathematical relational model, tuples are unique within a relation and their ordering is irrelevant. SQL tables may contain duplicate rows unless constraints or query operations prevent them, so a physical SQL table is not always a perfect implementation of the mathematical set abstraction.

## 6.2 Tuple

A tuple is one row of a relation.

For example:

```
(101, Amit, 22, CSE)
```

This tuple contains the details of one student.

Exam memory: Tuple = row.

## 6.3 Attribute

An attribute is a named property of a relation, commonly represented by a column.

In the example:

- `StudentID`
    
- `Name`
    
- `Age`
    
- `Department`
    

are attributes.

Exam memory: Attribute = column.

## 6.4 Domain

A domain is the set of allowed values for an attribute.

Examples:

- `Age`: valid non-negative integers within the application's rules.
    
- `Department`: values such as `CSE`, `IT`, and `ECE`.
    
- `StudentID`: permitted student identifier values.
    

The actual domain is determined by the database schema and business rules.

Exam trap: A domain is the set of permitted values for an attribute, not the collection of all rows in the table.

## 6.5 Degree and cardinality

Two terms are especially important for MCQs.

- Degree: Number of attributes (columns) in a relation.
    
- Cardinality: Number of tuples (rows) in a relation.
    

For our example:

|Property|Value|
|---|---|
|Attributes|4|
|Tuples|3|
|Degree|4|
|Cardinality|3|

Memory trick:

- Degree → columns.
    
- Cardinality → rows.
    

Some books use cardinality in other mathematical contexts with different meanings, but in the relational-model terminology above, it means the number of tuples.

## 6.6 Schema vs instance

A relation schema defines the structure and attributes of a relation. A relation instance is the actual set of tuples stored at a particular time.

For example:

```
Student(StudentID, Name, Age, Department)
```

is the schema.

The actual records for Amit, Neha, and Ravi form an instance of that relation.

|Term|Meaning|
|---|---|
|Schema|Structure or design of the relation|
|Instance|The current contents of the relation|

The schema usually changes less frequently than the data instance.

## 6.7 Keys in the relational model

A key is an attribute or combination of attributes used to identify tuples or establish relationships between relations.

Consider:

Student

|StudentID|Name|DepartmentID|
|---|---|---|
|101|Amit|D01|
|102|Neha|D02|
|103|Ravi|D01|

Department

|DepartmentID|DepartmentName|
|---|---|
|D01|CSE|
|D02|IT|

### Primary key

A primary key uniquely identifies each row and does not allow `NULL` values.

Here, `StudentID` is the primary key of `Student`, while `DepartmentID` is the primary key of `Department`.

### Candidate key

A candidate key is a minimal attribute set that can uniquely identify a tuple. A relation can have multiple candidate keys; one is selected as the primary key.

For example, if both `StudentID` and `Email` are guaranteed unique and non-null, each may be a candidate key.

### Superkey

A superkey is any attribute set that uniquely identifies a tuple, even if it contains unnecessary attributes.

For instance, if `StudentID` uniquely identifies a student, then both `{StudentID}` and `{StudentID, Name}` are superkeys. Only `{StudentID}` is minimal.

### Foreign key

A foreign key is an attribute or attribute set referencing a candidate key, commonly a primary key, in the same or another relation. It helps enforce referential integrity.

In the example above, `Student.DepartmentID` references `Department.DepartmentID`.

### Composite key

A composite key consists of two or more attributes.

For an enrollment table:

|StudentID|CourseID|Grade|
|---|---|---|
|101|C01|A|
|101|C02|B|
|102|C01|A|

`(StudentID, CourseID)` could be a composite primary key because the same student can take multiple courses, while each student-course pair uniquely identifies an enrollment.

### Key comparison

|Key type|Main purpose|
|---|---|
|Superkey|Uniquely identifies a tuple|
|Candidate key|Minimal superkey|
|Primary key|Candidate key chosen as the main identifier|
|Foreign key|References a candidate key in another or the same relation|
|Composite key|Key made from multiple attributes|

Exam traps:

- Every candidate key is a superkey, but every superkey is not necessarily a candidate key.
    
- A relation can have several candidate keys, but only one primary key constraint.
    
- A composite key has multiple attributes; it is not a special kind of foreign key.
    
- A foreign key may contain `NULL` values if the schema permits them and the constraint is not otherwise violated.
    

## 6.8 Integrity constraints

Integrity constraints help ensure that the data follows the rules of the database.

|Constraint|Purpose|
|---|---|
|Domain constraint|Values must belong to the attribute's allowed domain|
|Key constraint|Candidate key values must uniquely identify tuples|
|Entity integrity|A primary key cannot be `NULL`|
|Referential integrity|A non-null foreign key must reference an existing candidate key value, subject to the schema's rules|

In SQL, constraints can include `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, and `CHECK`.

Example:

```
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Age INT CHECK (Age >= 0),
    DepartmentID VARCHAR(10)
);
```

This is a simplified example of a table definition. The precise syntax and enforcement behavior of some constraints may vary by DBMS.

## 6.9 Relational operations — basic preview

The relational model supports operations for retrieving and combining data.

|Operation|Purpose|SQL concept commonly used|
|---|---|---|
|Selection|Chooses rows satisfying a condition|`WHERE`|
|Projection|Chooses particular attributes/columns|`SELECT` column list|
|Join|Combines related tuples from relations|`JOIN ... ON`|
|Union|Combines tuples from compatible relations|`UNION`|
|Difference|Returns tuples in one relation but not another|`EXCEPT` or equivalent|

For example:

```
SELECT Name
FROM Student
WHERE DepartmentID = 'D01';
```

This query selects student names from department `D01`.

Important distinction: In relational algebra, projection removes duplicate tuples because relations are sets. SQL's ordinary `SELECT` does not automatically remove duplicates; `SELECT DISTINCT` requests duplicate elimination.

## Final revision sheet

|Topic|Must remember|
|---|---|
|Database|Organized collection of related data|
|DBMS|Software for managing databases|
|RDBMS|DBMS based on the relational model|
|File system vs DBMS|Compare redundancy, querying, security, integrity, concurrency, and recovery|
|Data model|Describes data structure, relationships, and constraints|
|Hierarchical model|Tree-like parent-child organization|
|Network model|Interconnected records and relationships|
|ER model|Conceptual design using entities, attributes, and relationships|
|Relational model|Data organized as relations|
|Tuple|Row|
|Attribute|Column|
|Domain|Allowed values for an attribute|
|Degree|Number of attributes|
|Cardinality|Number of tuples|
|Primary key|Chosen candidate key; unique and non-null|
|Foreign key|References a candidate key|
|Schema|Database structure|
|Instance|Data stored at a particular time|

Highest-priority exam topics: DBMS vs RDBMS, file system vs DBMS, types of data models, relation/tuple/attribute/domain, degree vs cardinality, and the distinctions among primary, candidate, super, composite, and foreign keys.