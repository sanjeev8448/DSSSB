## 1. What is a process?

A process is a program in execution. It is an active entity that includes the executing code and the resources and state needed to run it.

A process may contain:

- Program code (text section).
    
- Data section and variables.
    
- Stack for function calls and local variables.
    
- Heap for dynamically allocated memory.
    
- CPU state, including the program counter and registers.
    
- Operating-system resources, such as open files.
    

Example: When you open a browser, the operating system creates one or more processes to run its code. Opening another browser window does not necessarily create exactly one new process; that depends on the browser's design.

## 2. Program vs Process

A program is a passive set of instructions stored as a file. A process is an executing instance of a program.

|Program|Process|
|---|---|
|Passive entity|Active entity|
|Usually stored as an executable file|Exists while being executed or managed by the OS|
|Does not itself need a current CPU state|Has execution state, such as a program counter and registers|
|A file can be used to create processes|A process may execute program code|
|No PCB is needed merely for the file to exist|The OS maintains process-management information, typically represented by a PCB or equivalent structures|

### Example

Suppose `calculator.exe` is stored on your computer.

- The executable file is the program.
    
- When you launch it, the OS creates a process.
    
- Multiple running instances can be created from the same program.
    
- Each process may have its own execution state and memory, although some resources can be shared.
    

Exam memory trick: Program = instructions; Process = program in execution.

## 3. Process states

A process changes state as it is created, scheduled, executed, interrupted, or made to wait for an event.

The five classical process states are:

1. New — the process is being created.
    
2. Ready — it is prepared to execute and waiting for CPU time.
    
3. Running — its instructions are currently executing on a CPU.
    
4. Waiting / Blocked — it is waiting for an event, such as completion of I/O.
    
5. Terminated / Exit — it has finished or has been stopped.
    

### Process-state diagram

New

Ready

Running

Waiting / Blocked

Waits for an event

Terminated

Execution ends

Simplified diagram. Ready, Running and Waiting can transition between states according to scheduling and events.

### Important state transitions

|Transition|Reason|
|---|---|
|New → Ready|Process is admitted and becomes eligible to run|
|Ready → Running|CPU scheduler dispatches the process|
|Running → Ready|Process is preempted, for example when its time slice expires|
|Running → Waiting|Process waits for I/O or another event|
|Waiting → Ready|The awaited event completes|
|Running → Terminated|Process completes or is terminated|

Exam traps:

- A Ready process is waiting for CPU allocation.
    
- A Waiting/Blocked process is waiting for an event, not simply for CPU time.
    
- A process can move from Running to Ready when preempted.
    
- A process usually becomes Ready after the I/O event it was waiting for completes.
    

### Ready vs Waiting

|Ready state|Waiting / Blocked state|
|---|---|
|Can execute if assigned a CPU|Cannot proceed until a required event occurs|
|Waiting for CPU allocation|Waiting for I/O completion or another event|
|Example: ready to calculate but not yet scheduled|Example: waiting for disk data|

This difference is one of the most common OS MCQ topics.

## 4. Extended process states

Some operating-system models include additional states, such as suspended states.

### Ready Suspended

A process is ready to execute but has been temporarily moved out of main memory in systems that support swapping or suspension.

### Blocked Suspended

A process is both waiting for an event and suspended or swapped out of main memory.

|State|Meaning|
|---|---|
|Ready Suspended|Ready to run, but suspended|
|Blocked Suspended|Waiting for an event and suspended|

Suspension may free RAM for other processes. When the process is resumed, it may need to return to main memory before it can execute.

Exam point: The five-state model is the standard starting point. Extended-state questions may include Ready Suspended and Blocked Suspended.

## 5. Process Control Block (PCB)

A Process Control Block (PCB) is an operating-system data structure that stores information required to manage a process.

Think of the PCB as the OS's record of a process.

### What does a PCB contain?

|PCB field|Purpose|
|---|---|
|Process ID (PID)|Identifies the process|
|Process state|Records whether it is ready, running, waiting, and so on|
|Program counter|Stores the address of the next instruction to execute|
|CPU registers|Stores saved CPU register values|
|CPU scheduling information|Priority, scheduling parameters and queue links|
|Memory-management information|Address-space mappings, page tables or related information|
|I/O status information|Information about I/O operations and open files|
|Accounting information|Resource usage and other accounting data|

The exact contents depend on the OS implementation.

### Why is the PCB important?

Suppose Process P1 is executing when its time slice ends. The OS needs to preserve enough of P1's execution state so that P1 can later resume from the correct point.

The OS records or preserves the required state in kernel-managed structures, including the PCB or associated thread-control structures.

Exam traps:

- The PCB stores process-management information; it is not the process's executable program.
    
- The program counter records the address of the next instruction, not the total number of instructions executed.
    
- Scheduling information and saved CPU context are associated with process management.
    
- In many OS designs, some CPU-specific state is kept in thread-control structures, rather than entirely in one process PCB. Introductory textbooks often describe the PCB as containing the saved CPU context.
    

## 6. Context switching

A context switch is the operation of saving the execution state of one process or thread and restoring the state of another, allowing the CPU to resume the other execution context.

A context switch can happen when:

- A process's time slice expires.
    
- A running process blocks for I/O.
    
- A higher-priority process becomes eligible to run.
    
- An interrupt or scheduling event leads the OS to select another process.
    

### Example

Suppose P1 is running and the scheduler decides to run P2.

P1 is running

CPU executes P1 instructions

Save P1's context

Save the needed CPU state

Restore P2's context

Load P2's saved execution state

P2 is running

CPU continues P2's execution

### What is saved or restored?

The required CPU execution state can include:

- Program counter.
    
- CPU registers.
    
- Stack pointer.
    
- Processor status information.
    

The OS also maintains process or thread state and scheduling data as required.

### Is context switching overhead?

Yes. Saving and restoring execution state consumes time, and scheduling may also affect cache and translation-lookaside-buffer performance.

During this work, the CPU is not making progress on the user-level instructions of the processes being switched between.

Exam trap: Context switching is necessary for multitasking, but the switch itself is generally considered overhead.

### Context switching vs mode switching

|Context switching|Mode switching|
|---|---|
|Changes the executing process or thread context|Changes processor privilege mode, such as user mode to kernel mode|
|Usually requires saving and restoring execution context|Does not necessarily change the running process|
|Has scheduling-related overhead|Can occur during a system call or interrupt without switching processes|

For example, a system call may switch from user mode to kernel mode and later back to user mode while the same process continues executing. That is not necessarily a process context switch.

## 7. Process creation

Process creation is the operation through which the operating system creates a new process and prepares it for execution.

A process may be created when:

- A user launches an application.
    
- An existing process starts another process.
    
- The OS starts a system service.
    
- A scheduled task or background operation starts.
    

### General steps in process creation

1. Assign a process identifier (PID).
    
2. Create the required process-management structures, including a PCB or equivalent.
    
3. Set up the address space and required resources.
    
4. Initialize the execution context.
    
5. Place the process into an appropriate scheduling state, commonly Ready when it is prepared to execute.
    

These are conceptual steps; actual implementation details vary by operating system.

### Parent and child processes

A process that creates another process is commonly called the parent process. The newly created process is the child process.

Example:

```
Parent Process
   |
   | creates
   v
Child Process
```

The child may inherit or share some resources with the parent, depending on the OS and creation mechanism.

Important terms:

|Term|Meaning|
|---|---|
|PID|Process identifier|
|PPID|Parent process identifier, where the OS provides this concept|
|Parent process|Process that creates another process|
|Child process|Process created by another process|
|Orphan process|A child whose parent has terminated, under the relevant OS process model|
|Zombie process|A terminated process whose exit status has not yet been collected by its parent, in Unix-like systems|

### Process creation in Unix/Linux: `fork()` and `exec()`

In traditional Unix-like process creation:

- `fork()` creates a new process.
    
- The child begins with a copy of the parent's process state, subject to the operating system's implementation.
    
- `exec()` replaces the current process's program image with a new program; it does not ordinarily create a new process by itself.
    

A common sequence is:

```
pid_t pid = fork();

if (pid == 0) {
    /* Child process */
    execlp("ls", "ls", "-l", (char *)NULL);
}
```

This simplified example creates a child using `fork()`. The child then requests execution of the `ls -l` program through `execlp()`. Production code should also handle failures and may need to wait for the child.

Exam trap: `fork()` creates a process in Unix-like systems; `exec()` replaces the running process's program image.

### Process creation in Windows

Windows provides process-creation APIs such as `CreateProcess()`, which creates a new process and its primary thread.

Exam point: The mechanisms differ between operating systems. Avoid assuming that every OS uses `fork()`.

## 8. Process vs thread — quick distinction

Although your current list focuses on processes, this comparison is useful because it frequently appears alongside process questions.

|Process|Thread|
|---|---|
|An executing program with its own process resources and address-space context|An execution unit within a process|
|Processes generally have separate address spaces|Threads in a process generally share its address space|
|Inter-process communication may require explicit mechanisms|Threads can communicate through shared memory within the process|
|Process switching may involve changing address-space context|Thread switching within the same process may involve less address-space work|

A process can contain multiple threads. Each thread has its own execution state, such as a stack, registers and program counter.

Memory trick: Process = resource and protection context; thread = execution path within a process.

## 9. Important exam traps

|Statement|Correct answer|
|---|---|
|A program is a process in execution.|True, as the standard introductory definition of a process|
|A program file is active in the same sense as a process.|False|
|A process in Ready state is waiting for CPU allocation.|True|
|A process in Waiting state is necessarily waiting for the CPU.|False|
|A PCB stores process-management information.|True|
|Context switching saves and restores execution state.|True|
|Every mode switch is a process context switch.|False|
|`fork()` creates a child process in Unix-like systems.|True|
|`exec()` ordinarily creates a new Unix process by itself.|False|
|A process can contain multiple threads.|True|
|Context-switching time is normally considered overhead.|True|
|A Ready process has completed execution.|False|
### Last-minute memory trick

- Program: Passive instructions.
    
- Process: Program in execution.
    
- Ready: Waiting for the CPU.
    
- Waiting: Waiting for an event.
    
- PCB: Process information maintained by the OS.
    
- Context switch: Save one context, restore another.
    
- `fork()`: Creates a child process in Unix-like systems.
    
- `exec()`: Replaces the current process's program image.
    
- Thread: An execution unit within a process.