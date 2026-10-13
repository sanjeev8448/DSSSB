The CPU (Central Processing Unit) is the main processing component of a computer. It executes instructions, performs arithmetic and logical operations, and coordinates the activities of other components.

The six topics to study are:

1. ALU — Arithmetic Logic Unit
    
2. Control Unit (CU)
    
3. Registers
    
4. Accumulator (ACC)
    
5. Program Counter (PC)
    
6. Instruction Register (IR)
    

## 1. Basic CPU architecture

A simplified CPU consists of the ALU, Control Unit and registers. These components work together to fetch, decode and execute program instructions.

## Basic CPU Block Diagram

Main Memory

Instructions and data

Data, address and control signals

## CPU

ALU

Calculations and logic

Control Unit

Coordinates execution

Registers

PC, IR, accumulator and other registers

The ALU performs operations, the Control Unit directs execution, and registers hold small amounts of information needed immediately by the CPU.

Exam point: The ALU, Control Unit and registers are the standard introductory components of CPU architecture. More advanced processors also contain caches, pipelines, branch predictors and other specialized structures.

# 2. ALU — Arithmetic Logic Unit

The ALU is the CPU component responsible for performing arithmetic and logical operations on data.

## Main functions

### A. Arithmetic operations

- Addition
    
- Subtraction
    
- Multiplication and division, when supported by the relevant execution unit
    
- Increment and decrement
    
- Comparisons implemented through arithmetic or related operations
    

### B. Logical operations

- AND
    
- OR
    
- NOT
    
- XOR
    
- Bitwise shifts and related operations, depending on the processor architecture
    

### C. Comparison operations

The CPU can compare values to determine whether one is equal to, greater than or less than another. The result may be represented through condition flags or a direct comparison result, depending on the instruction set.

### Example 1: Addition

Suppose the CPU must execute:

\[ A = 10 + 20 \]

The ALU performs the addition. The result, \(30\), is placed in a destination register or another location specified by the instruction.

### Example 2: Logical AND

For two 4-bit values:

```
A = 1100
B = 1010
---------
A AND B = 1000
```

A bit in the output is 1 only when both corresponding input bits are 1.

### Important status flags

An ALU operation may update status flags in a processor's status register.

|Flag|Meaning|
|---|---|
|Zero flag (Z)|Result is zero|
|Carry flag (C)|Indicates a carry or borrow-related condition, according to the instruction set|
|Sign/Negative flag (N)|Indicates the result's sign bit in common architectures|
|Overflow flag (V/O)|Indicates signed arithmetic overflow|

Exact flag behaviour depends on the CPU architecture and the operation performed.

### ALU vs Control Unit

|ALU|Control Unit|
|---|---|
|Performs arithmetic and logical operations|Coordinates instruction execution|
|Processes operands|Decodes instructions and issues control signals|
|Produces operation results and may update flags|Directs data movement and the actions of CPU components|

Exam traps:

- ALU stands for Arithmetic Logic Unit.
    
- Arithmetic and Boolean operations are associated with the ALU.
    
- Instruction decoding and control-signal generation are associated with the Control Unit.
    
- The ALU does not independently decide which program instruction should execute next.
    

# 3. Control Unit (CU)

The Control Unit coordinates and controls the execution of instructions inside the CPU.

It determines what actions are required for an instruction and generates control signals to coordinate the ALU, registers, memory and input/output operations.

## Main functions

- Fetches instructions from memory through the instruction-fetch mechanism.
    
- Decodes the fetched instruction.
    
- Directs the movement of data between registers, the ALU and memory.
    
- Issues control signals for the required operations.
    
- Coordinates the stages of instruction execution.
    
- Controls the sequence of instructions, including branches and jumps.
    

### Example

Consider the instruction:

```
ADD R1, R2
```

Assume this instruction means `R1 = R1 + R2`.

1. The Control Unit directs the instruction to be decoded.
    
2. It arranges for the required operands to be available.
    
3. The ALU performs the addition.
    
4. The result is written to the destination register.
    

The exact internal sequence depends on the processor design.

### Control Unit vs ALU

|Feature|Control Unit|ALU|
|---|---|---|
|Main role|Coordinates operations|Performs arithmetic and logic|
|Decodes instructions|Yes|No|
|Generates control signals|Yes|Not its primary role|
|Adds two numbers|Directs the operation|Performs the addition|
|Controls instruction flow|Yes|May provide flags used in decisions|

### Exam traps

- The Control Unit is responsible for coordination and control, not the actual arithmetic calculation.
    
- The Control Unit may be implemented using hardwired logic, microprogrammed control, or a combination of techniques.
    
- The Control Unit and ALU are distinct functions, even when integrated into a single processor chip.
    

# 4. Registers

Registers are small, high-speed storage locations inside the CPU. They hold instructions, addresses, operands, intermediate results and other information needed during execution.

Registers are generally faster to access than main memory and are much smaller in capacity.

## Why are registers needed?

Imagine that the CPU is adding two numbers. It needs quick access to the operands and a place to hold the result. Registers provide that storage without repeatedly accessing slower main memory for every intermediate step.

## Types of registers

|Register|Full form / role|Main purpose|
|---|---|---|
|PC|Program Counter|Holds the address of the next instruction to be fetched|
|IR|Instruction Register|Holds the current instruction being decoded or executed|
|ACC|Accumulator|Holds operands or intermediate arithmetic and logical results in accumulator-based designs|
|MAR|Memory Address Register|Holds the memory address involved in a memory access|
|MDR / MBR|Memory Data Register / Memory Buffer Register|Holds data being transferred to or from memory|
|General-purpose registers|Varies by architecture|Hold operands, addresses and intermediate results|
|Status / Flag register|Processor status register|Holds condition flags and status information|
|SP|Stack Pointer|Tracks the top of the current stack, according to the architecture|

Important: PC, IR, MAR and MDR are conventional textbook registers. Real CPUs may use different names, structures or implementation details.

## Register vs cache vs RAM

|Feature|Register|Cache|RAM|
|---|---|---|---|
|Location|Inside CPU core or processor execution structures|On or near the CPU|Main memory modules|
|Typical role|Immediate operands and CPU state|Stores recently or frequently used instructions/data|Holds active programs and data|
|Capacity|Very small|Larger than registers|Much larger|
|Access|Generally fastest|Very fast|Generally slower than registers and cache|
|Explicitly named in machine instructions|Often, for architectural registers|Usually not directly named by ordinary instructions|Accessed through addresses|

### Exam traps

- Registers are part of the processor's execution machinery.
    
- The PC stores an instruction address, not the instruction itself.
    
- The IR stores an instruction, not the address of the next instruction.
    
- Registers are not the same as cache or RAM.
    
- MAR and MDR are distinct: MAR holds an address; MDR holds data.
    

# 5. Accumulator (ACC)

The Accumulator is a CPU register used to hold operands and intermediate or final results of arithmetic and logical operations in accumulator-based architectures.

It is particularly important in traditional CPU models taught in introductory Computer Architecture.

### Example

Consider these simplified accumulator-based instructions:

```
LOAD  A
ADD   B
STORE C
```

Assume memory locations `A` and `B` contain 10 and 20.

|Step|Instruction|Accumulator after execution|
|---|---|---|
|1|`LOAD A`|10|
|2|`ADD B`|30|
|3|`STORE C`|30|

Explanation:

1. `LOAD A` loads the value stored at memory location A into the accumulator.
    
2. `ADD B` adds the value at memory location B to the accumulator.
    
3. `STORE C` stores the accumulator's result into memory location C.
    

This is a simplified instructional example; actual instruction syntax and operand behaviour vary by architecture.

### Why is the accumulator useful?

- Holds intermediate calculation results.
    
- Reduces the need to specify an explicit destination register in accumulator-based instruction sets.
    
- Supports arithmetic and logical operations in simple CPU designs.
    

### Accumulator vs general-purpose register

|Accumulator|General-purpose register|
|---|---|
|Has a specialized conventional role in accumulator-based designs|Can hold different kinds of data and addresses|
|Often implicitly used by arithmetic instructions|Frequently specified explicitly in instructions|
|Common in textbook and older CPU designs|Common in modern general-purpose processors|

Exam trap: Not every modern CPU has a single special accumulator register. Modern processors often use multiple general-purpose registers, although some instruction sets and operations still have accumulator-like behaviour.

# 6. Program Counter (PC)

The Program Counter is a CPU register that holds the address of the next instruction to be fetched, according to the processor's current instruction sequence.

It is also called the Instruction Pointer (IP) in some processor architectures.

## How does the PC work?

Suppose instructions are stored at memory addresses 100, 104 and 108. Assume each instruction occupies 4 bytes.

- Initially, PC = 100.
    
- The CPU fetches the instruction at address 100.
    
- For a simple sequential instruction, the PC advances to 104.
    
- The next instruction is fetched from address 104.
    

The example assumes 4-byte instruction spacing. Actual instruction sizes and PC update rules depend on the architecture.

### What happens during a branch or jump?

Suppose an instruction tells the CPU to jump to address 500. The PC is updated to 500 rather than continuing with the next sequential address.

This is why the PC is essential for:

- Sequential execution.
    
- Conditional branches.
    
- Unconditional jumps.
    
- Function calls and returns, together with other processor state.
    

### PC exam facts

- PC stores an instruction address.
    
- It does not ordinarily store the current instruction's contents.
    
- The PC usually advances during sequential execution.
    
- Branches and jumps can change the next instruction address.
    
- PC is also known as the instruction pointer in some architectures.
    

Exam trap: “PC always increases by 1” is not universally correct. The increment depends on instruction size and architecture, and control-flow instructions may replace the sequential address with a target address.

# 7. Instruction Register (IR)

The Instruction Register holds the instruction currently being processed by the CPU.

After an instruction is fetched from memory, the instruction-fetch mechanism places it into the appropriate instruction register or equivalent internal instruction storage. The Control Unit then decodes it and coordinates its execution.

### Example

Suppose memory contains an encoded instruction that means:

```
ADD R1, R2
```

The CPU fetches that instruction and places it in the IR or equivalent instruction storage. The Control Unit decodes the operation and directs the CPU to add the required operands.

### PC vs IR

|Feature|Program Counter (PC)|Instruction Register (IR)|
|---|---|---|
|Stores|Address of the next instruction to fetch|Current instruction being processed|
|Contains|An address|Instruction bits|
|Main purpose|Tracks instruction sequence|Holds the instruction for decoding/execution|
|Changes when|Sequential execution or control flow updates it|A new instruction is fetched into it|

### Example of their relationship

Assume PC = 100 and the instruction at address 100 is fetched.

- The instruction is loaded into the IR.
    
- The PC is updated according to the processor's instruction-fetch rules.
    
- The Control Unit decodes the IR's instruction.
    
- The processor executes it.
    
- The CPU then fetches the next instruction, unless control flow changes.
    

Exam trap: The PC and IR are not interchangeable. PC identifies where the next instruction is to be fetched; IR holds the fetched instruction itself.

# 8. Fetch–Decode–Execute cycle

The CPU repeats an instruction-processing cycle while a program runs.

Fetch

Decode

Execute

Main memoryAddress · Value

20ADD 42

21STORE 43

24LOAD 42

427

Address

Data

Control

Address

Data

Control

CPU

PC20

MAR—

MDR—

CIR—

CU

ALU

ACC5

Fetch

PC holds address 20.

Example

LoadAddBranch

Give feedback

## The three main stages

# 1

Fetch

The CPU uses the PC to locate the next instruction and fetches it from memory into the IR or equivalent instruction storage.

# 2

Decode

The Control Unit interprets the instruction's operation and determines which operands and resources are needed.

# 3

Execute

The processor performs the operation—for example, the ALU adds two values—and stores the result as required.

### Example with registers

Assume the instruction is `ADD R1, R2`, meaning `R1 = R1 + R2`.

|Component|Role|
|---|---|
|PC|Identifies the next instruction address|
|IR|Holds the fetched ADD instruction|
|Control Unit|Decodes ADD and coordinates the operation|
|Registers R1 and R2|Hold the operands|
|ALU|Adds the operands|
|R1|Receives the result in this example|

In a simplified textbook model, MAR holds the memory address for a fetch and MDR holds the instruction data during transfer.

Important: The fetch–decode–execute cycle is a conceptual model. Modern processors overlap instruction stages and may execute multiple instructions at once.

# 9. High-yield comparison table

|Component|Holds or performs|Key phrase|
|---|---|---|
|ALU|Arithmetic and logical operations|Calculation|
|Control Unit|Instruction decoding and control signals|Coordination|
|Registers|Small, fast CPU storage|Immediate data|
|Accumulator|Operands and intermediate results in accumulator-based designs|Calculation result|
|Program Counter|Next instruction address|Where to fetch|
|Instruction Register|Current fetched instruction|What to execute|
|MAR|Memory address for an access|Where in memory|
|MDR / MBR|Data being transferred to/from memory|Data moving|

## 10. Common exam traps

1. ALU vs CU: ALU calculates; Control Unit coordinates.
    
2. PC vs IR: PC holds an instruction address; IR holds the instruction.
    
3. MAR vs MDR: MAR holds a memory address; MDR holds the data being transferred.
    
4. Accumulator: Holds calculation operands or results in accumulator-based designs.
    
5. Fetch–Decode–Execute: Fetch the instruction, decode it, then execute it.
    
6. PC update: It does not always increment by one; the update depends on instruction size and control flow.
    
7. Registers vs RAM: Registers are small CPU storage locations; RAM is the larger main memory.
    
8. Instruction register vs program counter: The IR is not the register that normally determines the next sequential instruction address.

## Final revision in 30 seconds

- ALU: Performs calculations and logical operations.
    
- Control Unit: Decodes instructions and coordinates execution.
    
- Registers: Fast, small storage locations inside the CPU.
    
- Accumulator: Holds operands or results in accumulator-based designs.
    
- PC: Holds the next instruction address.
    
- IR: Holds the current fetched instruction.
    
- MAR: Holds the memory address.
    
- MDR: Holds data being transferred to or from memory.
    

Memory trick: PC = where next, IR = instruction now, MAR = memory address, MDR = memory data.

Next, study memory hierarchy, cache memory, RAM vs ROM, primary vs secondary memory, and the fetch–decode–execute cycle in more depth.