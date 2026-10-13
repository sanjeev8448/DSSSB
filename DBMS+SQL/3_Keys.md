## 1. Understand with an example

Consider these two tables.

STUDENT

|RollNo|Email|Name|DeptID|
|---|---|---|---|
|101|amit@example.com|Amit|10|
|102|neha@example.com|Neha|20|
|103|ravi@example.com|Ravi|10|

Assume `RollNo` and `Email` are both unique and cannot be NULL.

DEPARTMENT

|DeptID|DeptName|
|---|---|
|10|Computer Science|
|20|Electronics|

Here, `RollNo` and `Email` can each uniquely identify a student. `DeptID` connects a student to their department.

## 2. Six types of keys

### 1. Super Key

A super key is any attribute or combination of attributes that uniquely identifies a row in a table.

In the `STUDENT` table, these are examples of super keys:

- `{RollNo}`
    
- `{Email}`
    
- `{RollNo, Name}`
    
- `{RollNo, Email}`
    
- `{RollNo, Name, DeptID}`
    

Why is `{RollNo, Name}` a super key? Because `RollNo` already identifies the student uniquely. Adding `Name` does not remove that uniqueness.

Key point: A super key may contain unnecessary attributes.

### 2. Candidate Key

A candidate key is a minimal super key: it uniquely identifies each row, and no attribute can be removed from it without losing that uniqueness.

In our example:

- `{RollNo}` is a candidate key.
    
- `{Email}` is a candidate key.
    

But `{RollNo, Name}` is not a candidate key because `Name` is unnecessary.

Key point: Every candidate key is a super key, but not every super key is a candidate key.

### 3. Primary Key

A primary key is the candidate key selected to identify records as the main identifier of a table.

Suppose we select `RollNo` as the primary key.

```
CREATE TABLE Student (
    RollNo INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE NOT NULL,
    Name VARCHAR(50),
    DeptID INT
);
```

Primary key properties:

- Must uniquely identify each row.
    
- Cannot contain `NULL`.
    
- Cannot have duplicate values.
    
- Only one primary key constraint is defined per table, though it may consist of multiple columns.
    

Exam trap: One primary key does not necessarily mean one column. A primary key can be composite.

### 4. Alternate Key

An alternate key is a candidate key that was not selected as the primary key.

In our example:

- Candidate keys: `RollNo`, `Email`
    
- Selected primary key: `RollNo`
    
- Alternate key: `Email`
    

An alternate key can be enforced with a `UNIQUE` constraint. Whether it permits `NULL` depends on the database system and the constraints applied; in our example, `Email` is explicitly `NOT NULL`.

Exam trap: An alternate key is not just any unique-looking column. It must be a candidate key—that is, a minimal super key.

### 5. Foreign Key

A foreign key is an attribute or combination of attributes in one table that refers to a candidate key—commonly a primary key—in another table or, in some designs, the same table.

In `STUDENT`, `DeptID` references `DEPARTMENT.DeptID`.

```
CREATE TABLE Department (
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(50)
);

CREATE TABLE Student (
    RollNo INT PRIMARY KEY,
    Name VARCHAR(50),
    DeptID INT,
    FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
```

This helps maintain referential integrity: a non-NULL foreign-key value must match a referenced key value.

Important properties:

- A foreign key may contain duplicate values.
    
- It can be `NULL` unless the column is constrained otherwise.
    
- A table can have multiple foreign keys.
    
- A foreign key does not have to be unique.
    
- Foreign keys can consist of multiple columns.
    

For example, several students can have `DeptID = 10`, because many students can belong to the same department.

### 6. Composite Key

A composite key is a key consisting of two or more attributes used together to identify a row uniquely.

Consider an `ENROLLMENT` table:

|StudentID|CourseID|Grade|
|---|---|---|
|101|CS101|A|
|101|CS102|B|
|102|CS101|A|

A student may enrol in multiple courses, and each course may have multiple students. Neither `StudentID` nor `CourseID` alone uniquely identifies an enrollment. Together, they do.

```
CREATE TABLE Enrollment (
    StudentID INT,
    CourseID VARCHAR(10),
    Grade CHAR(1),
    PRIMARY KEY (StudentID, CourseID)
);
```

The composite primary key is `(StudentID, CourseID)`.

Key point: A composite key can be a primary key, candidate key, super key, or foreign key, depending on how it is used and defined.

## 3. Comparison table — revise this before the exam

|Key|Main meaning|Example|
|---|---|---|
|Super key|Any attribute set that uniquely identifies a row|`{RollNo, Name}`|
|Candidate key|Minimal super key|`{RollNo}`, `{Email}`|
|Primary key|Candidate key selected as the main identifier|`RollNo`|
|Alternate key|Candidate key not selected as primary|`Email`|
|Foreign key|References a key in a related table|`Student.DeptID`|
|Composite key|Key formed from 2 or more attributes|`(StudentID, CourseID)`|

## 4. Key relationships to remember

Super key and candidate key

Candidate key = minimal super key. Every candidate key qualifies as a super key.

Candidate key and primary key

A table can have multiple candidate keys but only one primary key constraint.

Primary key and alternate key

The chosen candidate key is primary; the remaining candidate keys are alternate keys.

Primary key and foreign key

A primary key uniquely identifies rows in its table. A foreign key establishes a reference to a key in a related table.

## 5. Common exam traps

| Statement                                          | Correct?                               |
| -------------------------------------------------- | -------------------------------------- |
| Every candidate key is a super key.                | Yes                                    |
| Every super key is a candidate key.                | No                                     |
| A primary key can contain NULL.                    | No                                     |
| A table can have multiple primary key constraints. | No                                     |
| A primary key can contain multiple columns.        | Yes                                    |
| A foreign key must always be unique.               | No                                     |
| A foreign key can contain NULL.                    | Yes, unless prohibited by a constraint |
| Every alternate key is a candidate key.            | Yes                                    |
| A composite key has at least two attributes.       | Yes                                    |
| A table can have multiple foreign keys.            | Yes                                    |
Last-minute memory trick: Super = any unique combination; Candidate = minimal; Primary = selected; Alternate = not selected; Foreign = reference between tables; Composite = multiple attributes together.