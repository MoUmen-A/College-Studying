# COA Practice Exam 8: Pipeline & Memory Hierarchy

This exam focuses on instruction pipelining (speedup, space-time diagrams, hazards) and memory hierarchy (DRAM vs. SRAM, memory types, hit/miss, and memory chip design).

---

## Topic Summary

This exam covers the following core concepts from the COA course:

- **Instruction Pipelining Mechanics:**
  - **Pipelined Execution Time:** $T_p = (k + n - 1) \cdot t_p$, where $k$ is the number of stages, $n$ is the number of instructions, and $t_p$ is the clock cycle time.
  - **Non-Pipelined Execution Time:** $T_{np} = n \cdot t_n$, where $t_n$ is the total execution time for one instruction.
  - **Speedup Ratio ($S$):** $S = \frac{T_{np}}{T_p}$.
  - **Theoretical Max Speedup:** $S_{max} = k$ (as $n \to \infty$).
  - **Space-Time Diagram:** Staggered diagonal representation of pipeline stages (Y-axis) versus clock cycles (X-axis).
- **Pipeline Stages:** Typical 6 stages are FI (Fetch Instruction), DI (Decode Instruction), EA (Calculate Effective Address), FO (Fetch Operand), EI (Execute Instruction), and SR (Store Result).
- **Pipeline Hazards:**
  - **Structural Hazards:** Resource conflict (e.g., instructions in different stages trying to access memory simultaneously).
  - **Data Hazards:** RAW (Read After Write - true data dependency), WAR (Write After Read - anti-dependency), WAW (Write After Write - output dependency).
  - **Control Hazards:** Branch instructions changing PC, stalling subsequent instructions until branch target is known.
- **Memory Types:**
  - **SRAM (Static RAM):** Flip-flop design, fast, expensive, low density, no refresh needed. Used in L1/L2/L3 cache.
  - **DRAM (Dynamic RAM):** Capacitor + transistor design, slower, cheap, dense, requires periodic refresh. Used in main memory.
  - **ROM (Read-Only Memory):** Non-volatile, stores firmware/boot logic.
- **Memory Hierarchy & Locality:** Layered architecture designed to achieve effective access speed of registers/caches with capacity/cost of disks, leveraging temporal and spatial locality.
- **Memory Chip Design:** Combining multiple RAM/ROM chips of smaller size/bit-width to build a larger target memory module, designing address decoder logic based on memory maps.

---

## How to Solve Questions in This Exam

### Pipeline Speedup and CPI Calculations (Q1, Q5)
1. **Pipelined Time Formula:** Use $T_p = (k + n - 1) \cdot t_p$. Ensure you don't confuse $n$ (instructions) and $k$ (stages).
2. **Speedup:** Compute $S = \frac{T_{np}}{T_p}$. It should be a number, usually between 1 and $k$.
3. **CPI with Hazards:**
   - Standard ideal CPI = 1.
   - For every stall cycle per instruction, add that value. E.g., 1 stall cycle per 4 instructions $\implies \text{CPI} = 1 + 0.25 = 1.25$.
   - Calculate effective time: $\text{CPI} \times t_p$.

### Drawing Space-Time Diagrams (Q2)
1. **Set up the grid:** Stages (rows, $S1$ to $Sk$) vs. Clock Cycles (columns, 1 to $k+n-1$).
2. **Stagger the tasks:** Task $i$ starts at Cycle $i$ in Stage 1 and progresses diagonally down-right to stage $k$ at Cycle $i+k-1$.
3. **Check final cycle:** Ensure the last task finishes at cycle $k + n - 1$.

### Identifying Data Hazards (Q4)
1. **Locate destination register of each instruction:** The register being written to (usually the first operand).
2. **Locate source registers of subsequent instructions:** Registers being read (usually the second and third operands).
3. **Check for RAW overlaps:** If a subsequent instruction reads a register before a previous instruction writes it, a RAW hazard exists.
4. **Choose resolution:**
   - If it's a RAW hazard between two ALU operations, **Forwarding** completely resolves it without stalls.
   - If it's a RAW hazard between a LOAD instruction and an ALU operation (LOAD-use), **Forwarding + 1-cycle stall** is required.

### Memory System Chip Count and Decoding Design (Q8)
1. **ROM Chip Count:** $\text{ROM count} = \frac{\text{ROM region size (bytes)}}{\text{ROM chip size (bytes)}}$.
2. **RAM Chip Count:** Pay attention to bit widths!
   - E.g., RAM region size is $7\text{ KB} = 7168\text{ bytes} = 7168 \times 8\text{ bits}$.
   - Available chip is $1024 \times 1\text{ bit}$.
   - $\text{RAM count} = \frac{7168 \times 8}{1024 \times 1} = 56\text{ chips}$ (organized as 7 rows of 8 chips in parallel to form 8-bit bytes).
3. **Address Bus Width:** Compute $\log_2(\text{Total capacity in bytes})$.
4. **Decoder Design:**
   - Partition address range into binary.
   - Identify which address bits are constant in each range (ROM vs RAM). Use those bits (e.g., $A_{12}, A_{11}, A_{10}$) as inputs to the chip-select decoder.

---

## Part 1: Instruction Pipelining [20 Marks]

### Q1 — Calculation | Bloom's: Apply | Difficulty: Medium | Marks: 4

**Question:**
A non-pipelined processor executes each instruction in $60\text{ ns}$. The processor is redesigned to use a **5-stage pipeline** with a clock cycle of $14\text{ ns}$.

**(a)** Calculate the time to execute 200 instructions without a pipeline. (1 Mark)
**(b)** Calculate the time to execute 200 instructions with the pipeline. (1 Mark)
**(c)** Calculate the speedup ratio. (1 Mark)
**(d)** What is the theoretical maximum speedup as the number of instructions approaches infinity? (1 Mark)

**Guide Answer:**

**(a) Non-pipelined Time:**
$$T_{np} = n \times t_n = 200 \times 60\text{ ns} = 12,000\text{ ns}$$

**(b) Pipelined Time:**
$$T_p = (k + n - 1) \times t_p = (5 + 200 - 1) \times 14\text{ ns} = 204 \times 14\text{ ns} = 2,856\text{ ns}$$

**(c) Speedup Ratio:**
$$S = \frac{T_{np}}{T_p} = \frac{12,000}{2,856} \approx 4.20$$

**(d) Theoretical Maximum Speedup:**
$$\lim_{n \to \infty} S = \frac{n \cdot k}{k + n - 1} \approx k = 5$$

As the number of instructions approaches infinity, the speedup approaches the number of pipeline stages ($k = 5$).

**Key Points to Include for Full Marks:**
- Correct formulas: $T_{np} = n \cdot t_n$ and $T_p = (k + n - 1) \cdot t_p$.
- Speedup = ratio of non-pipelined to pipelined time.
- Theoretical max = $k$ (the number of stages).

**Common Mistakes to Avoid:**
- Using $k \times n$ in the denominator for $T_p$ (that's $T_{np}$).
- Claiming speedup equals exactly $k$ for finite $n$.

---

### Q2 — Application (Design) | Bloom's: Apply | Difficulty: Medium | Marks: 4

**Question:**
Draw a space-time diagram for a **4-stage pipeline** processing **6 tasks**. Label each cell with the task number. How many clock cycles does it take to complete all 6 tasks?

**Guide Answer:**

**Space-Time Diagram:**
```text
Stage | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |  (Clock Cycles)
------+---+---+---+---+---+---+---+---+---+
  S1  |T1 |T2 |T3 |T4 |T5 |T6 |   |   |   |
  S2  |   |T1 |T2 |T3 |T4 |T5 |T6 |   |   |
  S3  |   |   |T1 |T2 |T3 |T4 |T5 |T6 |   |
  S4  |   |   |   |T1 |T2 |T3 |T4 |T5 |T6 |
```

**Total Clock Cycles:**
$$\text{Total Cycles} = k + n - 1 = 4 + 6 - 1 = 9\text{ cycles}$$

- The pipeline is **filling** during cycles 1–3 (not all stages are active).
- The pipeline is **fully utilized** from cycle 4 to cycle 6 (all 4 stages are processing different tasks).
- The pipeline is **draining** during cycles 7–9.

**Key Points to Include for Full Marks:**
- Correct diagonal staggering of tasks.
- Labeled axes (stages vs. clock cycles).
- Identification of filling, full utilization, and draining phases.

**Common Mistakes to Avoid:**
- Placing all tasks vertically (as if executing sequentially).
- Incorrect total cycle count.

---

### Q3 — Short Answer / Essay | Bloom's: Understand | Difficulty: Medium | Marks: 4

**Question:**
**(a)** Name the 6 stages of a typical instruction pipeline and briefly describe what each stage does. (3 Marks)
**(b)** Explain why increasing the number of pipeline stages does not always proportionally increase throughput. (1 Mark)

**Guide Answer:**

**(a) Six-Stage Pipeline:**

| Stage | Name | Description |
|---|---|---|
| S1 | **Fetch Instruction (FI)** | Read the instruction from memory using the PC. |
| S2 | **Decode Instruction (DI)** | Decode the opcode and identify the operands. |
| S3 | **Calculate Effective Address (EA)** | Compute the memory address for the operand (using addressing mode logic). |
| S4 | **Fetch Operand (FO)** | Read the operand from the calculated memory address. |
| S5 | **Execute Instruction (EI)** | Perform the operation in the ALU (e.g., add, subtract). |
| S6 | **Store Result (SR)** | Write the result to the destination register or memory location. |

**(b) Diminishing Returns:**
Increasing pipeline stages introduces several costs:
1. **Pipeline registers (latches)** between stages add delay to each cycle.
2. **Pipeline hazards** (data, control, structural) become more frequent and severe with deeper pipelines.
3. **Branch misprediction penalties** increase proportionally with pipeline depth (more stages must be flushed).
4. **Stage imbalance:** If stages have unequal work, the slowest stage becomes the bottleneck, and adding faster stages doesn't help.

**Key Points to Include for Full Marks:**
- All 6 stages named and described.
- At least 2 reasons for diminishing returns.

---

### Q4 — Short Answer / Essay | Bloom's: Analyse | Difficulty: Hard | Marks: 4

**Question:**
Consider a 5-stage pipeline (FI, DI, EA, FO, EI) executing the following instruction sequence:

```
I1: LOAD R1, 100      ; R1 ← M[100]
I2: ADD R2, R1, R3    ; R2 ← R1 + R3
I3: SUB R4, R2, R5    ; R4 ← R2 - R5
```

**(a)** Identify all data hazards in this sequence. (2 Marks)
**(b)** For each hazard, suggest a resolution technique (forwarding, stalling, or NOP insertion). (2 Marks)

**Guide Answer:**

**(a) Data Hazards:**

1. **RAW Hazard between I1 and I2 (R1):**
   - I1 writes to R1 (in the EI/Store stage).
   - I2 reads R1 (in the FO stage).
   - I2's FO stage occurs before I1's result is written back → **Read-After-Write (RAW) hazard**.

2. **RAW Hazard between I2 and I3 (R2):**
   - I2 writes to R2 (in the EI/Store stage).
   - I3 reads R2 (in the FO stage).
   - I3 reads R2 before I2 writes it → **RAW hazard**.

**(b) Resolution Techniques:**

1. **Hazard 1 (I1 → I2 on R1):**
   - **Forwarding (Data Bypassing):** Forward the loaded value from the memory output (after I1's FO stage) directly to I2's ALU input, bypassing the register file write.
   - **Alternative: Stalling (Pipeline Bubble):** Insert 1–2 NOPs between I1 and I2 to wait until R1 is written back. This reduces performance.
   - **Note:** LOAD-use hazards are particularly problematic because the data from memory isn't available until after the FO stage. Even with forwarding, a 1-cycle stall may be needed.

2. **Hazard 2 (I2 → I3 on R2):**
   - **Forwarding:** Forward the ALU result from I2's EI stage directly to I3's ALU input. This typically avoids any stall because the ALU result is available one cycle before it's needed.

**Key Points to Include for Full Marks:**
- Identify both RAW hazards with specific register names.
- Distinguish between ALU-result forwarding (no stall) and load-use forwarding (may need 1-cycle stall).

**Common Mistakes to Avoid:**
- Missing the I2 → I3 hazard.
- Confusing WAR/WAW hazards with RAW hazards.

---

### Q5 — Calculation | Bloom's: Apply | Difficulty: Hard | Marks: 4

**Question:**
A 6-stage pipeline has a clock cycle time of $5\text{ ns}$. Due to data and control hazards, the pipeline introduces an average of **1 stall cycle per 4 instructions**.

**(a)** Calculate the effective CPI (Cycles Per Instruction) of the pipelined processor. (1 Mark)
**(b)** Calculate the effective time per instruction. (1 Mark)
**(c)** If the non-pipelined equivalent takes $30\text{ ns}$ per instruction, what is the actual speedup? (1 Mark)
**(d)** How does this compare to the ideal speedup of $k = 6$? (1 Mark)

**Guide Answer:**

**(a) Effective CPI:**
- Ideal CPI for a pipeline = 1 cycle per instruction (one instruction completes each cycle after pipeline is full).
- Stall penalty: $1$ stall cycle per $4$ instructions = $0.25$ stall cycles per instruction.
$$\text{Effective CPI} = 1 + 0.25 = 1.25\text{ cycles/instruction}$$

**(b) Effective Time Per Instruction:**
$$T_{\text{eff}} = \text{CPI} \times t_p = 1.25 \times 5\text{ ns} = 6.25\text{ ns/instruction}$$

**(c) Actual Speedup:**
$$S = \frac{T_{np}}{T_{\text{eff}}} = \frac{30\text{ ns}}{6.25\text{ ns}} = 4.8$$

**(d) Comparison to Ideal:**
- Ideal speedup = $k = 6$.
- Actual speedup = $4.8$.
- Efficiency = $\frac{4.8}{6} \times 100\% = 80\%$.
- The pipeline achieves 80% of its theoretical maximum due to stall overhead.

**Key Points to Include for Full Marks:**
- CPI = 1 + stall rate.
- Effective time = CPI × cycle time.
- Show efficiency as a percentage.

---

## Part 2: Memory Types & Hierarchy [10 Marks]

### Q6 — Compare & Contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 3

**Question:**
Compare DRAM, SRAM, and ROM in a table covering: internal structure, volatility, speed, cost per bit, primary usage, and whether refresh is needed.

**Guide Answer:**

| Feature | DRAM | SRAM | ROM |
|---|---|---|---|
| **Internal Structure** | 1 transistor + 1 capacitor per bit | 4–6 transistors (flip-flop) per bit | Burned-in fuses or charge traps |
| **Volatility** | Volatile (loses data without power) | Volatile | Non-volatile (retains data without power) |
| **Speed** | Slow (capacitor charge/discharge + refresh overhead) | Fast (direct flip-flop switching) | Moderate (slower than SRAM, varies by type) |
| **Cost per Bit** | Low (very dense, simple structure) | High (large area per bit) | Low to moderate |
| **Primary Usage** | Main Memory | Cache Memory (L1, L2, L3) | Firmware, BIOS, boot code |
| **Refresh Needed?** | Yes (capacitors leak charge) | No | No |

**Key Points to Include for Full Marks:**
- DRAM needs refresh; SRAM does not.
- SRAM is fastest; ROM is non-volatile.
- Correct usage assignment (DRAM = main memory, SRAM = cache).

---

### Q7 — Short Answer / Essay | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
Explain the concept of the memory hierarchy. Why do computer systems use multiple levels of memory instead of using only the fastest type?

**Guide Answer:**
The memory hierarchy is a layered structure that organizes different types of memory based on **speed, size, and cost**:

1. **Registers** → Fastest, smallest, most expensive per bit (inside CPU).
2. **Cache (SRAM)** → Very fast, small, expensive.
3. **Main Memory (DRAM)** → Moderate speed, larger, cheaper.
4. **Secondary Storage (HDD/SSD)** → Slow, very large, very cheap.

**Why multiple levels?**
- Building an entire memory system from the fastest technology (like SRAM or registers) would be **prohibitively expensive** and physically impractical for large capacities.
- The hierarchy exploits **locality of reference** (temporal and spatial locality): most programs access a small subset of their total data at any given time.
- By caching frequently used data in faster, smaller memories and keeping the bulk of data in slower, larger memories, the system achieves an **effective access time close to the fastest level** at a **cost close to the cheapest level**.

**Key Points to Include for Full Marks:**
- Speed–cost–size trade-off.
- Locality of reference (temporal and spatial).
- Effective access time close to fastest level.

---

### Q8 — Calculation | Bloom's: Apply | Difficulty: Hard | Marks: 5

**Question:**
Design a memory system with the following specifications:
- Total memory capacity: **8 KB**
- Word size: **8 bits** (1 byte)
- Available ROM chips: $512 \times 8$ bits
- Available RAM chips: $1024 \times 1$ bit

The memory map allocates:
- Addresses `0x0000` to `0x03FF` (first 1 KB): ROM
- Addresses `0x0400` to `0x1FFF` (remaining 7 KB): RAM

**(a)** How many ROM chips are needed? (1 Mark)
**(b)** How many RAM chips are needed? (1 Mark)
**(c)** What is the total address bus width? (1 Mark)
**(d)** Describe the address decoding scheme for selecting between ROM and RAM regions. (2 Marks)

**Guide Answer:**

**(a) ROM Chips:**
- ROM region: 1 KB = $1024$ bytes.
- Each ROM chip: $512 \times 8$ bits = $512$ bytes.
$$\text{ROM chips} = \frac{1024}{512} = 2\text{ ROM chips}$$

**(b) RAM Chips:**
- RAM region: 7 KB = $7168$ bytes = $7168 \times 8$ bits.
- Each RAM chip: $1024 \times 1$ bit.
$$\text{RAM chips} = \frac{7168 \times 8}{1024 \times 1} = \frac{57,344}{1024} = 56\text{ RAM chips}$$

Organization: 7 rows × 8 chips per row.
- Each row of 8 chips provides $1024 \times 8$ bits (1 KB).
- 7 rows provide 7 KB.

**(c) Total Address Bus Width:**
- Total capacity: 8 KB = $8192$ bytes = $2^{13}$ bytes.
$$\text{Address bus width} = 13\text{ bits}$$

**(d) Address Decoding Scheme:**
- **Address Range Analysis:**
  - ROM: `0x0000` to `0x03FF` → $A_{12}A_{11}A_{10} = 000$ (first 1 KB).
  - RAM: `0x0400` to `0x1FFF` → $A_{12}A_{11}A_{10} = 001$ through `111` (remaining 7 KB).

- **ROM Selection:**
  - 2 ROM chips, each 512 bytes ($2^9$ locations).
  - Use $A_8 - A_0$ (9 address lines) directly to each ROM chip.
  - Use $A_9$ to select between the 2 ROM chips (via 1-to-2 decoder or direct chip select).
  - The ROM is selected when the upper address bits ($A_{12}$ to $A_{10}$) are `000`.

- **RAM Selection:**
  - 7 rows of 8 chips, each row is 1 KB ($2^{10}$ locations).
  - Use $A_9 - A_0$ (10 address lines) directly to each RAM chip.
  - Use $A_{12}$, $A_{11}$, $A_{10}$ through a decoder to select one of the 7 rows.
  - The RAM is enabled when the address is $\geq$ `0x0400`.

**Key Points to Include for Full Marks:**
- Correct chip counts (2 ROM, 56 RAM).
- 13-bit address bus.
- Clear separation of ROM and RAM address regions.
- Description of decoder usage for row/chip selection.

**Common Mistakes to Avoid:**
- Forgetting to multiply by 8 when converting RAM byte requirements to bit-wide chips.
- Using a single address line for both ROM and RAM without proper decoding.
