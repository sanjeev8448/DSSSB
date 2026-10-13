This topic covers three important concepts:

1. Instruction cycle — how the CPU executes an instruction.
    
2. Instruction format — how an instruction is represented in binary.
    
3. Addressing modes — how an instruction specifies where its operand is located or how to obtain it.
    

These concepts are connected: the CPU fetches an instruction, decodes its format and addressing mode, obtains the required operands, executes it, and stores the result.

## 1. Instruction Cycle

The instruction cycle is the complete sequence of steps the CPU performs to fetch and execute an instruction.

### Main stages

1. Fetch

Get the instruction from memory

2. Decode

Identify the operation and operands

3. Fetch operands

Obtain the required data, if needed

4. Execute

Perform the specified operation

5. Store result / update state

Write the result and update relevant flags or registers

The exact stages and their implementation vary by CPU architecture.

Some textbooks describe the basic instruction cycle using only three stages: fetch, decode, execute. Operand fetch and write-back may be treated as separate stages in more detailed models.

### Stage 1: Fetch

The CPU retrieves the next instruction from memory.

Typical roles of registers:

- PC (Program Counter): holds the address of the next instruction to be fetched.
    
- MAR (Memory Address Register): holds the memory address being accessed.
    
- MDR/MBR (Memory Data/Buffer Register): holds data or an instruction transferred to or from memory.
    
- IR (Instruction Register): holds the instruction currently being decoded or executed.
    

Simplified sequence:

1. The PC supplies the instruction address.
    
2. The address is sent to memory.
    
3. Memory returns the instruction.
    
4. The instruction is placed in the IR.
    
5. The PC is advanced to the next instruction address, unless the architecture or instruction flow requires a different update.
    

Exam trap: The PC does not necessarily increase by 1. It advances according to instruction length and the architecture.

### Stage 2: Decode

The Control Unit interprets the instruction in the IR.

It determines:

- The operation, such as ADD, SUB, LOAD, or JUMP.
    
- The source and destination operands.
    
- The addressing mode.
    
- The control signals needed for execution.
    

### Stage 3: Execute

The CPU performs the operation. For example, the ALU may add two numbers, or the CPU may transfer data between registers and memory.

A conditional branch may change the PC depending on the result of a condition check.

### Stage 4: Write-back

If required, the result is written to a register or memory location. Status flags may also be updated.

Not every instruction needs write-back—for example, a branch instruction may primarily update the PC.

### Worked example: `ADD R1, R2`

Assume the instruction means `R1 ← R1 + R2`.

Suppose:

- `R1 = 10`
    
- `R2 = 5`
    

Execution:

1. Fetch `ADD R1, R2` from memory.
    
2. Decode the ADD operation and identify registers R1 and R2.
    
3. Read the operands from the registers.
    
4. The ALU computes \(10+5=15\).
    
5. Write `15` into R1.
    

Final state: `R1 = 15`, `R2 = 5`.

### Interrupt cycle

An interrupt can cause the CPU to temporarily suspend the current program and execute an Interrupt Service Routine (ISR).

A simplified sequence is:

1. Complete the current instruction, where required by the architecture.
    
2. Save the necessary execution state.
    
3. Transfer control to the ISR.
    
4. Handle the interrupt.
    
5. Restore the state and resume the interrupted program.
    

Remember: An interrupt does not usually mean the CPU simply discards the current program.

## 2. Instruction Format

An instruction format specifies how the bits of a machine instruction are divided into fields.

A typical instruction may contain:

- Opcode: specifies the operation.
    
- Operand/address field: identifies an operand or its location.
    
- Register field: identifies a source or destination register.
    
- Addressing-mode field: specifies how to interpret an operand field.
    

Not every instruction contains all these fields.

### Example of a simplified instruction

### Illustrative 16-bit instruction

## 4 bits

Opcode

## 4 bits

Register

## 8 bits

Operand field

This is an illustrative layout, not a universal instruction format.

In this example, the total instruction length is:

\[ 4+4+8=16\text{ bits}=2\text{ bytes} \]

The opcode width determines how many distinct opcode bit patterns are possible. With 4 opcode bits, there are \(2^4=16\) possible patterns, although some may be reserved or unused.

### Types based on number of explicit addresses

|Type|Meaning|Example|
|---|---|---|
|Three-address|Three explicit operand/address fields|`ADD A, B, C`|
|Two-address|Two explicit operand/address fields|`ADD A, B`|
|One-address|One explicit address; often uses an accumulator implicitly|`ADD X`|
|Zero-address|No explicit address; often uses a stack|`ADD`|

These examples use simplified conventions. Actual assembly syntax varies across architectures.

#### Three-address instruction

`ADD A, B, C`

Meaning: \(A \leftarrow B+C\)

- A is the destination.
    
- B and C are the source operands.
    

#### Two-address instruction

`ADD A, B`

Meaning: \(A \leftarrow A+B\)

- A is both a source and destination.
    
- B is the other source.
    

#### One-address instruction

`ADD X`

In an accumulator-based machine, this may mean:

\[ ACC \leftarrow ACC+M[X] \]

Here, \(M[X]\) means the contents of memory location X.

#### Zero-address instruction

`ADD`

In a stack-based machine, this may pop two operands from the stack, add them, and push the result back.

### Instruction length

- Fixed-length instructions: instructions have a fixed size, simplifying some aspects of fetching and decoding.
    
- Variable-length instructions: instructions may have different sizes, allowing flexibility in encoding but making instruction boundaries more complex.
    

Exam trap: Zero-address does not mean zero operands. It means zero explicit address fields in the instruction.

## 3. Addressing Modes

An addressing mode defines how the CPU locates an operand or calculates its effective address (EA).

The effective address is the actual address used to access an operand in memory, when a memory address is required.

### 3.1 Immediate addressing

The operand value is included directly in the instruction.

Example:

`MOV R1, #25`

Meaning: place the constant `25` into R1.

- No separate memory read is needed to fetch the operand value itself, though the instruction must still be fetched.
    
- Useful for constants.
    
- The value is limited by the instruction's encoding.
    

Key point: The operand is the value itself, not a memory address.

### 3.2 Direct addressing

The instruction contains the memory address of the operand.

Example:

`LOAD R1, [500]`

Meaning: load the contents of memory location 500 into R1.

\[ EA=A \]

Here, \(A\) is the address field in the instruction.

Key point: The instruction directly specifies the operand's memory address.

### 3.3 Indirect addressing

The instruction's address field points to a location that contains the effective address of the operand.

Example:

- Address field = 500
    
- \(M[500]=800\)
    
- \(M[800]=42\)
    

The CPU uses address 500 to find address 800, then accesses the operand at address 800. The operand value is 42.

\[ EA=M[A] \]

Key point: One memory access may be needed to obtain the effective address, followed by another to fetch the operand.

### 3.4 Register addressing

The operand is stored in a CPU register named in the instruction.

Example:

`ADD R1, R2`

If `R1 = 10` and `R2 = 5`, the CPU adds the register values.

- Fast access to operands.
    
- Does not require a separate memory access to fetch the operand.
    
- Limited by the number of registers available.
    

### 3.5 Register indirect addressing

The instruction identifies a register that contains the memory address of the operand.

Example:

`LOAD R1, [R2]`

If `R2 = 800` and `M[800] = 42`, R1 receives 42.

\[ EA=(R2) \]

The parentheses here mean the contents of R2.

Difference: In register addressing, the register contains the operand. In register indirect addressing, the register contains the operand's address.

### 3.6 Indexed addressing

The effective address is calculated using an address field and an index register.

\[ EA=A+(Index\ Register) \]

Example:

- Address field = 1000
    
- Index register = 4
    
- Effective address = 1004
    

This is useful for accessing array elements and sequential data.

### 3.7 Base or displacement addressing

The effective address is calculated by adding a displacement (offset) to a base register.

\[ EA=(Base\ Register)+Displacement \]

Example:

- Base register = 2000
    
- Displacement = 12
    
- Effective address = 2012
    

This is useful for accessing fields within structures, local variables, and data blocks.

### 3.8 Relative addressing

The effective address is calculated relative to the Program Counter (PC), often for branch instructions.

\[ EA=(PC)+Displacement \]

Example:

- Relevant PC value = 1000
    
- Branch displacement = 20
    
- Target address = 1020
    

The exact PC value used (for example, the current instruction address or the next instruction address) depends on the architecture.

Key point: Relative addressing is useful for branches and position-independent code.

### 3.9 Implied or implicit addressing

The operand is implied by the instruction itself; it does not need to be explicitly specified.

Examples:

- `CLC` — clear carry flag on architectures that use this instruction.
    
- `NOP` — perform no operation.
    
- An accumulator-based instruction may implicitly use the accumulator.
    

### 3.10 Auto-increment and auto-decrement addressing

Some architectures support addressing modes that update a register automatically.

- Auto-increment: use the address in a register, then increment the register.
    
- Auto-decrement: decrement the register, then use the updated address.
    

The precise order and increment size depend on the architecture and instruction.

These modes can be useful for traversing arrays, buffers, and stacks.

## 4. Addressing modes comparison table

|Addressing mode|Where is the operand?|Simplified effective-address rule|
|---|---|---|
|Immediate|In the instruction|No operand memory EA required|
|Direct|At the specified memory address|\(EA=A\)|
|Indirect|At the address stored in memory location A|\(EA=M[A]\)|
|Register|In the specified register|Register named by instruction|
|Register indirect|In memory at the address held in a register|\(EA=(R)\)|
|Indexed|In memory at address plus index|\(EA=A+(Index)\)|
|Base/displacement|In memory at base plus offset|\(EA=(Base)+Displacement\)|
|Relative|At an address relative to the PC|\(EA=PC+Displacement\)|
|Implied|Determined by the instruction|No explicit operand address needed|

## 5. High-yield exam traps

Immediate vs direct

Immediate: `MOV R1, #25` means the value 25. Direct: `LOAD R1, [500]` means the value stored at address 500.

Register vs register indirect

Register addressing obtains the operand from the register. Register indirect obtains the operand from memory using the register's contents as an address.

Direct vs indirect

Direct: the instruction gives the operand address. Indirect: the instruction's address field leads to another address.

Instruction cycle vs machine cycle

An instruction cycle covers the processing of an instruction. A machine cycle is a lower-level operation, such as a memory read, in architectures that use this terminology.


### Final revision

- Instruction cycle: Fetch → Decode → Execute.
    
- Instruction format: Opcode + operand/address fields and possibly register or addressing-mode fields.
    
- Addressing modes: Immediate, Direct, Indirect, Register, Register indirect, Indexed, Base/displacement, Relative, and Implied.
    
- PC: next instruction address.
    
- IR: current instruction.
    
- EA: effective address of an operand in memory.
    

Next suggested topic: Computer Architecture — RISC vs CISC, pipelining, and instruction execution performance.