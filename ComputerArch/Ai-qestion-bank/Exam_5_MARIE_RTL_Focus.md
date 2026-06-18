# COA Practice Exam 5: MARIE Architecture & RTL Deep Dive

This exam focuses on the MARIE architecture, register details, RTL notation precision, and instruction execution tracing. Modeled after a mix of `25.txt` essay style and `26.txt` RTL precision.

---

## Topic Summary

This exam covers the following core concepts from the COA course:

- **MARIE Architecture Overview:** MARIE is a simple hypothetical computer with a stored-program concept, binary two's complement representation, and 4K×16-bit word-addressable memory.
- **Seven Registers:** AC (16-bit accumulator), MAR (12-bit address register), MBR (16-bit data buffer), PC (12-bit program counter), IR (16-bit instruction register), InREG (8-bit input), OutREG (8-bit output).
- **Instruction Format:** 16-bit instructions split into a 4-bit opcode (IR[15–12]) and a 12-bit address field (IR[11–0]). This allows up to 16 instructions and 4K addressable words.
- **Fetch-Decode-Execute Cycle (RTL):**
  - **Fetch:** `MAR ← PC` then `IR ← M[MAR], PC ← PC + 1`
  - **Decode:** `MAR ← IR[11-0]`, decode `IR[15-12]`
  - **Execute:** Depends on the instruction (LOAD, STORE, ADD, SUBT, etc.)
- **Key RTL Sequences:**
  - **LOAD X:** `MBR ← M[MAR]; AC ← MBR`
  - **STORE X:** `MAR ← X, MBR ← AC; M[MAR] ← MBR`
  - **ADD X:** `MBR ← M[MAR]; AC ← AC + MBR`
  - **SUBT X:** `MBR ← M[MAR]; AC ← AC − MBR`
- **Direct vs. Indirect Addressing:** Direct = 1 memory access in execute; Indirect (LOADI, STOREI, ADDI) = 2 memory accesses (read pointer, then access data).
- **Word-Addressable:** PC increments by 1 (not 2 or 4) because each address refers to one 16-bit word.
- **MBR–AC Connection:** A direct dedicated path exists between MBR and AC, bypassing the main bus.

---

## How to Solve Questions in This Exam

### RTL Trace Questions (Q6, Q7, Q8)
These are the highest-value questions. Follow this step-by-step method:

1. **Always start with the Fetch phase:**
   - Write `MAR ← PC` (copy PC value into MAR).
   - Write `IR ← M[MAR], PC ← PC + 1` (read instruction from memory, increment PC by **1**).
   - **Tip:** PC increments by 1 because MARIE is word-addressable. This is the #1 tested detail.

2. **Decode phase:**
   - Extract the lower 12 bits of IR → `MAR ← IR[11-0]`.
   - Identify the opcode from the upper 4 bits → `Decode IR[15-12]`.
   - **Tip:** Convert the hex instruction to binary, split into 4-bit opcode + 12-bit address.

3. **Execute phase** — depends on the instruction:
   - **LOAD:** `MBR ← M[MAR]` then `AC ← MBR` (AC gets the memory value).
   - **ADD:** `MBR ← M[MAR]` then `AC ← AC + MBR` (adds to AC, does NOT replace).
   - **SUBT:** `MBR ← M[MAR]` then `AC ← AC − MBR` (subtracts MBR **from** AC).
   - **STORE:** `MAR ← X, MBR ← AC` (same line!) then `M[MAR] ← MBR`.
   - **LOADI:** Extra steps: `MBR ← M[MAR]`, `MAR ← MBR`, `MBR ← M[MAR]`, `AC ← MBR`.

4. **After tracing, fill in the register table:**
   - Track PC, IR, MAR, MBR, AC after each instruction.
   - For multi-instruction traces (Q7), carry forward the register values from the previous instruction.

### Essay / Short Answer Questions (Q1–Q5)
- **Register questions:** Memorize all 7 registers with exact bit-widths. Key trap: MAR and PC are 12-bit, not 16-bit.
- **"Why" questions:** Always tie your answer to MARIE being word-addressable, having a fixed 16-bit instruction format, or having specific hardware paths.
- **Trade-off questions (Q5):** Use the formula $2^n$ to show how changing opcode/address bits affects instruction count and memory size.

### Fill-in-the-Blank Questions (Q9–Q13)
- Focus on exact terminology: MBR, PC, word-addressable, IR[15–12], IR[11–0].
- Pay attention to "next" vs. "current" — PC holds the **next** instruction address; IR holds the **current** instruction.

### True/False Questions (Q14–Q23)
- Read carefully for subtle word changes (e.g., "replaces" vs. "adds to" for ADD).
- Common traps: PC and MAR are 12-bit (not 16); InREG/OutREG are 8-bit; LOADI needs more cycles than LOAD.
- Always justify with a one-sentence explanation referencing the specific architectural detail.

---

## Part 1: Essay Questions [10 Marks]

### Q1 — Short Answer / Essay | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**
List all seven registers in the MARIE architecture. For each register, state its bit-width and its specific purpose.

**Guide Answer:**

| Register | Size | Purpose |
|---|---|---|
| AC (Accumulator) | 16-bit | Holds one operand or the result of ALU operations |
| MAR (Memory Address Register) | 12-bit | Holds the address of the memory location to be accessed |
| MBR (Memory Buffer Register) | 16-bit | Holds the data read from memory or the data to be written to memory |
| PC (Program Counter) | 12-bit | Holds the address of the **next** instruction to be fetched |
| IR (Instruction Register) | 16-bit | Holds the **current** instruction being executed |
| InREG (Input Register) | 8-bit | Holds data received from an input device |
| OutREG (Output Register) | 8-bit | Holds data to be sent to an output device |

**Key Points to Include for Full Marks:**
- All seven registers named correctly.
- Correct bit-widths (especially MAR and PC are 12-bit, not 16-bit).
- Distinction between PC (next instruction) and IR (current instruction).

**Common Mistakes to Avoid:**
- Stating MAR is 16-bit (it is 12-bit because MARIE has 4K words = $2^{12}$ addresses).
- Confusing InREG/OutREG with MBR.

---

### Q2 — Short Answer / Essay | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
Explain why the MARIE architecture increments the Program Counter (PC) by 1 during the fetch phase, rather than by 2 or 4 as seen in some other architectures.

**Guide Answer:**
MARIE is a **word-addressable** architecture. Each address in MARIE's memory refers to an entire 16-bit word, not an individual byte. Therefore, consecutive instructions are stored at consecutive word addresses (address 0, address 1, address 2, ...).

In contrast, byte-addressable architectures (like x86 or ARM) use byte addresses. If each instruction occupies 2 bytes, the PC must increment by 2; if 4 bytes, by 4. Since MARIE's addressing granularity is one word per address, incrementing PC by 1 moves to the next instruction word.

**Key Points to Include for Full Marks:**
- MARIE is word-addressable (each address = one 16-bit word).
- Byte-addressable systems need larger increments because each byte has its own address.
- PC + 1 correctly points to the next instruction in a word-addressable system.

**Common Mistakes to Avoid:**
- Stating that MARIE is byte-addressable.
- Claiming the increment depends on instruction length in bits.

---

### Q3 — Short Answer / Essay | Bloom's: Analyse | Difficulty: Medium | Marks: 2

**Question:**
In the MARIE fetch phase, the RTL notation shows `IR ← M[MAR], PC ← PC + 1` on the same line. Explain the significance of writing two operations on the same line in RTL notation and why these two specific operations can happen simultaneously.

**Guide Answer:**
In Register Transfer Language (RTL), writing two operations on the same line separated by a comma indicates that both operations occur **in the same clock cycle** (simultaneously/in parallel).

These two specific operations can happen simultaneously because they use **independent hardware resources**:
- `IR ← M[MAR]` uses the memory bus to transfer data from memory into the Instruction Register.
- `PC ← PC + 1` uses an independent incrementer circuit connected to the Program Counter.

Since the IR loading pathway and the PC incrementer are separate pieces of hardware, there is no resource conflict, and both operations can execute in the same cycle without interfering with each other.

**Key Points to Include for Full Marks:**
- Same line = same clock cycle (parallel execution).
- Independent hardware paths (memory bus for IR, incrementer for PC).
- No resource conflict between the two operations.

**Common Mistakes to Avoid:**
- Stating that all RTL operations always happen sequentially.
- Claiming that PC must wait until IR is loaded to increment.

---

### Q4 — Short Answer / Essay | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
Explain the special relationship between the MBR and AC registers in MARIE. Why can `AC ← MBR` be written on the same line as `MBR ← M[MAR]` in some RTL sequences?

**Guide Answer:**
In the MARIE architecture, there exists a **direct connection** (dedicated data path) between the MBR and the AC. This special hardware connection allows data to flow from MBR to AC without going through the main system bus.

However, typically `AC ← MBR` is written on a **separate line** from `MBR ← M[MAR]` because the AC needs the **new** value of MBR (the data just read from memory). The memory read (`MBR ← M[MAR]`) must complete before the AC can receive the correct value from MBR.

In some optimized designs or specific MARIE implementations, if the MBR output is available as a stable signal before the end of the cycle, `AC ← MBR` could theoretically be combined. However, in the standard MARIE model taught in courses, these are written on separate lines to show sequential dependency.

**Key Points to Include for Full Marks:**
- Direct connection between MBR and AC.
- The connection bypasses the main bus.
- Sequential dependency: MBR must have the correct data before AC can read it.

**Common Mistakes to Avoid:**
- Stating that MBR and AC are always updated simultaneously.
- Forgetting the direct connection exists.

---

### Q5 — Short Answer / Essay | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
In MARIE, the instruction format is 16 bits wide with a 4-bit opcode and a 12-bit address field. What is the maximum number of distinct instructions MARIE can support? What is the maximum addressable memory size?

**Guide Answer:**
1. **Maximum Instructions:**
   - The opcode field is 4 bits wide.
   - Maximum distinct instructions = $2^4 = 16$ instructions.

2. **Maximum Addressable Memory:**
   - The address field is 12 bits wide.
   - Maximum addressable locations = $2^{12} = 4096$ words = $4\text{K words}$.
   - Since MARIE is word-addressable and each word is 16 bits (2 bytes):
     - Total memory in bytes = $4096 \times 2 = 8192\text{ bytes} = 8\text{ KB}$.

**Key Points to Include for Full Marks:**
- $2^4 = 16$ instructions from 4-bit opcode.
- $2^{12} = 4\text{K}$ addressable words from 12-bit address.
- Distinction between word count (4K words) and byte capacity (8 KB).

**Common Mistakes to Avoid:**
- Confusing 4K words with 4 KB (4K words = 8 KB in MARIE).
- Forgetting that the maximum instructions comes from the opcode field alone.

---

## Part 2: RTL Tracing & Application [15 Marks]

### Q6 — Application (RTL Trace) | Bloom's: Apply | Difficulty: Medium | Marks: 4

**Question:**
Given the following MARIE memory contents and initial register values, trace the complete execution of the instruction at address `0x100` by showing the RTL for each phase (Fetch, Decode, Execute) and the final register values.

**Initial State:**
- PC = `0x100`
- AC = `0x0000`
- Memory contents:
  - Address `0x100`: `0x1500` (this is an ADD instruction; opcode `0001` = ADD, address = `0x500`)
  - Address `0x500`: `0x002A` (data value = 42 in decimal)

**Guide Answer:**

**1. Fetch Phase:**
```text
MAR ← PC           ; MAR = 0x100
IR ← M[MAR], PC ← PC + 1   ; IR = 0x1500, PC = 0x101
```

**2. Decode Phase:**
```text
MAR ← IR[11-0]     ; MAR = 0x500 (lower 12 bits of 0x1500)
Decode IR[15-12]    ; Opcode = 0x1 = ADD
```

**3. Execute Phase (ADD X):**
```text
MBR ← M[MAR]       ; MBR = M[0x500] = 0x002A
AC ← AC + MBR      ; AC = 0x0000 + 0x002A = 0x002A
```

**Final Register Values:**

| Register | Value |
|---|---|
| PC | `0x101` |
| IR | `0x1500` |
| MAR | `0x500` |
| MBR | `0x002A` |
| AC | `0x002A` |

**Key Points to Include for Full Marks:**
- Show all three phases with correct RTL notation.
- PC increments by 1 (not 2) since MARIE is word-addressable.
- MAR gets the lower 12 bits of IR during decode.
- AC accumulates (adds) the memory value, not replaces it.

**Common Mistakes to Avoid:**
- Incrementing PC by 2 instead of 1.
- Using LOAD RTL instead of ADD RTL (ADD adds to AC; LOAD replaces AC).

---

### Q7 — Application (RTL Trace) | Bloom's: Apply | Difficulty: Hard | Marks: 5

**Question:**
Trace the execution of a MARIE program consisting of two consecutive instructions. Show the complete RTL for each instruction including Fetch, Decode, and Execute phases. Track all register changes.

**Initial State:**
- PC = `0x010`
- AC = `0x00FF`

**Memory Contents:**

| Address | Content | Meaning |
|---|---|---|
| `0x010` | `0x2200` | SUBT `0x200` (opcode `0010` = SUBT) |
| `0x011` | `0x3300` | STORE `0x300` (opcode `0011` = STORE) |
| `0x200` | `0x0055` | Data value (85 decimal) |
| `0x300` | `0x0000` | Empty (will be written to) |

**Guide Answer:**

**--- Instruction 1: SUBT 0x200 ---**

**Fetch:**
```text
MAR ← PC           ; MAR = 0x010
IR ← M[MAR], PC ← PC + 1   ; IR = 0x2200, PC = 0x011
```

**Decode:**
```text
MAR ← IR[11-0]     ; MAR = 0x200
Decode IR[15-12]    ; Opcode = 0x2 = SUBT
```

**Execute (SUBT X):**
```text
MBR ← M[MAR]       ; MBR = M[0x200] = 0x0055
AC ← AC − MBR      ; AC = 0x00FF − 0x0055 = 0x00AA
```

**Register State After Instruction 1:**

| Register | Value |
|---|---|
| PC | `0x011` |
| IR | `0x2200` |
| MAR | `0x200` |
| MBR | `0x0055` |
| AC | `0x00AA` |

---

**--- Instruction 2: STORE 0x300 ---**

**Fetch:**
```text
MAR ← PC           ; MAR = 0x011
IR ← M[MAR], PC ← PC + 1   ; IR = 0x3300, PC = 0x012
```

**Decode:**
```text
MAR ← IR[11-0]     ; MAR = 0x300
Decode IR[15-12]    ; Opcode = 0x3 = STORE
```

**Execute (STORE X):**
```text
MAR ← X, MBR ← AC  ; MAR = 0x300, MBR = 0x00AA
M[MAR] ← MBR        ; M[0x300] = 0x00AA
```

**Register State After Instruction 2:**

| Register | Value |
|---|---|
| PC | `0x012` |
| IR | `0x3300` |
| MAR | `0x300` |
| MBR | `0x00AA` |
| AC | `0x00AA` |

**Memory Change:** Address `0x300` now contains `0x00AA` (previously `0x0000`).

**Key Points to Include for Full Marks:**
- Correct subtraction: $0x00FF - 0x0055 = 0x00AA$ (255 − 85 = 170).
- STORE writes AC value to memory (not the other way around).
- MBR ← AC and MAR ← X happen on the same line for STORE (same cycle).
- PC correctly increments to `0x012` after the second instruction.

**Common Mistakes to Avoid:**
- Subtracting in the wrong order (MBR − AC instead of AC − MBR).
- For STORE, reading from memory instead of writing to memory.

---

### Q8 — Application (RTL Trace) | Bloom's: Apply | Difficulty: Hard | Marks: 6

**Question:**
Write the complete RTL sequence for the following MARIE instructions, including the Fetch and Decode phases. Then explain how indirect addressing differs from direct addressing at the RTL level.

**(a)** LOAD X (Direct) where X = `0x400` and M[0x400] = `0x1234`. (2 Marks)
**(b)** LOADI X (Indirect) where X = `0x400`, M[0x400] = `0x600`, and M[0x600] = `0x5678`. (2 Marks)
**(c)** STOREI X (Indirect Store) where X = `0x400`, M[0x400] = `0x700`, AC = `0xABCD`. Show the RTL and state what memory location is modified. (2 Marks)

**Guide Answer:**

**(a) LOAD X (Direct):**
```text
; Fetch
MAR ← PC
IR ← M[MAR], PC ← PC + 1

; Decode
MAR ← IR[11-0]       ; MAR = 0x400
Decode IR[15-12]      ; Opcode = LOAD

; Execute
MBR ← M[MAR]         ; MBR = M[0x400] = 0x1234
AC ← MBR             ; AC = 0x1234
```
Result: AC = `0x1234`.

---

**(b) LOADI X (Indirect):**
```text
; Fetch
MAR ← PC
IR ← M[MAR], PC ← PC + 1

; Decode
MAR ← IR[11-0]       ; MAR = 0x400
Decode IR[15-12]      ; Opcode = LOADI

; Execute
MBR ← M[MAR]         ; MBR = M[0x400] = 0x600 (pointer)
MAR ← MBR            ; MAR = 0x600
MBR ← M[MAR]         ; MBR = M[0x600] = 0x5678 (actual data)
AC ← MBR             ; AC = 0x5678
```
Result: AC = `0x5678`.

---

**(c) STOREI X (Indirect Store):**
```text
; Fetch
MAR ← PC
IR ← M[MAR], PC ← PC + 1

; Decode
MAR ← IR[11-0]       ; MAR = 0x400
Decode IR[15-12]      ; Opcode = STOREI

; Execute
MBR ← M[MAR]         ; MBR = M[0x400] = 0x700 (pointer)
MAR ← MBR            ; MAR = 0x700
MBR ← AC             ; MBR = 0xABCD
M[MAR] ← MBR         ; M[0x700] = 0xABCD
```
Result: Memory location `0x700` now contains `0xABCD`.

---

**Key Difference Between Direct and Indirect:**
- **Direct addressing** requires **one** memory access during execute (to read/write the operand).
- **Indirect addressing** requires **two** memory accesses during execute (one to read the pointer from the operand address, and one to access the actual data at the pointer address).
- This means indirect instructions take more clock cycles to complete.

**Key Points to Include for Full Marks:**
- Exact RTL notation with arrows (`←`).
- The extra `MAR ← MBR` step that loads the pointer into MAR for indirect addressing.
- STOREI writes AC value to the memory location pointed to by the content of X.
- Clear explanation that indirect = two memory accesses vs. direct = one.

**Common Mistakes to Avoid:**
- Forgetting the extra memory access for indirect addressing.
- For STOREI, writing to address X instead of M[X].

---

## Part 3: Fill-in-the-Blank [5 Marks]

### Q9 — Fill-in-the-Blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
In MARIE, the register that temporarily holds data read from or to be written to main memory is called ________.

**Answer:** MBR (Memory Buffer Register)

---

### Q10 — Fill-in-the-Blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
During the Fetch phase of MARIE, the instruction `MAR ← PC` copies the address of the ________ instruction into the Memory Address Register.

**Answer:** next

---

### Q11 — Fill-in-the-Blank | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Question:**
In the MARIE instruction format, the opcode is extracted from bits ________ of the Instruction Register (IR), and the address is extracted from bits ________.

**Answer:** IR[15–12] (opcode), IR[11–0] (address)

---

### Q12 — Fill-in-the-Blank | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
MARIE uses a ________-addressable memory model, meaning each address refers to a complete 16-bit data unit.

**Answer:** word

---

### Q13 — Fill-in-the-Blank | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Question:**
The RTL for the STORE X instruction includes `MBR ← AC` and `MAR ← X` on the same line because they use ________ hardware resources and can execute in the same clock cycle.

**Answer:** independent (or separate/different)

---

## Part 4: True/False [10 Marks]

### Q14 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
The Program Counter (PC) in MARIE is 16 bits wide.

**Answer:** False
**Justification:** The PC in MARIE is **12 bits** wide because it needs to address 4K words ($2^{12} = 4096$), matching the 12-bit address space.

---

### Q15 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Statement:**
In MARIE, the ADD X instruction replaces the value of AC with the value stored at memory location X.

**Answer:** False
**Justification:** ADD X adds the value at memory location X **to** the current value of AC. The result is `AC ← AC + M[X]`. The instruction that replaces AC is LOAD X.

---

### Q16 — True/False | Bloom's: Analyse | Difficulty: Medium | Marks: 1

**Statement:**
The SUBT X instruction in MARIE computes M[X] − AC and stores the result in AC.

**Answer:** False
**Justification:** SUBT X computes `AC ← AC − MBR` (i.e., AC minus the value at address X), not the other way around.

---

### Q17 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
The Instruction Register (IR) holds the address of the next instruction to be executed.

**Answer:** False
**Justification:** The IR holds the **current** instruction being executed. The **Program Counter (PC)** holds the address of the next instruction.

---

### Q18 — True/False | Bloom's: Analyse | Difficulty: Hard | Marks: 1

**Statement:**
In MARIE, the LOADI X instruction requires exactly the same number of clock cycles as the LOAD X instruction.

**Answer:** False
**Justification:** LOADI X (indirect load) requires more clock cycles because it performs **two** memory accesses in the execute phase (one to read the pointer from X, one to read the data from the pointed address), whereas LOAD X (direct) only requires **one** memory access.

---

### Q19 — True/False | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Statement:**
The MAR (Memory Address Register) in MARIE is 16 bits wide to match the data word size.

**Answer:** False
**Justification:** The MAR is **12 bits** wide because it stores memory addresses, and MARIE's address space is $2^{12} = 4\text{K}$ words. The data word size (16 bits) is a separate concern.

---

### Q20 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Statement:**
During the Decode phase in MARIE, the opcode portion of the instruction (IR[15-12]) is used to generate control signals that direct the CPU to perform the correct operation.

**Answer:** True
**Justification:** The Control Unit decodes the opcode bits (IR[15-12]) during the Decode phase to determine which instruction is being executed and generates the appropriate control signals for the Execute phase.

---

### Q21 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
The InREG and OutREG registers in MARIE are both 16 bits wide, matching the word size.

**Answer:** False
**Justification:** Both InREG and OutREG are **8 bits** wide, not 16 bits. They handle I/O data at the byte level.

---

### Q22 — True/False | Bloom's: Analyse | Difficulty: Hard | Marks: 1

**Statement:**
If MARIE were redesigned with a 5-bit opcode and an 11-bit address field (still 16-bit instructions), it could support more instructions but would have a smaller addressable memory.

**Answer:** True
**Justification:** A 5-bit opcode allows $2^5 = 32$ instructions (up from 16). However, the 11-bit address field reduces addressable memory to $2^{11} = 2048$ words = $2\text{K}$ words (down from 4K). There is a trade-off between instruction count and address space.

---

### Q23 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Statement:**
In the MARIE fetch phase, the operation `IR ← M[MAR]` reads data from memory and places it in the MBR first, then transfers it to the IR.

**Answer:** False
**Justification:** In the standard MARIE RTL model, the fetch phase shows `IR ← M[MAR]` as a direct transfer. While the physical implementation may route through the MBR, the RTL abstraction treats it as a single operation from memory to IR.
