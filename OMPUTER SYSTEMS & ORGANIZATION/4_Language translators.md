# LANGUAGE TRANSLATORS — DSSSB TGT COMPUTER SCIENCE

Language translators are system software that convert a program from one language or representation into another so that it can be executed by a computer or processed by another software tool.

The three important language translators are:

1. **Assembler**
    
2. **Compiler**
    
3. **Interpreter**
    

**Important exam areas:** Definitions, input and output, translation process, error handling, and differences between translators.

## 1. Assembler

An **assembler** converts an assembly-language program into machine code.

Assembly language uses symbolic instructions such as `MOV`, `ADD`, and `SUB`, while machine code consists of binary-encoded instructions that the processor can execute.

### Example

```
MOV A, 5
ADD A, 3
```

An assembler translates valid assembly instructions into corresponding machine-code instructions for the target processor.

### Important points

- **Input:** Assembly language.
    
- **Output:** Machine code or an object file containing machine code and related information.
    
- Uses mnemonic instructions and symbolic names.
    
- Is specific to an instruction set or target architecture.
    
- Reports errors such as invalid mnemonics or incorrect operands.
    

**Remember:** Assembler = Assembly language → Machine code.

## 2. Compiler

A **compiler** translates a program written in a high-level programming language into another representation, often machine code or object code, before the resulting program is executed.

Languages such as C and C++ are commonly compiled to native machine code. Java commonly compiles source code into bytecode, which runs on the Java Virtual Machine (JVM).

### Basic compilation process

<box border radius="lg" padding={3} gap={2} align="center"> <box background="surface-secondary" radius="md" padding={3} width="100%" align="center"> **High-level source code**

```
<text color="secondary" size="sm">Example: C program</text>
```

</box> <icon name="arrow-down" size="lg" /> <box background="surface" border radius="md" padding={3} width="100%" align="center"> **Compiler**

```
<text color="secondary" size="sm">Translates and reports detected errors</text>
```

</box> <icon name="arrow-down" size="lg" /> <box background="surface-secondary" radius="md" padding={3} width="100%" align="center"> **Target code**

```
<text color="secondary" size="sm">Machine code, object code, or bytecode</text>
```

</box> <icon name="arrow-down" size="lg" /> <box background="surface" border radius="md" padding={3} width="100%" align="center"> **Execution**

```
<text color="secondary" size="sm">Runs through the appropriate execution environment</text>
```

</box> </box>

### Important points

- **Input:** Source code in a high-level language.
    
- **Output:** Target code, which may be machine code, object code, or an intermediate representation.
    
- Typically translates a larger program or compilation unit before execution.
    
- Can perform optimizations.
    
- Reports errors detected during compilation. The program must meet the compiler's requirements to produce the required target output.
    

**Remember:** Compiler = translates source code into target code before that code is executed.

## 3. Interpreter

An **interpreter** executes a program by interpreting its instructions or an intermediate representation at runtime.

In introductory computer-fundamentals questions, an interpreter is often described as translating and executing a program statement by statement. This is a useful basic model, although modern interpreters may use bytecode, runtime optimization, or other techniques.

Python and JavaScript commonly use interpreter-based or hybrid execution environments, depending on the implementation.

### Basic execution process

<box border radius="lg" padding={3} gap={2} align="center"> <box background="surface-secondary" radius="md" padding={3} width="100%" align="center"> **Source code or intermediate representation** </box> <icon name="arrow-down" size="lg" /> <box background="surface" border radius="md" padding={3} width="100%" align="center"> **Interpreter / runtime**

```
<text color="secondary" size="sm">Interprets instructions and performs operations</text>
```

</box> <icon name="arrow-down" size="lg" /> <box background="surface-secondary" radius="md" padding={3} width="100%" align="center"> **Program execution and output** </box> </box>

### Important points

- **Input:** Source code or an intermediate representation, depending on the implementation.
    
- Executes operations through an interpreter or runtime.
    
- May report errors when the relevant code is reached during execution.
    
- Does not necessarily create a standalone native executable.
    
- Many modern language implementations combine compilation and interpretation.
    

**Remember:** Interpreter = executes instructions through an interpreting runtime.

## 4. Compiler vs. Interpreter vs. Assembler

|Feature|Assembler|Compiler|Interpreter|
|---|---|---|---|
|Main input|Assembly language|High-level source code or another source representation|Source code or intermediate representation|
|Main role|Translates assembly instructions|Translates source code into target code|Executes by interpreting instructions|
|Typical output|Machine code / object file|Machine code, object code, bytecode, or intermediate code|Program behavior and output during execution|
|Execution model|Generated code is executed|Generated target code is executed by an appropriate environment|Instructions are interpreted at runtime|
|Error reporting|Assembly syntax and instruction errors|Errors detected during compilation|Errors may appear when relevant code executes|
|Common examples|NASM, GNU assembler|GCC, Clang|CPython runtime, many JavaScript execution environments|

### The most important distinction

- **Assembler:** Assembly language → Machine code.
    
- **Compiler:** Translates source code into target code.
    
- **Interpreter:** Executes instructions through an interpreting runtime.
    

Avoid assuming that every compiler produces native machine code or that every interpreter executes raw source text one line at a time. These are simplified textbook descriptions, not universal implementation rules.

## 5. Example to Understand the Difference

Suppose you want a computer to add two numbers.

### A. Assembly language

```
MOV R1, 5
ADD R1, 3
```

An assembler translates the assembly instructions into machine-code instructions for the relevant processor.

### B. High-level language — C

```
int result = 5 + 3;
```

A compiler can translate the C program into target code before execution.

### C. Interpreted execution — Python

```
result = 5 + 3
print(result)
```

A Python runtime executes the program through its language implementation, which commonly includes compilation to bytecode and interpretation.

All three approaches can ultimately produce the result `8`, but their translation and execution processes differ.

## 6. Quick Revision Sheet

|Concept|Remember|
|---|---|
|Assembler|Assembly language to machine code|
|Compiler|Source code to target code|
|Interpreter|Executes instructions through an interpreting runtime|
|Compiler output|May be machine code, object code, or bytecode|
|Assembly language|Uses mnemonics such as `MOV`, `ADD`, and `SUB`|
|Machine code|Binary-encoded instructions for a processor|
|Compilation|May include code optimization|
|Interpretation|Executes instructions through a runtime|
|Java compilation|Java source code is commonly compiled into bytecode|
|Python execution|Commonly involves bytecode and an interpreter|

## 7. Important DSSSB Exam Traps

1. An assembler translates **assembly language** into machine code.
    
2. A compiler translates source code into target code.
    
3. An interpreter executes instructions through an interpreting runtime.
    
4. A compiler may produce bytecode rather than native machine code.
    
5. Java source code is commonly compiled into JVM bytecode.
    
6. Python execution is not necessarily direct, raw-source interpretation; CPython commonly compiles source into bytecode first.
    
7. Assemblers are associated with assembly-language mnemonics.
    
8. Compilers can perform code optimization.
    
9. An interpreter may report an error when the relevant instruction or code is executed.
    
10. The compiler-versus-interpreter distinction is useful for basic MCQs, but real language implementations may combine both approaches.