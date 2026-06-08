# Lecture 11 — Multithreading Concurrency: Question Bank & Guide Answers

## Topic Summary

- **Concurrency Basics:** Comparison of Processes (isolated applications) vs. Threads (units of execution sharing memory).
- **Thread Lifecycle:** Transitioning Task objects (`Runnable`) into execution via `Thread` instances and the `start()` mechanism.
- **Thread Control:** Using `yield()`, `sleep()`, and `join()` to coordinate execution and handling checked `InterruptedExceptions`.
- **Scheduling Logic:** Understanding JVM's Preemptive and Round-Robin (Time Slicing) scheduling based on Priorities.

### Core Concept Comparison Tables

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

## Tone analysis

Following the patterns in previous exams, the questions focus on direct conceptual understanding, code problem-solving, and thread execution behavior tracing.

---

# Question Bank

Group order: Multiple choice → Fill-in-the-blank → Short answer → True/False + justify → Application → Compare & contrast → Essay / long answer

---

## Multiple choice (MCQ)

### Q1 — Multiple choice | Bloom's: Remember | Difficulty: Easy | Marks: 2
**Question:**
Which of the following methods temporarily pauses the executing thread to give other threads a chance to execute, but does not guarantee the CPU will remain idle?

A. `sleep(long)`  
B. `join()`  
C. `yield()`  
D. `start()`  

**Guide answer:**
C

**Key points to include for Full Marks:**
- `yield()` pauses the thread to allow other threads (typically of the same priority) to execute, but the CPU remains active.
- The thread transitions from Running to Runnable/Ready state.

**Common mistakes to avoid:**
Choosing `sleep()` which puts the thread in a timed waiting state and can allow the CPU to go idle.

### Q2 — Multiple choice | Bloom's: Understand | Difficulty: Easy | Marks: 2
**Question:**
What occurs if you directly call the `run()` method on a `Runnable` implementation inside `main` instead of passing it to a Thread's `start()` method?

A. A new thread is actively created and executes the run method.  
B. The code runs synchronously in the current main thread.  
C. A runtime `InterruptedException` is thrown.  
D. The compiler generates an error.  

**Guide answer:**
B

**Key points to include for Full Marks:**
- Direct invocation of `run()` executes as a standard sequential method call within the parent thread.
- No separate call stack (new thread) is created.

**Common mistakes to avoid:**
Thinking a separate thread is launched by calling `run()`.

---

## Fill-in-the-blank

### Q3 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2
**Question:**
To force a thread to wait until another specific thread has completely finished its execution, the ________ method should be invoked.

**Guide answer:**
`join()`

**Key points to include for Full Marks:**
- The current thread enters the WAITING state.
- Target thread termination is the trigger to resume.

**Common mistakes to avoid:**
Writing `wait()` which is for object-monitor locks, not thread termination waiting.

### Q4 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2
**Question:**
The situation where a lower-priority thread never gets a chance to run because higher-priority threads dominate the CPU is known as ________.

**Guide answer:**
starvation (or contention)

**Key points to include for Full Marks:**
- Exact term: "starvation" or "thread starvation".

**Common mistakes to avoid:**
Writing "deadlock" (which is mutual waiting, not priority starvation).

---

## Short answer

### Q5 — Short answer | Bloom's: Understand | Difficulty: Medium | Marks: 5
**Question:**
Explain the fundamental difference between a single-threaded Process and a Thread in terms of how they utilize memory resources.

**Guide answer:**
A Process acts as an isolated container; it has its own private memory and processing resources, meaning a crash in one process generally does not affect others. Conversely, a Thread is a smaller unit of execution existing *inside* a process. All threads running within the same process share the same memory and data space, making them faster to context-switch but susceptible to dangerous interference with each other.

**Key points to include for Full Marks:**
- Process: isolated private memory space.
- Thread: shares memory and data space with other threads in the same process.

**Common mistakes to avoid:**
Stating that threads have completely isolated memory spaces like processes.

### Q6 — Short answer | Bloom's: Apply | Difficulty: Medium | Marks: 5
**Question:**
Why is it mandatory by the Java compiler to place the `Thread.sleep()` method inside a `try-catch` block? Identify the specific exception that must be addressed.

**Guide answer:**
`Thread.sleep()` forces a thread into a timed pause. During this pause, another thread might invoke the sleeping thread's `interrupt()` method. Because this action is meant to abruptly wake the thread, it throws an `InterruptedException`. Java categorizes this as a *checked exception*, making it mandatory for the developer to explicitly handle it using a `try-catch` block to ensure system stability.

**Key points to include for Full Marks:**
- `InterruptedException` is a checked exception.
- Triggered if another thread interrupts the sleeping thread.

**Common mistakes to avoid:**
Vaguely writing `Exception` instead of identifying `InterruptedException`.

---

## True / False + justify

### Q7 — True / False + justify | Bloom's: Analyse | Difficulty: Medium | Marks: 3
**Question:**
**Statement:** Setting a thread's priority to `Thread.MAX_PRIORITY` (10) guarantees that the operating system will execute this thread uninterrupted before any other thread.

State True or False, and justify your reasoning.

**Guide answer:**
False.  
While the JVM provides a thread priority number as a strong "hint" to the Thread Scheduler, the underlying OS retains ultimate control. The OS can choose to ignore the priority or assign execution time differently based on its own preemptive or time-slicing rules. Priority is not an absolute guarantee of execution order or uninterrupted run.

**Key points to include for Full Marks:**
- Priorities are platform-dependent hints.
- The underlying OS thread scheduler determines actual execution.

**Common mistakes to avoid:**
Stating "True" based on the assumption that priority 10 is absolute.

### Q8 — True / False + justify | Bloom's: Understand | Difficulty: Medium | Marks: 3
**Question:**
**Statement:** On a standard single-core CPU, creating 10 threads means that all 10 are executing instructions at the exact same physical millisecond.

State True or False, and justify your reasoning.

**Guide answer:**
False.  
A single-core CPU can physically execute only one thread at a given time. The illusion of simultaneous execution is achieved by the OS performing rapid "context switching"—allocating a tiny time slice to each thread in rapid succession.

**Key points to include for Full Marks:**
- Single-core can only run one thread at a time.
- Pseudo-parallelism is achieved via context switching (time-slicing).

**Common mistakes to avoid:**
Confusing single-core timeslicing with multi-core physical parallelism.

---

## Application (scenario-based)

### Q9 — Application (multi-part) | Bloom's: Apply / Analyse | Difficulty: Hard | Marks: 10
**Question:**
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

**(a)** Identify the logical error on Line 13 in the code that will cause a crash at runtime and state the exception thrown. (4 marks)

**(b)** Rewrite the `main` method to correctly create and start two independent threads executing the `MyTask` task concurrently. (4 marks)

**(c)** What role does the JVM's Thread Scheduler play once both correctly written threads are started? (2 marks)

**Guide answer:**
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

**Key points to include for Full Marks:**
- State `IllegalThreadStateException` as the thrown exception.
- Create a distinct new `Thread` instance in the main rewrite.
- Identify scheduling swap control for thread execution queues.

**Common mistakes to avoid:**
Calling `t1.run()` to try and start it again; missing the exact class name `IllegalThreadStateException`.

---

## Compare & contrast

### Q10 — Compare & contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 8
**Question:**
Compare and contrast the `yield()` and `sleep(long)` methods in Java. Your answer must address:
(i) Their behavioral impact on thread execution.
(ii) Whether the CPU can enter an idle state.
(iii) Exception handling requirements.

**Guide answer:**

| Feature | `yield()` | `sleep(long)` |
|---|---|---|
| **Impact on Execution** | Tells the scheduler the thread lacks urgent work; steps aside to let other threads run. | Forces the thread to completely suspend operations for a strict, specified number of milliseconds. |
| **CPU State** | If no other threads require CPU, the yielding thread continues mapping resources. CPU does not idle. | CPU can become entirely idle (possibly entering power-saving modes) if no other process requires execution. |
| **Exception Handling** | Does not throw checked exceptions. | Throws checked `InterruptedException`. |

**Key points to include for Full Marks:**
- `yield()` keeps the thread in the RUNNABLE state; `sleep()` moves the thread to the TIMED_WAITING state.
- `sleep()` requires catching checked `InterruptedException`.

**Common mistakes to avoid:**
Stating that `yield()` pauses execution for a guaranteed duration.

---

## Essay / long answer

### Q11 — Essay / long answer | Bloom's: Evaluate / Create | Difficulty: Hard | Marks: 15
**Question:**
Thread starvation is a dangerous scenario in a heavily multithreaded application. Design an explanation that addresses the following:
- Define what causes contention and starvation with regard to thread priorities.
- Differentiate how "Preemptive Scheduling" vs. "Time Slicing" handles thread priorities.
- Detail at least two programmatic strategies a developer can implement within their `run()` methods to prevent starvation from happening.

**Guide answer:**
**Introduction:**  
Starvation occurs when a thread with a low-priority configuration never receives CPU execution time because threads with higher (or identical) priorities constantly populate the runnable queue.

**Body:**  
1. **Priority Contention & Starvation:** Threads compete for CPU allocation. If higher priority threads always reside in the ready pool, the scheduler continually schedules them, starving lower priority threads.
2. **Scheduling Handling:**
   - *Preemptive Scheduling:* A high-priority task aggressively monopolizes CPU execution until it is dead, waiting, or blocked. If new high-priority tasks keep appearing, the low-priority task starves indefinitely.
   - *Time Slicing:* The active thread is only given a prescribed quantum of time before being placed back in the ready pool. It guarantees fair rotation (Round-Robin) among threads of the *same* priority.
3. **Mitigation strategies within `run()`:**
   - *Strategic pausing:* The heavy/high-priority threads should periodically invoke `Thread.sleep(time)` to temporarily remove themselves from the ready pool, forcibly granting execution slices to starving threads.
   - *Yielding:* Developers can purposefully inject `Thread.yield()` in tight calculation loops of high-priority threads, signaling the OS to grant execution time to pending threads on the stack.

**Conclusion:**  
Mitigating starvation requires active thread cooperation. Programmers cannot rely solely on the OS scheduler to behave fairly across priority levels and should use strategic sleeps or yields.

**Key points to include for Full Marks:**
- Correct definition of starvation.
- Difference between preemptive allocation and time slicing.
- Explicit naming of sleep/yield as mitigation methods.

**Common mistakes to avoid:**
Confusing starvation with deadlock (deadlocked threads are waiting for each other, starved threads are waiting for the CPU).

---

## Study tips

- **The difference between `run()` and `start()`:** Very frequently tested. Remember that `run()` acts as a standard method call sequentially, while `start()` registers natively with the JVM to allocate a new, distinct call stack.
- **Exceptions on Thread Interruptions:** Be comfortable writing the exact `try { Thread.sleep(); } catch (InterruptedException e) {}` structure, as checked exceptions on concurrency methods are heavily graded.

## Coverage gap analysis

- **Runnable via Anonymous classes or Lambdas:** The provided lecture outlines instantiating Runnable normally (`public class Task implements Runnable`). Questions demonstrating lambda expressions for Runnable were ignored.
  - *Suggested question type:* Application — Fill in the blank or code replacement, replacing a verbose Thread creation syntax with an anonymous subclassing with an anonymous internal class implementation to ensure conceptual robustness.

---
*Generated from `AdvancedPro/Lect/Lect11_Scheduler_sleep_yield_join_Priority_MultiThreading1.md`.*