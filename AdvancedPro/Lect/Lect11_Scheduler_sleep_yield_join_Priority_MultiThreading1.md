# Multithreading and Parallel Programming

## Multithreading and Parallel Programming







- Lecture 11 – Multithreading Part 1Dr. Mohammad Hashim




- 1


## Multiple Core

- CPU, the Central Processing Unit is the brain of the computer. It is responsible for executing instructions. every line of code you write eventually becomes instructions that the CPU runs.”
- Originally, CPUs had a single core.
  - That meant the physical CPU had a single central processing unit on it.
- To increase performance, manufacturers add additional “cores,” or central processing units.
  - A dual-core CPU has two central processing units, so it appears to the operating system as two CPUs and could run two different processes at the same time.
  - This speeds up your system, because your computer can do multiple things at once. This is called Parallelism


- https://www.howtogeek.com/194756/cpu-basics-multiple-cpus-cores-and-hyper-threading-explained/


- 2


## Process

- A process is basically a running program.For example, when you open your browser, that’s a process. When you run your Java application, that’s another process.”
- Each process has:
  - its own memory
  - its own resources
  - and it runs independently from other processes
- That’s why if one application crashes, others usually keep running.


- 3


## Thread

- Inside each process, we have something smaller called threads.”
- A thread is a unit of execution inside a process.So instead of running one thing at a time, a process can split its work into multiple threads.
- Think of it like this:
  - Process = a company
  - Threads = employees working inside that company”
- All threads in the same process share:
  - the same memory
  - the same data”
- This makes threads faster and more lightweight than processes — but also more dangerous, because they can interfere with each other.


- 4


## Multithreading with Multiple cores

- How do threads actually run on the CPU?
- If you have:
  - 1 core → it can run only 1 thread at a time
  - multiple cores → multiple threads can run truly in parallel
- But even if you create, say, 10 threads on a 4-core CPU, they don’t all run at once.
- The operating system uses something called context switching — it rapidly switches between threads, giving each one a small time slice.
- This happens so fast that it looks like all threads are running at the same time, even if they’re not.


- 5


## Multithreading with Multiple cores

- With Java, you can launch multiple threads from a program concurrently.
- These threads can be executed simultaneously in multiprocessor systems, as shown in Figure 30.1a.


- 6


## Multithreading Advantages

- Multithreading  can make your program more responsive and interactive, as well as enhance performance.
- For example,
  - a good word processor lets you print or save a file while you are typing.
- In some cases, multithreaded programs run faster than single-threaded programs even on single-processor systems.


- 7


## Creating Tasks and Threads

- A task class must implement the Runnable interface.
- A task must be run from a thread.
- Tasks are objects. To create tasks, you have to first define a class for tasks, which implements the Runnable interface.
- The Runnable interface is rather simple.
- All it contains is the run method.


- 8


## Creating Tasks and Threads



- 9


## Example 1



- 10


## Example 1 – cont.



- 11


## Example 1 – cont.

- Sample Running


- 12


## Important Note

- The run() method in a task specifies how to perform the task.
- This method is automatically invoked by the JVM. You should not invoke it.
- Invoking run() directly merely executes this method in the same thread; no new thread is started.


- 13


## Slide 14

- The output will be:


- 14


- Calling the run() method without the Thread object


## Fix the error

- public class Test2 implements Runnable {
- public static void main(String[] args) {
- new Test2();
- }
- public Test2() {
- Thread t = new Thread(this);
- t.start();
- t.start();
- }
- public void run() {
- for(int i = 1 ; i<=100 ; i++)
- System.out.println(“ “ +i);
- }
- }


- 15


## Fix the error

- public class Test2 implements Runnable {
- public static void main(String[] args) {
- new Test2();
- }
- public Test2() {
- Thread t = new Thread(this);
- t.start();
- t.start();
- }
- public void run() {
- for(int i = 1 ; i<=100 ; i++)
- System.out.println(“ “ +i);
- }
- }




- You can’t call start method of the same thread two times, if you want to do this, you can define another thread object then call start again


- 16


## Fix the error

- public class Test2 implements Runnable {
- public static void main(String[] args) {
- new Test2();
- }
- public Test2() {
- Thread t = new Thread(this);
- t.start();
- t.start();
- }
- public void run() {
- for(int i = 1 ; i<=100 ; i++)
- System.out.println(“ “ +i);
- }
- }




- You can’t call start method of the same thread two times, if you want to do this, you can define another thread object then call start again




- Thread t = new Thread(this);
- t.start();
- Thread t2 = new Thread(this);
- t2.start();


- 17


## The Thread Class

- The Thread class contains the constructors for creating threads for tasks and the methods for controlling threads.


- 18


## Thread Scheduler in Java

- Thread scheduler in java is the part of the JVM that decides which thread should run.
- There is no guarantee that which runnable thread will be chosen to run by the thread scheduler.
- Only one thread at a time can run in a single process.
- The thread scheduler mainly uses preemptive or time slicing scheduling to schedule the threads.
  - In preemptive scheduling, the highest priority task executes until it enters the waiting or dead states, or a higher priority task comes into existence.
  - In time slicing, a task executes for a predefined slice of time and then reenters the pool of ready tasks. The scheduler then determines which task should execute next, based on priority and other factors.


- 19


## yield()

- The yield() method of thread class causes the currently executing thread object to temporarily pause and allow other threads to execute.
- For example, suppose you modify the code in the run() method for PrintChar in previous example as follows:


- 20


## Calling the yield() method

- 21


- Without yield()


- With yield()


## sleep(long)

- The sleep(long millis) method puts the thread to sleep for a specified time in milliseconds to allow other threads to execute.
- For example, suppose you modify the code in lines 53–57 in Listing 30.1, as follows:


- 22


## Calling the sleep() method

- 23


- Without sleep()


- With sleep()


## InterruptedException

- The sleep method may throw an InterruptedException, which is a checked exception.
- Such an exception may occur when a sleeping thread’s interrupt() method is called.
- The interrupt() method is very rarely invoked on a thread, so an InterruptedException  is unlikely to occur.
- But since Java forces you to catch checked exceptions, you have to put it in a try-catch block. If a sleep method is invoked in a loop, you should wrap the loop in a try-catch block, as shown in (a) below. If the loop is outside the try-catch block, as shown in (b), the thread may continue to execute even though it is being interrupted.


- 24


## InterruptedException



- 25


## join()

- You can use the join() method to force one thread to wait for another thread to finish.
- For example, suppose you modify the code in lines 53–57 in Listing 30.1 as follows:


- 26


## Differences between yield(), sleep() & join()

- sleep() causes the thread to definitely stop executing for a given amount of time; if no other thread or process needs to be run, the CPU will be idle (and probably enter a power saving mode).
- yield() basically means that the thread is not doing anything particularly important and if any other threads or processes need to be run, they should. Otherwise, the current thread will continue to run.
- join() If any executing thread t1 calls join() on t2 i.e; t2.join() immediately t1 will enter into waiting state until t2 completes its execution.


- 27


## setPriority(int)

- Java assigns every thread a priority.
- Priorities are numbers ranging from 1 to 10.
- The Thread class has the int constants
  - MIN_PRIORITY,  →    1
  - NORM_PRIORITY, → 5 and
  - MAX_PRIORITY, → 10
- setPriority method: increase or decrease the priority of any thread.
- getPriority methos: get the thread’s priority
- The priority of the main thread is Thread.NORM_PRIORITY.


- 28


## setPriority(int)

- The JVM always picks the currently runnable thread with the highest priority.
- A lower priority thread can run only when no higher-priority threads are running.
- If all runnable threads have equal priorities, each is assigned an equal portion of the CPU time in a circular queue.
  - This is called round-robin scheduling.
- Note that setting priority is only giving a hint to the schedule. However, the OS is still in control and can ignore priorities.


- 29


## setPriority(int)

- Tip
- A thread may never get a chance to run if there is always a higher-priority thread running or a same-priority thread that never yields.
- This situation is known as contention or starvation.
- To avoid contention,
  - the thread with higher priority must periodically invoke the sleep or yield method to give a thread with a lower or the same priority a chance to run.


- 30

