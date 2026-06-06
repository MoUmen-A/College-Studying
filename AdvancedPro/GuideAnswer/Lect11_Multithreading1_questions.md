### Section 1 — Topic Summary
- **Concurrency Basics:** Comparison of Processes (isolated applications) vs. Threads (units of execution sharing memory).
- **Thread Lifecycle:** Transitioning Task objects (`Runnable`) into execution via `Thread` instances and the `start()` mechanism.
- **Thread Control:** Using `yield()`, `sleep()`, and `join()` to coordinate execution and handling checked `InterruptedExceptions`.
- **Scheduling Logic:** Understanding JVM's Preemptive and Round-Robin (Time Slicing) scheduling based on Priorities.

#### Core Concept Comparison Tables

| Feature | Process | Thread |
| :--- | :--- | :--- |
| **Definition** | A standalone running program (e.g., Browser) | A unit of execution *inside* a process |
| **Memory** | Isolated (own memory/stack) | Shared memory/data among sibling threads |
| **Cost** | Heavyweight (expensive to create/switch) | Lightweight (fast switching and shared context) |
| **Safety** | High (crash in one process rarely affects others) | Low (shared data can lead to interference/crashes) |

| Method | Purpose | Impact on CPU | Checked Exception |
| :--- | :--- | :--- | :--- |
| `yield()` | Hints the CPU to give up the current time slice to other threads. | Thread remains in Ready state; CPU is not idle. | None |
| `sleep(ms)`| Forces the thread into a Timed Waiting state for a specific duration. | CPU can enter idle/low-power mode if no other tasks exist. | `InterruptedException` |
| `join()` | Forces the calling thread to wait until the target thread terminates. | Calling thread enters Waiting state; CPU switches to work elsewhere. | `InterruptedException` |

### Section 2 — Tone Analysis
The questions mimic the formal, academic pacing of university-level computer science exams (such as the provided CCY2001 samples). They strictly test conceptual bounds, code problem-solving, and theoretical justification. A unified, standalone exam paper structure is used at the top, followed by a completely separate marking scheme (Independent Guide Answers).

---

# PART A: EXAM QUESTION PAPER

*Instructions: Read each question carefully. Marks and estimated times are indicated for each question.*

### 1. Multiple Choice
**Q1 | Bloom's: Remember | Difficulty: Easy | Marks: 2 | Time: 2 mins**
Which of the following methods temporarily pauses the executing thread to give other threads a chance to execute, but does not guarantee the CPU will remain idle?
A) `sleep(long)`
B) `join()`
C) `yield()`
D) `start()`

**Q2 | Bloom's: Understand | Difficulty: Easy | Marks: 2 | Time: 2 mins**
What occurs if you directly call the `run()` method on a `Runnable` implementation inside `main` instead of passing it to a Thread's `start()` method?
A) A new thread is actively created and executes the run method.
B) The code runs synchronously in the current main thread.
C) A runtime `InterruptedException` is thrown.
D) The compiler generates an error.

### 2. Fill-in-the-blank
**Q3 | Bloom's: Remember | Difficulty: Easy | Marks: 2 | Time: 2 mins**
To force a thread to wait until another specific thread has completely finished its execution, the ________ method should be invoked.

**Q4 | Bloom's: Remember | Difficulty: Easy | Marks: 2 | Time: 2 mins**
The situation where a lower-priority thread never gets a chance to run because higher-priority threads dominate the CPU is known as ________.

### 3. Short Answer
**Q5 | Bloom's: Understand | Difficulty: Medium | Marks: 5 | Time: 5 mins**
Explain the fundamental difference between a single-threaded Process and a Thread in terms of how they utilize memory resources. 

**Q6 | Bloom's: Apply | Difficulty: Medium | Marks: 5 | Time: 5 mins**
Why is it mandatory by the Java compiler to place the `Thread.sleep()` method inside a `try-catch` block? Identify the specific exception that must be addressed.

### 4. True / False + Justify
**Q7 | Bloom's: Analyse | Difficulty: Medium | Marks: 3 | Time: 4 mins**
**Statement:** Setting a thread's priority to `Thread.MAX_PRIORITY` (10) guarantees that the operating system will execute this thread uninterrupted before any other thread.
State True or False, and justify your reasoning.

**Q8 | Bloom's: Understand | Difficulty: Medium | Marks: 3 | Time: 4 mins**
**Statement:** On a standard single-core CPU, creating 10 threads means that all 10 are executing instructions at the exact same physical millisecond.
State True or False, and justify your reasoning.

### 5. Application (Code / Scenario)
**Q9 | Bloom's: Apply / Analyse | Difficulty: Hard | Marks: 10 | Time: 12 mins**
Review the following Java code snippet:
```java
public class MyTask implements Runnable {
    public void run() {
        for(int i = 1; i <= 100; i++) {
            System.out.println("Processing: " + i);
        }
    }
}
public class ThreadTest {
    public static void main(String[] args) {
        MyTask task = new MyTask();
        Thread t1 = new Thread(task);
        t1.start();
        t1.start(); // line 13
    }
}
```
**(a)** Identify the logical error on Line 13 in the code that will cause a crash at runtime. (4 marks)
**(b)** Rewrite the `main` method to correctly create and start two independent threads executing the `MyTask` task concurrently. (4 marks)
**(c)** What role does the JVM's Thread Scheduler play once both correctly written threads are started? (2 marks)

### 6. Compare & Contrast
**Q10 | Bloom's: Analyse | Difficulty: Medium | Marks: 8 | Time: 10 mins**
Compare and contrast the `yield()` and `sleep(long)` methods in Java. Your answer must address:
(i) Their behavioral impact on thread execution.
(ii) Whether the CPU can enter an idle state.

### 7. Essay / Long Answer
**Q11 | Bloom's: Evaluate / Create | Difficulty: Hard | Marks: 15 | Time: 15 mins**
Thread starvation is a dangerous scenario in a heavily multithreaded application.
Design an explanation that addresses the following:
- Define what causes contention and starvation with regard to thread priorities.
- Differentiate how "Preemptive Scheduling" vs. "Time Slicing" handles thread priorities.
- Detail at least two programmatic strategies a developer can implement within their `run()` methods to prevent starvation from happening.

---
---

# PART B: INDEPENDENT GUIDE ANSWERS

### Q1 — Guide Answer
**Correct Answer:** C) `yield()`
**Key points:** `yield()` pauses the thread to allow other threads (typically of same priority) to execute, but CPU remains active.

### Q2 — Guide Answer
**Correct Answer:** B) The code runs synchronously in the current main thread.
**Key points:** Direct invocation of `run()` executes normally within the parent thread. No separate call stack (new thread) is created.

### Q3 — Guide Answer
**Correct Answer:** `join()`
**Key points:** `join()` pauses the current thread until the target thread upon which `join()` was called terminates.

### Q4 — Guide Answer
**Correct Answer:** Contention or Starvation
**Key points:** Starvation occurs when equal or higher priority threads continually lock CPU resources.

### Q5 — Guide Answer
**Model Answer:** A Process acts as an isolated container; it has its own private memory and processing resources, meaning a crash in one process generally does not affect others. Conversely, a Thread is a smaller unit of execution existing *inside* a process. All threads running within the same process share the same memory and data space, making them faster to context-switch but susceptible to dangerous interference with each other.

### Q6 — Guide Answer
**Model Answer:** `Thread.sleep()` forces a thread into a timed pause. During this pause, another thread might invoke the sleeping thread's `interrupt()` method. Because this action is meant to abruptly wake the thread, it throws an `InterruptedException`. Java categorizes this as a *checked exception*, making it mandatory for the developer to explicitly handle it using a `try-catch` block to ensure system stability.

### Q7 — Guide Answer
**Model Answer:** **False**. 
**Justification:** While the JVM provides a thread priority number as a strong "hint" to the Thread Scheduler, the underlying OS retains ultimate control. The OS can choose to ignore the priority or assign execution time differently based on its own preemptive or time-slicing rules. Priority is not an absolute guarantee of execution order.

### Q8 — Guide Answer
**Model Answer:** **False**. 
**Justification:** A single-core CPU can physically execute only one thread at a given time. The illusion of simultaneous execution is achieved by the OS performing rapid "context switching"—allocating a tiny time slice to each thread in rapid succession.

### Q9 — Guide Answer
**(a)** On Line 13, the code attempts to call `start()` a second time on the already active `t1` thread instance. An `IllegalThreadStateException` will be thrown because a single Java thread object cannot be reused or restarted once its execution has begun.
**(b)** 
```java
public static void main(String[] args) {
    MyTask task = new MyTask();
    Thread t1 = new Thread(task);
    t1.start();
    Thread t2 = new Thread(task); // Create a fresh thread object
    t2.start();
}
```
**(c)** The Thread Scheduler (operating via Time-Slicing or Preemptive scheduling) is now responsible for handling the execution queues. It rapidly swaps between `t1` and `t2`, dictating which runs at any given nanosecond.

### Q10 — Guide Answer
**Model Answer:**
| Feature | `yield()` | `sleep(long)` |
|---|---|---|
| **Impact on Execution** | Tells the scheduler the thread lacks urgent work; steps aside to let other threads run. | Forces the thread to completely suspend operations for a strict, specified number of milliseconds. |
| **CPU State** | If no other threads require CPU, the yielding thread continues mapping resources. CPU does not idle. | CPU can become entirely idle (possibly entering power-saving modes) if no other process requires execution. |
| **Exception Handling** | Does not throw checked exceptions. | Throws checked `InterruptedException`. |

### Q11 — Guide Answer
**Model Answer:**
*Starvation* (or contention) occurs when a thread with a low-priority configuration never receives CPU execution time because threads with higher (or identical) priorities constantly populate the runnable queue. 

In Java, thread scheduling primarily uses two strategies:
1. **Preemptive Scheduling:** A high-priority task aggressively monopolizes CPU execution until it is dead, waiting, or blocked. If new high-priority tasks keep appearing, the low-priority task starves indefinitely.
2. **Time Slicing:** The active thread is only given a prescribed quantum of time before being placed back in the ready pool. It guarantees fair rotation (Round-Robin) among threads of the *same* priority.

**Mitigation strategies within `run()`:**
1. **Strategic pausing:** The heavy/high-priority threads should periodically invoke `Thread.sleep(time)` to temporarily remove themselves from the ready pool, forcibly granting execution slices to starving threads.
2. **Yielding:** Developers can purposefully inject `Thread.yield()` in tight calculation loops of high-priority threads, signaling the OS to grant execution time to pending threads on the stack.

---

### Section 5 — Study Tips
- **The difference between `run()` and `start()`:** Very frequently mistested. Remember that `run()` acts as a standard method call sequentially, while `start()` registers natively with the JVM to allocate a new, distinct call stack.
- **Exceptions on Thread Interruptions:** Be comfortable writing the exact `try { Thread.sleep(); } catch (InterruptedException e) {}` structure, as checked exceptions on concurrency methods are heavily graded.

### Section 6 — Coverage Gap Analysis
- **Runnable via Anonymous classes or Lambdas:** The provided lecture outlines instantiating Runnable normally (`public class Task implements Runnable`). Questions demonstrating lambda expressions for Runnable were ignored.
- *Suggested question type: Application — Fill in the blank or code replacement, replacing a verbose Thread creation syntax with an anonymous subclassing with an anonymous internal class implementation to ensure conceptual robustness.*