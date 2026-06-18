# COA Practice Exam 3: Advanced Calculations & Control Logic

This exam focuses on quantitative evaluation and calculations: expanding opcodes, multi-level cache mapping, virtual memory address translation, Effective Access Time (EAT), and pipeline branching/hazards.

---

## Question 1: Expanding Opcode Design [6 Marks]

**Question:**
A system uses 8-bit instructions. We want to support the following instruction formats:
1. 3 instructions with two 3-bit operands
2. 2 instructions with one 4-bit operand
3. 4 instructions with one 3-bit operand

Is it possible to encode this instruction set? Show the mathematical verification using the fraction-of-states method, and then design a concrete binary prefix encoding scheme for the opcodes.

### Guide Answer:

**1. Mathematical Verification (State Space Analysis):**
* The instruction length is 8 bits, which gives a total of $2^8 = 256$ possible state combinations.
* Let's calculate the state combinations consumed by each instruction class:
  * **Class 1 (Two 3-bit operands):**
    * Uses $3$ opcodes.
    * Each instruction has $3 + 3 = 6$ operand bits.
    * States consumed = $3 \times 2^3 \times 2^3 = 3 \times 8 \times 8 = 192$ states.
  * **Class 2 (One 4-bit operand):**
    * Uses $2$ opcodes.
    * Each instruction has $4$ operand bits.
    * States consumed = $2 \times 2^4 = 2 \times 16 = 32$ states.
  * **Class 3 (One 3-bit operand):**
    * Uses $4$ opcodes.
    * Each instruction has $3$ operand bits.
    * States consumed = $4 \times 2^3 = 4 \times 8 = 32$ states.
* **Total States Needed:**
  $$\text{Total States} = 192 + 32 + 32 = 256\text{ states}$$
* Since the total states required ($256$) is exactly equal to the total available states ($256$), the instruction set **can be successfully encoded** with zero wasted codes.

**2. Opcode Design (Binary Prefix Scheme):**
* Let $Op_1$ be the prefix for Class 1, $Op_2$ for Class 2, and $Op_3$ for Class 3.
* **Class 1:** (2-bit opcode + two 3-bit operands = 8 bits)
  * Since we have 3 instructions, we can use the following prefixes:
    * `00` + 6 operand bits
    * `01` + 6 operand bits
    * `10` + 6 operand bits
  * The prefix `11` is left for expansion. This frees up $1/4$ of the state space ($64$ states).
* **Class 2:** (4-bit opcode + one 4-bit operand = 8 bits)
  * The prefix must start with `11`.
  * Since we have a 4-bit operand, the opcode is 4 bits long.
  * Within the `11xx` range, we need 2 opcodes:
    * `1100` + 4 operand bits
    * `1101` + 4 operand bits
  * Prefixes `1110` and `1111` are left for expansion (frees up $2/16 \times 256 = 32$ states).
* **Class 3:** (5-bit opcode + one 3-bit operand = 8 bits)
  * The prefix must start with `1110` or `1111`.
  * Since we have a 3-bit operand, the opcode is 5 bits long.
  * We have 4 instructions. We can split the remaining prefixes:
    * `11100` + 3 operand bits
    * `11101` + 3 operand bits
    * `11110` + 3 operand bits
    * `11111` + 3 operand bits

**Summary of Encoding Table:**

| Instruction Class | Format | Opcodes | Range / Count |
|---|---|---|---|
| **Class 1** | `OP (2b) \| OpA (3b) \| OpB (3b)` | `00`, `01`, `10` | 3 instructions |
| **Class 2** | `OP (4b) \| OpA (4b)` | `1100`, `1101` | 2 instructions |
| **Class 3** | `OP (5b) \| OpA (3b)` | `11100`, `11101`, `11110`, `11111` | 4 instructions |

**Key Points to Include for Full Marks:**
- Show state allocation math explicitly (e.g. $3 \times 64 = 192$, etc.).
- Identify that the sum of states equals $256$.
- Present a prefix table showing no overlap in variable-length opcodes.

**Common Mistakes to Avoid:**
- Overlapping prefixes (e.g., using `11` as an opcode for Class 1 while using `1100` for Class 2).
- Incorrect calculation of binary powers (e.g., $2^3 = 6$ instead of $8$).

---

## Question 2: Memory Hierarchy & Cache Effective Access Time [8 Marks]

**(a)** Consider a computer system with cache memory access time of $5\text{ ns}$ and main memory access time of $80\text{ ns}$. The system has a cache hit rate of $95\%$.
Calculate the Effective Access Time (EAT) under two design conditions:
1. **Concurrent Access Model:** The CPU accesses the cache and main memory in parallel. If there is a cache hit, the memory access is aborted. (2 Marks)
2. **Sequential Access Model:** The CPU accesses the cache first. If a cache miss occurs, the CPU then accesses main memory. (2 Marks)

**(b)** Suppose the cache parameters are changed: we add an L2 cache between L1 and Main Memory with an access time of $15\text{ ns}$ and a local hit rate of $80\%$. The L1 cache has a hit rate of $90\%$. Assuming sequential access across all three levels, calculate the new EAT. (4 Marks)

### Guide Answer:

**(a) EAT Calculations:**
1. **Concurrent Access Model:**
   * Formula:
     $$\text{EAT} = H \times T_c + (1 - H) \times T_m$$
     $$\text{EAT} = 0.95 \times 5\text{ ns} + (1 - 0.95) \times 80\text{ ns}$$
     $$\text{EAT} = 4.75\text{ ns} + 0.05 \times 80\text{ ns} = 4.75\text{ ns} + 4\text{ ns} = 8.75\text{ ns}$$

2. **Sequential Access Model:**
   * Formula (if cache misses, the time to search the cache is added to the memory access time):
     $$\text{EAT} = T_c + (1 - H) \times T_m$$
     $$\text{EAT} = 5\text{ ns} + (1 - 0.95) \times 80\text{ ns}$$
     $$\text{EAT} = 5\text{ ns} + 0.05 \times 80\text{ ns} = 5\text{ ns} + 4\text{ ns} = 9\text{ ns}$$

**(b) Multi-level (L1, L2, L3/Main Memory) Sequential EAT:**
* Parameters:
  * L1 hit rate ($H_1$) = 0.90, access time ($T_1$) = $5\text{ ns}$
  * L2 hit rate ($H_2$) = 0.80, access time ($T_2$) = $15\text{ ns}$
  * Main Memory access time ($T_m$) = $80\text{ ns}$
* Sequential Search Sequence:
  1. Access L1. Takes $T_1 = 5\text{ ns}$.
  2. If L1 misses (probability $1 - H_1 = 0.10$): Access L2. Takes $T_2 = 15\text{ ns}$.
  3. If L2 also misses (probability $(1 - H_1) \times (1 - H_2) = 0.10 \times 0.20 = 0.02$): Access Main Memory. Takes $T_m = 80\text{ ns}$.
* **Formula:**
  $$\text{EAT} = T_1 + (1 - H_1) \times [T_2 + (1 - H_2) \times T_m]$$
  $$\text{EAT} = 5 + 0.10 \times [15 + (1 - 0.80) \times 80]$$
  $$\text{EAT} = 5 + 0.10 \times [15 + 0.20 \times 80]$$
  $$\text{EAT} = 5 + 0.10 \times [15 + 16] = 5 + 0.10 \times [31]$$
  $$\text{EAT} = 5 + 3.1 = 8.1\text{ ns}$$

**Key Points to Include for Full Marks:**
- Correctly identify parallel vs. sequential formulas for part (a).
- Show expansion steps for part (b) using local hit rates and sequential miss penalties.
- Include units (`ns`) in the final answers.

**Common Mistakes to Avoid:**
- Using concurrent formula for sequential design.
- Incorrectly multiplying global hit rates in L2 calculations instead of using local rates.

---

## Question 3: Cache Mapping & Address Translation [8 Marks]

**Question:**
A computer has a byte-addressable physical address space of $16\text{ MB}$ ($2^{24}$ bytes). The cache memory has a total capacity of $64\text{ KB}$ ($2^{16}$ bytes), and the block size is $64\text{ bytes}$.
Determine the number of Tag, Index, and Offset bits, and show how the address `0x3F2A15` splits for:
**(a)** Direct-mapped cache. (3 Marks)  
**(b)** 4-way set-associative cache. (3 Marks)  
**(c)** Fully associative cache. (2 Marks)  

### Guide Answer:

**Basic Parameters:**
* Physical Address Space = $16\text{ MB} = 2^{24}$ bytes $\implies 24$ address bits.
* Block Size = $64\text{ bytes} = 2^6$ bytes $\implies$ Offset = $6\text{ bits}$.
* Physical address in binary: `0x3F2A15` = `0011 1111 0010 1010 0001 0101` (24 bits).

---

### (a) Direct-Mapped Cache:
1. **Fields:**
   * Offset = $6\text{ bits}$.
   * Total Cache Blocks = $\frac{\text{Cache Size}}{\text{Block Size}} = \frac{64\text{ KB}}{64\text{ bytes}} = 1024\text{ blocks} = 2^{10}\text{ blocks}$.
   * Index bits = $\log_2(1024) = 10\text{ bits}$.
   * Tag bits = $24 - (10 + 6) = 8\text{ bits}$.
2. **Address Partitioning:**
   * Write binary address: `00111111 0010101000 010101`
   * Partition:
     * **Tag (8 bits):** `00111111` $\implies$ `0x3F`
     * **Index (10 bits):** `0010101000` $\implies$ `0x0A8` (or $168$ in decimal)
     * **Offset (6 bits):** `010101` $\implies$ `0x15` (or $21$ in decimal)

---

### (b) 4-Way Set-Associative Cache:
1. **Fields:**
   * Offset = $6\text{ bits}$.
   * Total Blocks = $1024$.
   * Number of Sets = $\frac{\text{Total Blocks}}{\text{Way}} = \frac{1024}{4} = 256\text{ sets} = 2^8\text{ sets}$.
   * Index (Set Select) bits = $\log_2(256) = 8\text{ bits}$.
   * Tag bits = $24 - (8 + 6) = 10\text{ bits}$.
2. **Address Partitioning:**
   * Write binary address: `0011111100 10101000 010101`
   * Partition:
     * **Tag (10 bits):** `0011111100` $\implies$ `0x0FC`
     * **Index (8 bits):** `10101000` $\implies$ `0xA8` (or $168$ in decimal)
     * **Offset (6 bits):** `010101` $\implies$ `0x15` (or $21$ in decimal)

---

### (c) Fully Associative Cache:
1. **Fields:**
   * Offset = $6\text{ bits}$.
   * Index bits = $0$ (No index).
   * Tag bits = $24 - 6 = 18\text{ bits}$.
2. **Address Partitioning:**
   * Write binary address: `001111110010101000 010101`
   * Partition:
     * **Tag (18 bits):** `001111110010101000` $\implies$ `0x0FC28`
     * **Offset (6 bits):** `010101` $\implies$ `0x15` (or $21$ in decimal)

---

**Key Points to Include for Full Marks:**
- Correct calculation of offset bits ($6$).
- Correct index bit calculations for direct ($10$) and 4-way set-associative ($8$).
- Correct binary-to-hex conversion of the partitioned address fields.

**Common Mistakes to Avoid:**
- Dividing cache size by way count incorrectly.
- Omitting binary grouping steps when extracting hex fields.

---

## Question 4: Virtual Memory & Address Translation [8 Marks]

**Question:**
A virtual memory system uses 16-bit virtual addresses, 16-bit physical addresses, and a page size of $512\text{ bytes}$.
**(a)** How many bits are used for the virtual page number ($VPN$) and page offset? (2 Marks)  
**(b)** The page table for the active process is as follows:

| Virtual Page Number (VPN) | Frame Number (Hex) | Valid Bit |
|:---:|:---:|:---:|
| `0` | `0x1A` | `1` |
| `1` | `0x04` | `1` |
| `2` | `0x02` | `0` |
| `3` | `0x12` | `1` |

For each of the following virtual addresses:
1. `0x03FF` (2 Marks)
2. `0x052A` (2 Marks)

Translate to physical address, or explain what happens if it cannot be translated. (Show all calculation steps).

**(c)** If a physical memory access takes $100\text{ ns}$ and a page fault takes $8\text{ ms}$ to handle, calculate the Effective Access Time (EAT) of the memory system assuming a page fault rate of $0.1\%$. Include the page table lookup time (which is stored in physical memory). (2 Marks)

### Guide Answer:

**(a) Bit Widths:**
* Page size = $512\text{ bytes} = 2^9$ bytes $\implies$ Offset = $9\text{ bits}$.
* Virtual address = 16 bits.
* Virtual Page Number (VPN) bits = $16 - 9 = 7\text{ bits}$.

**(b) Translation:**
1. **Virtual Address `0x03FF`:**
   * Convert to binary: `0000 0011 1111 1111`
   * Split into VPN (highest 7 bits) and Offset (lowest 9 bits):
     * VPN: `0000001` (binary) = `1` (decimal)
     * Offset: `1 1111 1111` (binary) = `0x1FF`
   * Lookup VPN `1` in Page Table:
     * Frame Number = `0x04`
     * Valid Bit = `1` (Page is in memory)
   * Construct Physical Address:
     * Combined: Frame Number + Offset = `0x04` (in binary: `0000 0100` for 7 bits) + `1 1111 1111` (9 bits)
     * Physical address: `0000 1001 1111 1111` = `0x09FF`.

2. **Virtual Address `0x052A`:**
   * Convert to binary: `0000 0101 0010 1010`
   * Split into VPN (7 bits) and Offset (9 bits):
     * VPN: `0000010` (binary) = `2` (decimal)
     * Offset: `1 0010 1010` (binary) = `0x12A`
   * Lookup VPN `2` in Page Table:
     * Valid Bit = `0` (Page is on disk)
   * **Result:** A **page fault** occurs. The CPU halts the execution of the process and traps to the OS page fault handler to fetch page 2 from disk.

**(c) EAT with Page Faults:**
* Page fault rate ($p$) = $0.1\% = 0.001$.
* Accessing memory requires:
  1. Accessing page table in main memory ($100\text{ ns}$).
  2. Accessing the actual data in main memory ($100\text{ ns}$).
  * Total normal access time = $100\text{ ns} + 100\text{ ns} = 200\text{ ns}$.
* Page fault penalty ($T_{pf}$) = $8\text{ ms} = 8,000,000\text{ ns}$.
* **Formula:**
  $$\text{EAT} = (1 - p) \times \text{Normal Access Time} + p \times T_{pf}$$
  $$\text{EAT} = (1 - 0.001) \times 200\text{ ns} + 0.001 \times 8,000,000\text{ ns}$$
  $$\text{EAT} = 0.999 \times 200\text{ ns} + 8,000\text{ ns} = 199.8\text{ ns} + 8000\text{ ns} = 8199.8\text{ ns} \approx 8.2\text{ \mu s}$$

**Key Points to Include for Full Marks:**
- Virtual address splitting into 7-bit VPN and 9-bit Offset.
- Identification of page fault condition for address 2.
- Doubling physical memory access time in EAT formula (1 lookup + 1 access).

**Common Mistakes to Avoid:**
- Forgetting that the page table lookup itself requires a memory access (assuming access time is only $100\text{ ns}$ instead of $200\text{ ns}$).
- Mixing units (adding ms directly to ns without converting to $8,000,000\text{ ns}$).
