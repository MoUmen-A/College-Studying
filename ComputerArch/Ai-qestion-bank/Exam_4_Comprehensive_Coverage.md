# COA Practice Exam 4: Comprehensive System Coverage

This exam tests deep integration concepts: I/O interfacing techniques, pipeline hazard mitigation, virtual memory architectures, instruction-level stack evaluation, custom Register Transfer Language (RTL) instruction extensions, and memory subsystem engineering.

---

## Part 1: Comparative & Conceptual Analysis [10 Marks]

### Q1 — Short Answer / Essay | Bloom's: Analyse | Difficulty: Medium | Marks: 2.5

**Question:**
Compare Memory-Mapped I/O and Instruction-Based I/O (isolated I/O) in terms of address space allocation, hardware complexity, and instruction set design.

**Guide Answer:**
* **Address Space Allocation:**
  * **Memory-Mapped I/O:** The I/O devices share the same address space as main memory. A portion of the memory address range is reserved for I/O registers.
  * **Instruction-Based I/O:** The address space is isolated. I/O devices have a separate address space, distinct from main memory.
* **Instruction Set Design:**
  * **Memory-Mapped I/O:** No specialized I/O instructions are needed. The CPU uses standard memory access instructions (e.g., `LOAD`, `STORE`) to communicate with device registers.
  * **Instruction-Based I/O:** Requires specialized I/O instructions (e.g., `IN`, `OUT`) to access the isolated I/O address space.
* **Hardware Complexity:**
  * **Memory-Mapped I/O:** Simpler CPU control unit (fewer instructions), but requires more address decoding logic externally to recognize device addresses.
  * **Instruction-Based I/O:** Requires additional control lines from the CPU (to distinguish memory access from I/O access) and a more complex instruction decoder.

**Key Points to Include for Full Marks:**
- Explicit contrast of address spaces (shared/unified vs. separate/isolated).
- Mention of instructions used (standard memory instructions vs. specialized `IN`/`OUT` instructions).
- Contrast of internal CPU complexity vs. external decoding logic.

**Common Mistakes to Avoid:**
- Stating that memory-mapped I/O uses physical RAM to store I/O data (it uses device register addresses mapped to the bus).
- Confusing I/O mapping with virtual memory mapping.

---

### Q2 — Short Answer / Essay | Bloom's: Understand | Difficulty: Medium | Marks: 2.5

**Question:**
Pipelining can suffer from structural, data, and control hazards. Define each hazard and briefly explain one common hardware or compiler technique used to mitigate each.

**Guide Answer:**
1. **Structural Hazard:**
   * **Definition:** Occurs when two or more instructions in the pipeline require the same physical hardware resource at the same time (e.g., single memory port for fetching instructions and data).
   * **Mitigation:** Separate L1 caches for instructions (L1I) and data (L1D) (Harvard architecture), or duplicating execution units (e.g., multiple ALUs).
2. **Data Hazard:**
   * **Definition:** Occurs when an instruction depends on the result of a previous instruction that is still in progress in the pipeline (Read-After-Write, Write-After-Read, Write-After-Write).
   * **Mitigation:** **Data Forwarding** (bypassing the register file writeback and routing the ALU output directly to the ALU input of the next stage), or compiler scheduling (inserting NOPs/independent instructions).
3. **Control Hazard:**
   * **Definition:** Occurs when the pipeline cannot determine the next instruction to fetch because of a branch instruction whose condition or target address is not yet resolved.
   * **Mitigation:** **Branch Prediction** (predicting whether a branch is taken or not taken), or delayed branch slot scheduling by the compiler.

**Key Points to Include for Full Marks:**
- Define all three hazards.
- Match each hazard to a valid mitigation technique (e.g., L1 Cache separation for Structural, Forwarding/Bypassing for Data, Prediction for Control).

**Common Mistakes to Avoid:**
- Swapping the definitions (e.g., calling a branch hazard a data hazard).
- Suggesting software solutions like rebooting for structural hazards.

---

### Q3 — Short Answer / Essay | Bloom's: Analyse | Difficulty: Hard | Marks: 2.5

**Question:**
Compare Paging and Segmentation as virtual memory management techniques. Your comparison must cover: unit of allocation, presence of internal/external fragmentation, and address translation structure.

**Guide Answer:**

| Feature | Paging | Segmentation |
|---|---|---|
| **Unit of Allocation** | Fixed-size blocks called **pages** (determined by hardware/OS, typically 4KB). | Variable-size blocks called **segments** (determined by logical structures like code, stack, data). |
| **Address Fields** | Virtual Address: `[Page Number \| Offset]` | Virtual Address: `[Segment Number \| Offset]` |
| **Translation Table** | **Page Table** maps virtual page number to physical frame number. | **Segment Table** contains a Segment Base Address and a Limit/Length value. |
| **Fragmentation** | Suffers from **internal fragmentation** (space wasted in the last page). | Suffers from **external fragmentation** (free memory scattered in tiny unusable blocks over time). |

**Key Points to Include for Full Marks:**
- Fixed size (Paging) vs. Variable logical size (Segmentation).
- Internal fragmentation in paging vs. External fragmentation in segmentation.
- Mention of base and limit registers in segmentation table vs. simple frame lookup in page tables.

**Common Mistakes to Avoid:**
- Stating that paging has external fragmentation.
- Stating that segment sizes are fixed.

---

### Q4 — Short Answer / Essay | Bloom's: Analyse | Difficulty: Hard | Marks: 2.5

**Question:**
Compare Hardwired Control Units and Microprogrammed Control Units. Provide your comparison in a table covering: speed, flexibility/modification, physical area/cost, and complexity.

**Guide Answer:**

| Comparison Aspect | Hardwired Control Unit | Microprogrammed Control Unit |
|---|---|---|
| **Speed** | Very fast (combinational logic gates and flip-flops execute in real time). | Slower (requires an extra memory read cycle to fetch microinstructions from control ROM). |
| **Flexibility / Modification** | Extremely difficult (requires physically redesigning and rewiring logic gates/chips). | Easy (can update instructions by rewriting the microprogram stored in the control ROM). |
| **Physical Area & Cost** | Large silicon area for complex instruction sets, but cheaper for simple designs. | Compact layout, but has higher initial design cost due to control ROM/store. |
| **Complexity** | Very complex and error-prone to design as instruction set size increases. | Systematic and easier to design and debug using microprogramming concepts. |

**Key Points to Include for Full Marks:**
- Speed comparison (Hardwired = faster, Microprogrammed = slower).
- Flexibility comparison (Microprogrammed = flexible/firmware, Hardwired = rigid/hardwired).
- Correct association of control store/ROM with microprogrammed control.

---

## Part 2: Calculation & System Design [15 Marks]

### Q5 — Calculation | Bloom's: Apply | Difficulty: Hard | Marks: 5

**Question:**
Consider the following infix expression:
$$Z = \frac{A + B \times C}{D - E \times F}$$
**(a)** Convert this expression to postfix notation (RPN). (1 Mark)  
**(b)** Trace the step-by-step stack evaluation of the RPN expression, assuming the variable values are:
$$A = 4, B = 3, C = 2, D = 18, E = 4, F = 3$$
Show the evaluation as a trace table containing: Current Token, Action Performed, and Stack State (from bottom to top). (4 Marks)

### Guide Answer:

**(a) Postfix Conversion:**
* Expression: $\frac{A + (B \times C)}{D - (E \times F)}$
* Numerator in postfix: $A\ B\ C\ \times\ +$
* Denominator in postfix: $D\ E\ F\ \times\ -$
* Final division: $(A\ B\ C\ \times\ +)\ (D\ E\ F\ \times\ -)\ /$
* **Postfix Expression (RPN):** $A\ B\ C\ \times\ +\ D\ E\ F\ \times\ -\ /$

**(b) Stack Trace Evaluation:**
Values: $A = 4, B = 3, C = 2, D = 18, E = 4, F = 3$
The input RPN string is: $4\ 3\ 2\ \times\ +\ 18\ 4\ 3\ \times\ -\ /$

| Step | Current Token | Action Performed | Stack State (Bottom to Top) |
|:---:|:---:|:---|:---|
| 0 | - | Initialize Stack | `[` (Empty) `]` |
| 1 | `4` | Push operand | `[ 4 ]` |
| 2 | `3` | Push operand | `[ 4, 3 ]` |
| 3 | `2` | Push operand | `[ 4, 3, 2 ]` |
| 4 | `*` | Pop $2, 3$; Push $3 \times 2 = 6$ | `[ 4, 6 ]` |
| 5 | `+` | Pop $6, 4$; Push $4 + 6 = 10$ | `[ 10 ]` |
| 6 | `18` | Push operand | `[ 10, 18 ]` |
| 7 | `4` | Push operand | `[ 10, 18, 4 ]` |
| 8 | `3` | Push operand | `[ 10, 18, 4, 3 ]` |
| 9 | `*` | Pop $3, 4$; Push $4 \times 3 = 12$ | `[ 10, 18, 12 ]` |
| 10 | `-` | Pop $12, 18$; Push $18 - 12 = 6$ | `[ 10, 6 ]` |
| 11 | `/` | Pop $6, 10$; Push $10 / 6 \approx 1.67$ (or $5/3$) | `[ 1.67 ]` |

Final Result: $1.67$ (or $5/3$).

**Key Points to Include for Full Marks:**
- Correct postfix string.
- Detailed trace table showing intermediate evaluations ($3 \times 2 = 6$, $4 + 6 = 10$, $4 \times 3 = 12$, $18 - 12 = 6$).
- Correct pop ordering (e.g., $18 - 12 = 6$, not $12 - 18$).

**Common Mistakes to Avoid:**
- Evaluation order errors (e.g., popping $Y, X$ for division/subtraction and evaluating as $Y - X$ or $Y / X$ instead of $X - Y$ or $X / Y$).
- Confusing variable values.

---

### Q6 — RTL & Architecture Design | Bloom's: Create | Difficulty: Hard | Marks: 5

**Question:**
We wish to add a new indirect memory-reference instruction to MARIE called **LOADI X** (Load Indirect). This instruction takes an address $X$, retrieves the pointer value stored at location $X$, and then loads the data stored at that pointer address into the Accumulator (AC).
For example, if memory location `0x200` holds `0x300`, and location `0x300` holds `0x0055`, executing `LOADI 200` will load `0x0055` into the AC.

**(a)** Write the Register Transfer Language (RTL) sequence for the Execution phase of **LOADI X**. Explain each step. (3 Marks)  
**(b)** Compare this to the standard **LOAD X** instruction RTL sequence. Explain why LOADI X cannot execute in the same number of clock cycles as LOAD X. (2 Marks)

### Guide Answer:

**(a) RTL for LOADI X Execution:**
Assume Fetch and Decode are already completed (so address $X$ is loaded in the `MAR` register).
```text
MBR ← M[MAR]      ; Step 1: Read memory location X (pointer address) into MBR
MAR ← MBR         ; Step 2: Transfer pointer address from MBR to MAR
MBR ← M[MAR]      ; Step 3: Read memory location pointed to by MAR into MBR
AC ← MBR          ; Step 4: Transfer the target data from MBR to Accumulator
```

*Explanation:*
1. Step 1 accesses memory at the operand address $X$ to get the address of the actual data.
2. Step 2 loads this pointer address into the Memory Address Register (`MAR`) to prepare for a second memory access.
3. Step 3 retrieves the actual operand value from memory.
4. Step 4 moves that data value into the Accumulator.

**(b) Comparison with LOAD X:**
* **LOAD X RTL Sequence:**
  ```text
  MAR ← X
  MBR ← M[MAR]
  AC ← MBR
  ```
* **Analysis:**
  * `LOAD X` requires only **one** memory read cycle because the address of the operand is explicitly given in the instruction (direct addressing).
  * `LOADI X` requires **two** memory read cycles (one to retrieve the pointer, and one to retrieve the actual data). Because memory operations are slow and must happen on separate clock cycles, `LOADI X` requires more cycles to complete execution.

**Key Points to Include for Full Marks:**
- Exact arrow notation (`←`) in RTL.
- The step `MAR ← MBR` to translate pointer location to physical address lookup.
- Explanation that memory access takes separate clock cycles, which explains why indirect loading requires extra cycles.

---

### Q7 — Memory Subsystem Design | Bloom's: Create | Difficulty: Hard | Marks: 5

**Question:**
Design a $64\text{K} \times 16$-bit memory system using $16\text{K} \times 4$-bit RAM chips.
1. Calculate the total number of RAM chips required. (1 Mark)
2. How many chips will be in each row (word size scaling) and how many rows will there be (address space scaling)? (2 Marks)
3. Describe the address decoding scheme: How many address lines are connected to the decoder, what size decoder is needed, and which address lines connect directly to the chips? (2 Marks)

### Guide Answer:

**1. Total Chips Required:**
* Target size = $64\text{K} \times 16\text{ bits}$
* Chip size = $16\text{K} \times 4\text{ bits}$
$$\text{Total Chips} = \frac{64\text{K} \times 16\text{ bits}}{16\text{K} \times 4\text{ bits}} = 4 \times 4 = 16\text{ chips}$$

**2. Grid Organization (Rows & Columns):**
* **Columns (Word Size expansion):**
  * Target word width is 16 bits. Chip width is 4 bits.
  $$\text{Chips per row (columns)} = \frac{16\text{ bits}}{4\text{ bits}} = 4\text{ chips}$$
* **Rows (Address Space expansion):**
  * Target address space is 64K. Chip address capacity is 16K.
  $$\text{Number of Rows} = \frac{64\text{K}}{16\text{K}} = 4\text{ rows}$$
* **Grid Structure:** The system is organized as a $4 \times 4$ grid of chips (4 rows of 4 chips each).

**3. Address Lines & Decoder Scheme:**
* **Total Address Lines:**
  * Target capacity is $64\text{K} = 2^{16}$ words $\implies 16$ address lines ($A_{15} - A_0$).
* **Direct Chip Connections:**
  * Each chip has a capacity of $16\text{K} = 2^{14}$ words $\implies 14$ address pins are required.
  * Connect the lower 14 address lines ($A_{13} - A_0$) directly to the address inputs of all 16 chips in parallel.
* **Row Selection (Decoder):**
  * We need to select one of the 4 rows.
  * We use the remaining 2 highest-order address lines ($A_{15} - A_{14}$).
  * We route these 2 lines into a **$2 \times 4$ decoder**.
  * The 4 output lines of the decoder are connected to the Chip Select ($CS$) inputs of the 4 rows (each output line enables all 4 chips in a specific row).

**Key Points to Include for Full Marks:**
- Explicit chip count calculation ($16$).
- Row-column breakdown ($4 \times 4$ grid).
- Correct mapping of address lines: $A_{13} - A_0$ to chip inputs, $A_{15} - A_{14}$ to a $2 \times 4$ row-select decoder.

**Common Mistakes to Avoid:**
- Miscalculating the address line boundaries (e.g., connecting 12 lines instead of 14 lines).
- Confusing address lines with data lines (target data bus is 16 bits; each column chip connects to 4 pins of the bus).
