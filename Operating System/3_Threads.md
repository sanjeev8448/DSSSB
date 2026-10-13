## 1. What is a thread?

A thread is the smallest unit of CPU execution and scheduling commonly discussed in operating-system fundamentals. It is also called a lightweight process in many textbooks, although a thread and a process are technically different concepts.

A process can contain one or more threads. Threads within the same process generally share the process's resources but have their own execution state.

Each thread typically has its own:

- Thread ID.
    
- Program counter.
    
- CPU registers.
    
- Stack.
    
- Execution state.
    

Threads within a process generally share:

- Code.
    
- Global data and heap.
    
- Address space.
    
- Many process resources, such as open files.
    

### Example

Imagine opening a web browser. It may use different threads for tasks such as processing the user interface, executing JavaScript, and handling background work. Actual browser architecture varies.

### One process with multiple threads

### Browser Process

Shared address space and process resources

Thread 1

UI tasks

Thread 2

Script work

Thread 3

Background task

Conceptual example: threads share process resources, but each has its own execution context and stack.

Exam memory trick: A process is a resource and protection context; a thread is an execution path within that context.

## 2. Why do we need threads?

Threads allow a program to perform multiple activities with overlapping execution.

For example, a text editor could have one thread responding to user input while another performs background checking or autosaving.

### Main advantages

Responsiveness: One task can continue while another waits for an event.

Resource sharing: Threads in the same process can directly access shared process memory and resources.

Lower overhead: Creating and switching between threads within the same process can be cheaper than creating and switching between separate processes, although the exact cost depends on the OS and workload.

Parallelism: Threads can execute simultaneously on multiple CPU cores when the OS, hardware and program permit it.

### Multithreading

Multithreading means using multiple threads within one process.

A multithreaded program can make progress on multiple activities at once. On a single CPU core, this often happens through interleaving and context switching; on multiple cores, threads can also run in parallel.

### Concurrency vs parallelism

|Concurrency|Parallelism|
|---|---|
|Multiple tasks make progress over overlapping periods|Multiple tasks execute at the same instant|
|Can happen on a single CPU core through switching|Requires multiple execution units, such as CPU cores|
|Focuses on coordinating progress|Focuses on simultaneous execution|

Exam trap: Multithreading does not automatically mean that all threads execute simultaneously. Concurrent execution and parallel execution are related but distinct.

## 3. Process vs thread

This comparison is one of the most important OS MCQ topics.

|Feature|Process|Thread|
|---|---|---|
|Definition|Program in execution with its own process context|Execution unit within a process|
|Address space|Typically has its own virtual address space|Shares its process address space with other threads|
|Stack|Has process memory and execution resources|Each thread has its own stack|
|Registers and program counter|Maintains execution state|Each thread has its own execution state|
|Resource sharing|Separate processes normally require mechanisms to share data|Threads of the same process commonly share memory and resources|
|Communication|Often uses IPC, such as pipes or sockets|Can communicate through shared memory|
|Creation overhead|Generally higher|Often lower within an existing process|
|Context switching|May require changing address-space context|A thread switch in the same process may avoid changing address space|
|Fault isolation|Often better between separate protected processes|A faulty thread can corrupt shared process memory or crash the process|
|Failure effect|A process failure is often confined to that process|A thread failure can affect other threads in the same process|

### What does each thread have separately?

Remember this distinction:

### Shared by threads of a process

Code

Global data

Heap

Process resources

### Private to each thread

Stack

Registers

Program counter

Thread state

These are the standard textbook distinctions. Particular operating systems may maintain additional structures or provide exceptions to simplified descriptions.

### Example: Two separate processes vs two threads

Two processes: Two independent applications usually have separate virtual address spaces. One cannot directly access the other's private memory without an appropriate sharing mechanism.

Two threads in one process: Both usually access the same process heap and global data. This makes communication easier but requires care to avoid race conditions.

### Common exam traps

- Threads of the same process share the process's address space, but not their individual stacks.
    
- Each thread maintains its own program counter and registers.
    
- Process creation is generally more expensive than creating a thread inside an existing process, but exact costs vary.
    
- Threads are not fully isolated from one another when they share memory.
    
- A thread is not the same as a program or a process.
    

# 4. User-level threads (ULT)

User-level threads are managed by a user-space thread library rather than directly scheduled as individual threads by the kernel.

The thread library manages operations such as creating, scheduling and switching between user threads.

The kernel may see only the underlying process or kernel-schedulable entity, depending on the threading implementation.

### How user-level threads work

Suppose a process has three user-level threads: T1, T2 and T3.

A user-space thread library can switch execution between them without requiring a kernel transition for every thread switch.

### User-level thread model

### User process

Thread library schedules user threads

T1

T2

T3

Kernel-schedulable entity

The kernel may schedule the process, not each user thread individually

CPU

This diagram illustrates the traditional many-to-one user-thread model, not every modern user-level threading implementation.

### Advantages of user-level threads

- Thread creation and switching can be fast.
    
- Switching between user threads can avoid entering the kernel.
    
- Thread scheduling can be customized by the user-space library.
    
- The threading implementation can be portable across systems where the necessary primitives are available.
    

### Disadvantages of user-level threads

In a traditional many-to-one model:

- If one thread performs a blocking system call that blocks the whole process, the other user threads may also be unable to run.
    
- The kernel may be unaware of the individual user threads.
    
- Multiple user threads cannot independently execute in parallel on separate cores if they all map to a single kernel-schedulable thread.
    

Exam trap: The blocking limitation applies to the traditional many-to-one model. It is not a universal limitation of every user-level threading design, because user-level libraries can work with multiple kernel-schedulable threads.

# 5. Kernel-level threads (KLT)

Kernel-level threads are managed and scheduled by the operating-system kernel as individual threads.

The kernel knows about these threads and can schedule them separately.

### How kernel-level threads work

Suppose a process contains T1, T2 and T3. Under a typical kernel-thread model, the kernel knows about the individual threads and can schedule runnable threads on available CPU cores.

### Kernel-level thread model

### Process

T1

T2

T3

### Kernel scheduler

Schedules individual kernel threads

CPU Core 1

CPU Core 2

CPU Core 3

Runnable threads may execute in parallel when suitable CPU cores are available.

The diagram shows possible parallel scheduling, not a guarantee that all threads will run simultaneously.

### Advantages of kernel-level threads

- The kernel schedules threads individually.
    
- When one thread blocks, other runnable threads of the same process may still run.
    
- Threads can execute in parallel on multiple CPU cores.
    
- The OS can apply scheduling priorities and policies to kernel-schedulable threads.
    

### Disadvantages of kernel-level threads

- Creating and managing threads generally involves kernel-supported operations.
    
- Thread switching and management may be more expensive than purely user-space operations.
    
- Kernel-level thread implementations require OS support.
    

Exam trap: Kernel-level threads are not necessarily slower in every workload. Their cost depends on the OS, hardware and threading operation being measured.

## 6. User-level threads vs kernel-level threads

|Feature|User-level threads (traditional model)|Kernel-level threads|
|---|---|---|
|Thread management|User-space library|Kernel|
|Kernel awareness|Individual threads may be invisible to the kernel|Kernel knows individual threads|
|Creation and switching|Can be fast because operations may remain in user space|Usually involves kernel-supported management|
|Scheduling|User-space thread library|Kernel scheduler|
|Blocking system call|May block the whole process in a many-to-one model|Normally blocks the calling thread, not every thread in the process|
|Parallelism across cores|Not possible across multiple cores in a pure many-to-one mapping|Possible with multiple runnable kernel threads and available cores|
|Portability|Can be implemented largely in user space|Requires OS support for kernel threads|

### Most important exam points

1. ULT: Thread management is in user space.
    
2. KLT: Thread management and scheduling are supported by the kernel.
    
3. Blocking: In the traditional many-to-one user-thread model, a blocking system call can block the entire process.
    
4. Parallelism: Kernel threads can be scheduled on multiple cores if the system and mapping support it.
    
5. Overhead: ULT operations can be cheaper, but actual performance depends on the implementation.
    

# 7. Thread mapping models

Thread mapping describes how user-level threads correspond to kernel-level threads. Three classic models are important for operating-system MCQs.

## A. Many-to-one model

Many user threads map to one kernel thread.

### Many-to-one

U1

U2

U3

K1

Multiple user threads share one kernel-schedulable thread.

- Fast user-thread management can be possible.
    
- A blocking system call can block the whole process.
    
- Multiple user threads cannot execute in parallel across CPU cores through this single kernel thread.
    

## B. One-to-one model

Each user thread maps to its own kernel thread.

### One-to-one

U1

U2

U3

K1

K2

K3

Each user thread has a corresponding kernel thread.

- The kernel schedules each thread individually.
    
- If one thread blocks, other runnable threads can still execute.
    
- Parallel execution across cores is possible.
    
- Creating very many threads can impose greater kernel-management overhead.
    

## C. Many-to-many model

Many user threads are mapped onto a number of kernel threads.

### Many-to-many

U1

U2

U3

U4

K1

K2

K3

Many user threads are multiplexed over multiple kernel threads.

- Provides flexibility in mapping user threads to kernel threads.
    
- Can support parallelism when multiple kernel threads are available.
    
- User-space scheduling can coexist with kernel scheduling.
    
- The implementation is more complex.
    

### Mapping model comparison

|Model|Mapping|Multiple-core parallelism|Traditional blocking limitation|
|---|---|---|---|
|Many-to-one|Many ULTs → one KLT|No, through the single KLT|One blocking system call may block the process|
|One-to-one|One ULT → one KLT|Possible|Usually blocks only the calling thread|
|Many-to-many|Many ULTs → multiple KLTs|Possible|Other mapped threads may continue if resources are available|

Memory trick: Many-to-one = one kernel thread; one-to-one = one kernel thread per user thread; many-to-many = many user threads over multiple kernel threads.

## Last-minute revision

- Thread: Execution unit within a process.
    
- Shared: Code, global data, heap and process address space.
    
- Private per thread: Stack, registers, program counter and thread state.
    
- User-level threads: Managed by a user-space library.
    
- Kernel-level threads: Known to and scheduled by the kernel.
    
- Many-to-one: Multiple user threads map to one kernel thread.
    
- One-to-one: One user thread maps to one kernel thread.
    
- Many-to-many: Multiple user threads map onto multiple kernel threads.
    

The most important distinction to remember for MCQs is that threads share many process resources but maintain their own execution state. User-level versus kernel-level threads differs mainly in who manages and schedules the individual threads.ನೆ