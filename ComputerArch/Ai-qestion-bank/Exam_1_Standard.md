# COA Practice Exam 1: Standard Introductory Level

This exam is modeled after the standard introductory exam style (`25.txt`). It contains a balanced mix of Essay, Multiple Choice, True/False, and standard Calculation problems.

---

## Part 1: Essay Questions [10 Marks]

### Q1 — Short Answer / Essay | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
Describe the three main components of a computer and their roles.

**Guide Answer:**
The three main components of a computer are:
1. **The Central Processing Unit (CPU):** It is the brain of the computer that fetches, decodes, and executes program instructions. It consists of the datapath (ALU and registers) and the control unit.
2. **Main Memory (RAM/ROM):** It stores program instructions and data currently needed by the CPU for execution. It is volatile (for RAM) and allows quick read/write access.
3. **The Input/Output (I/O) Subsystem:** It manages communication between the computer's CPU/memory and the external world (devices like keyboards, displays, storage disks, etc.) through specialized interfaces.

**Key Points to Include for Full Marks:**
- Explicit naming of the three components (CPU, Memory, I/O).
- Brief explanation of the role of each component showing how they interact.

**Common Mistakes to Avoid:**
- Omitting the I/O subsystem or combining it with memory.
- Confusing main memory with secondary storage (like hard drives).

---

### Q2 — Short Answer / Essay | Bloom's: Analyse | Difficulty: Medium | Marks: 2

**Question:**
Compare DRAM and SRAM in terms of physical structure, speed, cost, and typical usage in a computer system.

**Guide Answer:**
* **Structure:** DRAM consists of one transistor and one capacitor per bit (leaks charge, needs periodic refreshing). SRAM consists of flip-flop circuits (typically 4-6 transistors per bit, holds state as long as power is applied).
* **Speed:** SRAM is significantly faster than DRAM because it does not require refreshing and its transistor states switch instantly.
* **Cost & Density:** DRAM is cheaper and denser (can store more bits per chip area). SRAM is more expensive, larger, and runs hotter.
* **Usage:** DRAM is used for Main Memory. SRAM is used for high-speed Cache Memory (L1, L2, L3).

**Key Points to Include for Full Marks:**
- Mentioning capacitors (DRAM) vs. flip-flops (SRAM).
- Explicit reference to the refresh cycle requirement for DRAM.
- Correct identification of their typical roles (DRAM = Main Memory, SRAM = Cache).

**Common Mistakes to Avoid:**
- Stating that SRAM needs refreshing.
- Confusing which memory is faster or cheaper.

---

### Q3 — Short Answer / Essay | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
What is a page fault, and how does the operating system handle it when a process requests an address?

**Guide Answer:**
A page fault occurs when a process attempts to access a virtual memory address whose corresponding page is not currently loaded into physical memory (RAM) (indicated by a valid bit of 0 in the page table).

The OS handles it as follows:
1. **Trap to OS:** The CPU detects the invalid page reference and interrupts execution, transferring control to the OS page fault handler.
2. **Locate Page:** The OS locates the requested page on disk (swap space).
3. **Find Free Frame:** The OS finds a free physical frame in RAM. If RAM is full, it uses a replacement algorithm (like LRU or FIFO) to evict a victim page, writing it back to disk if modified.
4. **Load Page:** The OS reads the requested page from disk into the free RAM frame.
5. **Update Table & Resume:** The OS updates the page table (sets the valid bit to 1 and stores the frame number) and restarts the CPU instruction that caused the fault.

**Key Points to Include for Full Marks:**
- Definition involving the "valid bit = 0" in the page table.
- Sequential steps: CPU trap → disk lookup → frame allocation (with potential eviction) → disk-to-memory load → page table update → instruction restart.

**Common Mistakes to Avoid:**
- Stating that a page fault is a fatal error that crashes the program.
- Forgetting to mention updating the page table or restarting the instruction.

---

### Q4 — Short Answer / Essay | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
Explain the purpose of virtual memory and how it enhances overall system performance.

**Guide Answer:**
The primary purpose of virtual memory is to allow a system to execute processes whose combined memory requirements exceed the physical RAM capacity. It does this by using secondary storage (disk) as an extension of main memory, presenting a contiguous virtual address space to each process.

It enhances performance by:
1. **Enabling Multiprogramming:** Allowing more programs to run concurrently by keeping only active portions of each program in RAM.
2. **Efficient RAM Allocation:** Loading only required pages/segments on-demand (demand paging), leaving more RAM available for other processes.
3. **Protection & Isolation:** Isolating the address space of each process, preventing one process from reading/writing to another's space.
4. **Simplifying Programming:** Freeing developers from managing physical memory layout constraints.

**Key Points to Include for Full Marks:**
- Abstraction of physical memory using disk storage.
- Benefits: higher degree of multiprogramming, memory protection, and efficient resource use.

**Common Mistakes to Avoid:**
- Stating that virtual memory increases the speed of the CPU.
- Stating that virtual memory completely eliminates disk latency.

---

### Q5 — Short Answer / Essay | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
Explain the fetch-decode-execute cycle in the MARIE architecture, showing the Register Transfer Language (RTL) for the Fetch and Decode phases.

**Guide Answer:**
The fetch-decode-execute cycle is the sequence of steps a processor repeats to execute instructions.
* **Fetch:** The instruction is retrieved from memory at the address held in the Program Counter (PC) and placed in the Instruction Register (IR). The PC is incremented.
* **Decode:** The opcode is separated from the address part, and control signals are generated.
* **Execute:** The ALU and registers perform the operation specified by the instruction.

**RTL for Fetch:**
```text
MAR ← PC
IR ← M[MAR], PC ← PC + 1
```

**RTL for Decode:**
```text
MAR ← IR[11-0]
Decode IR[15-12]
```

**Key Points to Include for Full Marks:**
- PC holds the address of the next instruction.
- Exact RTL statements showing PC incrementing by 1 (since MARIE is word-addressable).
- IR holds the current instruction.
- Split of 16-bit IR into 4-bit opcode (`IR[15-12]`) and 12-bit address (`IR[11-0]`).

**Common Mistakes to Avoid:**
- Incrementing PC by 2 (MARIE is word-addressable, not byte-addressable).
- Mixing up MAR and MBR in RTL statements.

---

## Part 2: Choose the Correct Answer [10 Marks]

### Q6 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
Which memory type is typically used to implement cache memory?
a) DRAM  
b) SRAM  
c) ROM  
d) Flash Memory  

**Answer:** b) SRAM

**Key Points for Full Marks:** SRAM is used due to its speed.
**Common Mistakes:** Choosing DRAM (which is for main memory).

---

### Q7 — MCQ | Bloom's: Apply | Difficulty: Medium | Marks: 1

**Question:**
In a direct-mapped cache with 8 blocks, which cache block does main memory block 15 map to?
a) Block 0  
b) Block 7  
c) Block 15  
d) Block 1  

**Answer:** b) Block 7

**Guide Calculation:**
$$\text{Cache Block} = (\text{Memory Block}) \bmod (\text{Number of Cache Blocks})$$
$$\text{Cache Block} = 15 \bmod 8 = 7$$

**Key Points for Full Marks:** Show the modulo calculation step.
**Common Mistakes:** Selecting Block 15 (which doesn't exist in an 8-block cache).

---

### Q8 — MCQ | Bloom's: Apply | Difficulty: Easy | Marks: 1

**Question:**
What is the postfix equivalent of the infix expression: $(A + B) * C$?
a) $A\ B\ +\ C\ *$  
b) $A\ B\ C\ *\ +$  
c) $A\ B\ +\ *\ C$  
d) $A\ B\ C\ +\ *$  

**Answer:** a) $A\ B\ +\ C\ *$

**Key Points for Full Marks:** Parentheses dictate that $A + B$ is evaluated first, producing $AB+$, then multiplied by $C$, resulting in $AB+C*$.
**Common Mistakes:** Forgetting order of operations or placing operators incorrectly.

---

### Q9 — MCQ | Bloom's: Apply | Difficulty: Easy | Marks: 1

**Question:**
How many bits are needed to address 32 general-purpose CPU registers?
a) 4 bits  
b) 5 bits  
c) 6 bits  
d) 32 bits  

**Answer:** b) 5 bits

**Guide Calculation:**
$$2^x = 32 \implies x = \log_2(32) = 5\text{ bits}$$

**Key Points for Full Marks:** $\log_2(N)$ formula.
**Common Mistakes:** Choosing 32 bits.

---

### Q10 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
A big-endian architecture stores:
a) The least significant byte of a word at the lowest memory address.  
b) The most significant byte of a word at the lowest memory address.  
c) Bytes in reverse bit order.  
d) The instruction opcode in the least significant bits.  

**Answer:** b) The most significant byte of a word at the lowest memory address.

**Key Points for Full Marks:** Big-endian puts the "big end" (MSB) first in memory.
**Common Mistakes:** Confusing it with little-endian (which stores LSB at lowest address).

---

### Q11 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
What must be done periodically to maintain the data contents of Dynamic RAM (DRAM)?
a) Defragmentation  
b) Refreshing  
c) Rebooting  
d) Compacting  

**Answer:** b) Refreshing

**Key Points for Full Marks:** DRAM capacitors leak charge and require periodic electrical refreshing.
**Common Mistakes:** Choosing defragmentation (disk optimization).

---

### Q12 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Question:**
Which type of pipeline hazard occurs when a instruction requires the output of a previous instruction that has not yet completed execution?
a) Structural hazard  
b) Control hazard  
c) Data hazard  
d) Memory hazard  

**Answer:** c) Data hazard

**Key Points for Full Marks:** Data hazard involves read/write dependencies between overlapping instructions.
**Common Mistakes:** Choosing structural hazard (resource conflict) or control hazard (branching).

---

### Q13 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
Which CPU architecture family uses zero-operand instructions?
a) Accumulator-based architecture (e.g., MARIE)  
b) General-Purpose Register (GPR) architecture  
c) Stack-based architecture  
d) Three-address register architecture  

**Answer:** c) Stack-based architecture

**Key Points for Full Marks:** Stack architectures use operations (like ADD) that pop implicit operands from the top of the stack and push results back.
**Common Mistakes:** Choosing accumulator (uses 1 operand).

---

### Q14 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
What are the two principal parts of a CPU?
a) ALU and Registers  
b) Datapath and Control Unit  
c) Cache and Main Memory  
d) Input/Output interface and Bus  

**Answer:** b) Datapath and Control Unit

**Key Points for Full Marks:** Datapath (registers/ALU/bus) and Control Unit (decoding/coordination).
**Common Mistakes:** Choosing ALU and Registers (which are parts of the datapath).

---

### Q15 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Question:**
If a system has 16-bit instructions, 4 bits for opcode, and wants to access a word-addressable memory of 4K words, what is the address field width and does it fit?
a) 12 bits, fits exactly.  
b) 16 bits, does not fit.  
c) 8 bits, requires scaling.  
d) 10 bits, fits with space left.  

**Answer:** a) 12 bits, fits exactly.

**Guide Calculation:**
$$4\text{K words} = 4096 = 2^{12} \text{ words} \implies 12\text{ bits needed}.$$
$$\text{Total size} = 4\text{ bits (opcode)} + 12\text{ bits (address)} = 16\text{ bits}.$$

**Key Points for Full Marks:** $2^{12} = 4\text{K}$.
**Common Mistakes:** Confusing memory words with bytes or incorrectly computing $2^{12}$.

---

## Part 3: True/False Questions [10 Marks]

*State whether the statement is True or False, and provide a brief justification.*

### Q16 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Statement:**
Fully associative cache mapping generally has the lowest conflict miss rate among all cache mapping schemes.

**Answer:** True  
**Justification:** Because any memory block can reside in any cache line, there is no restriction causing conflict misses (unlike direct-mapped). Eviction only happens when the entire cache is full.

---

### Q17 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
The Memory Buffer Register (MBR) in MARIE temporarily holds data retrieved from, or ready to be written to, the secondary storage disk.

**Answer:** False  
**Justification:** The MBR temporarily holds data retrieved from or before placement in **main memory**, not secondary storage disk.

---

### Q18 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
Set-associative cache mapping represents a compromise between direct-mapped cache and fully associative cache in terms of speed, cost, and complexity.

**Answer:** True  
**Justification:** It groups blocks into sets. Searching a set is faster and cheaper than searching the whole cache (fully associative) but has fewer conflict misses than direct mapping.

---

### Q19 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
Hardwired control units and microprogrammed control units are the two general ways to implement a CPU's control unit.

**Answer:** True  
**Justification:** Hardwired control uses digital logic gates and flip-flops (very fast but inflexible). Microprogrammed control uses a control store (ROM) containing microinstructions (slower but easily modifiable).

---

### Q20 — True/False | Bloom's: Analyse | Difficulty: Hard | Marks: 1

**Statement:**
Increasing the size of a CPU cache memory will always improve overall system execution speed.

**Answer:** False  
**Justification:** While a larger cache can reduce the miss rate, it can increase the search latency (hit time) due to larger multiplexing/comparison circuitry, potentially slowing down the clock cycle or increasing cache access cycles.

---

### Q21 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Statement:**
Fully associative cache addresses do not require an index field.

**Answer:** True  
**Justification:** Since blocks can go anywhere, there is no set or index calculation needed to select a cache line. The address is divided solely into Tag and Offset fields.

---

### Q22 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
Cache memory is faster than CPU registers.

**Answer:** False  
**Justification:** Registers reside inside the CPU datapath and are accessed within a single clock cycle, making them the fastest memory. Cache memory (SRAM) is located outside the registers and is slightly slower.

---

### Q23 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
Virtual memory allows processes to run and allocate memory spaces larger than the physical memory size available.

**Answer:** True  
**Justification:** It maps the logical address space of processes to a combination of physical RAM frames and secondary disk swap space.

---

### Q24 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
A page fault always results in a program crash.

**Answer:** False  
**Justification:** A page fault is an expected event handled by the OS. The OS fetches the missing page from disk, updates the page table, and resumes the process. It only crashes if the address is illegal (segmentation fault).

---

### Q25 — True/False | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Statement:**
MARIE is a byte-addressable architecture.

**Answer:** False  
**Justification:** MARIE is a **word-addressable** architecture where each address points to a 16-bit word, not an 8-bit byte.

---

## Part 4: Problems & Calculation [10 Marks]

### Q26 — Calculation | Bloom's: Apply | Difficulty: Hard | Marks: 2

**Question:**
A memory system uses 16 memory chips, each with a capacity of $2\text{K} \times 8$-bit capacity. How many address bits are needed to select a chip in high-order interleaving? What is the total memory capacity in bytes?

**Solution:**
1. **Total Memory Capacity:**
   $$\text{Chips} = 16$$
   $$\text{Capacity per chip} = 2\text{K} \times 8\text{ bits} = 2\text{KB}$$
   $$\text{Total Capacity} = 16 \times 2\text{KB} = 32\text{KB}$$

2. **Address Bits Calculation:**
   * Total capacity is $32\text{KB} = 32,768\text{ bytes} = 2^{15}\text{ bytes}$.
   * Therefore, the system requires a total of $15$ address bits.

3. **Interleaving Chip Selection:**
   * In **high-order interleaving**, the highest-order address bits are used to select the chip, while the lower-order bits address locations within the chosen chip.
   * Number of chips = $16 = 2^4$.
   * Therefore, $4$ address bits (the most significant bits, e.g., $A_{14}$ to $A_{11}$) are needed to select the chip.

**Key Points to Include for Full Marks:**
- Show total capacity computation ($32\text{KB}$).
- Show total address bits ($15$ bits).
- Identify that the highest $4$ bits are used for chip selection in high-order interleaving.

**Common Mistakes to Avoid:**
- Using low-order bits for chip selection (that is low-order interleaving).
- Confusing bits with bytes.

---

### Q27 — Calculation | Bloom's: Apply | Difficulty: Medium | Marks: 2

**Question:**
A direct-mapped cache has 128 blocks, and each block is 64 bytes. The main memory address is 32 bits. Calculate the bit widths of:
1. Offset field
2. Index field
3. Tag field

**Solution:**
1. **Offset Bits:**
   * Block size = $64\text{ bytes} = 2^6\text{ bytes}$.
   * Offset field = $\log_2(64) = 6\text{ bits}$.

2. **Index Bits:**
   * Number of blocks = $128 = 2^7$ blocks.
   * Index field = $\log_2(128) = 7\text{ bits}$.

3. **Tag Bits:**
   * Total address bits = $32$ bits.
   * Tag field = $\text{Total Address} - (\text{Index} + \text{Offset})$
   * Tag field = $32 - (7 + 6) = 32 - 13 = 19\text{ bits}$.

**Key Points to Include for Full Marks:**
- Explicit formula and calculations for Offset, Index, and Tag fields.
- Correct final bit widths: Offset = 6, Index = 7, Tag = 19.

**Common Mistakes to Avoid:**
- Adding the numbers incorrectly.
- Swapping the roles of Index and Offset fields.

---

### Q28 — Calculation | Bloom's: Apply | Difficulty: Medium | Marks: 2

**Question:**
A 2-way set-associative cache has 12 index bits and 32-byte blocks. What is the total cache size?

**Solution:**
1. **Number of Sets:**
   $$\text{Number of sets} = 2^{\text{Index bits}} = 2^{12} = 4096\text{ sets}$$

2. **Total Blocks:**
   * Since it is a **2-way** set-associative cache, there are 2 blocks per set.
   $$\text{Total blocks} = 2 \times 4096 = 8192\text{ blocks}$$

3. **Total Cache Size:**
   $$\text{Cache Size} = \text{Total blocks} \times \text{Block size}$$
   $$\text{Cache Size} = 8192 \times 32\text{ bytes} = 262,144\text{ bytes} = 256\text{ KB}$$

**Key Points to Include for Full Marks:**
- Show calculations for sets ($2^{12} = 4096$).
- Multiply sets by associativity ($2$) to get blocks.
- Convert final answer to KB ($256\text{ KB}$).

**Common Mistakes to Avoid:**
- Forgetting to multiply by 2 (calculating for a direct-mapped cache instead of 2-way).
- Mixing up bits and bytes during unit conversion.

---

### Q29 — Calculation | Bloom's: Apply | Difficulty: Medium | Marks: 2

**Question:**
A system uses 14-bit virtual addresses with 1KB page size. How many bits are used for the virtual page number, and how many are used for the offset?

**Solution:**
1. **Offset Bits:**
   * Page size = $1\text{KB} = 1024\text{ bytes} = 2^{10}\text{ bytes}$.
   * Offset bits = $\log_2(1024) = 10\text{ bits}$.

2. **Page Number Bits:**
   * Total virtual address size = $14$ bits.
   * Page number bits = $\text{Total virtual address} - \text{Offset}$
   * Page number bits = $14 - 10 = 4\text{ bits}$.

**Key Points to Include for Full Marks:**
- Show that page size of $1\text{KB}$ requires $10$ bits of offset.
- Show subtraction to find page number bits ($4$).

**Common Mistakes to Avoid:**
- Assuming page size is $1000$ bytes instead of $1024$ bytes.
- Getting the subtraction backwards.

---

### Q30 — Calculation | Bloom's: Apply | Difficulty: Hard | Marks: 2

**Question:**
Suppose a byte-addressable memory contains 1MB and cache consists of 32 blocks, where each block contains 16 bytes. Determine where the main memory address `0x326A0` maps to in cache using **Direct Mapping**.

**Solution:**
1. **Understand Main Memory Parameters:**
   * Memory size = $1\text{MB} = 2^{20}\text{ bytes} \implies 20\text{ address bits}$.
   * Address = `0x326A0` = `0011 0010 0110 1010 0000` in binary.

2. **Direct Mapping Address Fields:**
   * Offset bits = $\log_2(16\text{ bytes per block}) = 4\text{ bits}$.
   * Index (Block) bits = $\log_2(32\text{ cache blocks}) = 5\text{ bits}$.
   * Tag bits = $20 - (5 + 4) = 11\text{ bits}$.

3. **Break Down Binary Address:**
   * Address: `0011 0010 0110 1010 0000`
   * Let's partition the 20-bit address into Tag (11 bits), Index (5 bits), and Offset (4 bits):
     * Tag: `0011 0010 011` (binary) = `0x193`
     * Index: `0 1010` (binary) = `10` (decimal) = `0x0A`
     * Offset: `0000` (binary) = `0` (decimal) = `0x0`

4. **Result:**
   * The address `0x326A0` maps to **cache block 10** (or `0x0A` / binary `01010`).

**Key Points to Include for Full Marks:**
- Break down the 20-bit address correctly.
- Establish bit widths (Tag = 11, Index = 5, Offset = 4).
- Show the binary partition and extract the index bits `01010` to get block 10.

**Common Mistakes to Avoid:**
- Using incorrect address sizes (e.g., assuming 32-bit addresses instead of 1MB = 20-bit address space).
- Mapping based on word count instead of byte address.
