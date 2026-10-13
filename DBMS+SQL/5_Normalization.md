## 1. What is normalization?

Normalization is the process of organizing database tables to reduce unnecessary data redundancy and avoid data anomalies.

Consider this table:

|StudentID|StudentName|CourseID|CourseName|
|---|---|---|---|
|101|Amit|C01|DBMS|
|102|Neha|C01|DBMS|
|103|Ravi|C02|Networks|

The course name `DBMS` is repeated for every student taking course C01.

This creates potential problems:

- Update anomaly: If the course name changes, multiple rows may need updating.
    
- Insertion anomaly: You may be unable to store a course until a student enrols in it, depending on the table design.
    
- Deletion anomaly: Deleting the only student enrolled in a course may also remove the only stored information about that course.
    

Normalization helps address these problems by dividing data into well-designed related tables.

The main normal forms in your syllabus are:

## 1NF

First Normal Form

Atomic values; no repeating groups.

## 2NF

Second Normal Form

1NF + no partial dependency of non-prime attributes on a candidate key.

## 3NF

Third Normal Form

2NF + the formal 3NF dependency condition; eliminates many transitive dependencies.

## BCNF

Boyce–Codd Normal Form

Every determinant of a non-trivial functional dependency must be a superkey.

## 2. Functional dependency (FD)

A functional dependency describes a relationship between attributes: one attribute or group of attributes determines another attribute or group of attributes.

It is written as:

\[ X \rightarrow Y \]

Read this as: X functionally determines Y.

If two rows have the same value of X, they must have the same value of Y.

### Example

|StudentID|StudentName|Department|
|---|---|---|
|101|Amit|CSE|
|102|Neha|ECE|
|103|Ravi|CSE|

Assuming each StudentID identifies one student:

\[ StudentID \rightarrow StudentName \]

\[ StudentID \rightarrow Department \]

Here, `StudentID` determines the name and department.

But the reverse is not necessarily true:

\[ Department \not\rightarrow StudentID \]

Why? Multiple students can belong to the same department.

### Important FD terminology

|Term|Meaning|Example|
|---|---|---|
|Determinant|Attribute(s) on the left side of an FD|`StudentID`|
|Dependent|Attribute(s) on the right side|`StudentName`|
|Full functional dependency|The entire determinant is needed; no proper subset determines the dependent|`(StudentID, CourseID) → Grade`|
|Partial dependency|A proper subset of a composite determinant determines a non-prime attribute|`StudentID → StudentName` when the key is `(StudentID, CourseID)`|
|Transitive dependency|A dependency occurs through an intermediate attribute set|`EmpID → DeptID → DeptName`|

### Full vs partial dependency

Suppose the candidate key is `(StudentID, CourseID)`.

\[ (StudentID,CourseID)\rightarrow Grade \]

If neither `StudentID` alone nor `CourseID` alone determines `Grade`, this is a full functional dependency.

But suppose:

\[ StudentID\rightarrow StudentName \]

Then `StudentName` depends on only part of the composite key. This is a partial dependency, which is relevant to 2NF.

## 3. First Normal Form (1NF)

A table is in 1NF when every attribute contains a single atomic value for each row, with no repeating groups or multivalued cells.

### Example: Not in 1NF

|StudentID|Name|PhoneNumbers|
|---|---|---|
|101|Amit|9876, 8765|
|102|Neha|7654|

The `PhoneNumbers` cell for Amit contains multiple values.

### Convert to 1NF

One possible design is:

|StudentID|Name|PhoneNumber|
|---|---|---|
|101|Amit|9876|
|101|Amit|8765|
|102|Neha|7654|

Each cell now contains one phone number.

A more normalized design might store phone numbers in a separate table, avoiding repeated student details. The key for that table could be `(StudentID, PhoneNumber)` if duplicate numbers per student are not allowed.

Remember for the exam:

- 1NF → atomic values.
    
- No repeating groups or multivalued cells.
    
- 1NF does not guarantee that all data redundancy has been removed.
    

MCQ trap: Atomic means one value per cell, not necessarily one character or one word.

## 4. Second Normal Form (2NF)

A table is in 2NF if:

1. It is already in 1NF.
    
2. Every non-prime attribute is fully functionally dependent on every candidate key—there are no partial dependencies of non-prime attributes on candidate keys.
    

A prime attribute belongs to at least one candidate key. An attribute that belongs to no candidate key is a non-prime attribute.

### Example: Violates 2NF

Consider the relation:

`ENROLLMENT(StudentID, CourseID, StudentName, CourseName, Grade)`

Assume its candidate key is `(StudentID, CourseID)`.

|StudentID|CourseID|StudentName|CourseName|Grade|
|---|---|---|---|---|
|101|C01|Amit|DBMS|A|
|101|C02|Amit|Networks|B|
|102|C01|Neha|DBMS|A|

Functional dependencies:

\[ StudentID\rightarrow StudentName \]

\[ CourseID\rightarrow CourseName \]

\[ (StudentID,CourseID)\rightarrow Grade \]

The primary key is composite: `(StudentID, CourseID)`.

However:

- `StudentName` depends only on `StudentID`.
    
- `CourseName` depends only on `CourseID`.
    
- Both are partial dependencies on parts of the composite key.
    

Therefore, this relation violates 2NF.

### Convert to 2NF

Split the relation into three tables:

STUDENT

|StudentID (PK)|StudentName|
|---|---|
|101|Amit|
|102|Neha|

COURSE

|CourseID (PK)|CourseName|
|---|---|
|C01|DBMS|
|C02|Networks|

ENROLLMENT

|StudentID (PK part)|CourseID (PK part)|Grade|
|---|---|---|
|101|C01|A|
|101|C02|B|
|102|C01|A|

Now student names are stored with student IDs, course names with course IDs, and grades with the student-course combination.

Important exam rule: If a relation is in 1NF and every candidate key consists of a single attribute, it cannot have a partial dependency on a proper subset of that key. Therefore, it is in 2NF.

## 5. Third Normal Form (3NF)

A relation is in 3NF if it is in 2NF and satisfies the following formal condition:

For every non-trivial functional dependency \(X\rightarrow A\), at least one of these must hold:

1. \(X\) is a superkey, or
    
2. \(A\) is a prime attribute.
    

In simplified exam language, 3NF prevents problematic transitive dependencies of non-prime attributes on candidate keys.

### Example: Violates 3NF

Consider:

`EMPLOYEE(EmpID, EmpName, DeptID, DeptName)`

|EmpID|EmpName|DeptID|DeptName|
|---|---|---|---|
|101|Amit|D01|IT|
|102|Neha|D02|HR|
|103|Ravi|D01|IT|

Assume each employee belongs to one department, and each `DeptID` determines its department name.

Functional dependencies:

\[ EmpID\rightarrow EmpName,DeptID \]

\[ DeptID\rightarrow DeptName \]

Here, `EmpID` is the primary key.

The transitive dependency is:

\[ EmpID\rightarrow DeptID\rightarrow DeptName \]

The department name depends on the department ID rather than directly on the employee identity.

This relation is in 2NF because its candidate key is a single attribute, but it violates 3NF: `DeptID` is not a superkey, and `DeptName` is non-prime.

### Convert to 3NF

EMPLOYEE

|EmpID (PK)|EmpName|DeptID (FK)|
|---|---|---|
|101|Amit|D01|
|102|Neha|D02|
|103|Ravi|D01|

DEPARTMENT

|DeptID (PK)|DeptName|
|---|---|
|D01|IT|
|D02|HR|

Now department information is stored separately, and employee records refer to their department.

Remember for the exam:

- 3NF → remove problematic transitive dependencies.
    
- A relation in 3NF is also in 2NF and 1NF.
    
- The formal 3NF definition allows certain dependencies that do not satisfy BCNF, provided the right-hand attribute is prime.
    

## 6. Boyce–Codd Normal Form (BCNF)

BCNF is stricter than 3NF.

A relation is in BCNF if, for every non-trivial functional dependency:

\[ X\rightarrow Y \]

\(X\) must be a superkey.

In other words, every determinant must be a superkey.

### Example: In 3NF but not in BCNF

Consider:

`R(Student, Course, Instructor)`

Assume the following rules:

- A student has one instructor for a particular course.
    
- Every instructor teaches only one course.
    

The functional dependencies are:

\[ (Student,Course)\rightarrow Instructor \]

\[ Instructor\rightarrow Course \]

The candidate keys are:

- `(Student, Course)`
    
- `(Student, Instructor)`
    

Every attribute is a prime attribute because each appears in at least one candidate key.

Now consider:

\[ Instructor\rightarrow Course \]

`Instructor` alone cannot identify a complete row, since an instructor can teach many students. Therefore, `Instructor` is not a superkey.

However, `Course` is a prime attribute. This dependency satisfies the formal 3NF condition, but it violates BCNF because its determinant is not a superkey.

### Convert to BCNF

Decompose the relation into:

INSTRUCTOR_COURSE

|Instructor (PK)|Course|
|---|---|
|Prof X|DBMS|
|Prof Y|Networks|

STUDENT_INSTRUCTOR

|Student|Instructor|
|---|---|
|Amit|Prof X|
|Neha|Prof X|
|Amit|Prof Y|

Under the assumed rules, this removes the dependency `Instructor → Course` from the original three-attribute relation. BCNF decomposition is lossless here, though in general, BCNF decomposition may fail to preserve every original functional dependency.

Exam point: A relation in BCNF is necessarily in 3NF, but a relation in 3NF is not necessarily in BCNF.

## 7. Difference between 1NF, 2NF, 3NF and BCNF

|Normal form|Main requirement|What it addresses|
|---|---|---|
|1NF|Atomic values; no repeating groups|Multivalued cells and repeating groups|
|2NF|1NF + no partial dependencies of non-prime attributes on candidate keys|Partial dependency|
|3NF|2NF + formal 3NF FD condition|Problematic transitive dependencies|
|BCNF|Every determinant of a non-trivial FD is a superkey|Remaining determinant-related anomalies|

### The order to memorize

1NF

2NF

3NF

BCNF

Each successive form adds stronger constraints. BCNF is stricter than 3NF.

## 8. Common DSSSB exam traps

|Statement|Correct answer|
|---|---|
|1NF requires atomic values.|True|
|2NF eliminates partial dependency of non-prime attributes on candidate keys.|True|
|3NF eliminates every possible transitive FD, without exception.|False; use the formal definition|
|BCNF requires every determinant of a non-trivial FD to be a superkey.|True|
|Every BCNF relation is in 3NF.|True|
|Every 3NF relation is in BCNF.|False|
|A single-attribute candidate key can have a partial dependency on a proper subset of itself.|False|
|Decomposing tables always preserves every functional dependency.|False|
|Normalization is mainly used to increase redundant data.|False|
|A prime attribute belongs to at least one candidate key.|True|
### Final revision trick

- 1NF: Atomic values.
    
- 2NF: No partial dependency of non-prime attributes on candidate keys.
    
- 3NF: For every non-trivial FD, the determinant is a superkey or the dependent attribute is prime.
    
- BCNF: Every determinant of a non-trivial FD is a superkey.
    

For your preparation, make sure you can identify a candidate key and the functional dependencies first. Most normalization questions become much easier once those are clear.