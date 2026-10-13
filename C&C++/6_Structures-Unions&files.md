# Part 1: Structures and Unions

## 1. Structure in C

A structure (`struct`) is a user-defined data type that groups related variables, potentially of different data types, under one name.

For example, a student record may contain a roll number, name, and marks. Without a structure, you would need separate variables for each field.

### A. Structure declaration and definition

```

#include <stdio.h>

struct Student
{
    int roll;
    char grade;
    float marks;
};

int main(void)
{
    struct Student s1;

    s1.roll = 101;
    s1.grade = 'A';
    s1.marks = 87.5f;

    printf("Roll = %d\n", s1.roll);
    printf("Grade = %c\n", s1.grade);
    printf("Marks = %.1f\n", s1.marks);

    return 0;
}
```

Output

```
Roll = 101
Grade = A
Marks = 87.5
```

Understand each part:

- `struct Student` defines a structure type.
    
- `roll`, `grade`, and `marks` are its members.
    
- `struct Student s1;` creates a structure variable.
    
- `s1.roll` accesses the `roll` member using the dot (`.`) operator.
    

### B. Initializing a structure

You can initialize its members when declaring the variable.

```

#include <stdio.h>

struct Student
{
    int roll;
    float marks;
};

int main(void)
{
    struct Student s1 = {101, 92.5f};

    printf("%d %.1f\n", s1.roll, s1.marks);

    return 0;
}
```

Output

```
101 92.5
```

Values are assigned in member declaration order in this example: `roll` first, then `marks`.

### C. Accessing structure members

Use the dot operator with a structure variable:

```
s1.roll
s1.marks
```

If you have a pointer to a structure, use the arrow operator:

```
ptr->roll
```

The following two expressions are equivalent when `ptr` validly points to a structure:

```
ptr->roll
(*ptr).roll
```

Exam tip: `.` is used with a structure object; `->` is used with a pointer to a structure.

### D. Array of structures

An array of structures stores multiple records of the same structure type.

```

#include <stdio.h>

struct Student
{
    int roll;
    float marks;
};

int main(void)
{
    struct Student s[2] = {
        {101, 80.0f},
        {102, 91.5f}
    };

    for (int i = 0; i < 2; i++)
    {
        printf("%d %.1f\n", s[i].roll, s[i].marks);
    }

    return 0;
}
```

Output

```
101 80.0
102 91.5
```

Here, `s[0]` and `s[1]` are separate structure objects.

## 2. Union in C

A union (`union`) is a user-defined data type whose members share the same memory region.

Unlike a structure, where each member has its own storage within the structure object, union members overlap in storage.

### A. Union declaration and use

```

#include <stdio.h>

union Data
{
    int i;
    float f;
    char ch;
};

int main(void)
{
    union Data d;

    d.i = 10;
    printf("%d\n", d.i);

    d.ch = 'A';
    printf("%c\n", d.ch);

    return 0;
}
```

Output

```
10
A
```

The first assignment stores `10` through `d.i`. The next assignment stores `'A'` through `d.ch`, using the same union storage.

Important: A union can hold different types of values at different times, but its members share storage. You should generally read the member that was most recently written. Reading another member may produce a representation-dependent result and is not a portable way to convert between types.

### B. How does union memory work?

Conceptually:

Structure: separate member storage

`int i`

`float f`

`char ch`

Union: shared member storage

`int i`

`float f`

`char ch`

These are alternative interpretations of overlapping storage, not three independent memory blocks.

The size of a union is at least large enough to accommodate its largest member, with possible additional padding to satisfy alignment requirements.

For example:

```
union Example
{
    int a;
    double b;
    char c;
};
```

Its size is at least `sizeof(double)`, but the exact size is implementation-dependent.

## 3. Difference between structure and union

This is a high-value comparison for theory and MCQs.

|Feature|Structure (`struct`)|Union (`union`)|
|---|---|---|
|Memory|Each member has its own storage|Members share overlapping storage|
|Member values|Can be stored independently at the same time|Writing one member can affect the representation of others|
|Size|At least enough for all members, including padding|At least enough for the largest member, including alignment|
|Member access|Uses `.` or `->`|Uses `.` or `->`|
|Typical use|Student, employee, or product records|Variant data where one of several representations is used at a time|

### Output-based example

```

#include <stdio.h>

struct S
{
    int x;
    int y;
};

union U
{
    int x;
    int y;
};

int main(void)
{
    struct S s = {10, 20};
    union U u;

    u.x = 10;
    u.y = 20;

    printf("%d %d\n", s.x, s.y);
    printf("%d\n", u.y);

    return 0;
}
```

Output

```
10 20
20
```

Why?

- Structure `s` retains both values independently.
    
- Union `u` shares storage between `x` and `y`. After `u.y = 20`, `u.y` is the member that was most recently written, so it prints `20`.
    

Do not use this example to assume that reading `u.x` afterward must print `10`. It is not a portable way to preserve both values.

## 4. Nested structures

A nested structure is a structure that contains another structure as one of its members.

For example, a student record may include a date of birth, with day, month, and year grouped into a separate structure.

```

#include <stdio.h>

struct Date
{
    int day;
    int month;
    int year;
};

struct Student
{
    int roll;
    struct Date dob;
};

int main(void)
{
    struct Student s = {
        101,
        {15, 8, 2005}
    };

    printf("Roll = %d\n", s.roll);
    printf("DOB = %02d-%02d-%d\n",
           s.dob.day, s.dob.month, s.dob.year);

    return 0;
}
```

Output

```
Roll = 101
DOB = 15-08-2005
```

Understand the member access:

- `s.roll` accesses the student's roll number.
    
- `s.dob` accesses the nested `Date` structure.
    
- `s.dob.day` accesses the day inside that nested structure.
    

You can also assign nested members individually:

```
s.dob.day = 15;
s.dob.month = 8;
s.dob.year = 2005;
```

Exam tip: A nested structure is different from a pointer to a structure. Here, `dob` is a structure member contained directly inside `Student`.

# Part 2: File handling in C

File handling allows a program to save data to a file and retrieve it later. Unlike ordinary local variables, file data can remain available after the program terminates.

The standard C file API uses `FILE *` and functions from `<stdio.h>`.

## 5. Opening and closing a file

The most common pattern is:

```
FILE *fp = fopen("data.txt", "r");
```

- `FILE` is a type declared by the standard I/O library.
    
- `fp` is a pointer used to manage the open file stream.
    
- `fopen()` opens a file with the specified mode.
    
- `fclose()` closes an open stream.
    

Always check whether `fopen()` succeeds before reading or writing.

```

#include <stdio.h>

int main(void)
{
    FILE *fp = fopen("data.txt", "r");

    if (fp == NULL)
    {
        printf("Could not open file\n");
        return 1;
    }

    printf("File opened successfully\n");

    fclose(fp);
    return 0;
}
```

If `data.txt` exists and can be opened for reading, the output is:

```
File opened successfully
```

Otherwise, the program prints the error message.

## 6. File modes in C

The mode string determines whether a file is read, written, appended to, or opened for both reading and writing.

|Mode|Meaning|If file does not exist|
|---|---|---|
|`"r"`|Read text|Fails|
|`"w"`|Write text; truncate existing file|Creates it|
|`"a"`|Append text|Creates it|
|`"r+"`|Read and write without truncating|Fails|
|`"w+"`|Read and write; truncate existing file|Creates it|
|`"a+"`|Read and append|Creates it|
|`"rb"`|Read binary|Fails|
|`"wb"`|Write binary; truncate existing file|Creates it|
|`"ab"`|Append binary|Creates it|
|`"rb+"` / `"r+b"`|Read and write binary|Fails|
|`"wb+"` / `"w+b"`|Read and write binary; truncate|Creates it|
|`"ab+"` / `"a+b"`|Read and append binary|Creates it|

The `b` indicates binary mode. On systems that distinguish text and binary streams, this affects how data is interpreted and transferred.

### Most important mode differences

- `r` — existing file required; read only.
    
- `w` — creates a file or truncates an existing one; writing.
    
- `a` — writes at the end, preserving existing contents.
    
- `r+` — reading and writing, but an existing file is required.
    
- `w+` — reading and writing, but existing contents are erased.
    
- `a+` — reading and appending; writes go to the end of the file.
    

Exam trap: Opening an existing file in `"w"` or `"w+"` can erase its previous contents. Use append mode if you need to preserve them.

## 7. Writing to a text file

Use `fprintf()` to write formatted text to a file, or `fputs()` to write a string.

### Example: writing student data

```

#include <stdio.h>

int main(void)
{
    FILE *fp = fopen("student.txt", "w");

    if (fp == NULL)
    {
        perror("student.txt");
        return 1;
    }

    fprintf(fp, "Roll: %d\n", 101);
    fprintf(fp, "Marks: %.1f\n", 87.5);

    if (fclose(fp) == EOF)
    {
        perror("Error closing file");
        return 1;
    }

    printf("Data written\n");
    return 0;
}
```

Console output

```
Data written
```

The file `student.txt` will contain:

```
Roll: 101
Marks: 87.5
```

Remember that the output above is the file's content, not the console output.

### What do the functions do?

- `fprintf(fp, ...)` writes formatted text to the stream.
    
- `fputs("Hello", fp)` writes a string to the stream.
    
- `fputc('A', fp)` writes one character.
    
- `fclose(fp)` closes the stream and flushes buffered output, reporting a failure if one occurs.
    

## 8. Reading from a text file

You can use `fscanf()`, `fgets()`, or `fgetc()` depending on the data.

### A. Reading line by line with `fgets()`

```

#include <stdio.h>

int main(void)
{
    FILE *fp = fopen("student.txt", "r");
    char line[100];

    if (fp == NULL)
    {
        perror("student.txt");
        return 1;
    }

    while (fgets(line, sizeof line, fp) != NULL)
    {
        printf("%s", line);
    }

    if (ferror(fp))
        perror("Error reading file");

    fclose(fp);
    return 0;
}
```

If `student.txt` contains:

```
Roll: 101
Marks: 87.5
```

The console prints:

```
Roll: 101
Marks: 87.5
```

`fgets()` reads at most one less than the buffer capacity and null-terminates the string when it succeeds. It retains a newline if one fits in the buffer.

### B. Reading one character at a time

```

#include <stdio.h>

int main(void)
{
    FILE *fp = fopen("student.txt", "r");
    int ch;

    if (fp == NULL)
    {
        perror("student.txt");
        return 1;
    }

    while ((ch = fgetc(fp)) != EOF)
    {
        putchar(ch);
    }

    fclose(fp);
    return 0;
}
```

This reads each character until the end of the file. The variable is `int`, not `char`, because `fgetc()` must represent every possible unsigned-character value as well as the special `EOF` result.

### C. Reading formatted data with `fscanf()`

Suppose a file contains:

```
101 87.5
```

You can read those values as follows:

```

#include <stdio.h>

int main(void)
{
    FILE *fp = fopen("marks.txt", "r");
    int roll;
    float marks;

    if (fp == NULL)
    {
        perror("marks.txt");
        return 1;
    }

    if (fscanf(fp, "%d %f", &roll, &marks) == 2)
    {
        printf("%d %.1f\n", roll, marks);
    }

    fclose(fp);
    return 0;
}
```

Output

```
101 87.5
```

The return value of `fscanf()` is the number of input items successfully assigned. Checking it helps prevent using uninitialized or incomplete data.

## 9. Text files vs binary files

A text file stores data as characters intended to represent text. A binary file stores bytes without requiring them to be interpreted as human-readable text.

### Text representation

Number 1234

Stored as character digits such as `'1'`, `'2'`, `'3'`, `'4'` when written as text.

### Binary representation

Integer value 1234

Stored using the machine's binary representation of the integer, typically occupying `sizeof(int)` bytes when written with `fwrite()`.

### A. Writing a binary file using `fwrite()`

```

#include <stdio.h>

int main(void)
{
    int numbers[] = {10, 20, 30};

    FILE *fp = fopen("numbers.bin", "wb");

    if (fp == NULL)
    {
        perror("numbers.bin");
        return 1;
    }

    size_t written = fwrite(numbers, sizeof numbers[0],
                            3, fp);

    if (written != 3)
    {
        perror("Error writing file");
        fclose(fp);
        return 1;
    }

    fclose(fp);
    printf("Binary data written\n");

    return 0;
}
```

Console output

```
Binary data written
```

`fwrite()` writes three elements, each of size `sizeof numbers[0]`, from the memory area beginning at `numbers`.

### B. Reading a binary file using `fread()`

```

#include <stdio.h>

int main(void)
{
    int numbers[3];

    FILE *fp = fopen("numbers.bin", "rb");

    if (fp == NULL)
    {
        perror("numbers.bin");
        return 1;
    }

    size_t count = fread(numbers, sizeof numbers[0],
                         3, fp);

    fclose(fp);

    if (count != 3)
    {
        fprintf(stderr, "Could not read 3 integers\n");
        return 1;
    }

    for (int i = 0; i < 3; i++)
        printf("%d ", numbers[i]);

    printf("\n");
    return 0;
}
```

If the file was written by the previous example on the same compatible implementation, the output is:

```
10 20 30
```

Important limitation: Writing raw integers with `fwrite()` is convenient, but the representation of integer values, byte order, and other representation details can vary between systems. Raw binary files like this are not automatically portable across different platforms or compiler environments.

### Text vs binary comparison

|Feature|Text file|Binary file|
|---|---|---|
|Data representation|Characters representing text|Bytes representing data|
|Human readability|Usually readable in a text editor|Often not directly readable|
|Common functions|`fprintf`, `fscanf`, `fgets`, `fputs`|`fread`, `fwrite`|
|Common modes|`"r"`, `"w"`, `"a"`|`"rb"`, `"wb"`, `"ab"`|
|Conversion|Formatting/parsing may occur|Data is transferred as bytes|
|Portability|Often easier for simple textual data|May depend on data representation and format|

## 10. Important file-handling functions

|Function|Purpose|
|---|---|
|`fopen()`|Opens a file|
|`fclose()`|Closes a file|
|`fprintf()`|Writes formatted text|
|`fscanf()`|Reads formatted input|
|`fputs()`|Writes a string|
|`fgets()`|Reads a line or part of a line|
|`fputc()`|Writes one character|
|`fgetc()`|Reads one character|
|`fwrite()`|Writes blocks of bytes|
|`fread()`|Reads blocks of bytes|
|`fseek()`|Moves the file position indicator|
|`ftell()`|Reports the current file position|
|`rewind()`|Returns the file position to the beginning|
|`feof()`|Tests whether the end-of-file indicator is set|
|`ferror()`|Tests whether the error indicator is set|
|`remove()`|Removes a file|
|`rename()`|Renames a file|

### Common exam trap: `EOF`

`EOF` is a special negative integer constant used to indicate end-of-file or an input failure by functions such as `fgetc()`. It is not simply the character `'0'` or the null character `'\0'`.

Also, checking `feof(fp)` before attempting a read is not the right general pattern. Instead, test the read function's return value, then use `feof()` or `ferror()` if you need to distinguish why reading stopped.