# Lecture 12 — ThreadPool & Synchronization: Question Bank & Guide Answers

## Topic Summary

- **Thread Pools:** Utilizing `Executor` and `ExecutorService` to manage groups of threads efficiently, preventing the overhead of creating a new thread for every individual task.
- **Race Conditions:** Understanding how simultaneous access to shared resources (like an account balance) by multiple threads can lead to data corruption.
- **Concurrency Control:** Defining "Thread-safe" classes and using the `synchronized` keyword to manage access to critical regions.
- **Locking Mechanisms:** Distinguishing between object-level locks (instance methods) and class-level locks (static methods).

## Tone analysis

Following the patterns in previous exams, the questions focus on predicting output, justifying behavior, and fixing errors, with heavy emphasis on the "Critical Region" concept.

---

# Question Bank

Group order: Multiple choice → Fill-in-the-blank → Short answer → True/False + justify → Application → Compare & contrast → Essay / long answer

---

## Multiple choice (MCQ)

### Q1 — Multiple choice | Bloom's: Remember | Difficulty: Easy | Marks: 2
**Question:**
Which interface should be used if you need to manage and control task execution within a thread pool in Java?

A. `Thread`  
B. `Runnable`  
C. `ExecutorService`  
D. `TaskScheduler`  

**Guide answer:**
C

**Key points to include for Full Marks:**
- `ExecutorService` inherits from `Executor` and provides lifecycle control methods like `shutdown()` and `submit()`.
- Distinguish that `Runnable` is the task representation, not the coordinator.

**Common mistakes to avoid:**
Selecting `Runnable` or `Thread` which are for individual execution tasks rather than pool management.

### Q2 — Multiple choice | Bloom's: Understand | Difficulty: Medium | Marks: 2
**Question:**
If a thread invokes a `synchronized static` method, where is the lock acquired?

A. On the specific object instance.  
B. On the class itself.  
C. On the `ExecutorService`.  
D. No lock is acquired for static methods.  

**Guide answer:**
B

**Key points to include for Full Marks:**
- Static synchronized methods lock the Class object (`ClassName.class`), which is shared across all instances of that class.
- Instance synchronized methods lock the individual object (`this`).

**Common mistakes to avoid:**
Selecting A (instance locking) or D.

---

## Fill-in-the-blank

### Q3 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2
**Question:**
A part of a program where more than one thread is prevented from entering simultaneously because it accesses a shared resource is known as a ________ ________.

**Guide answer:**
critical region (or critical section)

**Key points to include for Full Marks:**
- Must explicitly state the standard phrase "critical region" or "critical section".

**Common mistakes to avoid:**
Using descriptive terms like "synchronized block" or "protected area".

### Q4 — Fill-in-the-blank | Bloom's: Understand | Difficulty: Easy | Marks: 2
**Question:**
A class is considered ________-________ if its objects do not cause race conditions even when accessed by multiple threads simultaneously.

**Guide answer:**
thread-safe

**Key points to include for Full Marks:**
- Exact term: "thread-safe" or "thread safe".

**Common mistakes to avoid:**
Writing "synchronized" or "immutable" (which are methods to achieve thread-safety, not the definition itself).

---

## Short answer

### Q5 — Short answer | Bloom's: Understand | Difficulty: Easy | Marks: 5
**Question:**
Explain why using `new Thread(task).start()` for a large number of tasks (e.g., 10,000) is considered inefficient compared to using a thread pool.

**Guide answer:**
Creating a new thread for each task is inefficient because thread creation and destruction incur significant OS-level overhead. For 10,000 tasks, this means 10,000 thread creations/destructions, exhausting system memory and CPU resources due to context-switching overhead. A thread pool reuses a fixed number of threads, dramatically reducing this overhead and improving throughput.

**Key points to include for Full Marks:**
- High OS-level creation and destruction overhead.
- Context switching limits and memory/CPU exhaustion under high thread counts.
- Thread reuse concept in pools.

**Common mistakes to avoid:**
Failing to explain *why* threads are resource-heavy (missing context switching and creation overhead).

### Q6 — Short answer | Bloom's: Analyse | Difficulty: Medium | Marks: 5
**Question:**
Describe what happens to a "Task 2" if it attempts to enter a `synchronized` instance method while "Task 1" is currently executing that same method on the same object.

**Guide answer:**
Task 2 enters a **Blocked** state. It waits in a lock acquisition queue until Task 1 completes the method execution and releases the object's monitor lock. The JVM's Thread Scheduler moves Task 2 from the runnable pool to the blocked queue. Only when the lock is released can Task 2 compete to acquire it and proceed.

**Key points to include for Full Marks:**
- State that Task 2 becomes **Blocked** (waiting for lock).
- Reference the object-level lock (monitor) release.

**Common mistakes to avoid:**
Confusing the BLOCKED state with the WAITING state (which is for explicit signals like `wait()`).

---

## True / False + justify

### Q7 — True / False + justify | Bloom's: Analyse | Difficulty: Medium | Marks: 3
**Question:**
**Statement:** If you have two different objects of the same class, a thread accessing a `synchronized` instance method on Object A will block a second thread from accessing the same method on Object B.

State True or False, and justify your reasoning.

**Guide answer:**
False.  
Instance-level locks are tied to the specific object instance (`this`). When a thread locks Object A by entering a synchronized method, only that object is locked. Object B has its own independent lock and can be accessed by another thread simultaneously. The blocking applies per object, not per class (unless the method is static).

**Key points to include for Full Marks:**
- Instance locks are per-object, not per-class.
- Object A and Object B have distinct locks.

**Common mistakes to avoid:**
Confusing instance synchronization locks with static/class-level synchronization locks.

### Q8 — True / False + justify | Bloom's: Understand | Difficulty: Easy | Marks: 3
**Question:**
**Statement:** Thread synchronization is used to speed up the execution of threads by allowing them to run without coordination.

State True or False, and justify your reasoning.

**Guide answer:**
False.  
Synchronization is a coordination mechanism that prevents conflicts when threads access shared resources. It enforces sequential access to critical regions, which inherently *reduces* speed/concurrency compared to unsynchronized code because threads must wait for their turn to acquire locks. The benefit is data correctness and safety, not speed.

**Key points to include for Full Marks:**
- Synchronization coordinates access sequentially, reducing parallel execution speed.
- Trade-off: correctness over speed.

**Common mistakes to avoid:**
Claiming that synchronization speeds up execution.

---

## Application (scenario-based)

### Q9 — Application (multi-part) | Bloom's: Apply | Difficulty: Hard | Marks: 10
**Question:**
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

**Guide answer:**
**(a)**
```java
ExecutorService executor = Executors.newFixedThreadPool(3);
// ...
executor.shutdown();
```

**(b)**
```java
public synchronized void deposit(double amount) {
    balance += amount;
}
```

**(c)** Without `synchronized`, a race condition occurs during the Read-Modify-Write cycle:
1. Thread A reads balance = 100.
2. Thread B reads balance = 100 (same value, before A writes).
3. Thread A adds 5 ⇒ writes 105.
4. Thread B adds 10 ⇒ writes 110.
The final result is 110 instead of 115. Thread B's write overwrites Thread A's work, resulting in data loss.

**Key points to include for Full Marks:**
- Correct pool initialization using `Executors.newFixedThreadPool(3)`.
- Explicit call to `executor.shutdown()`.
- Use of the exact keyword `synchronized` on deposit method.
- Step-by-step description of interleaved read, modify, and write steps.

**Common mistakes to avoid:**
Using `newThreadPool` instead of `newFixedThreadPool`; writing `executor.stop()` (which is deprecated); forgetting to show the interleaving steps in part (c).

---

## Compare & contrast

### Q10 — Compare & contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 8
**Question:**
Compare the use of the `Thread` class versus the `Executor` interface with respect to:
(i) Efficiency for multiple tasks.
(ii) Resource management.
(iii) When to prefer one over the other.

**Guide answer:**

| Feature | `Thread` Class | `Executor` Interface |
|---|---|---|
| **Efficiency (many tasks)** | Low — each task = new thread creation overhead | High — reuses thread pool, minimal overhead |
| **Resource Management** | Manual — developer must track, start, stop each thread | Automatic — `ExecutorService` manages lifecycle |
| **Shutdown Control** | `thread.join()` or manual tracking | `executor.shutdown()`, `shutdownNow()` |
| **Use Case** | Single long-running task or one-off execution | Batch processing, request handling, concurrent workloads |

**Key points to include for Full Marks:**
- Thread creation overhead vs Pool thread reuse.
- Lifecycle controls (`shutdown()` vs join).
- Concrete prefer-cases.

**Common mistakes to avoid:**
Failing to specify when one is preferred over the other.

---

## Essay / long answer

### Q11 — Essay / long answer | Bloom's: Evaluate / Create | Difficulty: Hard | Marks: 15
**Question:**
"Synchronization is a trade-off between data integrity and performance." 
Discuss this statement by addressing the following:
- How does the `synchronized` keyword protect the "Critical Region"?
- What is the performance "cost" of using synchronization (mention blocking/waiting and context switching)?
- Provide a scenario where over-synchronization might lead to poor performance, even if the data remains correct.

**Guide answer:**
**Introduction:**  
Synchronization ensures data consistency by enforcing mutual exclusion in concurrent applications, but at the cost of reduced concurrency and potential performance degradation.

**Body:**  
1. **Critical Region Protection:** The `synchronized` keyword acquires a monitor lock before entering the critical region. Only one thread can hold the lock at a time; others are blocked. Upon exit, the lock is released, allowing the next thread in queue to acquire it. This guarantees that read-modify-write operations are atomic and indivisible.
2. **Performance Cost:** 
   - *Blocking/Waiting:* Contended threads spend CPU cycles in a blocked/waiting state instead of doing useful work.
   - *Context Switching:* The OS must frequently swap thread states from runnable to blocked, wasting CPU overhead.
   - *Lock Contention:* High lock competition turns parallel pathways into execution bottlenecks.
3. **Over-Synchronization Scenario:** Synchronizing every method in a class (like utility getters that only read immutable data). Threads are forced to wait on unrelated operations, destroying concurrency. A better approach is synchronizing only the writing critical blocks or using fine-grained locks.

**Conclusion:**  
Correct concurrency design requires balancing mutual exclusion with performance. Developers should minimize the synchronized block scope to only the necessary mutable critical region.

**Key points to include for Full Marks:**
- Explaining locks/monitors.
- Context switching and blocking overhead costs.
- A concrete over-synchronization example (e.g., locking a pure read method).

**Common mistakes to avoid:**
Talking about thread execution without mentioning locks/monitors; omitting the context switching overhead.

---

## Study tips

- **The Lock Hierarchy:** Remember that `static synchronized` locks the class, while `synchronized` (instance) locks the object.
- **Race Condition Steps:** Be able to explain the "Read-Modify-Write" cycle step-by-step to show how updates overwrite each other.

## Coverage gap analysis

- **Cached Thread Pool:** The lecture mentions thread pools but doesn't compare `newFixedThreadPool` with `newCachedThreadPool`.
  - *Suggested question type:* Multiple choice on distinguishing these two pool types.

---
*Generated from `AdvancedPro/Lect/Lect12 ThreadPool(Exuotor ,RaceCondition, Sync)-MultiThreading part 2`.*
