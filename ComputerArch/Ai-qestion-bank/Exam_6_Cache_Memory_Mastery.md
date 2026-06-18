# COA Practice Exam 6: Cache Memory Mastery

This exam provides deep coverage of cache memory topics: direct mapping, fully associative, set-associative mapping, address field calculations, EAT computations, and replacement policies.

---

## Part 1: Cache Concepts & Comparisons [10 Marks]

### Q1 — Compare & Contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 3

**Question:**
Compare Direct-Mapped, Fully Associative, and Set-Associative cache mapping techniques in a table covering: mapping rule, address field structure, hardware complexity, conflict miss rate, and best use case.

**Guide Answer:**

| Feature | Direct-Mapped | Fully Associative | Set-Associative (N-way) |
|---|---|---|---|
| **Mapping Rule** | Each memory block maps to exactly one cache line: $Y = X \bmod N$ | A memory block can be placed in **any** cache line | A memory block maps to a specific **set**, and can be placed in any line within that set |
| **Address Fields** | Tag \| Index \| Offset | Tag \| Offset (no index) | Tag \| Set-Index \| Offset |
| **Hardware Complexity** | Low — single comparator needed | Very High — requires parallel comparators for every cache line | Medium — comparators equal to associativity (N comparators per set) |
| **Conflict Miss Rate** | Highest — blocks mapping to the same line constantly evict each other | Lowest — no conflict misses (only capacity misses) | Moderate — reduced conflicts compared to direct-mapped |
| **Best Use Case** | Simple, low-cost cache designs where speed is paramount | Small caches where miss rate must be minimized (e.g., TLBs) | General-purpose L1/L2 cache in modern CPUs (balance of speed and miss rate) |

**Key Points to Include for Full Marks:**
- Direct-mapped uses the formula $Y = X \bmod N$.
- Fully associative has **no index field** in the address.
- Set-associative is a hybrid (N-way means N lines per set).
- Complexity grows with associativity (more comparators needed).

**Common Mistakes to Avoid:**
- Saying fully associative has an index field.
- Confusing capacity misses with conflict misses.

---

### Q2 — Short Answer / Essay | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**
Explain the four common cache replacement policies: LRU, FIFO, Random, and Optimal. Which one is used as a theoretical benchmark and why?

**Guide Answer:**

1. **LRU (Least Recently Used):** Evicts the cache block that has not been accessed for the longest time. It exploits temporal locality — recently used blocks are likely to be used again soon.

2. **FIFO (First In, First Out):** Evicts the cache block that has been in the cache for the longest time, regardless of how often or recently it was accessed.

3. **Random:** Evicts a randomly selected cache block. Simple to implement (no tracking needed), but unpredictable performance.

4. **Optimal (Bélády's Algorithm):** Evicts the block that will not be used for the longest time in the future. This requires knowledge of future memory accesses, making it **impossible to implement** in hardware. It is used as a **theoretical benchmark** to evaluate other replacement policies — if a policy's miss rate approaches the Optimal miss rate, it is considered highly effective.

**Key Points to Include for Full Marks:**
- LRU uses recent access history; FIFO uses arrival order; Random is stateless; Optimal uses future knowledge.
- Optimal is the theoretical benchmark because it gives the minimum possible miss rate.

**Common Mistakes to Avoid:**
- Confusing LRU and FIFO (LRU is based on access time, FIFO on insertion order).
- Claiming Optimal is a practical replacement policy.

---

### Q3 — Short Answer / Essay | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**
Define the following terms in the context of cache memory: Hit, Miss, Hit Rate, Miss Rate, Hit Time, and Miss Penalty.

**Guide Answer:**

| Term | Definition |
|---|---|
| **Hit** | The requested data is found in the cache. |
| **Miss** | The requested data is **not** found in the cache and must be fetched from a lower level of the memory hierarchy (e.g., main memory). |
| **Hit Rate (H)** | The fraction (or percentage) of memory accesses that result in a cache hit. $H = \frac{\text{Number of Hits}}{\text{Total Accesses}}$. |
| **Miss Rate** | The fraction of accesses that result in a miss. $\text{Miss Rate} = 1 - H$. |
| **Hit Time** | The time required to access data from the cache when a hit occurs (includes tag comparison and data retrieval). |
| **Miss Penalty** | The additional time required to fetch data from main memory (or next cache level) when a miss occurs. |

**Key Points to Include for Full Marks:**
- Hit rate and miss rate sum to 1 (or 100%).
- Hit time is the cache access time; miss penalty is the main memory access time.

**Common Mistakes to Avoid:**
- Confusing miss penalty with total access time on a miss.

---

### Q4 — Short Answer / Essay | Bloom's: Analyse | Difficulty: Hard | Marks: 3

**Question:**
A system architect is deciding between a direct-mapped cache and a 4-way set-associative cache for an L1 data cache. Both caches have the same total capacity. Discuss the trade-offs in terms of: (i) hit time, (ii) miss rate, (iii) hardware cost, and (iv) power consumption. Under what workload conditions would each design be preferred?

**Guide Answer:**

**(i) Hit Time:**
- Direct-mapped has **faster** hit time because it only needs to check one cache line (single tag comparison, simple multiplexing).
- 4-way set-associative is **slower** because it must compare 4 tags in parallel and use a 4-to-1 multiplexer to select the correct data.

**(ii) Miss Rate:**
- Direct-mapped has a **higher** miss rate due to conflict misses (multiple memory blocks compete for the same single cache line).
- 4-way set-associative has a **lower** miss rate because each set has 4 lines, reducing the probability of conflict evictions.

**(iii) Hardware Cost:**
- Direct-mapped is **cheaper** — requires 1 comparator and simple control logic.
- 4-way requires **4 comparators**, 4-to-1 multiplexers, and LRU/replacement policy logic per set.

**(iv) Power Consumption:**
- Direct-mapped uses **less power** (fewer comparators activated).
- 4-way uses **more power** (4 tag comparisons per access, more circuitry active).

**Workload Preference:**
- **Direct-mapped** is preferred when hit time is critical (high clock frequency designs), and the working set has good spatial/temporal locality with few conflicts.
- **4-way set-associative** is preferred for workloads with poor locality or many address conflicts (e.g., pointer-chasing, random access patterns).

**Key Points to Include for Full Marks:**
- Clear trade-off between hit time and miss rate.
- More associativity = more hardware = more power = lower miss rate.
- Workload-dependent recommendation.

---

## Part 2: Cache Calculations [20 Marks]

### Q5 — Calculation | Bloom's: Apply | Difficulty: Medium | Marks: 4

**Question:**
A byte-addressable computer has a 20-bit physical address space and a direct-mapped cache with the following parameters:
- Cache size: 4 KB
- Block size: 32 bytes

Calculate:
**(a)** The number of cache blocks. (1 Mark)
**(b)** The bit widths of the Offset, Index, and Tag fields. (2 Marks)
**(c)** For the address `0xAB1C0`, identify the Tag, Index, and Offset values. (1 Mark)

**Guide Answer:**

**(a) Number of Cache Blocks:**
$$\text{Number of blocks} = \frac{\text{Cache Size}}{\text{Block Size}} = \frac{4\text{KB}}{32\text{ bytes}} = \frac{4096}{32} = 128\text{ blocks}$$

**(b) Bit Widths:**
- **Offset** = $\log_2(32) = 5$ bits
- **Index** = $\log_2(128) = 7$ bits
- **Tag** = Total address bits − Index − Offset = $20 - 7 - 5 = 8$ bits

Address format: `[Tag: 8 bits | Index: 7 bits | Offset: 5 bits]`

**(c) Address `0xAB1C0` Breakdown:**
- Convert to 20-bit binary: `0xAB1C0` = `1010 1011 0001 1100 0000`
- Partition:
  - **Tag (8 bits):** `10101011` = `0xAB`
  - **Index (7 bits):** `0001110` = $14$ (decimal)
  - **Offset (5 bits):** `00000` = $0$ (decimal)
- This address maps to **cache block 14**.

**Key Points to Include for Full Marks:**
- Show formulas for offset, index, and tag.
- Correctly partition the binary address.
- Convert partitioned fields to hex/decimal.

**Common Mistakes to Avoid:**
- Incorrectly computing $\log_2$ values.
- Partitioning bits in the wrong order (Tag is always the most significant bits).

---

### Q6 — Calculation | Bloom's: Apply | Difficulty: Medium | Marks: 4

**Question:**
A 4-way set-associative cache has:
- Total cache size: 16 KB
- Block size: 64 bytes
- Physical address: 24 bits

Calculate:
**(a)** The number of sets. (1 Mark)
**(b)** The bit widths of Offset, Set-Index, and Tag fields. (2 Marks)
**(c)** Which set does the byte address `0x1F3A80` map to? (1 Mark)

**Guide Answer:**

**(a) Number of Sets:**
$$\text{Total blocks} = \frac{16\text{KB}}{64\text{ bytes}} = \frac{16384}{64} = 256\text{ blocks}$$
$$\text{Number of sets} = \frac{\text{Total blocks}}{\text{Ways}} = \frac{256}{4} = 64\text{ sets}$$

**(b) Bit Widths:**
- **Offset** = $\log_2(64) = 6$ bits
- **Set-Index** = $\log_2(64\text{ sets}) = 6$ bits
- **Tag** = $24 - 6 - 6 = 12$ bits

Address format: `[Tag: 12 bits | Set-Index: 6 bits | Offset: 6 bits]`

**(c) Mapping Address `0x1F3A80`:**
- Convert to 24-bit binary: `0x1F3A80` = `0001 1111 0011 1010 1000 0000`
- Partition:
  - **Tag (12 bits):** `000111110011` = `0x1F3`
  - **Set-Index (6 bits):** `101010` = $42$ (decimal)
  - **Offset (6 bits):** `000000` = $0$ (decimal)
- This address maps to **set 42**.

**Key Points to Include for Full Marks:**
- Divide total blocks by way count to get number of sets.
- Set-Index bits from $\log_2(\text{number of sets})$.

**Common Mistakes to Avoid:**
- Using total blocks instead of number of sets for the index bits.
- Forgetting to divide by the associativity.

---

### Q7 — Calculation | Bloom's: Apply | Difficulty: Medium | Marks: 4

**Question:**
A fully associative cache has:
- Cache size: 2 KB
- Block size: 128 bytes
- Physical address space: 32 bits

**(a)** How many cache blocks are there? (1 Mark)
**(b)** What are the bit widths of the Tag and Offset fields? (1 Mark)
**(c)** Where does address `0x00F14380` map in this cache? Explain your answer. (2 Marks)

**Guide Answer:**

**(a) Number of Cache Blocks:**
$$\text{Number of blocks} = \frac{2\text{KB}}{128\text{ bytes}} = \frac{2048}{128} = 16\text{ blocks}$$

**(b) Bit Widths:**
- **Offset** = $\log_2(128) = 7$ bits
- **Index** = $0$ bits (fully associative has **no index field**)
- **Tag** = $32 - 0 - 7 = 25$ bits

Address format: `[Tag: 25 bits | Offset: 7 bits]`

**(c) Mapping Address `0x00F14380`:**
- In a fully associative cache, there is **no fixed mapping**. The block containing this address can be placed in **any** of the 16 cache blocks.
- The cache controller compares the Tag field of the incoming address against the tags of **all 16** cache blocks simultaneously (parallel tag search).
- If there is a match (hit), the data is read from that block using the Offset.
- If there is no match (miss), the new block replaces an existing block according to the replacement policy (LRU, FIFO, etc.).

- **Tag** of `0x00F14380`:
  - Binary: `0000 0000 1111 0001 0100 0011 1000 0000`
  - Tag (25 bits): `0000000011110001010000111` = `0x01E287`
  - Offset (7 bits): `0000000` = $0$

**Key Points to Include for Full Marks:**
- Fully associative = no index field (0 index bits).
- Any block can go anywhere (parallel search of all tags).
- Replacement policy decides which block to evict on a miss.

**Common Mistakes to Avoid:**
- Adding an index field to a fully associative cache.
- Stating that the block maps to a specific line.

---

### Q8 — Calculation | Bloom's: Apply | Difficulty: Hard | Marks: 4

**Question:**
A computer system has the following cache hierarchy:
- L1 Cache: Access time = 2 ns, Hit rate = 92%
- L2 Cache: Access time = 10 ns, Local hit rate = 85%
- Main Memory: Access time = 100 ns

Using the **sequential access model** (each level is accessed only on a miss from the previous level), calculate:
**(a)** The Effective Access Time (EAT). (2 Marks)
**(b)** The global miss rate (probability of accessing main memory). (1 Mark)
**(c)** If the L1 hit rate improves to 96%, what is the new EAT? What percentage improvement does this represent? (1 Mark)

**Guide Answer:**

**(a) EAT Calculation:**
$$\text{EAT} = T_{L1} + (1 - H_1) \times [T_{L2} + (1 - H_2) \times T_{MM}]$$
$$\text{EAT} = 2 + (1 - 0.92) \times [10 + (1 - 0.85) \times 100]$$
$$\text{EAT} = 2 + 0.08 \times [10 + 0.15 \times 100]$$
$$\text{EAT} = 2 + 0.08 \times [10 + 15]$$
$$\text{EAT} = 2 + 0.08 \times 25 = 2 + 2 = 4\text{ ns}$$

**(b) Global Miss Rate:**
$$\text{Global Miss Rate} = (1 - H_1) \times (1 - H_2) = 0.08 \times 0.15 = 0.012 = 1.2\%$$
Only 1.2% of all accesses reach main memory.

**(c) Improved EAT (H₁ = 96%):**
$$\text{EAT}_{\text{new}} = 2 + (1 - 0.96) \times [10 + 0.15 \times 100]$$
$$\text{EAT}_{\text{new}} = 2 + 0.04 \times 25 = 2 + 1 = 3\text{ ns}$$

$$\text{Improvement} = \frac{4 - 3}{4} \times 100\% = 25\%$$

A 4% improvement in L1 hit rate resulted in a 25% improvement in EAT.

**Key Points to Include for Full Marks:**
- Sequential access formula with nested brackets.
- Global miss rate = product of local miss rates.
- Show percentage improvement calculation.

**Common Mistakes to Avoid:**
- Using concurrent access formula instead of sequential.
- Adding access times instead of nesting them.

---

### Q9 — Calculation | Bloom's: Apply | Difficulty: Hard | Marks: 4

**Question:**
A byte-addressable memory system has a 16 MB address space. The cache consists of 256 blocks, each 32 bytes. For the address `0x5C7A60`:

**(a)** Determine the Tag, Index, and Offset for a **direct-mapped** cache. (2 Marks)
**(b)** Determine the Tag, Set-Index, and Offset for a **2-way set-associative** cache. (2 Marks)

**Guide Answer:**

**Common Parameters:**
- Address space = $16\text{MB} = 2^{24}$ bytes → $24$ address bits
- Block size = $32\text{ bytes} = 2^5$ → Offset = $5$ bits
- Total blocks = $256$
- Address `0x5C7A60` in 24-bit binary: `0101 1100 0111 1010 0110 0000`

**(a) Direct-Mapped:**
- Index = $\log_2(256) = 8$ bits
- Tag = $24 - 8 - 5 = 11$ bits
- Partition: `[Tag: 11 | Index: 8 | Offset: 5]`
  - Tag (11 bits): `01011100011` = `0x2E3`
  - Index (8 bits): `11010011` = $211$ (decimal)
  - Offset (5 bits): `00000` = $0$
- Maps to **cache block 211**.

**(b) 2-Way Set-Associative:**
- Number of sets = $256 / 2 = 128$ sets
- Set-Index = $\log_2(128) = 7$ bits
- Tag = $24 - 7 - 5 = 12$ bits
- Partition: `[Tag: 12 | Set-Index: 7 | Offset: 5]`
  - Tag (12 bits): `010111000111` = `0x5C7`
  - Set-Index (7 bits): `1010011` = $83$ (decimal)
  - Offset (5 bits): `00000` = $0$
- Maps to **set 83**.

**Key Points to Include for Full Marks:**
- Correct index/set-index calculation for each mapping type.
- Binary partitioning shown clearly.

**Common Mistakes to Avoid:**
- Using the same index bits for both mapping types (set-associative has fewer index bits).

---

## Part 3: MCQ [10 Marks]

### Q10 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
In a direct-mapped cache, memory block X maps to cache block Y using which formula?
a) $Y = X \div N$
b) $Y = X \bmod N$
c) $Y = N \bmod X$
d) $Y = X \times N$

**Answer:** b) $Y = X \bmod N$

---

### Q11 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Question:**
A fully associative cache address is divided into:
a) Tag, Index, and Offset fields
b) Tag and Offset fields only
c) Index and Offset fields only
d) Tag, Set-Index, and Offset fields

**Answer:** b) Tag and Offset fields only

**Explanation:** Fully associative caches have no index field because any block can go anywhere — only the Tag and Offset are needed.

---

### Q12 — MCQ | Bloom's: Apply | Difficulty: Medium | Marks: 1

**Question:**
A cache has a hit rate of 90% and an access time of 5 ns. Main memory has an access time of 100 ns. Using the concurrent access model, what is the EAT?
a) 14.5 ns
b) 14 ns
c) 15 ns
d) 50 ns

**Answer:** a) 14.5 ns

**Calculation:**
$$\text{EAT} = H \times T_c + (1 - H) \times T_m = 0.90 \times 5 + 0.10 \times 100 = 4.5 + 10 = 14.5\text{ ns}$$

---

### Q13 — MCQ | Bloom's: Apply | Difficulty: Medium | Marks: 1

**Question:**
A direct-mapped cache has 64 blocks. What are the index bits?
a) 5
b) 6
c) 7
d) 8

**Answer:** b) 6

**Calculation:** $\log_2(64) = 6$ bits.

---

### Q14 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Question:**
Which cache replacement policy requires knowledge of future memory accesses?
a) LRU
b) FIFO
c) Random
d) Optimal

**Answer:** d) Optimal

---

### Q15 — MCQ | Bloom's: Apply | Difficulty: Hard | Marks: 1

**Question:**
A 4-way set-associative cache has 512 total blocks and a block size of 16 bytes. How many sets does this cache have?
a) 64
b) 128
c) 256
d) 512

**Answer:** b) 128

**Calculation:** $\text{Sets} = 512 / 4 = 128$.

---

### Q16 — MCQ | Bloom's: Apply | Difficulty: Medium | Marks: 1

**Question:**
If a cache block size is 256 bytes, how many offset bits are needed?
a) 6
b) 7
c) 8
d) 16

**Answer:** c) 8

**Calculation:** $\log_2(256) = 8$ bits.

---

### Q17 — MCQ | Bloom's: Understand | Difficulty: Easy | Marks: 1

**Question:**
Which cache mapping technique has the highest conflict miss rate?
a) Fully Associative
b) 4-way Set-Associative
c) 2-way Set-Associative
d) Direct-Mapped

**Answer:** d) Direct-Mapped

---

### Q18 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 1

**Question:**
In a set-associative cache, the number of comparators needed per access equals:
a) The number of sets
b) The number of cache blocks
c) The associativity (number of ways)
d) The block size in bytes

**Answer:** c) The associativity (number of ways)

---

### Q19 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 1

**Question:**
The EAT formula for a single-level cache with concurrent access is:
a) $\text{EAT} = T_c + (1 - H) \times T_m$
b) $\text{EAT} = H \times T_c + (1 - H) \times T_m$
c) $\text{EAT} = H \times T_m + (1 - H) \times T_c$
d) $\text{EAT} = T_c + T_m$

**Answer:** b) $\text{EAT} = H \times T_c + (1 - H) \times T_m$
