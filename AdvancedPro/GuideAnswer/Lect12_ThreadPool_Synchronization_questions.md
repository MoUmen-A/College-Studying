### Section 1 — Topic Summary (Advanced Programming)
- **Thread Pools:** Utilizing `Executor` and `ExecutorService` to manage groups of threads efficiently, preventing the overhead of creating a new thread for every individual task.
- **Race Conditions:** Understanding how simultaneous access to shared resources (like an account balance) by multiple threads can lead to data corruption.
- **Concurrency Control:** Defining "Thread-safe" classes and using the `synchronized` keyword to manage access to critical regions.
- **Locking Mechanisms:** Distinguishing between object-level locks (instance methods) and class-level locks (static methods).

### Section 2 — Tone Analysis
Following the patterns in the CCY2001 cybersecurity exams, the tone is formal and calibration is centered on "Predict the outcome," "Justify," and "Fix the error." There is a heavy emphasis on mapping code behavior to theoretical concepts like the "Critical Region."

---

# PART A: EXAM QUESTION BANK

### 1. Multiple Choice (MCQ)
**Q1 | Bloom's: Remember | Difficulty: Easy | Marks: 2 | Course: AP**
Which interface should be used if you need to manage and control task execution within a thread pool in Java?
A) `Thread`
B) `Runnable`
C) `ExecutorService`
D) `TaskScheduler`

**Q2 | Bloom's: Understand | Difficulty: Medium | Marks: 2 | Course: AP**
If a thread invokes a `synchronized static` method, where is the lock acquired?
A) On the specific object instance.
B) On the class itself.
C) On the `ExecutorService`.
D) No lock is acquired for static methods.

### 2. Fill-in-the-blank
**Q3 | Bloom's: Remember | Difficulty: Easy | Marks: 2 | Course: AP**
A part of a program where more than one thread is prevented from entering simultaneously because it accesses a shared resource is known as a ________ ________.

**Q4 | Bloom's: Understand | Difficulty: Easy | Marks: 2 | Course: AP**
A class is considered ________-________ if its objects do not cause race conditions even when accessed by multiple threads simultaneously.

### 3. Short Answer
**Q5 | Bloom's: Understand | Difficulty: Easy | Marks: 5 | Course: AP**
Explain why using `new Thread(task).start()` for a large number of tasks (e.g., 10,000) is considered inefficient compared to using a thread pool.

**Q6 | Bloom's: Analyse | Difficulty: Medium | Marks: 5 | Course: AP**
Describe what happens to a "Task 2" if it attempts to enter a `synchronized` instance method while "Task 1" is currently executing that same method on the same object.

### 4. True / False + Justify
**Q7 | Bloom's: Analyse | Difficulty: Medium | Marks: 3 | Course: AP**
**Statement:** If you have two different objects of the same class, a thread accessing a `synchronized` instance method on Object A will block a second thread from accessing the same method on Object B.
State True or False, and justify your reasoning.

**Q8 | Bloom's: Understand | Difficulty: Easy | Marks: 3 | Course: AP**
**Statement:** Thread synchronization is used to speed up the execution of threads by allowing them to run without coordination.
State True or False, and justify your reasoning.

### 5. Application (Code / Scenario)
**Q9 | Bloom's: Apply | Difficulty: Hard | Marks: 10 | Course: AP**
**(a)** Complete the code below to create a fixed thread pool with **3 threads** and execute a task 10 times. (Marks: 4)

```java
public class PoolDemo {
    public static void main(String[] args) {
        // 1. Create the executor service
        ____________________________________________________
        
        for(int i = 0; i < 10; i++) {
            executor.execute(new MyTask());
        }
        
        // 2. Shut down the service
        ____________________________________________________
    }
}
```

**(b)** The `Account` class below is not thread-safe. Add the necessary keyword to ensure that the balance cannot be corrupted when multiple threads deposit money at the same time. (Marks: 2)

```java
public class Account {
    private double balance = 0;
    public _______ void deposit(double amount) {
        balance += amount;
    }
}
```

**(c)** Explain the "Race Condition" that would occur in part (b) if the keyword was omitted. Refer to the steps of "Read" and "Write". (Marks: 4)

### 6. Compare & Contrast
**Q10 | Bloom's: Analyse | Difficulty: Medium | Marks: 8 | Course: AP**
Compare the use of the `Thread` class versus the `Executor` interface with respect to:
(i) Efficiency for multiple tasks.
(ii) Resource management.
(iii) When to prefer one over the other.

### 7. Essay / Long Answer
**Q11 | Bloom's: Evaluate | Difficulty: Hard | Marks: 15 | Course: AP**
"Synchronization is a trade-off between data integrity and performance." 
Discuss this statement by addressing the following:
- How does the `synchronized` keyword protect the "Critical Region"?
- What is the performance "cost" of using synchronization (mention blocking/waiting)?
- Provide a scenario where over-synchronization might lead to poor performance, even if the data remains correct.

---

# PART B: INSTRUCTOR'S MARKING GUIDE

---

## Q1 — Multiple Choice | Bloom's: Remember | Marks: 2

**Correct Answer:** C) `ExecutorService`

### Marking Rubric
| Score | Criteria |
|---|---|
| **2 marks** | Student selects C and provides reasoning mentioning lifecycle management OR interface hierarchy. |
| **1 mark** | Student selects C but no explanation or vague reasoning. |
| **0 marks** | Student selects A, B, or D. |

### Instructor Notes
- **Common mistake:** Students select B (`Runnable`) confusing it with execution. Clarify: `Runnable` is the *task*, not the *manager*.
- **Distractors:** A) Thread — used for single tasks. D) TaskScheduler — does not manage thread pools in this context.
- **Why this matters:** Students must distinguish between the `Executor` (interface for execution) and `ExecutorService` (interface for lifecycle control: `shutdown()`, `shutdownNow()`, `isTerminated()`).

---

## Q2 — Multiple Choice | Bloom's: Understand | Marks: 2

**Correct Answer:** B) On the class itself.

### Marking Rubric
| Score | Criteria |
|---|---|
| **2 marks** | Selects B and mentions Class object or notes that static methods have no instance. |
| **1 mark** | Selects B with unclear or incomplete explanation. |
| **0 marks** | Selects A, C, or D. |

### Instructor Notes
- **Key distinction:** Instance `synchronized` methods lock the **object instance**. Static `synchronized` methods lock the **Class object** itself (shared across all instances).
- **Common mistake:** Students confuse this with instance-level locking. Emphasize: "Static methods belong to the class, not to objects."
- **Example clarification:** If two threads call `synchronized static foo()` on different instances, they will still block each other because both are locking the Class.

---

## Q3 — Fill-in-the-blank | Bloom's: Remember | Marks: 2

**Correct Answer:** `critical region` (or "critical section").

### Marking Rubric
| Score | Criteria |
|---|---|
| **2 marks** | Exact phrase: "critical region" or "critical section". |
| **1 mark** | Close approximation (e.g., "critical area", "restricted region") showing understanding. |
| **0 marks** | Incorrect term (e.g., "synchronized zone", "thread area"). |

### Instructor Notes
- **Definition to reinforce:** A critical region is a code segment where shared resources are accessed. Only one thread is permitted at a time.
- **Terminology consistency:** Use "critical region" consistently in lectures to avoid student confusion.

---

## Q4 — Fill-in-the-blank | Bloom's: Understand | Marks: 2

**Correct Answer:** `thread-safe` (hyphenated).

### Marking Rubric
| Score | Criteria |
|---|---|
| **2 marks** | Exact phrase: "thread-safe" or "thread safe". |
| **1 mark** | Approximate: "thread safe" (without hyphen, still acceptable). |
| **0 marks** | Incorrect (e.g., "synchronized", "protected"). |

### Instructor Notes
- **Definition:** A class is thread-safe if it guarantees that concurrent access by multiple threads does not corrupt the object's state.
- **Related concepts:** Thread-safety is achieved through synchronization, immutability, or other concurrency mechanisms.

---

## Q5 — Short Answer | Bloom's: Understand | Marks: 5

**Model Answer:**
"Creating a new thread for each task is inefficient because thread creation and destruction incur significant OS-level overhead. For 10,000 tasks, this means 10,000 thread creations/destructions, exhausting system memory and CPU resources due to context-switching overhead. A thread pool reuses a fixed number of threads, dramatically reducing this overhead and improving throughput."

### Marking Rubric
| Score | Criteria |
|---|---|
| **5 marks** | Addresses overhead of creation, memory exhaustion, context switching, and mentions thread reuse efficiency. |
| **4 marks** | Addresses 3 of the 4 points above clearly. |
| **3 marks** | Mentions overhead and inefficiency but lacks detail on context switching or thread reuse benefits. |
| **2 marks** | Vague statement about inefficiency without supporting reasoning. |
| **0 marks** | Blank or incorrect response. |

### Instructor Notes
- **Common mistakes:**
  - Students say "threads are bad" without explaining *why*.
  - They forget to mention **resource exhaustion** (memory/CPU).
  - They may confuse this with general multithreading inefficiency.
- **Expected depth:** For 5 marks, expect 3–4 sentences with specific technical justification.

---

## Q6 — Short Answer | Bloom's: Analyse | Marks: 5

**Model Answer:**
"Task 2 enters a **Blocked** state. It waits in a queue until Task 1 completes and releases the object's lock. The JVM's Thread Scheduler removes Task 2 from the runnable pool and places it in the waiting queue. Only after Task 1 exits the synchronized method and releases the lock can Task 2 acquire the lock and proceed."

### Marking Rubric
| Score | Criteria |
|---|---|
| **5 marks** | Clearly states "Blocked" state, explains lock release dependency, and mentions the scheduling mechanism. |
| **4 marks** | Explains blocking and lock dependency but misses scheduling detail. |
| **3 marks** | States blocking correctly but vague on the mechanism or lock release. |
| **2 marks** | Mentions waiting/blocking but lacks detail. |
| **0 marks** | Incorrect response (e.g., "Task 2 runs in parallel"). |

### Instructor Notes
- **Thread states to emphasize:**
  - **RUNNABLE:** Ready to execute (on CPU or waiting for CPU time).
  - **BLOCKED:** Waiting to acquire a monitor lock on a synchronized object.
  - **WAITING:** Waiting indefinitely for another thread's signal.
- **Common mistake:** Students confuse BLOCKED (waiting for lock) with WAITING (indefinite wait). Clarify the distinction.

---

## Q9 — Application (Code) | Bloom's: Apply | Marks: 10

### Part (a) — Marks: 4

**Model Answer:**
```java
ExecutorService executor = Executors.newFixedThreadPool(3);

for(int i = 0; i < 10; i++) {
    executor.execute(new MyTask());
}

executor.shutdown();
```

### Marking Rubric
| Score | Criteria |
|---|---|
| **4 marks** | Both lines correct: `newFixedThreadPool(3)` and `shutdown()`. |
| **3 marks** | Correct pool creation; `shutdown()` missing or named differently (e.g., `stop()`). |
| **2 marks** | Correct pool creation but wrong shutdown method. |
| **1 mark** | Partial understanding (e.g., correct method names but wrong syntax). |
| **0 marks** | Incorrect or missing code. |

### Common Mistakes to Flag
- **Mistake 1:** Writing `Executors.newThreadPool(3)` — method doesn't exist; must be `newFixedThreadPool()`.
- **Mistake 2:** Writing `executor.stop()` instead of `shutdown()` — `stop()` is a deprecated Thread method.
- **Mistake 3:** Forgetting `shutdown()` — leaves threads running indefinitely (resource leak).
- **Correction:** Emphasize that `shutdown()` gracefully terminates the pool after pending tasks complete.

---

### Part (b) — Marks: 2

**Model Answer:**
```java
public synchronized void deposit(double amount) {
    balance += amount;
}
```

### Marking Rubric
| Score | Criteria |
|---|---|
| **2 marks** | Correct: `synchronized` keyword added. |
| **1 mark** | Added a synchronization mechanism but used wrong keyword (e.g., `private synchronized`). |
| **0 marks** | Missing or incorrect keyword. |

### Common Mistakes to Flag
- **Mistake:** Students write `public atomic void` or `public volatile void` — these are different mechanisms and incorrect for this context.
- **Clarification:** `volatile` ensures visibility of value changes but does NOT provide mutual exclusion. `synchronized` is required here.

---

### Part (c) — Marks: 4

**Model Answer:**
"Without `synchronized`, a race condition occurs during the Read-Modify-Write cycle:
1. Thread A reads balance = 100.
2. Thread B reads balance = 100 (same value, before A writes).
3. Thread A adds 5 → writes 105.
4. Thread B adds 10 → writes 110.
Final result: 110 (incorrect; should be 115). Thread B's write overwrites Thread A's work, losing 5."

### Marking Rubric
| Score | Criteria |
|---|---|
| **4 marks** | All 4 steps shown clearly; identifies final incorrect value and root cause. |
| **3 marks** | Shows the race condition with 3–4 steps but misses the "overwrite" explanation. |
| **2 marks** | Mentions race condition but steps are unclear or incomplete. |
| **1 mark** | Vague mention of "threads interfering" without step-by-step detail. |
| **0 marks** | Blank or incorrect. |

### Instructor Notes
- **Key concept:** Emphasize the **Interleaving** of operations. The race occurs because Read and Write are not atomic (not indivisible).
- **Teach this pattern:** This is the classic "Check-Then-Act" race condition. Students should recognize it in other contexts (file updates, database operations).

---

## Q10 — Compare & Contrast | Bloom's: Analyse | Marks: 8

**Model Answer (Structured Table Format):**
| Feature | `Thread` Class | `Executor` Interface |
|---|---|---|
| **Efficiency (many tasks)** | Low — each task = new thread creation overhead | High — reuses thread pool, minimal overhead |
| **Resource Management** | Manual — developer must track, start, stop each thread | Automatic — `ExecutorService` manages lifecycle |
| **Scalability** | Poor — 1000 tasks = 1000 thread objects in memory | Good — 1000 tasks managed by fixed pool |
| **Use Case** | Single long-running task or one-off execution | Batch processing, request handling, concurrent workloads |
| **Shutdown Control** | `thread.join()` or manual tracking | `executor.shutdown()`, `shutdownNow()` |

### Marking Rubric
| Score | Criteria |
|---|---|
| **8 marks** | All three points (i, ii, iii) addressed comprehensively with concrete examples. Table format or clear prose comparison. |
| **6 marks** | Two of three points clearly addressed; third is vague. |
| **4 marks** | One point well explained; others missing or superficial. |
| **2 marks** | Brief comparison but lacks depth or misses key distinctions. |
| **0 marks** | Blank or irrelevant response. |

### Expected Student Responses (Scoring Guide)
- **Efficiency point (i):** Expect mention of "overhead," "reuse," "throughput."
- **Resource management point (ii):** Expect mention of "automatic," "lifecycle," "`shutdown()`."
- **Preference point (iii):** Expect concrete scenario (e.g., "use Thread for a single background task; use Executor for handling 1000s of web requests").

---

## Q11 — Essay / Long Answer | Bloom's: Evaluate | Marks: 15

**Model Answer (Structured Response):**

**Introduction:**
Synchronization ensures data consistency by enforcing mutual exclusion, but at the cost of reduced concurrency and potential performance degradation.

**Body - Part 1: How `synchronized` Protects the Critical Region**
- The `synchronized` keyword acquires a lock (monitor) before entering the critical region.
- Only one thread can hold the lock at a time; all others wait.
- Upon exit, the lock is released, allowing the next waiting thread to acquire it.
- This guarantees that read-modify-write operations are atomic and indivisible.

**Body - Part 2: Performance Cost**
- **Blocking overhead:** Threads in contention spend CPU cycles in waiting state instead of executing useful work.
- **Context switching cost:** The OS must manage thread queues, reducing CPU efficiency.
- **Lock contention:** If many threads compete for the same lock, throughput drops significantly.
- Example: A single synchronized method serving 100 concurrent requests becomes a bottleneck.

**Body - Part 3: Over-Synchronization Scenario**
- **Bad example:** Synchronizing every method in a class, even if only one accesses shared state.
- **Result:** Threads waiting unnecessarily on methods that don't need synchronization, reducing parallelism.
- **Better approach:** Synchronize only the critical regions or use fine-grained locking (lock only the shared variable, not the entire object).

**Conclusion:**
Developers must balance correctness (synchronization) with performance (minimal locking). Use synchronization judiciously; prefer immutability, thread-local storage, or concurrent data structures when possible.

### Marking Rubric
| Score | Criteria |
|---|---|
| **15 marks** | All three parts (protection, performance cost, over-sync scenario) addressed with depth and specific examples. Well-structured prose. |
| **12 marks** | Two of three parts thoroughly explained; third is brief. Clear understanding demonstrated. |
| **9 marks** | All three parts mentioned but lack concrete examples or depth. |
| **6 marks** | Explains the concept but misses one major part or is superficial overall. |
| **3 marks** | Vague or incomplete discussion; minor understanding shown. |
| **0 marks** | Blank or irrelevant response. |

### Instructor Notes on Common Errors
- **Error 1:** Students say "synchronization always slows things down" without explaining *why* or mentioning trade-offs.
- **Error 2:** They fail to provide a concrete over-synchronization example.
- **Error 3:** They confuse synchronization *cost* (lock contention) with the *benefit* (data safety).
- **Correction:** Emphasize that synchronization is a necessary evil; the goal is to minimize its scope.

---

---

## Q7 — True/False + Justify | Bloom's: Analyse | Marks: 3

**Correct Answer:** **False**

**Model Justification:**
"Instance-level locks are tied to the specific object instance. When a thread locks Object A by entering a synchronized method, only that object is locked. Object B has its own independent lock and can be accessed by another thread simultaneously. The blocks apply per object, not per class (unless the method is static)."

### Marking Rubric
| Score | Criteria |
|---|---|
| **3 marks** | Correctly states "False" and explains the per-object nature of instance locks with clarity. |
| **2 marks** | States "False" with a reasonable but incomplete explanation. |
| **1 mark** | States "False" but justification is weak or vague. |
| **0 marks** | States "True" or blank. |

### Instructor Notes
- **Common mistake:** Students incorrectly believe that all synchronized methods of a class are guarded by a single class-level lock.
- **Clarification needed:** Emphasize the distinction:
  - **Instance synchronized methods:** Lock is per object. Each object has its own lock.
  - **Static synchronized methods:** Lock is per class. All threads accessing any static method must acquire the same class lock.
- **Example to reinforce:** If you have 2 Account objects (A1, A2), Thread 1 can call `A1.deposit()` while Thread 2 calls `A2.deposit()` without blocking.

---

## Q8 — True/False + Justify | Bloom's: Understand | Marks: 3

**Correct Answer:** **False**

**Model Justification:**
"Synchronization is a coordination mechanism that prevents conflicts when threads access shared resources. It enforces sequential access to critical regions, which inherently *slows down* execution compared to unsynchronized code because threads must wait for their turn to acquire locks. The benefit is data correctness and safety, not speed."

### Marking Rubric
| Score | Criteria |
|---|---|
| **3 marks** | Correctly states "False" and explains that synchronization *reduces* speed while providing safety. |
| **2 marks** | States "False" with basic explanation; may lack depth on trade-off concept. |
| **1 mark** | States "False" but justification is incomplete or unclear. |
| **0 marks** | States "True" or blank. |

### Instructor Notes
- **Key teaching point:** Synchronization has a **performance cost** but provides a **correctness benefit**.
- **Common misconception:** Students confuse "coordination" with "speed." Emphasize that coordination means *controlled sequential access*, not faster execution.
- **Analogy:** Like a checkout line at a store — enforcing single-file order (synchronization) prevents chaos but doesn't speed up checkout. It ensures fairness and correctness.

---
- **The Lock Hierarchy:** Students often forget that `static synchronized` locks the class, while `synchronized` (instance) locks the object. This is a common exam trick.
- **Race Condition Steps:** Be able to explain the "Read-Modify-Write" cycle. Corruption happens if the "Read" steps overlap.

### Section 5 — Coverage Gap Analysis
- **Cached Thread Pool:** The lecture mentions thread pools but doesn't explicitly compare `newFixedThreadPool` with `newCachedThreadPool`. This is worth testing as an MCQ distractor.
- **Explicit Locks (ReentrantLock):** Not covered in this lecture.
- **Inter-thread communication (`wait`/`notify`):** Not covered in this lecture.
