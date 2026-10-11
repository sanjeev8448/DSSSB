## 1. Text files

A text file stores data as characters that can be decoded using a character encoding, such as UTF-8.

Examples include `.txt`, `.py`, `.csv`, and `.html` files.

Suppose `sample.txt` contains:

```
Hello Python
Welcome to DSSSB
```

Python can read it like this:

```
with open("sample.txt", "r", encoding="utf-8") as file:    content = file.read()print(content)
```

Output, assuming the file contains the two lines shown above:

```
Hello Python
Welcome to DSSSB
```

Important points:

- Text mode is the default mode when opening a file.
    
- Python decodes the file's bytes into strings using the specified encoding.
    
- UTF-8 is a common choice for text files.
    
- `with` automatically closes the file when the block exits, even if an exception occurs.
    

## 2. Binary files

Binary mode reads and writes raw bytes without decoding them into text.

Examples include images (`.jpg`, `.png`), audio files, PDFs, and compiled executables.

```
with open("image.png", "rb") as file:    data = file.read()print(type(data))print(len(data))
```

The output type is:

```
<class 'bytes'>
```

The actual length depends on the contents of `image.png`.

### Text vs binary files

|Feature|Text mode|Binary mode|
|---|---|---|
|Mode examples|`"r"`, `"w"`, `"a"`|`"rb"`, `"wb"`, `"ab"`|
|Data read|`str`|`bytes`|
|Encoding/decoding|Performed|Not performed|
|Typical use|Text, source files, logs|Images, PDFs, audio, arbitrary bytes|
|`read()` result|String|Bytes|
|`write()` expects|String|Bytes-like data|

Exam trap: You cannot write a Python string directly to a binary file, or bytes directly to a text file, using the ordinary `write()` operation. The data types must match the file mode.

## 3. `open()` function

The `open()` function opens a file and returns a file object.

Syntax:

```
open(file, mode="r", encoding=None)
```

This is a simplified representation of its parameters.

Example:

```
file = open("sample.txt", "r", encoding="utf-8")content = file.read()print(content)file.close()
```

Here, the file is opened in read-text mode and closed manually.

### Recommended approach: `with open()`

```
with open("sample.txt", "r", encoding="utf-8") as file:    content = file.read()    print(content)# The file is closed automatically here.
```

Using `with` is generally safer than manually calling `close()` because it ensures cleanup when the block is exited.

### What happens when a file cannot be opened?

Opening a missing file in `"r"` mode normally raises `FileNotFoundError`.

```
try:    with open("missing.txt", "r", encoding="utf-8") as file:        print(file.read())except FileNotFoundError:    print("File not found")
```

Output, if the file does not exist:

```
File not found
```

Exam trap: `"r"` does not create a missing file. `"w"` can create one, but it truncates an existing file.

## 4. File modes

A file mode specifies how a file should be opened: for reading, writing, appending, or combinations of these operations.

### 4.1 Main file modes

|Mode|Purpose|If the file exists|If it does not exist|
|---|---|---|---|
|`"r"`|Read|Reads existing file|Raises `FileNotFoundError`|
|`"w"`|Write|Truncates existing file|Creates file|
|`"a"`|Append|Writes at the end|Creates file|
|`"x"`|Exclusive creation|Raises `FileExistsError`|Creates file|
|`"r+"`|Read and write|Opens without truncating|Raises `FileNotFoundError`|
|`"w+"`|Read and write|Truncates existing file|Creates file|
|`"a+"`|Read and append|Writes at the end|Creates file|

### 4.2 Text and binary mode modifiers

|Modifier|Meaning|Example|
|---|---|---|
|`"t"`|Text mode; the default|`"rt"`, `"wt"`|
|`"b"`|Binary mode|`"rb"`, `"wb"`|
|`"+"`|Enables both reading and writing|`"r+"`, `"w+"`, `"a+"`|

These modifiers can be combined, such as `"rb+"` or `"wb+"`.

### 4.3 Important examples

Mode `"r"` — reading

```
with open("data.txt", "r", encoding="utf-8") as f:    print(f.read())
```

The file must already exist.

Mode `"w"` — writing

```
with open("data.txt", "w", encoding="utf-8") as f:    f.write("Hello")print("Written")
```

Output:

```
Written
```

The file now contains `Hello`. If it previously contained other text, that content was truncated.

Mode `"a"` — appending

```
with open("data.txt", "a", encoding="utf-8") as f:    f.write("\nPython")print("Appended")
```

Output:

```
Appended
```

The text is added at the end of the file. The leading newline moves `Python` onto a new line when the existing file does not already end with a newline.

Mode `"x"` — exclusive creation

```
with open("newfile.txt", "x", encoding="utf-8") as f:    f.write("First creation")
```

This creates the file only if it does not already exist. If the file exists, Python raises `FileExistsError`.

Exam traps:

- `"w"` destroys the previous contents when opening an existing file.
    
- `"a"` preserves existing content and appends new content.
    
- `"x"` fails if the target already exists.
    
- `"r+"` does not truncate an existing file, but `"w+"` does.
    
- Binary modes work with bytes rather than strings.
    

## 5. `read()`

`read()` reads data from the current file position.

Syntax:

```
file.read(size=-1)
```

If `size` is omitted or negative, it reads the remaining content. A non-negative `size` limits how much is read.

Assume `sample.txt` contains:

```
Python
DSSSB
```

Example:

```
with open("sample.txt", "r", encoding="utf-8") as f:    print(repr(f.read(3)))    print(repr(f.read()))
```

Output:

```
'Pyt'
'hon\nDSSSB'
```

The first call reads three characters. The second reads everything remaining.

`repr()` displays newline characters as `\n`, making the returned string's contents easier to inspect.

### Reading a file repeatedly

```
with open("sample.txt", "r", encoding="utf-8") as f:    print(repr(f.read()))    print(repr(f.read()))
```

Output:

```
'Python\nDSSSB'
''
```

The second call returns an empty string because the file pointer has reached the end of the file.

Exam trap: `read()` does not automatically reset the file pointer to the beginning.

## 6. `readline()`

`readline()` reads a single line from the current file position, generally including its terminating newline character if one is present.

Assume `sample.txt` contains:

```
Apple
Banana
Mango
```

```
with open("sample.txt", "r", encoding="utf-8") as f:    print(repr(f.readline()))    print(repr(f.readline()))    print(repr(f.readline()))    print(repr(f.readline()))
```

Output:

```
'Apple\n'
'Banana\n'
'Mango\n'
''
```

The fourth call returns an empty string because the end of the file has been reached.

Important points:

- One call reads one line.
    
- The newline is included when it exists.
    
- The final line may not end with a newline.
    
- At the end of the file, `readline()` returns `''`.
    

### Limiting the number of characters

`readline(size)` can limit the number of characters returned.

```
# Suppose the file begins with "Python\n"with open("sample.txt", "r", encoding="utf-8") as f:    print(repr(f.readline(3)))
```

Output:

```
'Pyt'
```

## 7. `readlines()`

`readlines()` reads the remaining lines and returns them as a list of strings.

Assume `sample.txt` contains:

```
Apple
Banana
Mango
```

```
with open("sample.txt", "r", encoding="utf-8") as f:    lines = f.readlines()print(lines)print(type(lines))print(len(lines))
```

Output:

```
['Apple\n', 'Banana\n', 'Mango\n']
<class 'list'>
3
```

Newline characters remain in the strings when they are present in the file.

### `read()` vs `readline()` vs `readlines()`

|Method|What it reads|Return type|
|---|---|---|
|`read()`|Remaining content, or a specified number of characters|`str` in text mode|
|`readline()`|One line|`str` in text mode|
|`readlines()`|Remaining lines|`list` of strings in text mode|

Important exam trap: `readlines()` returns a list, not one combined string.

For large files, iterating through the file directly is usually more memory-efficient than loading every line with `readlines()`.

```
with open("sample.txt", "r", encoding="utf-8") as f:    for line in f:        print(line, end="")
```

This reads the file one line at a time.

## 8. `write()`

`write()` writes a string to a text file or bytes to a binary file. It returns the number of characters written in text mode, or the number of bytes written in binary mode.

Example:

```
with open("output.txt", "w", encoding="utf-8") as f:    count = f.write("Hello Python")print(count)
```

Output:

```
12
```

The string `Hello Python` contains 12 characters, including the space.

### Does `write()` add a newline?

No. `write()` does not automatically append a newline.

```
with open("output.txt", "w", encoding="utf-8") as f:    f.write("Hello")    f.write("Python")with open("output.txt", "r", encoding="utf-8") as f:    print(repr(f.read()))
```

Output:

```
'HelloPython'
```

To add a newline, include `\n`:

```
f.write("Hello\n")f.write("Python\n")
```

### Writing binary data

```
with open("data.bin", "wb") as f:    count = f.write(b"ABC")print(count)
```

Output:

```
3
```

The `b` prefix creates a bytes literal, which is appropriate for binary mode.

Exam trap: `f.write("ABC")` in binary mode raises a `TypeError`. Use `f.write(b"ABC")` instead.

## 9. `writelines()`

`writelines()` writes an iterable of strings to a file. It does not automatically insert newline characters between elements.

```
lines = ["Apple\n", "Banana\n", "Mango\n"]with open("fruits.txt", "w", encoding="utf-8") as f:    f.writelines(lines)with open("fruits.txt", "r", encoding="utf-8") as f:    print(repr(f.read()))
```

Output:

```
'Apple\nBanana\nMango\n'
```

Notice that newline characters were included in the original strings.

### What if no newlines are supplied?

```
with open("output.txt", "w", encoding="utf-8") as f:    f.writelines(["Apple", "Banana", "Mango"])with open("output.txt", "r", encoding="utf-8") as f:    print(f.read())
```

Output:

```
AppleBananaMango
```

### `write()` vs `writelines()`

|Feature|`write()`|`writelines()`|
|---|---|---|
|Input|A string in text mode|Iterable of strings|
|Adds newlines automatically?|No|No|
|Return value|Number of characters written|`None`|
|Typical use|Write one string|Write several strings|

Exam trap: `writelines()` is not equivalent to printing each item on a separate line.

## 10. `tell()`

`tell()` returns the current file position.

Think of a file as a sequence of characters or bytes and the file pointer as the current reading or writing position.

```
# Assume sample.txt contains "Python"with open("sample.txt", "r", encoding="utf-8") as f:    print(f.tell())    print(f.read(2))    print(f.tell())    print(f.read(2))    print(f.tell())
```

Output for this ASCII-only file:

```
0
Py
2
th
4
```

Explanation:

1. The initial position is `0`.
    
2. Reading two characters advances the position.
    
3. After another two characters, the position advances again.
    

Important: In text mode, `tell()` returns a position value suitable for restoring the position using `seek()`. It is not necessarily a raw byte offset, especially with multibyte encodings.

## 11. `seek()`

`seek()` changes the current file position so that subsequent reading or writing starts from a specified location.

Syntax:

```
file.seek(offset, whence=0)
```

- `offset`: the position adjustment.
    
- `whence=0`: measure from the beginning.
    
- `whence=1`: measure from the current position.
    
- `whence=2`: measure from the end.
    

The full `whence` options are primarily useful in binary files. Text files have restrictions: use `seek(0)` to return to the start, or restore a position previously returned by `tell()`.

### Example 1: Move back to the beginning

```
# Assume sample.txt contains "Python"with open("sample.txt", "r", encoding="utf-8") as f:    print(f.read(3))    f.seek(0)    print(f.read(3))
```

Output:

```
Pyt
Pyt
```

After the first read, `seek(0)` resets the position to the beginning.

### Example 2: Seeking in binary mode

Binary-mode seeks support byte offsets. Suppose `data.bin` contains the three bytes representing `ABC`.

```
with open("data.bin", "rb") as f:    print(f.read(1))    print(f.tell())    f.seek(2)    print(f.read(1))
```

Output:

```
b'A'
1
b'C'
```

Here, `seek(2)` moves to byte offset `2`, where `C` is stored.

### `seek()` vs `tell()`

|Method|Purpose|
|---|---|
|`tell()`|Reports the current position|
|`seek()`|Changes the current position|

Exam trap: `read()` advances the file position. Calling `seek(0)` lets you read from the start again.

## 12. CSV file handling

CSV stands for Comma-Separated Values. It is a text-based format used to store tabular data, with rows and fields separated according to CSV rules.

Example `students.csv`:

```
name,age,marks
Amit,22,85
Neha,21,92
Ravi,23,78
```

Python provides a built-in `csv` module for reading and writing CSV files.

### 12.1 Reading CSV using `csv.reader()`

```
import csvwith open("students.csv", "r", newline="", encoding="utf-8") as f:    reader = csv.reader(f)    for row in reader:        print(row)
```

Output, for the sample file above:

```
['name', 'age', 'marks']
['Amit', '22', '85']
['Neha', '21', '92']
['Ravi', '23', '78']
```

Each row is returned as a list of strings.

Exam trap: CSV fields are generally strings when returned by `csv.reader()`. Convert numeric fields explicitly when doing arithmetic.

### 12.2 Reading CSV as dictionaries

`csv.DictReader()` maps each row to a dictionary using the header row as field names.

```
import csvwith open("students.csv", "r", newline="", encoding="utf-8") as f:    reader = csv.DictReader(f)    for row in reader:        print(row["name"], row["marks"])
```

Output:

```
Amit 85
Neha 92
Ravi 78
```

In this example, the header row is used to identify the columns and is not returned as an ordinary data row.

### 12.3 Writing CSV using `csv.writer()`

```
import csvrows = [    ["name", "age"],    ["Amit", 22],    ["Neha", 21]]with open("output.csv", "w", newline="", encoding="utf-8") as f:    writer = csv.writer(f)    writer.writerows(rows)
```

The generated file contains:

```
name,age
Amit,22
Neha,21
```

Use `writerow()` to write one row and `writerows()` to write multiple rows.

### 12.4 Important CSV facts

|Function or setting|Purpose|
|---|---|
|`csv.reader(f)`|Reads rows as lists|
|`csv.DictReader(f)`|Reads data rows as dictionaries|
|`csv.writer(f)`|Writes rows|
|`writerow(row)`|Writes one row|
|`writerows(rows)`|Writes multiple rows|
|`newline=""`|Recommended when opening CSV files|
|`encoding="utf-8"`|Specifies the text encoding|

Why use `newline=""`? It allows the CSV module to handle newline conventions itself and helps prevent extra blank rows on some platforms when writing CSV files.

Exam trap: CSV is a text format, not a binary format, even though computers ultimately store file contents as bytes.

## Final revision sheet

|Topic|Remember|
|---|---|
|Text file|Reads and writes text as `str`|
|Binary file|Reads and writes raw data as `bytes`|
|CSV file|Use the built-in `csv` module|
|`open()`|Opens a file and returns a file object|
|`read()`|Reads content; returns `str` in text mode|
|`readline()`|Reads one line|
|`readlines()`|Returns a list of lines|
|`write()`|Writes one string or bytes object|
|`writelines()`|Writes an iterable of strings without adding newlines|
|`tell()`|Returns the current file position|
|`seek()`|Changes the file position|
|`"r"`|Read existing file|
|`"w"`|Create or truncate|
|`"a"`|Append or create|
|`"x"`|Create only if absent|
|`"+"`|Enable reading and writing|
|`"b"` / `"t"`|Binary / text mode|

Highest-priority revision: Learn the `"r"`, `"w"`, `"a"`, and `"x"` modes first; then compare `read()`, `readline()`, and `readlines()`. Finally, practise `seek()`/`tell()` and the distinction between CSV rows returned by `reader()` and `DictReader()`.