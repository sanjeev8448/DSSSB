
These notes cover eight important topics, including truth tables, Boolean expressions, worked examples, important differences, and exam-focused facts.

**Revision priority:** Half adder and full adder, multiplexers and demultiplexers, encoders and decoders, flip-flops, and combinational versus sequential circuits.

# 1. Half Adder

A half adder is a combinational logic circuit that adds two 1-bit binary inputs, A and B, and produces two outputs: Sum (S) and Carry (C).

- Sum represents the least significant bit of the addition.
    
- Carry represents the bit carried into the next binary position.
    

## Boolean Expressions

Sum: S = A ⊕ B

Carry: C = A · B = AB

Here, ⊕ denotes XOR and · denotes AND.

## Truth Table

|A|B|Sum (S)|Carry (C)|
|---|---|---|---|
|0|0|0|0|
|0|1|1|0|
|1|0|1|0|
|1|1|0|1|

## Gate Implementation

- One XOR gate generates the Sum.
    
- One AND gate generates the Carry.
    

Example: 1 + 1 = 10₂.

Therefore, Sum = 0 and Carry = 1.

**Limitation:** A half adder has no carry-in input, so it cannot directly add three input bits.

# 2. Full Adder

A full adder adds three 1-bit inputs: A, B, and carry-in (Cᵢₙ). It produces Sum (S) and carry-out (Cₒᵤₜ).

## Boolean Expressions

Sum: S = A ⊕ B ⊕ Cᵢₙ

Carry-out:

Cₒᵤₜ = AB + ACᵢₙ + BCᵢₙ

An equivalent expression is:

Cₒᵤₜ = AB + Cᵢₙ(A ⊕ B)

## Truth Table

|A|B|Cᵢₙ|S|Cₒᵤₜ|
|---|---|---|---|---|
|0|0|0|0|0|
|0|0|1|1|0|
|0|1|0|1|0|
|0|1|1|0|1|
|1|0|0|1|0|
|1|0|1|0|1|
|1|1|0|0|1|
|1|1|1|1|1|

## Implementation Using Two Half Adders

**Half Adder 1**

Inputs: A, B

Outputs:

S₁ = A ⊕ B

C₁ = AB

**Half Adder 2**

Inputs: S₁, Cᵢₙ

Outputs:

S = S₁ ⊕ Cᵢₙ

C₂ = S₁Cᵢₙ

**Final carry:**

Cₒᵤₜ = C₁ + C₂

An OR gate combines the two carry outputs.

Thus, a full adder can be built using two half adders and one OR gate.

## Worked Example

Calculate the output when A = 1, B = 1, and Cᵢₙ = 1.

Sum:

S = 1 ⊕ 1 ⊕ 1 = 1

Carry-out:

Cₒᵤₜ = (1 × 1) + (1 × 1) + (1 × 1) = 1

The result is 11₂, which represents decimal 3.

## Half Adder vs Full Adder

|Feature|Half Adder|Full Adder|
|---|---|---|
|Inputs|2|3|
|Outputs|Sum and Carry|Sum and Carry-out|
|Carry-in|No|Yes|
|Truth-table rows|4|8|
|Typical construction|XOR + AND|Two half adders + OR|

**Exam trap:** A full adder's carry-out is 1 whenever at least two of its three inputs are 1.

# 3. Multiplexer (MUX)

A multiplexer is a combinational circuit that selects one of several data inputs and forwards it to a single output. It is also called a **data selector**.

For n selection lines, a standard MUX can select among 2ⁿ inputs.

Number of inputs = 2ⁿ

## Important MUX Sizes

|MUX|Data Inputs|Select Lines|Output|
|---|---|---|---|
|2:1|2|1|1|
|4:1|4|2|1|
|8:1|8|3|1|
|16:1|16|4|1|

## 2:1 MUX

Inputs: I₀ and I₁

Select line: S

Output: Y

### Selection Table

|S|Output|
|---|---|
|0|I₀|
|1|I₁|

### Boolean Expression

Y = S′I₀ + SI₁

## 4:1 MUX Selection Table

|S₁|S₀|Output|
|---|---|---|
|0|0|I₀|
|0|1|I₁|
|1|0|I₂|
|1|1|I₃|

For a 4:1 MUX, two select lines are sufficient because 2² = 4.

## Applications

- Data routing
    
- Communication systems
    
- Processor datapaths
    
- Implementing Boolean functions
    

**Exam shortcut:** A MUX selects one input from many inputs and sends it to one output.

# 4. Demultiplexer (DEMUX)

A demultiplexer takes one data input and routes it to one of several outputs based on the select lines. It is also called a **data distributor**.

For n select lines, a standard DEMUX has 2ⁿ outputs.

## 1:4 DEMUX

Inputs: Data D and select lines S₁, S₀.

The following table assumes an active-high data input and active-high outputs.

|S₁|S₀|Y₀|Y₁|Y₂|Y₃|
|---|---|---|---|---|---|
|0|0|D|0|0|0|
|0|1|0|D|0|0|
|1|0|0|0|D|0|
|1|1|0|0|0|D|

## MUX vs DEMUX

|Feature|MUX|DEMUX|
|---|---|---|
|Main function|Selects one input|Selects one output path|
|Data inputs|Many|One|
|Data outputs|One|Many|
|Select lines|Choose input|Choose output|
|Analogy|Many roads merge into one|One road branches into many|

**Memory trick:** MUX = many to one; DEMUX = one to many.

# 5. Encoder

An encoder is a combinational circuit that converts an active input line into a coded binary output.

For a standard encoder with 2ⁿ input lines, the output has n bits.

2ⁿ input lines → n output bits

## 4-to-2 Encoder

Assume exactly one input is HIGH at a time.

|Active Input|Y₁|Y₀|
|---|---|---|
|D₀ = 1|0|0|
|D₁ = 1|0|1|
|D₂ = 1|1|0|
|D₃ = 1|1|1|

The output is the binary code corresponding to the active input's index.

## Boolean Expressions

Y₁ = D₂ + D₃

Y₀ = D₁ + D₃

These expressions assume only one input is active.

## Priority Encoder

A normal encoder may give ambiguous results if multiple inputs are HIGH. A priority encoder resolves this by assigning priority to particular inputs.

Example: If D₃ has the highest priority and both D₁ and D₃ are HIGH, the encoder produces the code for D₃.

## Applications

- Keyboard encoding
    
- Interrupt handling
    
- Converting input signals into binary codes
    

**Exam shortcut:** An encoder converts an active input line into a binary code.

# 6. Decoder

A decoder converts an n-bit binary input into one of up to 2ⁿ output lines.

In a standard active-high decoder, exactly one output is HIGH for each valid input combination.

n input bits → 2ⁿ outputs

## 2-to-4 Decoder

|A|B|Y₀|Y₁|Y₂|Y₃|
|---|---|---|---|---|---|
|0|0|1|0|0|0|
|0|1|0|1|0|0|
|1|0|0|0|1|0|
|1|1|0|0|0|1|

## Boolean Expressions

Y₀ = A′B′

Y₁ = A′B

Y₂ = AB′

Y₃ = AB

## Encoder vs Decoder

|Feature|Encoder|Decoder|
|---|---|---|
|Conversion|Active input to binary code|Binary code to output line|
|Typical example|4-to-2|2-to-4|
|Number of lines|More inputs than outputs|More outputs than inputs|
|Applications|Keyboard, interrupts|Memory address selection, display circuits|

**Exam trap:** A decoder does not simply reverse every encoder in every practical situation. Priority handling, enable inputs, and output polarity can differ.

# 7. Flip-Flops

A flip-flop is a bistable sequential circuit that stores one bit of information. Its output depends on its input and its previous state, according to its triggering and control rules.

Flip-flops are fundamental building blocks of registers, counters, and memory circuits.

## A. SR (Set–Reset) Flip-Flop

- S = 1, R = 0: Set Q = 1.
    
- S = 0, R = 1: Reset Q = 0.
    
- S = 0, R = 0: Hold the previous state.
    
- S = 1, R = 1: Forbidden or invalid for the conventional active-high NOR-based SR latch.
    

## B. D (Data or Delay) Flip-Flop

At the active clock edge, the output takes the value of D.

Q(next) = D

It avoids the forbidden input combination of the conventional SR flip-flop.

## C. JK Flip-Flop

It improves on the conventional SR flip-flop by defining the case J = K = 1 as toggle.

|J|K|Next State|
|---|---|---|
|0|0|Hold|
|0|1|Reset|
|1|0|Set|
|1|1|Toggle|

## D. T (Toggle) Flip-Flop

|T|Next State|
|---|---|
|0|Hold|
|1|Toggle|

Characteristic equation:

Q(next) = T ⊕ Q

T flip-flops are frequently used in counter designs.

## Characteristic Table: All Four Types

The following table assumes that inputs are sampled at the active triggering event and ignores asynchronous preset/clear controls.

|Flip-Flop|Inputs|Next State|
|---|---|---|
|SR|S = 0, R = 0|Q|
|SR|S = 0, R = 1|0|
|SR|S = 1, R = 0|1|
|SR|S = 1, R = 1|Invalid for conventional SR|
|D|D = 0|0|
|D|D = 1|1|
|JK|J = 0, K = 0|Q|
|JK|J = 0, K = 1|0|
|JK|J = 1, K = 0|1|
|JK|J = 1, K = 1|Q′|
|T|T = 0|Q|
|T|T = 1|Q′|

## Important Concepts

- **Clock:** A timing signal used to coordinate state changes.
    
- **Active clock edge:** The rising or falling edge on which an edge-triggered flip-flop samples its input.
    
- **Present state:** The current output state Q.
    
- **Next state:** The output state after the triggering event.
    
- **Race-around condition:** In a level-triggered JK flip-flop, when J = K = 1 and the clock pulse is too wide, the output may toggle repeatedly. A master–slave or edge-triggered design avoids this repeated-toggle problem under its intended operating conditions.
    

## Flip-Flop Applications

- Registers: Store multiple bits.
    
- Counters: Count clock pulses.
    
- Frequency division: A T flip-flop, or a JK flip-flop with J = K = 1, can divide the clock frequency by 2 under the usual triggering conditions.
    
- State machines: Store the current state of a sequential system.
    

**Exam traps:**

- D copies its input at the active clock edge.
    
- JK toggles when both inputs are 1.
    
- T toggles when its input is 1.
    
- A flip-flop stores one bit.
    

# 8. Sequential Circuits

A sequential circuit is a digital circuit whose output depends on its current inputs and its stored state (past information).

In contrast, a combinational circuit's output depends only on its current inputs.

## Combinational vs Sequential Circuits

|Feature|Combinational|Sequential|
|---|---|---|
|Output depends on|Current inputs|Current inputs and previous state|
|Memory|No internal state memory|Has stored state|
|Clock|Not inherently required|Commonly clocked; asynchronous designs also exist|
|Feedback|Not required|Often present|
|Examples|Adders, MUX, decoder|Registers, counters, state machines|

## Types of Sequential Circuits

### 1. Synchronous Sequential Circuits

State changes are coordinated by a clock, typically at a specified clock edge.

Examples: Edge-triggered registers and synchronous counters.

### 2. Asynchronous Sequential Circuits

State changes can occur in response to input changes without waiting for a common clock edge.

Examples: Certain asynchronous control circuits and ripple counters.

## Registers and Counters

- **Register:** A collection of flip-flops used to store a multi-bit value. An 8-bit register typically uses 8 one-bit storage elements.
    
- **Counter:** A sequential circuit that advances through a sequence of states in response to clock events.
    
- **Shift register:** A register that shifts stored bits left or right under control of clock signals.
    

## Worked Example: 3-Bit Binary Counter

A 3-bit binary counter has 2³ = 8 possible states.

|Count|Q₂Q₁Q₀|
|---|---|
|0|000|
|1|001|
|2|010|
|3|011|
|4|100|
|5|101|
|6|110|
|7|111|
|Next|000|

It cycles through 8 states, so it is a mod-8 counter.

A binary counter with n bits can represent 2ⁿ distinct states.

# 9. Quick Revision Table

|Topic|Key Fact to Remember|
|---|---|
|Half adder|2 inputs; XOR Sum, AND Carry|
|Full adder|3 inputs, including carry-in|
|MUX|Many inputs to one output|
|DEMUX|One input to many possible outputs|
|Encoder|2ⁿ input lines to n code bits|
|Decoder|n input bits to up to 2ⁿ outputs|
|Flip-flop|Stores 1 bit|
|Sequential circuit|Output depends on input and stored state|

## Final Exam Preparation Checklist

- Memorize half-adder and full-adder truth tables.
    
- Practise the Sum and Carry expressions.
    
- Learn MUX and DEMUX selection tables.
    
- Understand encoder and decoder input-output relationships.
    
- Memorize SR, D, JK, and T flip-flop operations.
    
- Understand the race-around condition.
    
- Differentiate combinational and sequential circuits.
    
- Practise counter states and mod-N concepts.
    

Note: The provided source ends just as the model practice quiz begins, so its actual quiz questions were not included in these notes.