Input/Output (I/O) refers to communication between the computer and external devices such as keyboards, monitors, printers, disks, and network adapters.

The CPU and I/O devices operate at different speeds, so the computer uses different techniques to manage data transfers.

Your five topics are:

1. Programmed I/O
    
2. Interrupt-driven I/O
    
3. Direct Memory Access (DMA)
    
4. I/O modules
    
5. I/O channels
    

## 1. Programmed I/O

In Programmed I/O, the CPU controls the I/O operation by repeatedly checking the device's status and transferring data itself.

This repeated checking is called polling.

### How it works

1. CPU sends an I/O command to the device.
    
2. CPU repeatedly checks whether the device is ready.
    
3. Once the device is ready, the CPU transfers the data.
    
4. CPU continues with the next task or instruction.
    

Example: The CPU repeatedly checks whether a device is ready to provide input.

CPU

Checks status and transfers data

I/O Module

I/O Device

### Advantages and disadvantages

- Simple to implement.
    
- Does not require an interrupt for every readiness notification.
    
- Wastes CPU time if the device is slow because the CPU keeps polling.
    
- The CPU is directly involved in each data transfer.
    

Exam keyword: Polling or busy waiting.

## 2. Interrupt-driven I/O

In Interrupt-driven I/O, the CPU starts an I/O operation and can perform other work while the device operates. When the device needs attention or completes an operation, it sends an interrupt to the CPU.

### How it works

1. CPU issues an I/O command.
    
2. CPU continues executing other instructions.
    
3. The I/O device or its controller raises an interrupt when attention is required.
    
4. CPU temporarily suspends its current execution and runs an Interrupt Service Routine (ISR).
    
5. After handling the interrupt, CPU resumes the interrupted program.
    

6. CPU starts I/O

The device performs its operation.

2. CPU does other work

It need not repeatedly check the device.

3. Interrupt is raised

The CPU handles it through an ISR.

Example: A keyboard controller generates an interrupt when a key is pressed, allowing the CPU to respond without continuously polling the keyboard.

### Advantages and disadvantages

- Better CPU utilization than continuous polling in many situations.
    
- The CPU can perform other work while waiting for an I/O event.
    
- Interrupt handling introduces overhead.
    
- If the CPU must transfer every byte or word itself, large transfers can still consume substantial CPU time.
    

Exam keyword: Interrupt Service Routine (ISR).

## 3. DMA — Direct Memory Access

DMA allows an I/O device or controller to transfer a block of data directly between the device and main memory, without requiring the CPU to handle every individual data item.

The CPU usually initializes the transfer by providing information such as the memory address, transfer size, and direction.

### How DMA works

1. CPU configures the DMA controller.
    
2. DMA controller obtains access to the system bus when needed.
    
3. Data is transferred between the I/O device and main memory.
    
4. DMA controller typically interrupts the CPU when the transfer completes or requires attention.
    

CPU

Configures DMA transfer

DMA Controller

Controls the data transfer

I/O Device

Main Memory

The DMA-controlled transfer does not require the CPU to move each data item.

### Example

When a storage device reads a large block of data, DMA can transfer the block into RAM. The CPU can do other work while the transfer proceeds, subject to bus and memory contention.

### DMA transfer modes

|Mode|Explanation|
|---|---|
|Burst or block mode|Transfers a block of data in a burst, potentially occupying the bus during the burst|
|Cycle stealing|DMA takes individual bus cycles that might otherwise be used by the CPU|
|Transparent mode|DMA transfers when the bus can be used without interfering with CPU bus activity, according to the implementation|

### Advantages

- Reduces CPU involvement in bulk data transfers.
    
- Often improves throughput for large transfers.
    
- Frees the CPU to execute other instructions during transfer.
    

Exam keyword: Block transfer with reduced CPU involvement.

Important: DMA does not mean the CPU is never involved. The CPU normally sets up the operation and may handle completion interrupts.

## 4. I/O Modules

An I/O module is the hardware interface between the system bus and an external I/O device. It allows the CPU and operating system to communicate with devices that may use different speeds, data formats, and control mechanisms.

### Main functions of an I/O module

- Control and timing: coordinates I/O operations.
    
- Communication with the CPU: receives commands and exchanges status information.
    
- Communication with devices: sends commands and receives device responses.
    
- Data buffering: temporarily holds data to accommodate speed differences.
    
- Error detection: detects and reports certain transfer or device errors.
    

### Common I/O module registers

|Register|Purpose|
|---|---|
|Data register|Holds data being transferred|
|Status register|Indicates whether the device is ready, busy, or has an error|
|Control/command register|Holds commands or configuration information|

These are common logical functions; the exact register arrangement varies by device.

Example: A storage controller communicates with the CPU and manages operations involving a storage drive.

Exam trap: An I/O module is an interface/controller; it is not the external device itself.

## 5. I/O Channels

An I/O channel is a specialized hardware mechanism, traditionally found in mainframe and larger computer systems, that can manage I/O operations with less continuous CPU intervention.

An I/O channel can execute channel commands and coordinate transfers between peripheral devices and memory, depending on the system architecture.

### Functions

- Manages I/O operations.
    
- Executes I/O-related commands in channel-based architectures.
    
- Reduces the CPU's direct involvement in device control.
    
- Can coordinate multiple I/O operations or devices, depending on its capabilities.
    

### I/O channel vs I/O module

|Feature|I/O module|I/O channel|
|---|---|---|
|Main role|Interfaces the system bus with a device|Manages I/O operations more independently|
|Typical scope|Device communication and control|Higher-level coordination of I/O operations|
|CPU involvement|Depends on the transfer technique|Designed to reduce ongoing CPU involvement|
|Typical association|General-purpose computer systems|Traditionally larger systems and mainframes|

Remember: An I/O channel is more than simply a cable or physical bus. It is a mechanism capable of managing I/O operations.

## 6. Most important comparison: Programmed I/O vs Interrupt-driven I/O vs DMA

This comparison is particularly useful for objective exam questions.

|Feature|Programmed I/O|Interrupt-driven I/O|DMA|
|---|---|---|---|
|Who checks device status?|CPU repeatedly polls|Device/controller can notify CPU through interrupts|DMA/controller manages the configured transfer|
|CPU involvement|High|Lower while waiting; may be high during data transfer|Low for individual data items|
|Data transfer|CPU transfers data|CPU typically transfers data in the ISR or associated handler|DMA-controlled transfer between device and memory|
|CPU can do other work while waiting?|Often limited by polling|Yes|Yes, during the transfer, subject to contention|
|Best suited for|Simple or small transfers|Event-driven or modest I/O operations|Bulk data transfers|
|Main drawback|Wastes time polling|Interrupt and handling overhead|Setup complexity and bus contention|

### Easy memory trick

- Programmed I/O: CPU keeps checking.
    
- Interrupt-driven I/O: device/controller signals the CPU.
    
- DMA: controller transfers the block with minimal CPU involvement.
## Final revision checklist

Before moving to the next Computer Architecture topic, make sure you can explain:

- Why programmed I/O uses polling.
    
- How interrupts reduce repeated polling.
    
- How DMA transfers data between devices and memory.
    
- The roles of data, status, and control registers in an I/O module.
    
- The difference between an I/O module and an I/O channel.
    
- The differences among programmed I/O, interrupt-driven I/O, and DMA.
    

Next suggested topic: Instruction formats, instruction cycle, and addressing modes.