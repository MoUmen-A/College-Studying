# COA Practice Exam 2: Advanced Design & Architecture

This exam is modeled after the advanced, design-heavy exam style (`26.txt`). It includes instruction format design, register tracing, logic control gates design, RPN/infix conversions, status flag calculations, control word decoding, pipeline speedup, and memory chip interfacing.

---

## Question 1: Instruction Word Format & Memory Interfacing [6 Marks]

**(a)** A computer uses a memory unit with 256K words of 32 bits each. A binary instruction code is stored in one word of memory. The instruction has four parts:
1. An indirect bit ($I$)
2. An operation code (opcode)
3. A register code part to specify one of 64 registers
4. An address part

How many bits are there in the operation code, the register code part, and the address part? Draw the instruction word format indicating the number of bits in each part. (3 Marks)

**(b)** For the memory unit described in (a), how many bits are there in the data and address inputs of the memory? (3 Marks)

### Guide Answer:

**(a) Calculation & Format:**
1. **Total Instruction Length:** The word size is 32 bits, and since an instruction is stored in one word, the instruction has **32 bits** total.
2. **Indirect Bit ($I$):** Requires **1 bit**.
3. **Register Code Part:** The system has 64 registers.
   $$\text{Register Bits} = \log_2(64) = 6\text{ bits}$$
4. **Address Part:** The memory has 256K words.
   $$256\text{K} = 256 \times 1024 = 262,144\text{ words} = 2^{18}\text{ words} \implies 18\text{ bits}$$
5. **Opcode Part:** The remaining bits are allocated to the opcode.
   $$\text{Opcode Bits} = 32\text{ total} - (1\text{ indirect} + 6\text{ register} + 18\text{ address})$$
   $$\text{Opcode Bits} = 32 - 25 = 7\text{ bits}$$

**Instruction Word Format Diagram:**
```text
 31   30           24 23         18 17                               0
+----+---------------+-------------+----------------------------------+
| I  |    Opcode     |  Register   |             Address              |
+----+---------------+-------------+----------------------------------+
|1bit|    7 bits     |   6 bits    |             18 bits              |
```

**(b) Memory Inputs:**
1. **Data Inputs:** The memory word size is 32 bits. Therefore, the memory data inputs require **32 bits** (to match the word size).
2. **Address Inputs:** The memory capacity is 256K words ($2^{18}$ addressable locations). Therefore, the memory address inputs require **18 bits**.

**Key Points to Include for Full Marks:**
- Correct calculation of register bits ($\log_2(64) = 6$) and address bits ($\log_2(256\text{K}) = 18$).
- Correct subtraction from 32 to get 7 opcode bits.
- Drawn diagram with bit-index markers (e.g., 0 to 31) showing all four sections.
- Distinction between data inputs (32 bits) and address inputs (18 bits).

**Common Mistakes to Avoid:**
- Calculating 256K address bits as 16 or 20.
- Forgetting to include the 1-bit indirect selection.
- Confusing data line count with total byte capacity.

---

## Question 2: Register-Reference Tracing [6 Marks]

**Question:**
The content of the Accumulator (AC) in a basic computer is hexadecimal `A937`, and the initial value of the overflow/extend flip-flop $E$ is `1`. The Program Counter (PC) is at hexadecimal `021`. 
Determine the contents of AC, $E$, PC, AR, and IR in hexadecimal after the execution of the following independent register-reference instructions. Note that the instruction is fetched from memory location `021` (so the initial IR contains the instruction code itself).

Assume the instruction codes are:
* **CLA** (Clear AC): Instruction code `0x7800`
* **CLE** (Clear E): Instruction code `0x7400`
* **CMA** (Complement AC): Instruction code `0x7200`

Fill in the table for each independent instruction starting from the same initial conditions:
* Initial AC = `A937`
* Initial E = `1`
* Initial PC = `021`

| Instruction | AC (Hex) | E (Bin) | PC (Hex) | AR (Hex) | IR (Hex) |
|---|---|---|---|---|---|
| **CLA** | | | | | |
| **CLE** | | | | | |
| **CMA** | | | | | |

### Guide Answer:

**Analysis of the Fetch-Decode-Execute Phase:**
1. **Fetch:**
   * `AR ← PC` $\implies$ AR gets `021`.
   * `IR ← M[AR]` $\implies$ IR gets the instruction code (e.g., `7800` for CLA).
   * `PC ← PC + 1` $\implies$ PC increments to `022`.
2. **Decode:**
   * `AR ← IR[11-0]` $\implies$ AR gets the address part of the instruction (bits 11-0 of the IR register).
     * For CLA (`7800`): address part is `800`.
     * For CLE (`7400`): address part is `400`.
     * For CMA (`7200`): address part is `200`.
3. **Execution:**
   * **CLA:** Clears AC. AC becomes `0000`. E is unaffected (`1`).
   * **CLE:** Clears E. E becomes `0`. AC is unaffected (`A937`).
   * **CMA:** Complements AC. Binary of `A937` = `1010 1001 0011 0111`. Complemented = `0101 0110 1100 1000` = `56C8`. E is unaffected (`1`).

**Final Table:**

| Instruction | AC (Hex) | E (Bin) | PC (Hex) | AR (Hex) | IR (Hex) |
|---|---|---|---|---|---|
| **CLA** | `0000` | `1` | `022` | `800` | `7800` |
| **CLE** | `A937` | `0` | `022` | `400` | `7400` |
| **CMA** | `56C8` | `1` | `022` | `200` | `7200` |

**Key Points to Include for Full Marks:**
- PC must be incremented to `022` for all instructions.
- IR must show the exact instruction code.
- AR must show the correct address portion `IR[11-0]`.
- CMA must show the correct bitwise complement of `A937` (which is `56C8`).

**Common Mistakes to Avoid:**
- Forgetting to increment the PC (leaving it as `021`).
- Forgetting that the address registers (AR) receive the lowest 12 bits of the instruction code (`IR[11-0]`) during decoding.
- Doing two instructions sequentially instead of independently.

---

## Question 3: Control Gates Design [7 Marks]

**(a)** Design the control gates for the Address Register (AR) register in a basic computer. Identify the micro-operations that load data into AR, increment AR, and clear AR, then write the logic expression for the control inputs $LD$ (load), $INR$ (increment), and $CLR$ (clear). (3 Marks)

**(b)** Show the complete logic control gate expression for the Read and Write operations of the main memory in the basic computer. (4 Marks)

*Assume standard basic computer control signals:*
* $T_0, T_1, T_2, ...$ are timing states.
* $D_0, D_1, D_2, ...$ are instruction decoders.
* $I$ is the indirect bit.
* $x$ represents the condition for register-reference or I/O instructions.

### Guide Answer:

**(a) AR Control Gates Design:**
1. **Identify Micro-operations affecting AR:**
   * **Load AR ($LD$):**
     * During Fetch: `AR ← PC` $\implies$ occurs at timing state $T_0$.
     * During Decode: `AR ← IR[11-0]` $\implies$ occurs at timing state $T_2$.
     * During Indirect address fetch: `AR ← M[AR]` $\implies$ occurs when decoder indicates indirect addressing ($D_7'\cdot I\cdot T_3$).
   * **Increment AR ($INR$):**
     * Execution of certain instructions (e.g., Increment and Skip if Zero - ISZ: `AR` is not directly incremented, but PC is. However, if there are specific micro-operations like `AR ← AR + 1` in instruction execution, they map to specific states). In the standard basic computer, $AR$ is incremented during execution of branch and save return address `BSA` at timing $T_4$ (i.e. `AR ← AR + 1`).
   * **Clear AR ($CLR$):**
     * Occurs at the start of interrupt handling: `AR ← 0` $\implies$ timing state $T_0'$ (assuming interrupt cycle control $R \cdot T_0$).

2. **Logic Control Expressions:**
   * $LD_{AR} = T_0 + T_2 + D_7' \cdot I \cdot T_3$
   * $INR_{AR} = D_6 \cdot T_4$ (for instructions like ISZ, or BSA)
   * $CLR_{AR} = R \cdot T_0$

**(b) Memory Read and Write Logic:**
1. **Memory Read ($RD$):**
   * Memory is read when instructions are fetched: `IR ← M[AR]` at timing state $T_1$.
   * Memory is read during indirect address calculation: `AR ← M[AR]` at $D_7'\cdot I\cdot T_3$.
   * Memory is read during execution of memory-reference read operations (LDA, ADD, SUB, AND) at timing state $T_4$.
     * $RD = T_1 + D_7' \cdot I \cdot T_3 + (D_0 + D_1 + D_2 + D_6) \cdot T_4$

2. **Memory Write ($WR$):**
   * Memory is written to during STORE operations (STA) at state $T_4$ or $T_5$: `M[AR] ← MBR` or `M[AR] ← AC`.
   * Memory is written to during branch and save return address (BSA) at $T_4$: `M[AR] ← PC`.
   * Memory is written to during Increment and Skip if Zero (ISZ) writeback at $T_5$: `M[AR] ← MBR`.
     * $WR = D_3 \cdot T_4 + D_5 \cdot T_4 + D_6 \cdot T_5$ (STA, BSA, ISZ depending on specific computer control states)

**Key Points to Include for Full Marks:**
- Explicit list of the micro-operations and timing states that require AR/Memory access.
- Correct boolean logic terms (use of AND ($\cdot$) and OR ($+$) gates).
- Separation of Read and Write logic.

**Common Mistakes to Avoid:**
- Missing the timing states ($T_0, T_1, T_2$).
- Mixing up read and write control conditions.

---

## Question 4: RPN & Infix Conversions [4 Marks]

**(a)** Convert the following arithmetic expressions from infix notation to Reverse Polish Notation (RPN): (2 Marks)
1. $A * B + C * D + E * F$
2. $A * B + A * (B * D + C * E)$

**(b)** Convert the following arithmetic expressions from Reverse Polish Notation (RPN) to standard Infix notation: (2 Marks)
1. $A\ B\ C\ D\ E\ +\ *\ -\ /$
2. $A\ B\ C\ D\ E\ +\ /\ -\ +$

### Guide Answer:

**(a) Infix to RPN:**
1. Expression: $A * B + C * D + E * F$
   * Terms: $(A * B)$ becomes $A\ B\ *$.
   * $(C * D)$ becomes $C\Delta D\ *$.
   * $(E * F)$ becomes $E\ F\ *$.
   * Combine terms with addition from left to right:
     * $(A * B) + (C * D) \implies A\ B\ *\ C\ D\ *\ +$
     * Add $(E * F) \implies A\ B\ *\ C\ D\ *\ +\ E\ F\ *\ +$
   * **RPN:** $A\ B\ *\ C\ D\ *\ +\ E\ F\ *\ +$

2. Expression: $A * B + A * (B * D + C * E)$
   * Parenthesis first: $(B * D + C * E) \implies B\ D\ *\ C\ E\ *\ +$
   * Multiply by $A \implies A\ B\ D\ *\ C\ E\ *\ +\ *$
   * Multiply left term: $A * B \implies A\ B\ *$
   * Add terms: $A\ B\ *\ A\ B\ D\ *\ C\ E\ *\ +\ *\ +$
   * **RPN:** $A\ B\ *\ A\ B\ D\ *\ C\ E\ *\ +\ *\ +$

**(b) RPN to Infix:**
1. Expression: $A\ B\ C\ D\ E\ +\ *\ -\ /$
   * $E + D$ is evaluated $\implies (D + E)$
   * Multiply by $C \implies C * (D + E)$
   * Subtract from $B \implies B - C * (D + E)$
   * Divide $A$ by the result:
   * **Infix:** $A / (B - C * (D + E))$

2. Expression: $A\ B\ C\ D\ E\ +\ /\ -\ +$
   * $E + D$ is evaluated $\implies (D + E)$
   * Divide $C$ by the result $\implies C / (D + E)$
   * Subtract from $B \implies B - C / (D + E)$
   * Add to $A$:
   * **Infix:** $A + (B - C / (D + E))$

**Key Points to Include for Full Marks:**
- Step-by-step resolution showing operator precedence.
- Correct placement of parentheses in the infix results.

**Common Mistakes to Avoid:**
- Changing variable order (RPN maintains operand order $A, B, C...$).
- Incorrect associativity or precedence (e.g., executing addition before multiplication).

---

## Question 5: Processor Status Flags [2 Marks]

**Question:**
An 8-bit computer contains a register $R$. Determine the values of the status flags $C$ (carry), $S$ (sign), $Z$ (zero), and $V$ (overflow) after executing each of the following independent instructions. Assume that the initial value of register $R$ is hexadecimal `72` ($0111\ 0010$ in binary). All operands are given in hexadecimal.
1. Add the immediate operand `C6` to register $R$. (1 Mark)
2. Perform a bitwise AND between register $R$ and the immediate operand `8D`. (1 Mark)

### Guide Answer:

**Initial State:** $R = \text{0x72} = 0111\ 0010_2$

**1. Instruction: Add `C6` to $R$**
* Immediate value: $\text{0xC6} = 1100\ 0110_2$
* Addition:
  ```text
    0111 0010  (0x72 = 114 in decimal)
  + 1100 0110  (0xC6 = 198 in decimal)
  -----------
  1 0011 1000  (0x138 = 312 in decimal)
  ```
* Result in 8-bit register $R$: `0x38` ($0011\ 1000_2$).
* **Flags:**
  * **$C$ (Carry):** `1` (The addition produced a carry-out of the MSB).
  * **$S$ (Sign):** `0` (The MSB of the result `0011 1000` is `0`, indicating positive).
  * **$Z$ (Zero):** `0` (The result is non-zero).
  * **$V$ (Overflow):** `0` (Adding a positive number and a negative number can never overflow). Let's verify: carry-in to MSB = 1, carry-out from MSB = 1. $V = C_{in} \oplus C_{out} = 1 \oplus 1 = 0$.

**2. Instruction: Bitwise AND with `8D`**
* Immediate value: $\text{0x8D} = 1000\ 1101_2$
* Operation:
  ```text
    0111 0010  (R)
  & 1000 1101  (0x8D)
  -----------
    0000 0000  (0x00)
  ```
* Result in $R$: `0x00` ($0000\ 0000_2$).
* **Flags:**
  * **$C$ (Carry):** `0` (Logical operations do not generate a carry).
  * **$S$ (Sign):** `0` (MSB is `0`).
  * **$Z$ (Zero):** `1` (The result is zero).
  * **$V$ (Overflow):** `0` (Logical operations do not overflow).

**Key Points to Include for Full Marks:**
- Show binary conversion of hex numbers.
- Show binary arithmetic calculation.
- Evaluate each flag individually: $C$ (carry), $S$ (sign bit), $Z$ (equality to zero), $V$ (2's complement overflow).

**Common Mistakes to Avoid:**
- Miscalculating the sign flag (treating the carry bit as the sign).
- Claiming overflow ($V$) occurs when it's simple carry ($C$). For 2's complement, overflow occurs only when two numbers of same sign yield a result of opposite sign.

---

## Question 6: Control Word Decoding [3 Marks]

**Question:**
A processor uses a 14-bit control word format to manage its internal bus and ALU. Determine the micro-operations that will be executed in the processor when the following 14-bit control words are applied.
1. `010 011 001 00101`
2. `110 000 110 00001`
3. `010 000 000 00000`

*Assume standard control word fields mapping:*
* Bits 13-11: Source Register Select (e.g., `010` = R2, `110` = PC, `000` = None)
* Bits 10-8: Destination Register Select (e.g., `011` = R3, `000` = None)
* Bits 7-5: Bus Select (e.g., `001` = Bus A, `110` = Bus B)
* Bits 4-0: ALU Operation Select (e.g., `00101` = ADD, `00001` = SHL, `00000` = NOP)

### Guide Answer:

**1. Control Word: `010 011 001 00101`**
* **Source (13-11):** `010` $\implies$ R2
* **Destination (10-8):** `011` $\implies$ R3
* **Bus (7-5):** `001` $\implies$ Bus A
* **ALU Op (4-0):** `00101` $\implies$ ADD
* **Micro-operation:** The contents of register R2 are placed on Bus A, processed by the ALU to perform addition, and stored in destination register R3. (e.g., `R3 ← R2 + [second input]` or `R3 ← R2`).

**2. Control Word: `110 000 110 00001`**
* **Source (13-11):** `110` $\implies$ PC
* **Destination (10-8):** `000` $\implies$ None (No register store)
* **Bus (7-5):** `110` $\implies$ Bus B
* **ALU Op (4-0):** `00001` $\implies$ SHL (Shift Left)
* **Micro-operation:** The contents of the PC are placed on Bus B and shifted left by the ALU, without storing the result in any destination register (often used for test/flags update).

**3. Control Word: `010 000 000 00000`**
* **Source (13-11):** `010` $\implies$ R2
* **Destination (10-8):** `000` $\implies$ None
* **Bus (7-5):** `000` $\implies$ None
* **ALU Op (4-0):** `00000` $\implies$ NOP (No operation)
* **Micro-operation:** No operation (idle state) or R2 content read without execution.

**Key Points to Include for Full Marks:**
- Decode each field based on the mapping definitions.
- Write a clear statement describing what data moves where and what operation is performed.

---

## Question 7: Pipeline Speedup & Space-Time Diagram [4 Marks]

**(a)** A non-pipelined system takes $50\text{ ns}$ to process a single task. The same task can be processed in a six-segment pipeline with a clock cycle of $10\text{ ns}$. Determine the speedup ratio of the pipeline for $100$ tasks. (2 Marks)

**(b)** Draw a space-time diagram for the six-segment pipeline showing the time it takes to process eight tasks. (2 Marks)

### Guide Answer:

**(a) Speedup Calculation:**
1. **Non-pipelined Time ($T_{np}$):**
   * To process $n=100$ tasks without a pipeline:
     $$T_{np} = n \times \text{time per task} = 100 \times 50\text{ ns} = 5000\text{ ns}$$

2. **Pipelined Time ($T_p$):**
   * Number of segments ($k$) = 6
   * Clock cycle ($t_p$) = $10\text{ ns}$
   * Formula for time to complete $n$ tasks in $k$-stage pipeline:
     $$T_p = (k + n - 1) \times t_p$$
     $$T_p = (6 + 100 - 1) \times 10\text{ ns} = 105 \times 10\text{ ns} = 1050\text{ ns}$$

3. **Speedup Ratio ($S$):**
   $$S = \frac{T_{np}}{T_p} = \frac{5000\text{ ns}}{1050\text{ ns}} \approx 4.76$$

**(b) Space-Time Diagram (6 segments, 8 tasks):**
* Vertical axis: Segments (S1 to S6)
* Horizontal axis: Clock Cycles (1 to 13)

```text
Segment | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10| 11| 12| 13|  (Cycles)
--------+---+---+---+---+---+---+---+---+---+---+---+---+---+
   S1   | T1| T2| T3| T4| T5| T6| T7| T8|   |   |   |   |   |
   S2   |   | T1| T2| T3| T4| T5| T6| T7| T8|   |   |   |   |
   S3   |   |   | T1| T2| T3| T4| T5| T6| T7| T8|   |   |   |
   S4   |   |   |   | T1| T2| T3| T4| T5| T6| T7| T8|   |   |
   S5   |   |   |   |   | T1| T2| T3| T4| T5| T6| T7| T8|   |
   S6   |   |   |   |   |   | T1| T2| T3| T4| T5| T6| T7| T8|
```
*Note: $T_i$ represents Task $i$. The pipeline is full from cycle 6 to cycle 8, and the last task (T8) completes at cycle 13.*

**Key Points to Include for Full Marks:**
- Show formulas: $T_{np} = n \cdot t_n$ and $T_p = (k + n - 1) \cdot t_p$.
- Correct numerical speedup ratio ($\approx 4.76$).
- Correctly drawn space-time diagram with labeled axes, showing tasks shifting diagonally and finishing at cycle 13.

**Common Mistakes to Avoid:**
- Using the simple $S = k$ formula (that is the theoretical limit as $n \to \infty$, not for 100 tasks).
- Drawing the tasks parallel in the diagram (which contradicts pipeline overlap).

---

## Question 8: ROM & RAM Interfacing Design [7 Marks]

**(a)** A ROM chip of size $1024 \times 8$ bits has four select inputs ($CS$) and operates from a 5-volt power supply. How many pins are needed for the IC package? Draw a block diagram showing all input and output terminals of the ROM. (2 Marks)

**(b)** A computer uses RAM chips of capacity $1024 \times 1$ bit.
1. How many chips are needed, and how should their address lines be connected to provide a memory capacity of 1024 bytes? (2 Marks)
2. How many chips are needed to provide a memory capacity of 16K bytes? (3 Marks)

### Guide Answer:

**(a) ROM Pin Count & Diagram:**
1. **Address Pins:**
   * Capacity = 1024 words ($2^{10}$ words) $\implies 10$ address lines ($A_0 - A_9$).
2. **Data Pins:**
   * Word size = 8 bits $\implies 8$ data lines ($D_0 - D_7$).
3. **Control & Selection Pins:**
   * 4 select inputs ($CS_1, CS_2, CS_3, CS_4$).
   * 1 Read/Output Enable control input ($OE$).
4. **Power Pins:**
   * 2 pins ($V_{CC}$ for 5V supply, $GND$ for ground).
5. **Total Pin Count:**
   $$\text{Total Pins} = 10\text{ (address)} + 8\text{ (data)} + 4\text{ (select)} + 1\text{ (enable)} + 2\text{ (power)} = 25\text{ pins}$$

**ROM Block Diagram:**
```text
           +---------------------+
  A0-A9    |                     |   D0-D7
=========> |                     | =========>
(10 Addr)  |                     |  (8 Data)
           |    ROM 1024 x 8     |
CS1-CS4    |                     |
---------> |                     |
(4 Select) |                     |
           |                     |
   OE      |                     |
---------> |                     |
           +----------+----------+
                      |
                   Vcc GND (Power)
```

**(b) RAM Chip Configuration:**

1. **Memory capacity of 1024 bytes (1 KB):**
   * Target memory is $1024 \times 8$ bits.
   * Chip capacity is $1024 \times 1$ bit.
   * **Number of Chips:**
     $$\text{Chips} = \frac{1024 \times 8\text{ bits}}{1024 \times 1\text{ bit}} = 8\text{ chips}$$
   * **Connection:**
     * Connect all 10 address lines ($A_0 - A_9$) in parallel to the address inputs of all 8 chips.
     * Connect each chip's single data line to a different line of the 8-bit bidirectional data bus ($D_0 - D_7$) to read/write one bit of the byte simultaneously.

2. **Memory capacity of 16K bytes (16 KB):**
   * Target memory is $16 \times 1024 \times 8\text{ bits} = 16,384 \times 8\text{ bits}$.
   * Chip capacity is $1024 \times 1$ bit.
   * **Number of Chips:**
     $$\text{Chips} = \frac{16,384 \times 8\text{ bits}}{1024 \times 1\text{ bit}} = 16 \times 8 = 128\text{ chips}$$
   * **Connection Structure:**
     * The chips are organized in a grid of 16 rows and 8 columns.
     * Each row of 8 chips provides a $1024 \times 8$ bit (1 KB) memory block.
     * $16\text{ rows} \times 1\text{ KB} = 16\text{ KB}$.
     * Address bus has 14 lines ($A_0 - A_{13}$) since $16\text{ KB} = 2^{14}$ locations:
       * Lower 10 address lines ($A_0 - A_9$) go in parallel to all 128 chips.
       * Higher 4 address lines ($A_{10} - A_{13}$) are decoded using a $4 \times 16$ decoder to enable one of the 16 rows.

**Key Points to Include for Full Marks:**
- Explicit list of pin counts (10 address, 8 data, 4 chip select, 1 enable, 2 power = 25 total).
- Labeled block diagram.
- Grid architecture calculation for RAM (e.g., 8 chips in parallel for 1KB; 128 chips with $4 \times 16$ decoder for 16KB).

**Common Mistakes to Avoid:**
- Miscounting the power pins or omitting chip select inputs from the total count.
- Dividing byte capacity by bit capacity without conversion (e.g., saying 16 chips are needed instead of 128).
