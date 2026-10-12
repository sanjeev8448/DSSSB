# 1. What is a file?

A file is a named collection of related information stored on secondary storage, such as an SSD or hard disk.

A file may contain text, images, programs, audio, video or other data.

Examples:

- `notes.txt` — text file
    
- `photo.jpg` — image file
    
- `program.exe` — executable file on Windows
    
- `report.pdf` — document
    
- `data.csv` — tabular data
    

The operating system provides mechanisms to create, read, write, rename, organize and delete files.

## Common file attributes

A file's metadata may include:

|Attribute|Meaning|
|---|---|
|Name|Human-readable file name|
|Identifier|Internal identifier used by the file system|
|Type|File type or format|
|Location|Information used to locate the file's stored data|
|Size|Amount of data in the file|
|Protection|Access permissions|
|Timestamps|Creation, modification or access times, where supported|
|Owner|User or account associated with the file|

Not all file systems store or expose every attribute in the same way.

## Common file operations

|Operation|Purpose|
|---|---|
|Create|Create a new file|
|Open|Open a file for access|
|Read|Retrieve file data|
|Write|Store or modify file data|
|Append|Add data to the end|
|Seek|Change the current access position|
|Close|Close an open file handle|
|Rename|Change the file name|
|Delete|Remove the file-system entry and eventually reclaim its storage, according to file-system behavior|

Exam trap: A file name is not necessarily the file's physical storage location. The file system maintains metadata and structures used to locate its contents.

# 2. Directory

A directory is a file-system structure used to organize files and, in hierarchical file systems, other directories.

Directories help users and applications locate files using paths.

Example:

```
College/
├── Notes/
│   ├── OS.txt
│   └── DBMS.txt
├── Programs/
│   └── main.c
└── Results/
    └── marks.csv
```

Here, `College` is the top-level directory shown, with subdirectories `Notes`, `Programs` and `Results`.

## Directory operations

Common operations include:

- Create a directory.
    
- Remove a directory.
    
- Search for a file.
    
- List directory contents.
    
- Rename a file or directory.
    
- Traverse the directory hierarchy.
    

## Directory structures

### A. Single-level directory

All files are kept in one directory.

Directory

A.txt

B.txt

C.txt

Advantages: Simple to implement.

Disadvantages: File-name conflicts and poor organization when many users or files exist.

### B. Two-level directory

Each user has a separate directory under a master directory.

```
Master Directory
├── User A
│   ├── A.txt
│   └── B.txt
└── User B
    ├── A.txt
    └── C.txt
```

Different users can have files with the same name because the files reside in separate user directories.

### C. Tree-structured directory

Directories may contain subdirectories, forming a hierarchy.

```
Root
├── Home
│   ├── User1
│   └── User2
└── System
    ├── Config
    └── Logs
```

This structure supports hierarchical grouping and is common in modern operating systems.

### D. Acyclic-graph directory

An acyclic-graph directory permits shared files or subdirectories while preventing cycles in the directory graph.

For example, two users may access a shared project directory without needing separate physical copies of every file.

Exam point: Sharing can create complications when deleting files or maintaining references, so reference-management rules are important.

### E. General graph directory

A general graph directory permits cycles. Searching and deletion can be more complex because the file system must handle cycles and potentially revisit directory entries.

### Directory structure comparison

|Structure|Main feature|Common limitation|
|---|---|---|
|Single-level|One directory for all files|Name conflicts, poor organization|
|Two-level|Separate directory per user|Limited nesting|
|Tree|Hierarchical structure|Sharing can require additional mechanisms|
|Acyclic graph|Shared files/directories without cycles|Reference and deletion management|
|General graph|Cycles may exist|Traversal and cycle management are harder|

## Paths

A path identifies a file or directory within the file system.

- Absolute path: Starts from the file system's root or root context.
    
- Relative path: Interpreted relative to the current working directory.
    

Examples on a Unix-like system:

```
/home/student/Notes/OS.txt
```

This is an example of an absolute path.

```
Notes/OS.txt
```

This may be a relative path, depending on the current directory.

Exam trap: The same relative path can refer to different files when the current working directory changes.

# 3. File allocation methods — Very important

File allocation methods determine how a file's data blocks are assigned to storage blocks on a disk.

The three classical methods are:

1. Contiguous allocation
    
2. Linked allocation
    
3. Indexed allocation
    

## A. Contiguous allocation

In contiguous allocation, the file occupies a sequence of consecutive disk blocks.

For example, a file may occupy blocks 10, 11, 12 and 13.

### Contiguous allocation

8

Free/Other

9

Free/Other

10

File A

11

File A

12

File A

13

File A

File A occupies four consecutive blocks, starting at block 10.

The file system can record the starting block and the file's length.

### Advantages

- Fast sequential access.
    
- Efficient direct access because the block location can be calculated.
    
- Low metadata overhead for locating the allocated extent.
    

### Disadvantages

- Can suffer from external fragmentation.
    
- Finding a sufficiently large contiguous region can be difficult.
    
- Growing a file may be difficult if the following blocks are already occupied.
    
- Files may require relocation or additional extents to grow.
    

### Address calculation

For a zero-based logical block number \(i\):

\[ \boxed{\text{Physical block}=\text{Starting block}+i} \]

Example: A file starts at block 10. Logical block 3 is stored at:

\[ 10+3=\boxed{13} \]

Exam trap: Contiguous allocation supports efficient direct access, but external fragmentation and file growth are major concerns.

## B. Linked allocation

In linked allocation, a file's blocks can be located anywhere on the disk. Each block stores a pointer to the next block, or the file system stores equivalent linking information.

Example:

```
Block 4 → Block 11 → Block 7 → Block 19 → EOF
```

The blocks are not physically consecutive.

### Linked allocation

Block 4

Block 11

Block 7

Block 19

Each block points to the next block in the file.

### Advantages

- Avoids the need to allocate one contiguous region.
    
- File growth is relatively straightforward when free blocks are available.
    
- External fragmentation from the requirement for a large contiguous file extent is avoided.
    

### Disadvantages

- Direct access is inefficient because the chain may need to be traversed.
    
- Pointer information occupies storage.
    
- A corrupted pointer can make subsequent blocks difficult to locate.
    
- Blocks may be physically scattered, causing extra disk seeks on traditional rotating disks.
    

### FAT (File Allocation Table)

A related technique is the File Allocation Table (FAT) approach. Instead of storing each next-block pointer inside the data block itself, links are maintained in a separate table.

Exam trap: Linked allocation is suitable for sequential traversal, but random access is less efficient than in contiguous allocation.

## C. Indexed allocation

In indexed allocation, the file system maintains an index block or equivalent index structure containing pointers to the file's data blocks.

Example:

```
Index block:
  Entry 0 → Block 4
  Entry 1 → Block 11
  Entry 2 → Block 7
  Entry 3 → Block 19
```

The file's data blocks can be scattered across the disk. The index provides a mapping from logical block positions to physical blocks.

Index block

Contains data-block pointers

Block 4

Block 11

Block 7

Block 19

The index maps logical file positions to data blocks.

### Advantages

- Supports efficient direct access to logical file blocks.
    
- Does not require one contiguous disk region.
    
- Avoids external fragmentation caused by requiring a file to occupy one contiguous extent.
    

### Disadvantages

- Index structures consume storage.
    
- Small files may incur index overhead.
    
- Large files may need multilevel indexes or other mechanisms if one index block cannot hold all pointers.
    

### Indexed vs linked allocation

|Feature|Linked allocation|Indexed allocation|
|---|---|---|
|How blocks are located|Follow pointers through a chain|Follow pointers in an index structure|
|Direct access|Generally inefficient|Generally efficient|
|Extra metadata|Links between blocks|Index block or equivalent structure|
|External fragmentation|Avoids contiguous-extent requirement|Avoids contiguous-extent requirement|
|Main limitation|Chain traversal and pointer reliability|Index overhead and index capacity|

## D. Comparison of the three methods

|Feature|Contiguous|Linked|Indexed|
|---|---|---|---|
|Disk blocks consecutive?|Yes, within the allocated extent|Not required|Not required|
|Sequential access|Very efficient|Efficient for traversal|Supported|
|Direct access|Efficient|Generally poor|Efficient through index|
|External fragmentation from allocation requirement|Yes|No|No|
|Growth|Can be difficult|Relatively easy|Relatively easy, subject to index capacity|
|Extra pointer/index overhead|Low|Links required|Index storage required|

Memory trick:

- Contiguous = consecutive blocks.
    
- Linked = pointers connect blocks.
    
- Indexed = an index points to blocks.
    

# 4. File permissions

File permissions determine which users or groups can perform particular operations on files and directories.

They are part of the operating system's protection and access-control mechanisms.

## A. Read, write and execute permissions

In Unix-like systems, the classical permission symbols are:

|Permission|Symbol|Regular file|Directory|
|---|---|---|---|
|Read|`r`|Read file contents|List directory entries|
|Write|`w`|Modify file contents|Create, delete or rename entries, subject to other rules|
|Execute|`x`|Execute the file if it is executable and otherwise permitted|Search/traverse the directory|

Important: Directory permissions have different meanings from regular-file permissions. Write permission on a directory does not, by itself, necessarily mean that a user can read every file inside it.

## B. User, group and others

Traditional Unix permission bits apply to three classes:

- User (u): The file's owner.
    
- Group (g): Users in the file's relevant group.
    
- Others (o): Other users not covered by the owner or group class.
    

Example:

```
-rwxr-xr--
```

The leading `-` indicates a regular file. The permissions are:

|Class|Permission string|Meaning|
|---|---|---|
|User|`rwx`|Read, write and execute|
|Group|`r-x`|Read and execute|
|Others|`r--`|Read only|

The file owner can read, modify and execute the file. Group members can read and execute it, while others can only read it, subject to other system controls.

## C. Numeric permissions (octal notation)

Unix-like systems commonly represent the `r`, `w`, `x` bits numerically:

|Permission|Value|
|---|---|
|Read (`r`)|4|
|Write (`w`)|2|
|Execute (`x`)|1|
|No permission|0|

The values are added for each user class.

### Example: `chmod 754 file.txt`

- User: \(4+2+1=7\) → `rwx`
    
- Group: \(4+0+1=5\) → `r-x`
    
- Others: \(4+0+0=4\) → `r--`
    

Therefore, `754` means:

```
rwxr-xr--
```

### Common numeric permissions

|Numeric mode|Symbolic permissions|Meaning|
|---|---|---|
|`777`|`rwxrwxrwx`|All classes have all three basic permissions|
|`755`|`rwxr-xr-x`|Owner has all; group and others can read and execute|
|`644`|`rw-r--r--`|Owner can read/write; group and others can read|
|`700`|`rwx------`|Owner only has the three basic permissions|
|`600`|`rw-------`|Owner can read/write; group and others have none|

### Command example

```
chmod 644 notes.txt
```

This sets the basic permission bits to `rw-r--r--`, subject to the OS and file-system permissions model.

Exam trap: The digits correspond to owner, group and others, in that order. For `754`, the first digit is 7, the second is 5 and the third is 4.

These examples describe traditional Unix-style permission bits. Windows commonly uses access-control lists (ACLs), and more advanced Unix-like file systems may also support ACLs and other security controls.

# 5. File allocation vs file permissions

Do not confuse these topics.

|File allocation|File permissions|
|---|---|
|Determines how file data blocks are stored and located|Determines who can access or modify a file|
|Examples: contiguous, linked, indexed|Examples: read, write, execute|
|Primarily concerns storage organization|Primarily concerns access control and protection|

The file system uses allocation metadata to locate data, while permissions and other security checks govern access.

# 6. File access methods — useful related topic

Three classical file access methods often appear alongside allocation questions.

|Access method|Meaning|Example|
|---|---|---|
|Sequential access|Records are processed in order|Reading a text file from beginning to end|
|Direct / random access|A particular block or position can be accessed directly|Accessing a specific block in a data file|
|Indexed access|An index helps locate records or blocks|Finding a record using an index key|

These are access methods, not allocation methods. For example, indexed allocation describes how blocks are mapped to a file, while indexed access describes how records are located using an index.

# 7. Important exam traps

| Statement                                                                               | Correct answer |
| --------------------------------------------------------------------------------------- | -------------- |
| Contiguous allocation stores file blocks consecutively.                                 | True           |
| Linked allocation requires all file blocks to be adjacent.                              | False          |
| Indexed allocation uses an index structure containing block pointers.                   | True           |
| Contiguous allocation supports efficient direct access.                                 | True           |
| Linked allocation is generally efficient for random block access.                       | False          |
| Paging and file allocation refer to exactly the same mechanism.                         | False          |
| A directory organizes file-system entries.                                              | True           |
| `rwx` represents read, write and execute permissions.                                   | True           |
| The permission mode `754` means `rwxr-xr--`.                                            | True           |
| The execute permission on a directory enables traversal/search, subject to other rules. | True           |
| File allocation determines who can read a file.                                         | False          |
| File permissions determine where disk blocks are allocated.                             | False          |
## Last-minute memory trick

- File: Named collection of stored information.
    
- Directory: Organizes files and other directories.
    
- Contiguous allocation: Consecutive blocks.
    
- Linked allocation: Blocks connected through pointers.
    
- Indexed allocation: Index structure points to data blocks.
    
- Permissions: Control access to files and directories.
    
- `rwx`: Read, write and execute.
    
- `754`: `rwxr-xr--`.
    
- Sequential access: Process data in order.
    
- Direct access: Locate a particular block or position.
    

For DSSSB, make sure you can differentiate contiguous vs linked vs indexed allocation without hesitation, and practise converting Unix permission numbers such as `755`, `644` and `700` into `rwx` notation.