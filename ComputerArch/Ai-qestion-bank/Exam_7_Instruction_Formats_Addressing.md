# COA Practice Exam 7: Instruction Formats & Addressing Modes

This exam covers instruction format design, ISA types (three-address, two-address, one-address, zero-address), addressing modes with effective address calculations, endianness, and expanding opcode techniques.

---

## Part 1: Instruction Format Design [12 Marks]

### Q1 — Application (Design) | Bloom's: Create | Difficulty: Hard | Marks: 4

**Question:**
Design an instruction word format for a computer system with the following specifications:
- **Memory:** 128K words
- **Registers:** 32 general-purpose registers
- **Instruction word size:** 24 bits
- **Instruction fields:** Indirect bit ($I$), Opcode, Register Selector, and Address

Determine the number of bits in each field. Draw a labeled instruction word diagram and state the maximum number of distinct opcodes supported.

**Guide Answer:**

**1. Field Width Calculations:**
- **Indirect bit ($I$):** 1 bit
- **Register Selector:**
  $$32\text{ registers} = 2^5 \implies 5\text{ bits}$$
- **Address Field:**
  $$128\text{K words} = 128 \times 1024 = 131,072 = 2^{17} \implies 17\text{ bits}$$
- **Opcode:**
  $$\text{Opcode bits} = 24 - 1 - 5 - 17 = 1\text{ bit}$$

**2. Maximum Distinct Opcodes:**
$$2^1 = 2\text{ opcodes}$$

**3. Instruction Word Diagram:**
```text
 23  22    21         17 16                                        0
+----+----+------------+------------------------------------------+
| I  | Op |  Register  |                  Address                  |
+----+----+------------+------------------------------------------+
|1bit|1bit|   5 bits   |                 17 bits                   |
```

**Note:** With only 2 possible opcodes, this design is extremely limited in instruction variety. This illustrates the fundamental trade-off between address space size and instruction set richness.

**Key Points to Include for Full Marks:**
- Correct computation: $\log_2(128\text{K}) = 17$, $\log_2(32) = 5$.
- Correct remaining bits for opcode.
- Labeled diagram with bit positions.
- Acknowledgment that only 2 opcodes is a severe limitation.

**Common Mistakes to Avoid:**
- Computing $128\text{K} = 2^{16}$ (wrong; $128\text{K} = 2^{17}$).
- Forgetting the indirect bit.

---

### Q2 — Application (Design) | Bloom's: Create | Difficulty: Hard | Marks: 4

**Question:**
A 32-bit instruction computer has 256 opcodes and 16 general-purpose registers.
**(a)** Design a three-address instruction format where each address field specifies a register. How many bits remain unused? (2 Marks)
**(b)** Design a two-address instruction format where one address is a register and the other is a direct memory address. Given a 16-bit memory address field, how many bits remain unused? (2 Marks)

**Guide Answer:**

**(a) Three-Address (Register-Register-Register):**
- **Opcode:** $\log_2(256) = 8$ bits
- **Each register field:** $\log_2(16) = 4$ bits
- **Three register fields:** $3 \times 4 = 12$ bits
- **Total used:** $8 + 12 = 20$ bits
- **Unused:** $32 - 20 = 12$ bits remaining

```text
 31          24 23     20 19     16 15     12 11                 0
+--------------+---------+---------+---------+-------------------+
|    Opcode    |  Reg 1  |  Reg 2  |  Reg 3  |     Unused        |
+--------------+---------+---------+---------+-------------------+
|    8 bits    |  4 bits |  4 bits |  4 bits |     12 bits       |
```

**(b) Two-Address (Register + Memory):**
- **Opcode:** $8$ bits
- **Register field:** $4$ bits
- **Memory address field:** $16$ bits
- **Total used:** $8 + 4 + 16 = 28$ bits
- **Unused:** $32 - 28 = 4$ bits remaining

```text
 31          24 23     20 19                    4 3             0
+--------------+---------+----------------------+---------------+
|    Opcode    |   Reg   |    Memory Address     |    Unused     |
+--------------+---------+----------------------+---------------+
|    8 bits    |  4 bits |       16 bits         |    4 bits     |
```

**Key Points to Include for Full Marks:**
- Correct log₂ calculations for opcode and register fields.
- Clear bit diagrams with labeled fields.
- Correct computation of unused bits.

---

### Q3 — Application (Calculation) | Bloom's: Apply | Difficulty: Hard | Marks: 4

**Question:**
Consider the expression $X = (A + B) \times (C - D)$. Write the equivalent instruction sequence using:
**(a)** Three-address instructions (2 Marks)
**(b)** Two-address instructions (1 Mark)
**(c)** One-address (accumulator) instructions (1 Mark)

Assume standard arithmetic operations: ADD, SUB, MUL, LOAD, STORE, and MOV.

**Guide Answer:**

**(a) Three-Address Instructions:**
Each instruction has the form: `OP Dest, Src1, Src2`
```
ADD R1, A, B        ; R1 ← A + B
SUB R2, C, D        ; R2 ← C - D
MUL X, R1, R2       ; X  ← R1 × R2
```
Total: **3 instructions**.

**(b) Two-Address Instructions:**
Each instruction has the form: `OP Dest, Src` (result stored in Dest)
```
MOV R1, A           ; R1 ← A
ADD R1, B           ; R1 ← R1 + B = A + B
MOV R2, C           ; R2 ← C
SUB R2, D           ; R2 ← R2 - D = C - D
MUL R1, R2          ; R1 ← R1 × R2 = (A+B)×(C-D)
MOV X, R1           ; X  ← R1
```
Total: **6 instructions**.

**(c) One-Address (Accumulator) Instructions:**
All operations use the AC (accumulator) implicitly.
```
LOAD A              ; AC ← A
ADD  B              ; AC ← AC + B = A + B
STORE T             ; T  ← AC (temporary)
LOAD C              ; AC ← C
SUB  D              ; AC ← AC - D = C - D
MUL  T              ; AC ← AC × T = (C-D)×(A+B)
STORE X             ; X  ← AC
```
Total: **7 instructions**.

**Key Points to Include for Full Marks:**
- Three-address is most compact (fewest instructions).
- One-address requires temporary storage.
- Correct operation semantics for each ISA type.

**Common Mistakes to Avoid:**
- Using three operands in a two-address instruction.
- Forgetting the temporary STORE in one-address mode.

---

## Part 2: Addressing Modes [12 Marks]

### Q4 — Application (Calculation) | Bloom's: Apply | Difficulty: Medium | Marks: 6

**Question:**
A computer instruction specifies an address field value of `0x200`. Given the following register and memory contents, calculate the **effective address (EA)** and the **operand value** for each addressing mode.

**Given:**
- PC = `0x400` (after fetch, pointing to next instruction)
- Index Register (R1) = `0x050`
- Base Register (R2) = `0x1000`
- Memory contents:
  - M[`0x200`] = `0x350`
  - M[`0x250`] = `0x0077`
  - M[`0x350`] = `0x0088`
  - M[`0x600`] = `0x0099`
  - M[`0x1200`] = `0x00AA`

Calculate EA and operand for:
**(a)** Immediate Addressing (1 Mark)
**(b)** Direct Addressing (1 Mark)
**(c)** Indirect Addressing (1 Mark)
**(d)** Indexed Addressing (using R1) (1 Mark)
**(e)** Based Addressing (using R2) (1 Mark)
**(f)** Relative Addressing (1 Mark)

**Guide Answer:**

| Mode | EA Formula | EA Value | Operand |
|---|---|---|---|
| **(a) Immediate** | No EA; operand = address field | N/A | `0x200` (the value itself) |
| **(b) Direct** | EA = address field | `0x200` | M[`0x200`] = `0x350` |
| **(c) Indirect** | EA = M[address field] | M[`0x200`] = `0x350` | M[`0x350`] = `0x0088` |
| **(d) Indexed** | EA = address field + R1 | `0x200 + 0x050 = 0x250` | M[`0x250`] = `0x0077` |
| **(e) Based** | EA = address field + R2 | `0x200 + 0x1000 = 0x1200` | M[`0x1200`] = `0x00AA` |
| **(f) Relative** | EA = address field + PC | `0x200 + 0x400 = 0x600` | M[`0x600`] = `0x0099` |

**Key Points to Include for Full Marks:**
- Immediate mode: the address field IS the operand (no memory access).
- Indirect mode: requires TWO memory accesses.
- Relative mode: uses PC value (not the instruction address, but the PC after fetch).
- Indexed and Based: add a register value to the address field.

**Common Mistakes to Avoid:**
- Using the instruction address instead of the post-fetch PC for relative addressing.
- Confusing indirect (M[M[addr]]) with direct (M[addr]).

---

### Q5 — Short Answer / Essay | Bloom's: Analyse | Difficulty: Medium | Marks: 3

**Question:**
Explain why the Register-Indirect addressing mode is useful. Compare it with both Direct addressing and Indirect (memory-indirect) addressing in terms of flexibility and speed.

**Guide Answer:**

**Register-Indirect Addressing:** The address of the operand is held in a CPU register, not in the instruction or in memory. The effective address is: $EA = \text{contents of register}$.

**Why it is useful:**
1. **Pointer Support:** It naturally implements pointer-based data structures (linked lists, trees) where the address of data changes dynamically.
2. **Array Traversal:** By incrementing the register, the CPU can walk through arrays without modifying the instruction.
3. **Large Address Space:** The register can hold a full-width address (e.g., 32 bits) even if the instruction's address field is narrow.

**Comparison:**

| Aspect | Direct | Register-Indirect | Indirect (Memory) |
|---|---|---|---|
| **EA Calculation** | EA = address field | EA = contents of register | EA = M[address field] |
| **Memory Accesses** | 1 (read operand) | 1 (read operand via register) | 2 (read pointer from memory, then read operand) |
| **Speed** | Fast (1 memory access) | Fast (register access + 1 memory access) | Slow (2 memory accesses) |
| **Flexibility** | Low (fixed address in instruction) | High (register can be changed dynamically) | High (address can be changed in memory) |

**Key Points to Include for Full Marks:**
- Register-indirect is faster than memory-indirect (avoids extra memory access).
- Register-indirect supports dynamic addressing without instruction modification.
- Show comparison with both direct and memory-indirect.

---

### Q6 — Short Answer / Essay | Bloom's: Understand | Difficulty: Medium | Marks: 3

**Question:**
A 32-bit value `0xDEADBEEF` is stored starting at memory address `0x1000`. Show the byte layout in memory for:
**(a)** Big-endian storage
**(b)** Little-endian storage

Which endianness is used by the MIPS architecture? Which by x86?

**Guide Answer:**

The 32-bit value `0xDEADBEEF` has 4 bytes: `DE`, `AD`, `BE`, `EF` (from most significant to least significant).

**(a) Big-Endian (MSB at lowest address):**

| Address | `0x1000` | `0x1001` | `0x1002` | `0x1003` |
|---|---|---|---|---|
| **Byte** | `DE` | `AD` | `BE` | `EF` |

**(b) Little-Endian (LSB at lowest address):**

| Address | `0x1000` | `0x1001` | `0x1002` | `0x1003` |
|---|---|---|---|---|
| **Byte** | `EF` | `BE` | `AD` | `DE` |

- **MIPS** uses **Big-Endian** (stores MSB first).
- **x86** uses **Little-Endian** (stores LSB first).

**Key Points to Include for Full Marks:**
- Big-endian: MSB at the **lowest** address.
- Little-endian: LSB at the **lowest** address.
- Correct byte order for both layouts.

**Common Mistakes to Avoid:**
- Reversing individual bits instead of bytes.
- Swapping the endianness of MIPS and x86.

---

## Part 3: Expanding Opcodes [8 Marks]

### Q7 — Application (Design) | Bloom's: Create | Difficulty: Hard | Marks: 8

**Question:**
A 16-bit instruction set must support the following instruction classes:
1. **4 instructions** with three 4-bit register operands
2. **24 instructions** with two 4-bit register operands
3. **120 instructions** with one 4-bit register operand
4. **Remaining** instructions with no operands

**(a)** Verify that this encoding is possible using the state-space method. (3 Marks)
**(b)** Design the complete opcode prefix scheme. Show the opcode ranges for each class. (3 Marks)
**(c)** How many zero-operand instructions can be encoded? (2 Marks)

**Guide Answer:**

**(a) State-Space Verification:**
Total instruction states = $2^{16} = 65,536$.

| Class | Instructions | Operand Bits | States Per Instruction | Total States |
|---|---|---|---|---|
| 1 (3 regs) | 4 | $3 \times 4 = 12$ | $2^{12} = 4096$ | $4 \times 4096 = 16,384$ |
| 2 (2 regs) | 24 | $2 \times 4 = 8$ | $2^8 = 256$ | $24 \times 256 = 6,144$ |
| 3 (1 reg) | 120 | $1 \times 4 = 4$ | $2^4 = 16$ | $120 \times 16 = 1,920$ |
| 4 (0 regs) | ? | 0 | $1$ | ? |

Total states used by classes 1–3: $16,384 + 6,144 + 1,920 = 24,448$.
Remaining states: $65,536 - 24,448 = 41,088$ for zero-operand instructions.
Since $41,088 \geq 1$, the encoding is **possible**.

**(b) Opcode Prefix Scheme:**

**Class 1 (4-bit opcode + 12 operand bits):**
- Opcode range: `0000` to `0011` (4 opcodes).
- Format: `[4-bit opcode | Reg1 (4b) | Reg2 (4b) | Reg3 (4b)]`
- Prefix `0100` through `1111` (12 prefixes) reserved for expansion.

**Class 2 (8-bit opcode + 8 operand bits):**
- Must start with one of the 12 remaining 4-bit prefixes (`0100` to `1111`).
- Each 4-bit prefix gives 16 sub-codes (4 more bits). We have 12 prefixes → $12 \times 16 = 192$ possible 8-bit opcodes.
- We need 24 opcodes. Use prefixes `0100` and `0101`:
  - `0100 xxxx` → 16 opcodes (use `0100 0000` to `0100 1111`)
  - `0101 xxxx` → 8 opcodes (use `0101 0000` to `0101 0111`)
  - Total: 24 opcodes.
  - Remaining 8-bit prefix: `0101 1000` to `0101 1111` (8 codes) + `0110` through `1111` (10 × 16 = 160 codes) = 168 free 8-bit prefixes.

**Class 3 (12-bit opcode + 4 operand bits):**
- 168 free 8-bit prefixes → $168 \times 16 = 2,688$ possible 12-bit opcodes.
- We need 120 opcodes. Use a subset.
- Remaining 12-bit codes: $2,688 - 120 = 2,568$ free 12-bit prefixes.

**Class 4 (16-bit opcode + 0 operand bits):**
- Remaining 12-bit prefixes: $2,568 \times 16 = 41,088$ possible 16-bit opcodes.

**(c) Zero-Operand Instructions:**
$$\text{Maximum zero-operand instructions} = 41,088$$

**Key Points to Include for Full Marks:**
- State-space calculation showing total = $65,536$.
- Progressive prefix expansion from 4-bit → 8-bit → 12-bit → 16-bit.
- Final count of zero-operand instructions.

**Common Mistakes to Avoid:**
- Overlapping opcode prefixes between classes.
- Incorrectly computing remaining states at each level.

---

## Part 4: True/False [8 Marks]

### Q8 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
In immediate addressing mode, the operand value is embedded directly in the instruction itself.

**Answer:** True
**Justification:** In immediate addressing, the address field of the instruction contains the actual operand value, not a memory address. No memory access is needed to fetch the operand.

---

### Q9 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Statement:**
A three-address instruction always requires three memory accesses per instruction.

**Answer:** False
**Justification:** A three-address instruction has three operand specifiers, but if the operands are registers (register-register instructions), no memory accesses are needed for operand fetching. Only register-to-register transfers occur within the CPU.

---

### Q10 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Statement:**
In a stack-based (zero-address) architecture, arithmetic operations like ADD implicitly use operands from the top of the stack.

**Answer:** True
**Justification:** In a zero-address architecture, operations pop their operands from the stack and push the result back. No address fields are needed in the instruction because the operands are always at the top of the stack.

---

### Q11 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
Little-endian architectures store the most significant byte at the lowest memory address.

**Answer:** False
**Justification:** Little-endian stores the **least** significant byte (LSB) at the lowest address. It is **big-endian** that stores the most significant byte (MSB) at the lowest address.

---

### Q12 — True/False | Bloom's: Analyse | Difficulty: Hard | Marks: 1

**Statement:**
Expanding opcode encoding allows a fixed-length instruction to support more opcodes for instructions with fewer operands.

**Answer:** True
**Justification:** Expanding opcodes use a variable-length opcode within a fixed-length instruction. Instructions with fewer operands have more bits available for the opcode field, allowing more opcodes. This is the core principle of expanding opcode design.

---

### Q13 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Statement:**
Relative addressing mode calculates the effective address by adding the address field to the contents of the base register.

**Answer:** False
**Justification:** Relative addressing adds the address field to the **Program Counter (PC)**, not a base register. Adding to a base register is called **based addressing** (or base-register addressing).

---

### Q14 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
An accumulator-based architecture (like MARIE) is a one-address architecture because the accumulator (AC) serves as an implicit operand.

**Answer:** True
**Justification:** In an accumulator architecture, one operand is always implicitly the AC. The instruction only needs to specify one address (the second operand in memory), making it a one-address ISA.

---

### Q15 — True/False | Bloom's: Analyse | Difficulty: Hard | Marks: 1

**Statement:**
Indexed addressing mode is particularly useful for accessing array elements because the index register can be incremented to traverse consecutive elements.

**Answer:** True
**Justification:** In indexed addressing, $EA = \text{address field} + \text{index register}$. The address field holds the array base address, and the index register holds the offset. Incrementing the index register moves to the next array element, making it ideal for loop-based array processing.
