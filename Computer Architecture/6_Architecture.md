RISC and CISC are two major approaches to designing a CPU's instruction set. For the DSSSB exam, focus on their full forms, instruction complexity, instruction length, addressing modes, execution characteristics, pipelining, and examples of processors.

## 1. RISC — Reduced Instruction Set Computer

RISC is a CPU design approach that emphasizes a relatively simple instruction set, often allowing instructions to execute efficiently with streamlined hardware.

![File:MIPS Architecture (Pipelined).svg - Wikimedia Commons](https://images.openai.com/static-rsc-4/ASN1f0p3h1-idzL-ybowpF3m-FQNP4C7nSMxZKsPjA9u7c9vm60I2k_xnQ1BddpQFtGjcCTql8xG7PeN23UekejYgG9PyIVAMr7CQdQQFrPsKbtm27WyHA3iv3hWU7XE8o2NlRc6pYzOls4vulDQZXX3dOsMneqa0Lm7APLKCO8?purpose=inline)

[commons.wikimedia.org](https://commons.wikimedia.org/wiki/File%3AMIPS_Architecture_%28Pipelined%29.svg)

Key characteristics

- Relatively simple instructions.
    
- Often uses fixed-length instruction encoding.
    
- Typically has many general-purpose registers.
    
- Commonly follows a load/store design: memory is accessed mainly through load and store instructions.
    
- Designed to support efficient pipelining.
    
- Many instructions can complete in one clock cycle in simplified textbook models, though real execution varies.
    
- May require more instructions to complete some tasks than a CISC design.
    

Examples: ARM, RISC-V, and MIPS are common RISC-family examples.

### Example

Suppose a processor needs to add two values stored in memory.

A simplified RISC-style sequence could be:

```
LOAD R1, [A]
LOAD R2, [B]
ADD  R3, R1, R2
STORE [C], R3
```

The processor loads the values into registers, adds them, and stores the result. This illustrates the load/store approach.

## 2. CISC — Complex Instruction Set Computer

CISC is a CPU design approach that provides a comparatively rich instruction set, including instructions that may perform several lower-level operations.

![The Shift from x86 to ARM in Laptops and Desktops: What's Driving the Trend?](https://images.openai.com/static-rsc-4/nByYHbIvv2yjqg6TouLwGN5FjtCTKdijx2YAzHRTh2pQi0fLlNiMT9nVdbADXF_wz5PtNTQQ2n3pAJHoZO8pTmYwq4j0PdZmtZjWqlNUQi8FlKbftukHqOkGq8wElIHuO7rl1e3Pa8gknatVcrd82YzAFHPEL9ds_33GLjt9FL0?purpose=inline)

[linkedin.com](https://www.linkedin.com/pulse/shift-from-x86-arm-laptops-desktops-whats-driving-trend-p-m-5ouic)

Key characteristics

- A relatively large and complex instruction set.
    
- Often supports variable-length instructions.
    
- May support many addressing modes.
    
- Some instructions can operate directly on memory operands.
    
- Complex instructions may require multiple internal steps or micro-operations.
    
- Instruction decoding can be more complex.
    
- A single instruction may perform work that takes several simpler instructions in another architecture.
    

Examples: Intel x86 and AMD64 (x86-64) are commonly classified as CISC instruction-set architectures.

### Example

A hypothetical CISC-style instruction might combine a memory operand and arithmetic operation:

```
ADD [A], 5
```

In an architecture that supports this form, the instruction could read the value at address A, add 5, and write the result back. The exact syntax and behavior depend on the instruction set.

## 3. RISC vs CISC: Important comparison table

|Feature|RISC|CISC|
|---|---|---|
|Full form|Reduced Instruction Set Computer|Complex Instruction Set Computer|
|Instruction set|Relatively simple|Relatively complex|
|Instruction length|Often fixed-length|Often variable-length|
|Addressing modes|Typically fewer|Traditionally more|
|Memory operations|Usually load/store instructions|May allow arithmetic directly on memory operands|
|Registers|Typically many general-purpose registers|Depends on architecture|
|Instruction decoding|Often simpler|Often more complex|
|Pipelining|Often easier to design in traditional implementations|Can require more complex decoding and sequencing|
|Code size|May require more instructions for some tasks|Complex instructions may reduce instruction count|
|Execution time|Depends on implementation and workload|Depends on implementation and workload|
|Examples|ARM, RISC-V, MIPS|x86, x86-64|

Important exam note: These are traditional design tendencies, not absolute rules. Modern RISC and CISC processors have adopted techniques from one another. For example, modern x86 processors often translate complex instructions into simpler internal micro-operations.

## 4. Advantages and disadvantages

### RISC

Advantages

- Simpler instruction decoding in many designs.
    
- Efficient pipelining is often easier to implement.
    
- Load/store architecture gives a regular approach to memory access.
    

Limitations

- Some tasks may require more instructions.
    
- More instructions do not automatically mean slower execution; implementation matters.
    
    ### CISC
    
    Advantages
    
- Complex instructions can perform multiple operations.
    
- May achieve compact machine-code programs for some tasks.
    
- Provides flexible instruction and addressing options.
    

Limitations

- Complex instruction decoding can require more hardware.
    
- Instruction execution may involve multiple internal steps.
    

## 5. Common DSSSB exam traps

- RISC stands for Reduced Instruction Set Computer, not Reduced Instruction Speed Computer.
    
- CISC stands for Complex Instruction Set Computer.
    
- ARM and RISC-V are examples of RISC architectures.
    
- x86 and x86-64 are examples of CISC architectures.
    
- RISC is commonly associated with load/store architecture.
    
- CISC traditionally supports more complex instructions and variable-length encoding.
    
- RISC does not mean every instruction always executes in one clock cycle.
    
- CISC does not mean every instruction is slow.
    
- RISC does not always produce larger programs, and CISC does not always execute programs faster.
Quick revision: RISC = simpler instructions, load/store design, ARM and RISC-V. CISC = more complex instructions, often variable-length encoding, x86 and x86-64.