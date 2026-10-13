A system bus is a communication pathway that connects the CPU, main memory, and input/output (I/O) devices. It carries data, addresses, and control signals between these components.

The three main types are:

1. Data bus — carries data.
    
2. Address bus — carries addresses.
    
3. Control bus — carries control and timing signals.
    

## 1. Data Bus

The data bus transfers the actual data and instructions between the CPU, memory, and I/O devices.

- Generally bidirectional: data can travel in both directions.
    
- Its width determines how many bits can be transferred in one bus operation.
    
- A wider data bus can transfer more bits at once, all else being equal.
    

Example: A 32-bit data bus can transfer 32 bits (4 bytes) in one bus operation.

## 2. Address Bus

The address bus carries the address of the memory location or I/O device that the CPU wants to access.

- Traditionally unidirectional from the CPU to memory or I/O devices in a basic system-bus model.
    
- Its width determines the number of distinct addresses that can be represented.
    
- With \(n\) address bits, the system can represent \(2^n\) distinct addresses.
    

For example, a 16-bit address bus can represent:

\[ 2^{16}=65,536\text{ addresses} \]

If each address identifies one byte, this corresponds to 64 KiB of addressable space.

Exam trap: Address-bus width determines the addressable space; data-bus width determines how many bits can be transferred at a time.

## 3. Control Bus

The control bus carries signals that coordinate and manage operations between the CPU, memory, and I/O devices.

Common control signals include:

- Memory Read: requests data from memory.
    
- Memory Write: requests that data be written to memory.
    
- I/O Read / I/O Write: control input/output operations.
    
- Interrupt: signals a request for CPU attention.
    
- Clock: provides timing coordination in systems where clock signals are part of the bus.
    
- Bus Request / Bus Grant: may coordinate which component gets control of the bus.
    

The control bus can carry signals in different directions depending on the signal and system design.

## 4. Difference between the three buses

|Feature|Data bus|Address bus|Control bus|
|---|---|---|---|
|Main function|Transfers data|Identifies destination or source address|Coordinates operations|
|Carries|Data and instruction bits|Memory or I/O addresses|Read, write, interrupt and timing signals|
|Typical direction|Bidirectional|CPU to memory/I/O in the basic model|Depends on the signal|
|Width indicates|Bits transferred per operation|Number of representable addresses|Depends on supported control signals|
|Example|32-bit data bus|16-bit address bus|Memory Read signal|

## 5. How the system bus works

Suppose the CPU wants to read a value stored at memory address `1000`.

CPU

Address bus

CPU sends address `1000`

Control bus

CPU sends Memory Read

Data travels back to the CPU

Main Memory (RAM)

Returns the value stored at address 1000

The sequence is:

1. The CPU places address `1000` on the address bus.
    
2. The CPU issues a Memory Read signal on the control bus.
    
3. Memory places the requested value on the data bus.
    
4. The CPU receives the value.
    

For a write operation, the CPU supplies the destination address, the data to be stored, and the appropriate write-control signal.

### Last-minute revision

- Data bus = what is transferred.
    
- Address bus = where it is transferred from or to.
    
- Control bus = what operation should happen.
    
- \(n\)-bit address bus → \(2^n\) distinct addresses.
    
- 32-bit data bus → 4 bytes per full-width transfer.