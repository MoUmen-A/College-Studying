# COA Practice Exam 9: Virtual Memory & Address Translation

This exam provides deep coverage of virtual memory systems: paging, segmentation, page tables, page fault handling, TLBs, EAT with paging, and fragmentation types.

---

## Topic Summary

This exam covers the following core concepts from the COA course:

- **Virtual Memory Overview:** Provides processes with a large, contiguous, private address space by abstraction over physical RAM and secondary disk storage.
- **Paging Systems:**
  - Memory is divided into fixed-size blocks: **pages** (logical) and **frames** (physical).
  - Virtual addresses are split: `[Virtual Page Number (VPN) | Offset]`.
  - Physical addresses are split: `[Physical Frame Number (PFN) | Offset]`.
  - The **offset** is identical in both virtual and physical addresses.
  - Page Table Entry (PTE) flags: **Valid bit** (1 = in RAM, 0 = Page Fault), **Dirty bit** (1 = modified, write-back to disk required on eviction).
- **Segmentation:** Memory is divided into variable-size blocks based on logical structures (code, stack, heap). Leads to external fragmentation (wasted space between segments) rather than internal fragmentation (wasted space within a page).
- **TLB (Translation Lookaside Buffer):** A small, high-speed cache of recent address translations.
  - TLB Hit: Translation is instant; only 1 memory access to read the actual data.
  - TLB Miss: Extra memory accesses are required to walk the page table before retrieving data.
- **Effective Access Time (EAT) with VM:**
  - $\text{EAT}_{\text{no fault}} = H_{\text{TLB}} \cdot (T_{\text{TLB}} + T_{\text{mem}}) + (1 - H_{\text{TLB}}) \cdot (T_{\text{TLB}} + 2 \cdot T_{\text{mem}})$.
  - $\text{EAT}_{\text{full}} = (1 - p) \cdot \text{EAT}_{\text{no fault}} + p \cdot T_{\text{fault\_service}}$, where $p$ is the page fault rate.
- **Multi-Level Page Tables:** Reduces memory footprint of page tables by allocating sub-tables only for active address spaces.

---

## How to Solve Questions in This Exam

### Virtual/Physical Address Field Conversions (Q4, Q7)
1. **Find Page Offset bits:** $\text{Offset} = \log_2(\text{Page Size in bytes})$.
2. **Compute VPN bits:** $\text{VPN} = \text{Virtual Address bits} - \text{Offset}$.
3. **Compute PFN bits:** $\text{PFN} = \text{Physical Address bits} - \text{Offset}$.
4. **Number of virtual pages:** $2^{\text{VPN}}$.
5. **Page Table Size:** $\text{Number of entries (same as pages)} \times \text{Size of each PTE (bytes)}$.

### Translating Virtual Addresses via Page Table (Q5)
1. **Determine field widths:** Convert page size to get offset bits.
2. **Convert the hex address to binary:** Write it out completely.
3. **Partition the binary address:**
   - Extract the rightmost `Offset` bits.
   - Extract the remaining leftmost bits to get the `VPN`.
4. **Convert VPN to decimal:** Use this index to look up the entry in the page table.
5. **Perform validation check:**
   - If the Valid Bit = 0, stop and report a **Page Fault**.
   - If Valid Bit = 1, retrieve the PFN (convert from hex to binary if necessary).
6. **Construct Physical Address:** Concatenate the binary PFN and the binary Offset. Convert the result back to hex.

### EAT with TLB and Page Faults (Q6)
1. **Formulate the TLB paths:**
   - Hit time: $T_{\text{TLB}} + T_{\text{mem}}$.
   - Miss time: $T_{\text{TLB}} + 2 \cdot T_{\text{mem}}$ (1 access to read page table + 1 access to read data).
2. **Calculate EAT without page faults:** $H_{\text{TLB}} \cdot T_{\text{hit}} + (1 - H_{\text{TLB}}) \cdot T_{\text{miss}}$.
3. **Incorporate Page Faults:**
   - Ensure all time units are matched (convert $10\text{ ms}$ page fault service time to $10,000,000\text{ ns}$).
   - Use $\text{EAT}_{\text{full}} = (1 - p) \cdot \text{EAT}_{\text{no fault}} + p \cdot T_{\text{fault\_service}}$.

---

## Part 1: Virtual Memory Concepts [10 Marks]

### Q1 — Short Answer / Essay | Bloom's: Understand | Difficulty: Medium | Marks: 3

**Question:**
Explain the concept of demand paging. How does it differ from pre-paging? What is the advantage of demand paging in terms of memory utilization?

**Guide Answer:**

**Demand Paging:**
Pages are loaded into physical memory **only when they are needed** (i.e., when a page fault occurs). Initially, no pages of a process are in memory. As the process executes and references addresses, only the required pages are brought from disk into RAM.

**Pre-paging:**
The OS predicts which pages will be needed and loads them into memory **before** they are actually referenced, hoping to reduce future page faults.

**Advantages of Demand Paging:**
1. **Efficient Memory Utilization:** Only pages that are actually used occupy RAM, leaving more frames available for other processes.
2. **Faster Program Startup:** The program begins executing immediately without waiting for all pages to load.
3. **Support for Large Programs:** Programs larger than physical memory can run because only a small active subset of pages needs to be in RAM at any time.

**Key Points to Include for Full Marks:**
- Demand paging = load on fault; pre-paging = load in advance.
- Memory efficiency: only used pages occupy RAM.
- Faster startup since not all pages need to be loaded initially.

**Common Mistakes to Avoid:**
- Stating that demand paging loads all pages at program start.
- Confusing demand paging with demand segmentation.

---

### Q2 — Compare & Contrast | Bloom's: Analyse | Difficulty: Hard | Marks: 4

**Question:**
Compare paging and segmentation in detail. Your comparison must address:
**(a)** How memory is divided (fixed vs. variable size). (1 Mark)
**(b)** Types of fragmentation each produces. (1 Mark)
**(c)** Address translation mechanism. (1 Mark)
**(d)** Programmer visibility. (1 Mark)

**Guide Answer:**

| Aspect | Paging | Segmentation |
|---|---|---|
| **(a) Memory Division** | Memory is divided into **fixed-size** blocks called **pages** (logical) and **frames** (physical). Typical size: 4 KB. | Memory is divided into **variable-size** blocks called **segments**, corresponding to logical program structures (code, data, stack, heap). |
| **(b) Fragmentation** | Produces **internal fragmentation**: the last page of a process may not be fully used, wasting space within the frame. | Produces **external fragmentation**: as segments are allocated and deallocated, free memory becomes scattered into small, non-contiguous holes. |
| **(c) Address Translation** | Virtual address = `[Page Number | Offset]`. The Page Table maps page number → frame number. Physical address = Frame Number + Offset. | Virtual address = `[Segment Number | Offset]`. The Segment Table contains Base Address and Limit. Physical address = Base + Offset (after checking Offset < Limit). |
| **(d) Programmer Visibility** | **Invisible** to the programmer. The OS and hardware handle paging transparently. The programmer sees a flat, contiguous address space. | **Visible** to the programmer (or compiler). Segments reflect the logical structure of the program (e.g., code segment, data segment). |

**Key Points to Include for Full Marks:**
- Fixed-size (paging) vs. variable-size (segmentation).
- Internal fragmentation (paging) vs. external fragmentation (segmentation).
- Page table (frame lookup) vs. segment table (base + limit).
- Paging is transparent; segmentation is programmer-aware.

**Common Mistakes to Avoid:**
- Saying paging has external fragmentation.
- Saying segmentation uses fixed-size blocks.

---

### Q3 — Short Answer / Essay | Bloom's: Understand | Difficulty: Medium | Marks: 3

**Question:**
Explain the role of the valid bit in a page table entry. What happens when the CPU encounters a page table entry with valid bit = 0? Describe the complete sequence of events.

**Guide Answer:**

**Role of the Valid Bit:**
The valid bit indicates whether the corresponding page is currently **loaded in physical memory (RAM)**:
- Valid bit = **1**: The page is in RAM, and the frame number in the page table entry is valid. The address translation proceeds normally.
- Valid bit = **0**: The page is **not** in RAM (it is on disk or has not been allocated). Accessing this page triggers a **page fault**.

**Sequence of Events When Valid Bit = 0 (Page Fault):**

1. **CPU Exception (Trap):** The Memory Management Unit (MMU) detects the invalid bit and raises a page fault exception. The CPU saves the current state and transfers control to the OS page fault handler.

2. **Locate Page on Disk:** The OS consults internal tables to find the location of the requested page on the disk (swap space or file system).

3. **Find Free Frame:** The OS searches for a free physical frame in RAM.
   - If no free frame is available, the OS uses a **replacement algorithm** (LRU, FIFO, etc.) to select a **victim page** to evict.
   - If the victim page has been modified (dirty bit = 1), it must be written back to disk first.

4. **Load Page:** The OS initiates a disk I/O operation to read the requested page from disk into the free frame.

5. **Update Page Table:** The OS updates the page table entry:
   - Sets the frame number to the newly loaded frame.
   - Sets the valid bit to **1**.

6. **Restart Instruction:** The CPU restarts the instruction that caused the page fault. This time, the page is in RAM, and the access succeeds.

**Key Points to Include for Full Marks:**
- Valid bit = 1 means in RAM; valid bit = 0 means page fault.
- Complete sequence: trap → disk locate → frame allocation → disk I/O → page table update → instruction restart.
- Mention of dirty bit and victim page eviction when RAM is full.

**Common Mistakes to Avoid:**
- Stating that a page fault crashes the program.
- Forgetting to restart the faulting instruction.

---

## Part 2: Address Translation Calculations [20 Marks]

### Q4 — Calculation | Bloom's: Apply | Difficulty: Medium | Marks: 5

**Question:**
A virtual memory system has the following specifications:
- Virtual address: 20 bits
- Physical address: 16 bits
- Page size: 4 KB

**(a)** Calculate the number of bits for the virtual page number (VPN) and the page offset. (1 Mark)
**(b)** Calculate the number of bits for the physical frame number (PFN). (1 Mark)
**(c)** How many virtual pages can a process have? How many physical frames exist? (1 Mark)
**(d)** How many entries does the page table need? (1 Mark)
**(e)** If each page table entry is 2 bytes, what is the total size of the page table? (1 Mark)

**Guide Answer:**

**(a) VPN and Offset:**
- Page size = $4\text{ KB} = 4096 = 2^{12}$ bytes → **Offset = 12 bits**
- Virtual address = 20 bits
- **VPN = 20 − 12 = 8 bits**

**(b) Physical Frame Number:**
- Physical address = 16 bits
- **PFN = 16 − 12 = 4 bits**

**(c) Number of Pages and Frames:**
- Virtual pages = $2^{VPN} = 2^8 = 256$ pages
- Physical frames = $2^{PFN} = 2^4 = 16$ frames

**(d) Page Table Entries:**
- The page table must have one entry per virtual page.
- **Page table entries = 256**

**(e) Page Table Size:**
$$\text{Page table size} = 256 \times 2\text{ bytes} = 512\text{ bytes}$$

**Key Points to Include for Full Marks:**
- Offset bits from $\log_2(\text{page size})$.
- VPN and PFN from subtracting offset from virtual/physical address widths.
- Page table size = entries × bytes per entry.

---

### Q5 — Calculation | Bloom's: Apply | Difficulty: Hard | Marks: 5

**Question:**
Given the following virtual memory configuration:
- Virtual address: 24 bits
- Physical address: 20 bits
- Page size: 2 KB

And the partial page table:

| VPN (Decimal) | PFN (Hex) | Valid Bit |
|:---:|:---:|:---:|
| 0 | `0x0A` | 1 |
| 1 | `0x15` | 1 |
| 2 | `0x08` | 0 |
| 3 | `0x1F` | 1 |
| 4 | `0x03` | 1 |
| 5 | `0x12` | 0 |

Translate the following virtual addresses to physical addresses, or explain what happens:
**(a)** `0x000ABC` (2 Marks)
**(b)** `0x001234` (2 Marks)
**(c)** `0x002800` (1 Mark)

**Guide Answer:**

**Setup:**
- Page size = $2\text{ KB} = 2048 = 2^{11}$ bytes → Offset = 11 bits
- VPN bits = $24 - 11 = 13$ bits
- PFN bits = $20 - 11 = 9$ bits

**(a) Virtual Address `0x000ABC`:**
- Binary (24 bits): `0000 0000 0000 1010 1011 1100`
- VPN (13 bits): `0000000000001` = **1** (decimal)
- Offset (11 bits): `01010111100` = `0x2BC`
- Page Table Lookup: VPN 1 → PFN = `0x15`, Valid = 1 ✓
- PFN in 9-bit binary: `000010101`
- Physical Address = PFN (9 bits) + Offset (11 bits):
  - `000010101` + `01010111100` = `00001010101010111100`
  - = `0x0AABC`
- **Physical Address: `0x0AABC`**

**(b) Virtual Address `0x001234`:**
- Binary (24 bits): `0000 0000 0001 0010 0011 0100`
- VPN (13 bits): `0000000001001` = **9** (decimal)
  - Wait, let me recalculate: `0000 0000 0001 | 0010 0011 0100`
  - VPN (13 bits): `0000000000010` = **2** (decimal)
  - Offset (11 bits): `01000110100` = `0x234`
- Page Table Lookup: VPN 2 → Valid = **0** ❌
- **Result: PAGE FAULT.** The page is not in physical memory. The OS page fault handler is invoked to load page 2 from disk.

**(c) Virtual Address `0x002800`:**
- Binary (24 bits): `0000 0000 0010 1000 0000 0000`
- VPN (13 bits): `0000000000101` = **5** (decimal)
- Offset (11 bits): `00000000000` = `0x000`
- Page Table Lookup: VPN 5 → Valid = **0** ❌
- **Result: PAGE FAULT.** Page 5 is not loaded in physical memory.

**Key Points to Include for Full Marks:**
- Correct offset bits (11 for 2 KB pages).
- Proper VPN extraction from the virtual address.
- Physical address construction by concatenating PFN and offset.
- Identification of page faults for valid bit = 0.

**Common Mistakes to Avoid:**
- Incorrect binary-to-VPN conversion.
- Adding PFN and offset instead of concatenating.

---

### Q6 — Calculation | Bloom's: Apply | Difficulty: Hard | Marks: 5

**Question:**
A virtual memory system has the following parameters:
- Physical memory access time: $120\text{ ns}$
- TLB access time: $10\text{ ns}$
- TLB hit rate: $95\%$
- Page fault rate: $0.5\%$
- Page fault service time: $10\text{ ms}$

Assume that on a TLB miss, the page table must be accessed from physical memory (one extra memory access). Calculate:

**(a)** The EAT when there are no page faults (TLB-only system). (2 Marks)
**(b)** The full EAT including page faults. (3 Marks)

**Guide Answer:**

**(a) EAT Without Page Faults (TLB-only):**

- **TLB Hit:** Access TLB ($10\text{ ns}$) + Access memory for data ($120\text{ ns}$) = $130\text{ ns}$
- **TLB Miss:** Access TLB ($10\text{ ns}$) + Access memory for page table ($120\text{ ns}$) + Access memory for data ($120\text{ ns}$) = $250\text{ ns}$

$$\text{EAT}_{\text{no fault}} = 0.95 \times 130 + 0.05 \times 250$$
$$= 123.5 + 12.5 = 136\text{ ns}$$

**(b) Full EAT Including Page Faults:**

We incorporate the page fault rate ($p = 0.005$) into the calculation. A page fault occurs only on a TLB miss (since the TLB would have the translation if the page were in memory).

Effective page fault probability on any access: On a TLB miss (5% of accesses), we access the page table. Of all accesses, 0.5% result in a page fault.

$$\text{EAT}_{\text{full}} = (1 - p) \times \text{EAT}_{\text{no fault}} + p \times T_{\text{page fault}}$$

Where:
- $p = 0.005$
- $T_{\text{page fault}} = 10\text{ ms} = 10,000,000\text{ ns}$

$$\text{EAT}_{\text{full}} = (1 - 0.005) \times 136 + 0.005 \times 10,000,000$$
$$= 0.995 \times 136 + 50,000$$
$$= 135.32 + 50,000$$
$$= 50,135.32\text{ ns} \approx 50.1\text{ μs}$$

**Key Points to Include for Full Marks:**
- TLB hit path: TLB access + 1 memory access.
- TLB miss path: TLB access + 2 memory accesses (page table + data).
- Page fault penalty dominates EAT even at 0.5% rate.
- Convert ms to ns for consistent units.

**Common Mistakes to Avoid:**
- Forgetting the TLB access time on a hit.
- Not converting ms to ns (mixing units).
- Forgetting the double memory access on TLB miss.

---

### Q7 — Calculation | Bloom's: Apply | Difficulty: Medium | Marks: 5

**Question:**
A system has:
- 32-bit virtual addresses
- 28-bit physical addresses
- 8 KB page size

**(a)** How many bits are in the VPN and the page offset? (1 Mark)
**(b)** How many virtual pages can a process have? (1 Mark)
**(c)** How many physical frames exist? (1 Mark)
**(d)** If a two-level page table is used where the first level has 10 bits and the second level has the remaining VPN bits, how many entries does each level have? (2 Marks)

**Guide Answer:**

**(a) VPN and Offset:**
- Page size = $8\text{ KB} = 8192 = 2^{13}$ bytes → **Offset = 13 bits**
- VPN = $32 - 13 = 19$ bits
- PFN = $28 - 13 = 15$ bits

**(b) Number of Virtual Pages:**
$$\text{Virtual pages} = 2^{19} = 524,288\text{ pages}$$

**(c) Number of Physical Frames:**
$$\text{Physical frames} = 2^{15} = 32,768\text{ frames}$$

**(d) Two-Level Page Table:**
- First level: 10 bits → $2^{10} = 1024$ entries
- Second level: $19 - 10 = 9$ bits → $2^9 = 512$ entries per second-level table
- There can be up to $1024$ second-level page tables, each with $512$ entries.

**Advantage of two-level paging:**
A single-level page table would need $2^{19} = 524,288$ entries. If each entry is 4 bytes, the table is $2\text{ MB}$. With two-level paging, only the first-level table (1024 entries = 4 KB) must always be in memory. Second-level tables are loaded on demand.

**Key Points to Include for Full Marks:**
- Correct offset from $\log_2(8\text{K}) = 13$.
- Correct split of VPN into two levels.
- Explanation of memory savings with multi-level paging.

---

## Part 3: True/False [10 Marks]

### Q8 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
Virtual memory allows a process to use more memory than the physical RAM installed in the system.

**Answer:** True
**Justification:** Virtual memory maps the process's virtual address space to a combination of physical RAM and disk swap space. The process sees a large contiguous address space regardless of the actual RAM size.

---

### Q9 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Statement:**
In a paging system, the offset within a page is the same in both the virtual address and the physical address.

**Answer:** True
**Justification:** Address translation only changes the page/frame number. The offset within the page remains unchanged because the page size is the same in both virtual and physical memory.

---

### Q10 — True/False | Bloom's: Analyse | Difficulty: Hard | Marks: 1

**Statement:**
A higher page fault rate always leads to a higher Effective Access Time (EAT).

**Answer:** True
**Justification:** Page faults involve accessing the disk, which takes milliseconds (orders of magnitude slower than RAM access in nanoseconds). Any increase in page fault rate adds a massive penalty to EAT. Even a 0.01% increase in page fault rate can significantly degrade performance.

---

### Q11 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
Segmentation divides memory into fixed-size blocks called segments.

**Answer:** False
**Justification:** Segmentation divides memory into **variable-size** blocks called segments. Each segment corresponds to a logical unit of the program (code, data, stack) and has a different size. **Paging** uses fixed-size blocks.

---

### Q12 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Statement:**
A Translation Lookaside Buffer (TLB) is a small, fast cache that stores recently used page table entries to speed up address translation.

**Answer:** True
**Justification:** The TLB acts as a cache for the page table. On a TLB hit, the physical frame number is obtained directly from the TLB without accessing the page table in main memory, significantly reducing address translation time.

---

### Q13 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Statement:**
In a paging system, internal fragmentation occurs because the last page of a process may not be completely filled with data.

**Answer:** True
**Justification:** If a process's total memory requirement is not a perfect multiple of the page size, the last page will have unused space. This wasted space within the allocated page is called internal fragmentation. On average, half a page is wasted per process.

---

### Q14 — True/False | Bloom's: Analyse | Difficulty: Hard | Marks: 1

**Statement:**
Increasing the page size reduces the number of page table entries but increases internal fragmentation.

**Answer:** True
**Justification:** Larger pages mean fewer total pages are needed to cover the address space (fewer page table entries). However, larger pages also mean more potential waste in the last page of each process, increasing internal fragmentation.

---

### Q15 — True/False | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Statement:**
A page fault can only occur when a process first starts executing.

**Answer:** False
**Justification:** Page faults can occur at any time during execution whenever the CPU accesses a virtual page that is not currently in physical memory. They are not limited to program startup — they occur throughout execution, especially when accessing new code or data regions.

---

### Q16 — True/False | Bloom's: Analyse | Difficulty: Hard | Marks: 1

**Statement:**
In a system using virtual memory with paging, the physical address space can be larger than the virtual address space.

**Answer:** True
**Justification:** While less common, it is architecturally possible. The virtual address width and physical address width are independent design choices. For example, a system could have 16-bit virtual addresses and 20-bit physical addresses. However, in practice, virtual address spaces are usually larger than physical address spaces to support the illusion of abundant memory.

---

### Q17 — True/False | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Statement:**
The dirty bit in a page table entry indicates that the page has been modified in memory and must be written back to disk before it can be replaced.

**Answer:** True
**Justification:** When a page is modified (written to) in RAM, the dirty bit is set to 1. When this page needs to be evicted, the OS must write it back to disk to preserve the changes. If the dirty bit is 0, the page can be discarded without a disk write (the copy on disk is still current).
