# 1. Definition of an Operating System

An Operating System (OS) is system software that manages computer hardware and software resources and provides services for application programs.

It acts as an interface between the user, applications and computer hardware.

Examples include Microsoft Windows, Linux, macOS, Android and iOS.

### User

Person interacting with the computer

### Applications

Browser, editor, games, database software

### Operating System

Resource management and system services

### Hardware

CPU, RAM, storage, keyboard, display and other devices

### Main objectives of an OS

1. Convenience: Makes a computer easier to use.
    
2. Efficiency: Uses CPU, memory and devices effectively.
    
3. Resource management: Allocates resources among competing programs and users.
    
4. Protection and security: Controls access to system resources.
    
5. Reliability: Handles errors and helps maintain stable operation.
    

Exam point: The OS is system software, not application software.

# 2. Functions of an Operating System

The OS performs several essential tasks.

## A. Process management

A process is a program in execution.

The OS manages the creation, scheduling, synchronization and termination of processes.

Its responsibilities include:

- Creating and terminating processes.
    
- Scheduling processes for CPU time.
    
- Suspending and resuming processes.
    
- Supporting inter-process communication.
    
- Managing synchronization and deadlocks.
    

Example: When a browser and a music player run together, the OS manages their execution and CPU access.

Exam trap: A program is a set of instructions; a process is an executing instance of a program.

## B. Memory management

Memory management controls the use of main memory (RAM).

Its responsibilities include:

- Tracking which memory areas are in use.
    
- Allocating and freeing memory.
    
- Managing virtual memory.
    
- Providing address-space protection.
    
- Supporting paging and segmentation where applicable.
    

Example: The OS allocates memory to a browser and prevents one process from freely overwriting another process's protected memory.

## C. File system management

The OS organizes information into files and directories.

Common functions include:

- Creating and deleting files.
    
- Creating and deleting directories.
    
- Reading and writing file contents.
    
- Managing file permissions and metadata.
    
- Allocating storage space to files.
    

Examples of file systems include NTFS, ext4, FAT32 and APFS.

Exam trap: A file system is the mechanism used to organize and manage stored data; it is not the same thing as the entire operating system.

## D. Device and I/O management

The OS coordinates input/output devices such as keyboards, printers, disks and network interfaces.

Typical responsibilities include:

- Communicating with devices through device drivers.
    
- Managing device access.
    
- Buffering and caching I/O where appropriate.
    
- Queuing and scheduling device operations.
    

Example: The OS uses a suitable printer driver to communicate with a connected printer.

## E. CPU scheduling and resource allocation

The OS decides which eligible process receives CPU time and how resources are allocated.

Common CPU scheduling algorithms studied in OS are:

- First Come, First Served (FCFS).
    
- Shortest Job First (SJF).
    
- Priority Scheduling.
    
- Round Robin (RR).
    

Example: Round Robin assigns each eligible process a time quantum, helping time-sharing systems provide responsive CPU access.

## F. Security and protection

The OS controls access to resources and helps protect the system.

Examples include:

- User authentication.
    
- File and directory permissions.
    
- Access control.
    
- Process isolation.
    
- Privilege separation.
    

Exam distinction: Authentication checks who a user is; authorization determines what that user is permitted to do.

## G. User interface

The OS provides ways for people to interact with the computer, such as a graphical desktop or a command-line shell.

Examples include desktop windows, icons, menus and text commands.

## H. Error detection and handling

The OS detects and responds to conditions such as device failures, invalid operations and resource problems.

It may log errors, notify users, stop an affected process or attempt recovery.

## I. Networking and communication

Modern operating systems provide networking services, protocol support and interfaces for applications to communicate with other machines.

## J. Accounting and performance monitoring

The OS may track resource usage, such as CPU time, memory use, disk activity and user activity, for monitoring, diagnostics or administration.

### Function revision table

|Function|Main responsibility|
|---|---|
|Process management|Processes and CPU execution|
|Memory management|RAM allocation and virtual memory|
|File management|Files, folders and permissions|
|Device management|I/O devices and drivers|
|CPU scheduling|Selecting processes for CPU time|
|Security|Protection and access control|
|User interface|Interaction with users|
|Error handling|Detecting and responding to failures|
|Networking|Communication between systems|

# 3. Types of Operating Systems

Operating systems can be classified according to how they execute tasks, share resources and interact with users.

## A. Batch Operating System

A batch OS collects jobs and processes them in batches, generally without requiring interactive input from the user during each job's execution.

Example: Traditional payroll processing where many employee records are processed together.

Characteristics:

- Jobs are grouped and executed in batches.
    
- Direct interaction during execution is limited.
    
- Jobs may wait in queues.
    
- Turnaround time can be high.
    

Exam clue: Jobs collected and processed together with little or no interactive user involvement → Batch OS.

## B. Multiprogramming Operating System

A multiprogramming OS keeps multiple programs in memory so the CPU can work on another program when the current program is waiting, such as for I/O.

Example: While one program waits for disk input, the CPU executes another ready program.

Main objective: Improve CPU utilization.

Exam trap: Having multiple programs in memory does not mean the CPU is necessarily executing them simultaneously.

## C. Multitasking Operating System

A multitasking OS allows multiple tasks to make progress over overlapping periods of time, usually by switching CPU execution between tasks.

Example: Editing a document while downloading a file.

On a single-core CPU, tasks generally share the processor through switching. On a multicore CPU, some can also execute simultaneously.

## D. Time-Sharing Operating System

A time-sharing OS divides CPU time among multiple users or tasks, often using small time slices, to provide interactive responsiveness.

Example: Many users interacting with a shared computer system through separate terminals.

Main objective: Make the system responsive to multiple users or interactive tasks.

### Multiprogramming vs multitasking vs time-sharing

|Feature|Multiprogramming|Multitasking|Time-sharing|
|---|---|---|---|
|Main objective|High CPU utilization|Manage multiple tasks|Interactive responsiveness|
|Multiple programs/tasks|Yes|Yes|Yes|
|CPU switches tasks|Often when a program waits or is rescheduled|Typically|Typically using time slices|
|User interaction|May be limited|Common|Central to the model|

These concepts overlap in modern OS designs; the distinctions above represent common textbook emphasis.

## E. Multiprocessing Operating System

A multiprocessing system uses two or more processing units or CPU cores to execute work.

Example: A computer whose OS schedules processes across multiple CPU cores.

Advantages:

- Can execute work in parallel.
    
- May improve throughput.
    
- Can improve responsiveness under suitable workloads.
    

Exam trap: Multiprocessing refers to multiple processors or cores; multiprogramming refers to keeping multiple programs available for CPU execution.

## F. Real-Time Operating System (RTOS)

A real-time OS is designed to provide predictable responses within specified timing constraints.

Two major categories are:

- Hard real-time: Missing a required deadline is considered a system failure.
    
- Soft real-time: Missing a deadline degrades service quality but is not always catastrophic.
    

Examples include certain industrial control systems, automotive controllers and embedded control applications.

Exam trap: Real-time does not simply mean "very fast." It means meeting timing requirements predictably.

## G. Distributed Operating System

A distributed OS coordinates resources across multiple networked computers and may present them as a more integrated system.

Key ideas include resource sharing, coordination and managing work across machines.

Distinction: A distributed system may use different operating systems on its machines; not every distributed system is a distributed operating system.

## H. Network Operating System

A network OS provides services for computers connected by a network, such as shared files, printers, user accounts and centralized administration.

Example: A server OS providing file-sharing and authentication services to networked machines.

Exam trap: A network OS provides network services; a distributed OS aims for more integrated coordination across multiple machines.

## I. Embedded Operating System

An embedded OS is designed for a dedicated device or specialized task, often with limits on processing power, memory or energy use.

Examples include systems in routers, consumer electronics and some vehicle controllers.

## J. Mobile Operating System

A mobile OS is designed for mobile devices and typically manages touch interaction, wireless communication, battery usage, sensors and applications.

Examples include Android and iOS.

## K. Single-user and multi-user systems

- Single-user OS: Designed primarily for one user to use the system at a time.
    
- Multi-user OS: Supports multiple user accounts or sessions with controlled resource sharing.
    

These labels can describe different dimensions of an OS. A single-user system can still support multitasking.

### Types — exam revision table

|Type|Key phrase|
|---|---|
|Batch|Jobs processed in batches|
|Multiprogramming|Multiple programs in memory; better CPU utilization|
|Multitasking|Multiple tasks make progress|
|Time-sharing|Interactive sharing through time slices|
|Multiprocessing|Multiple processors or cores|
|Real-time|Predictable response within deadlines|
|Distributed|Integrated management across multiple machines|
|Network|Network services and shared resources|
|Embedded|Specialized device or task|
|Mobile|Phone/tablet-oriented platform|
|Multi-user|Multiple users or sessions|

# 4. Operating System Organization

OS organization describes how operating-system components are arranged and how they interact.

Common textbook architectures include monolithic, layered, microkernel, modular and hybrid structures.

## A. Monolithic structure

In a monolithic OS, many core OS services run together in a large kernel address space.

These services may include process management, memory management, file systems and device drivers.

### Monolithic architecture

User applications

### Large kernel

Process management

Memory management

File systems

Device drivers

Hardware

Advantages

- Services can communicate efficiently within the kernel.
    
- The structure can deliver high performance.
    
- Many operations avoid extra user-space/kernel-space communication steps.
    

Disadvantages

- A fault in a privileged kernel component can seriously affect the entire system.
    
- A large kernel can be difficult to maintain and debug.
    

Traditional Unix is a common textbook example of a monolithic design, although modern implementations can include modular features.

## B. Layered structure

In a layered OS, components are organized into layers. Each layer generally uses services from lower layers and provides services to higher layers.

### Layered architecture

Layer 4

User interface / applications

Layer 3

System services

Layer 2

Memory and process management

Layer 1

Device and I/O management

Layer 0

Hardware

The diagram illustrates a conceptual arrangement; actual OS layer counts and service placement differ.

Advantages

- Clear organization and separation of responsibilities.
    
- Easier to reason about and test individual layers.
    
- Changes can be localized if interfaces are well-designed.
    

Disadvantages

- Defining suitable layers can be difficult.
    
- Requests that cross many layers can introduce overhead.
    
- Strict layering can limit implementation flexibility.
    

## C. Microkernel structure

A microkernel keeps a relatively small set of essential mechanisms in kernel space. Other services—such as many drivers and file-system services—can run as user-space servers.

Typical microkernel responsibilities include basic scheduling, low-level memory management and inter-process communication mechanisms.

### Microkernel architecture

Applications

User-space services

File system • Drivers • Other servers

### Microkernel

Essential mechanisms and IPC

Hardware

Advantages

- Smaller trusted kernel core can reduce the amount of privileged code.
    
- Many services can be isolated from one another.
    
- Some service failures can be contained or recovered from more easily.
    

Disadvantages

- Communication between user-space services and the kernel may introduce overhead.
    
- Designing interfaces and coordination between servers is complex.
    

Examples often discussed with microkernel designs include MINIX 3 and QNX.

## D. Modular structure

A modular OS has a core kernel that supports components or modules that can be loaded or unloaded as needed.

Modules may provide driver support, file systems or other services.

Advantages

- Extensible without rebuilding the entire kernel for every module change.
    
- Maintains many performance benefits of in-kernel services.
    
- Components can be developed and maintained separately.
    

Disadvantages

- A faulty privileged module can still crash or compromise the kernel.
    
- Module compatibility and dependencies must be managed.
    

Linux is commonly described as a modular monolithic kernel because it supports loadable kernel modules while many services execute in kernel space.

## E. Hybrid structure

A hybrid kernel combines design ideas from monolithic and microkernel approaches.

The goal is often to balance performance, modularity and service organization.

Modern Windows NT-family systems and macOS are commonly described in textbooks as using hybrid approaches, though the specific internal designs differ.

### Architecture comparison

|Architecture|Main idea|Main trade-off|
|---|---|---|
|Monolithic|Many core services in one kernel space|Performance vs fault isolation|
|Layered|Components arranged in layers|Clarity vs cross-layer overhead|
|Microkernel|Minimal core with more services in user space|Isolation/modularity vs communication cost|
|Modular|Core with loadable modules|Extensibility vs risks from privileged modules|
|Hybrid|Combines architectural approaches|Attempts to balance multiple goals|

Exam trap: Modular and monolithic are not necessarily opposites. A monolithic kernel can also be modular.

# 5. Kernel

The kernel is the central, privileged component of an operating system. It manages essential system resources and provides controlled access to hardware.

It runs with elevated privileges so it can perform operations ordinary applications cannot perform directly.

## Main functions of the kernel

### A. Process and thread management

- Creates and terminates processes and threads.
    
- Schedules CPU execution.
    
- Performs context switching.
    
- Supports synchronization and communication mechanisms.
    

### B. Memory management

- Manages memory allocation and protection.
    
- Maintains address-space information.
    
- Supports mechanisms such as virtual memory and paging where applicable.
    

### C. Device management

- Coordinates device access.
    
- Works with device drivers.
    
- Processes interrupts and I/O requests.
    

### D. System calls

A system call is a controlled interface through which a program requests a service from the OS kernel.

Examples include requesting file access, creating processes or changing memory mappings, depending on the OS.

A simplified interaction is:

User application

Requests a service

System call interface

Controlled transition to kernel service

Kernel

Performs the authorized operation

Hardware or managed resource

A system call may involve a switch from user mode to kernel mode. It is not necessarily the same as an ordinary function call within an application.

### E. Interrupt handling

An interrupt signals an event that requires CPU attention. The OS kernel participates in handling hardware interrupts and certain software exceptions, according to the architecture and OS design.

Example: A network device may signal that incoming data is ready for processing.

## Kernel mode vs user mode

|Feature|Kernel mode|User mode|
|---|---|---|
|Privileges|High|Restricted|
|Direct access to privileged hardware operations|Permitted subject to system architecture|Generally prohibited|
|Typical code|Kernel and trusted privileged components|Ordinary applications|
|Fault impact|Can affect the entire system|Often confined to the affected process|

Exam trap: Applications normally run in user mode. The kernel runs with elevated privileges. A user-mode program requests privileged services through controlled OS interfaces.

## Kernel vs shell

These terms are often confused.

|Kernel|Shell|
|---|---|
|Core of the OS|User-facing command interpreter or interface|
|Manages resources and privileged operations|Accepts commands and launches programs|
|Works close to hardware and system resources|Requests OS services to carry out commands|
|Examples: Linux kernel, XNU kernel|Examples: Bash, PowerShell, Zsh|

A shell is not the same as the kernel, and the OS can support different shells and graphical interfaces.

# 6. User Interface in an OS

A user interface (UI) is the means by which users interact with a computer system.

The main textbook categories are the Command-Line Interface (CLI) and Graphical User Interface (GUI). Other interfaces, such as touch and voice interfaces, are also common.

## A. Command-Line Interface (CLI)

A CLI accepts commands as text.

Examples include Bash, Zsh, Windows Command Prompt and PowerShell.

Example:

```
mkdir DSSSB
```

This command requests creation of a directory called `DSSSB`.

Advantages

- Efficient for automation and repetitive tasks.
    
- Supports scripts and command pipelines.
    
- Often uses fewer graphical resources.
    

Disadvantages

- Requires knowledge of commands and syntax.
    
- Typing errors may produce unexpected results.
    
- Less discoverable for some beginners.
    

## B. Graphical User Interface (GUI)

A GUI lets users interact using visual elements such as windows, icons, menus, pointers and buttons.

Examples include Windows desktop, macOS desktop and graphical Linux environments.

Advantages

- Often easier for beginners.
    
- Provides visual feedback.
    
- Supports intuitive point-and-click interaction.
    

Disadvantages

- Can consume more resources than a minimal CLI.
    
- Some repetitive or advanced operations may be slower without automation.
    

## C. Touch, voice and other interfaces

Modern systems also support:

- Touch interface: Interaction using taps, swipes and gestures.
    
- Voice interface: Commands using speech recognition.
    
- Menu-driven interface: Users select from displayed options.
    
- Gesture-based interface: Input using gestures or body movement.
    

A system may combine several interface types. For example, a smartphone commonly supports touch and voice interaction.

### CLI vs GUI

|Feature|CLI|GUI|
|---|---|---|
|Input|Text commands|Visual elements, pointer, touch|
|Automation|Strong scripting support|May support automation through additional tools|
|Learning curve|Commands must be learned|Often more discoverable|
|Resource use|Can be low in a minimal environment|Often requires more graphical resources|
|Typical example|Bash or PowerShell|Windows desktop|

Exam trap: A GUI is an interface, not the kernel. A CLI shell is also an interface component, not the entire operating system.

# 7. Quick revision sheet

|Topic|One-line definition|
|---|---|
|Operating System|System software managing resources and offering services to applications|
|Process management|Manages running processes and CPU allocation|
|Memory management|Allocates and protects memory|
|File management|Organizes files and directories|
|Device management|Coordinates devices and I/O|
|Batch OS|Processes jobs in batches|
|Multiprogramming|Keeps several programs available to improve CPU utilization|
|Time-sharing|Shares CPU time for interactive responsiveness|
|Multiprocessing|Uses multiple processors or cores|
|Real-time OS|Designed to meet timing constraints predictably|
|Monolithic kernel|Many OS services run in kernel space|
|Layered OS|Organizes OS components into layers|
|Microkernel|Keeps a small core and moves more services to user space|
|Kernel|Privileged core of the OS|
|System call|Controlled request for an OS service|
|CLI|Text-command interface|
|GUI|Visual interface using windows, icons, menus or similar elements|
### Final memory trick

- OS = manages resources.
    
- Multiprogramming = improves CPU utilization.
    
- Time-sharing = interactive CPU sharing.
    
- Multiprocessing = multiple CPUs or cores.
    
- Real-time = timing deadlines.
    
- Kernel = privileged core.
    
- Shell = command interpreter.
    
- CLI = text commands.
    
- GUI = graphical interaction.
    
- Microkernel = small kernel, more services outside it.