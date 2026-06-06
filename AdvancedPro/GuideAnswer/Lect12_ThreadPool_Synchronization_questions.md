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

# PART B: GUIDE ANSWERS

### Q1 — MCQ
- **Answer:** C) `ExecutorService`
- **Key points:** `ExecutorService` extends `Executor` and adds methods for lifecycle management.

### Q2 — MCQ
- **Answer:** B) On the class itself.
- **Key points:** Static methods lack an instance, so the JVM locks the Class object.

### Q3 — Fill-in-the-blank
- **Answer:** critical region.

### Q4 — Fill-in-the-blank
- **Answer:** thread-safe.

### Q5 — Short Answer
- **Answer:** Starting a new thread for every task causes high overhead because thread creation and destruction are resource-intensive. It can limit throughput, exhaust system memory, and cause poor performance due to excessive context switching.

### Q6 — Short Answer
- **Answer:** Task 2 becomes "Blocked." It must wait in a queue until Task 1 finishes the method and releases the object's lock. Only then can Task 2 acquire the lock and begin execution.

### Q7 — True/False
- **Answer:** False.
- **Justification:** Instance locks are tied to the specific object instance. Locking Object A only prevents other threads from accessing synchronized methods on Object A. Object B has its own independent lock.

### Q8 — True/False
- **Answer:** False.
- **Justification:** Synchronization coordinates threads to prevent conflicts. It actually slows down execution slightly because it forces threads to wait for turns to access the critical region.

### Q9 — Application
**(a)**
1. `ExecutorService executor = Executors.newFixedThreadPool(3);`
2. `executor.shutdown();`

**(b)**
`public synchronized void deposit(double amount)`

**(c)** Without `synchronized`, a race condition occurs: 
1. Thread A reads balance (e.g., 100).
2. Thread B reads same balance (100).
3. Thread A adds 5 and writes 105.
4. Thread B adds 10 and writes 110.
The result `110` is incorrect (should be 115) because Thread B overrode Thread A's update.

### Q10 — Compare & Contrast
| Feature | Thread Class | Executor Interface |
|---|---|---|
| **Efficiency** | Low for many tasks (high creation cost) | High (reuses existing threads) |
| **Management** | Manual (must track each thread) | Automated (Service handles the pool) |
| **Preference** | Use for a single, long-running task | Use for many small, concurrent tasks |

---

### Section 4 — Study Tips
- **The Lock Hierarchy:** Students often forget that `static synchronized` locks the class, while `synchronized` (instance) locks the object. This is a common exam trick.
- **Race Condition Steps:** Be able to explain the "Read-Modify-Write" cycle. Corruption happens if the "Read" steps overlap.

### Section 5 — Coverage Gap Analysis
- **Cached Thread Pool:** The lecture mentions thread pools but doesn't explicitly compare `newFixedThreadPool` with `newCachedThreadPool`. This is worth testing as an MCQ distractor.
- **Explicit Locks (ReentrantLock):** Not covered in this lecture.
- **Inter-thread communication (`wait`/`notify`):** Not covered in this lecture.
