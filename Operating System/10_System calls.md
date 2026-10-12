# 1. What is a system call?

A system call is a controlled interface through which a user program requests a service from the operating system kernel.

Applications often need to perform privileged or OS-managed operations, such as creating processes, accessing files, requesting memory mappings, or communicating with devices. They use system calls or APIs that ultimately invoke the appropriate operating-system services.

### Example

Suppose a program wants to read a file from storage.

1. The program requests that a file be opened.
    
2. The OS checks the request and access permissions.
    
3. The program requests data from the file.
    
4. The OS manages the operation and returns data or an error.
    

### User program

Requests an OS service

### System-call interface

Controlled request to the kernel

### OS kernel

Checks and performs the requested operation

Managed resource

Process, file, memory or I/O device

The system-call mechanism normally involves a controlled transition from user mode to kernel mode. The kernel validates the request, performs or coordinates the service, and returns a result.

Exam trap: A system call is not the same as an ordinary function call. An ordinary function call usually transfers control within a program; a system call requests an OS service through a controlled interface.

# 2. Types of system calls

Your syllabus lists four important categories:

1. Process control
    
2. File management
    
3. Memory management
    
4. Device / I/O management
    

Textbooks may list additional categories such as information maintenance, communication and protection.

## A. Process-control system calls

Process-control system calls help create, execute, manage and terminate processes.

Typical operations include:

- Creating a process.
    
- Executing a program.
    
- Waiting for a child process.
    
- Terminating a process.
    
- Obtaining process information.
    
- Sending signals or controlling execution, depending on the OS.
    

### Common Unix/POSIX examples

|System call / API|Purpose|
|---|---|
|`fork()`|Creates a child process in Unix-like systems|
|`execve()`|Replaces the calling process's program image with another program|
|`wait()` / `waitpid()`|Waits for a child process's state change, commonly its termination|
|`_exit()`|Terminates the calling process|
|`getpid()`|Returns the calling process's ID|
|`kill()`|Sends a signal to a process; it does not necessarily terminate it|

These names are examples from Unix-like systems, not universal names used by every operating system.

### Example: `fork()` and `exec()`

In Unix-like operating systems, a common pattern is to create a child process using `fork()` and then have the child execute another program using an `exec`-family function.

```

#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main(void) {
    pid_t pid = fork();

    if (pid < 0) {
        perror("fork");
        return 1;
    }

    if (pid == 0) {
        /* Child process */
        execlp("ls", "ls", "-l", (char *)NULL);

        /* Reached only if exec fails */
        perror("execlp");
        _exit(1);
    }

    /* Parent process */
    if (waitpid(pid, NULL, 0) < 0) {
        perror("waitpid");
        return 1;
    }

    puts("Child process finished.");
    return 0;
}
```

Concepts to remember:

- `fork()` creates a child process.
    
- `exec` replaces the current process's program image; it does not ordinarily create a new process by itself.
    
- `waitpid()` lets the parent wait for the child.
    
- `getpid()` returns a process ID.
    

Exam trap: Do not confuse process creation with program execution. In the traditional Unix pattern, `fork()` creates the process and `exec()` loads the new program image.

## B. File-management system calls

File-management system calls allow programs to create, open, read, write, reposition and close files.

### Common Unix/POSIX examples

|System call|Purpose|
|---|---|
|`open()`|Opens a file and returns a file descriptor|
|`creat()`|Traditionally creates a file or truncates an existing file|
|`read()`|Reads data from a file descriptor|
|`write()`|Writes data to a file descriptor|
|`close()`|Closes a file descriptor|
|`lseek()`|Changes the file offset for a seekable file|
|`unlink()`|Removes a file-system name/link|
|`stat()`|Retrieves file metadata|

### Example: Open, read and close a file

```

#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int main(void) {
    char buffer[101];

    int fd = open("notes.txt", O_RDONLY);
    if (fd == -1) {
        perror("open");
        return 1;
    }

    ssize_t n = read(fd, buffer, 100);
    if (n == -1) {
        perror("read");
        close(fd);
        return 1;
    }

    buffer[n] = '\0';
    printf("%s", buffer);

    if (close(fd) == -1) {
        perror("close");
        return 1;
    }

    return 0;
}
```

This example reads up to 100 bytes from `notes.txt`. It is a simple demonstration, not a complete general-purpose file-copy or binary-file implementation.

### Important concepts

- `open()` commonly returns a file descriptor, a small integer representing an open file.
    
- `read()` can return fewer bytes than requested; it does not guarantee that the entire buffer will be filled in one call.
    
- `write()` can also perform a partial write, so robust programs may need to loop.
    
- `close()` releases the descriptor.
    
- `lseek()` changes the current file offset for files that support seeking.
    
- `unlink()` removes a name from the file system; the underlying data may remain accessible through open descriptors until they are closed, subject to file-system semantics.
    

Exam trap: `open()` opens a file and returns a file descriptor; it does not return the file's contents.

## C. Memory-management system calls

Memory-management system calls or OS interfaces request changes to a process's address space or memory mappings.

Common operations include:

- Allocating or mapping memory.
    
- Releasing memory mappings.
    
- Changing memory protections.
    
- Mapping files into a process's address space.
    

### Common Unix/POSIX examples

|System call / interface|Purpose|
|---|---|
|`mmap()`|Creates a memory mapping|
|`munmap()`|Removes a memory mapping|
|`mprotect()`|Changes protection on memory pages|
|`brk()` / `sbrk()`|Historically used to adjust the process data-segment break; not preferred for general modern allocation|

### Example: Memory mapping

```

#include <sys/mman.h>
#include <unistd.h>
#include <stdio.h>

int main(void) {
    long page_size = sysconf(_SC_PAGESIZE);
    if (page_size <= 0) {
        perror("sysconf");
        return 1;
    }

    size_t size = (size_t)page_size;

    void *ptr = mmap(
        NULL,
        size,
        PROT_READ | PROT_WRITE,
        MAP_PRIVATE | MAP_ANONYMOUS,
        -1,
        0
    );

    if (ptr == MAP_FAILED) {
        perror("mmap");
        return 1;
    }

    ((char *)ptr)[0] = 'A';

    printf("%c\n", ((char *)ptr)[0]);

    if (munmap(ptr, size) == -1) {
        perror("munmap");
        return 1;
    }

    return 0;
}
```

On a suitable Unix-like system that supports these flags, the program maps one page of private anonymous memory, writes `'A'`, prints it, and releases the mapping.

### Important distinctions

- `mmap()` creates a mapping; it does not necessarily mean that all underlying physical pages are immediately allocated.
    
- `munmap()` removes a mapping, making that range unavailable through that mapping.
    
- `mprotect()` changes access permissions for a mapped region.
    
- The C library function `malloc()` requests dynamic memory for a program. It is not itself a system call; an implementation may obtain memory through system calls or other mechanisms internally.
    

Exam trap: Memory allocation by an application library and an OS system call are different abstraction levels.

## D. Device / I/O system calls

I/O-related system calls allow applications to interact with devices or OS-managed input/output abstractions.

Examples include keyboard input, terminal output, storage access, and communication with devices.

### Common Unix/POSIX examples

|System call / interface|Purpose|
|---|---|
|`read()`|Reads data from a file descriptor, which can represent a device or other I/O endpoint|
|`write()`|Writes data to a file descriptor|
|`ioctl()`|Performs device- or descriptor-specific control operations|
|`open()`|Opens a device or other supported object|
|`close()`|Closes the associated descriptor|

### Example: Writing to standard output

```

#include <unistd.h>

int main(void) {
    const char message[] = "Hello from write()\n";

    ssize_t n = write(
        STDOUT_FILENO,
        message,
        sizeof(message) - 1
    );

    return n == (ssize_t)(sizeof(message) - 1) ? 0 : 1;
}
```

Here, `write()` sends the message to standard output. In a terminal, the text normally appears on the screen; if standard output has been redirected, the bytes may go elsewhere.

### What is `ioctl()`?

`ioctl()` performs control operations that are specific to a device or file descriptor, depending on the OS and driver.

For example, a program may use an appropriate `ioctl()` request to query or change certain device settings.

Exam trap: `ioctl()` is not one single universal device operation. The operation depends on the request code and the relevant device or subsystem.

# 3. Comparison of system-call categories

|Category|Main purpose|Common Unix/POSIX examples|
|---|---|---|
|Process control|Create, execute, wait for or terminate processes|`fork()`, `execve()`, `waitpid()`, `_exit()`|
|File management|Open, read, write and manage files|`open()`, `read()`, `write()`, `close()`, `lseek()`|
|Memory management|Manage address spaces and mappings|`mmap()`, `munmap()`, `mprotect()`|
|Device / I/O|Access devices and perform I/O control|`read()`, `write()`, `ioctl()`|

Notice that `read()` and `write()` can appear under both file management and I/O. These categories describe the purpose of the operation, not mutually exclusive sets of function names.

## 4. System call vs library function vs command

This distinction is useful for MCQs.

|Term|What it means|Example|
|---|---|---|
|System call|Controlled request for an OS kernel service|`read()` in the Unix/POSIX model|
|Library function|Function supplied by a software library|`printf()`, `malloc()`|
|Shell command|Command interpreted or launched through a shell|`ls`, `mkdir`, `cat`|
|API|Interface through which software requests functionality|POSIX API, Windows API|

A library function may invoke one or more system calls internally. For example, `printf()` formats text in the C library and may eventually use `write()` to send it to a file descriptor.

A shell command such as `mkdir` may invoke OS APIs or system calls to create a directory. The command itself is not necessarily a system call.

Exam traps:

- `fork()` → process creation in Unix-like systems.
    
- `execve()` → replaces the current program image.
    
- `open()` → opens a file and obtains a descriptor.
    
- `read()` → reads bytes.
    
- `write()` → writes bytes.
    
- `mmap()` → creates a memory mapping.
    
- `munmap()` → removes a memory mapping.
    
- `ioctl()` → device- or descriptor-specific control.
    
- `printf()` → library function, not a system call by itself.
    
- `malloc()` → library allocation function, not a system call by itself.
## Last-minute revision

- Process control: `fork()`, `execve()`, `waitpid()`, `_exit()`.
    
- File management: `open()`, `read()`, `write()`, `close()`, `lseek()`.
    
- Memory management: `mmap()`, `munmap()`, `mprotect()`.
    
- I/O: `read()`, `write()`, `ioctl()`.
    
- System call: Requests an OS service through a controlled interface.
    
- Library function: Can wrap or invoke system calls but is not automatically one.
    
- Most important distinction: `fork()` creates a child process; `execve()` replaces the program image of the calling process.