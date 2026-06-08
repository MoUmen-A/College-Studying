# Exam 25 — Guide Answers

---

## Question 1 — MCQ Answers

| # | Answer | Key Reason |
|---|--------|-----------|
| 1 | **C** | `@Scope("request")` restricts a bean's lifecycle to a single HTTP request. |
| 2 | **D** | Correct: create an instance `X obj = new X()`, wrap it in `Thread t = new Thread(obj)`, then call `t.start()`. |
| 3 | **A** | `th:text="${expression}"` renders a variable's value as element text content. |
| 4 | **A** | A JavaBean must *implement* `Serializable`, not *extend* it (you extend classes, not interfaces). |
| 5 | **D** | Calling `t.start()` twice on the same thread object throws `IllegalThreadStateException` at runtime → runtime exception, not a compiler error and not duplicate output. |
| 6 | **B** | `join()` forces the calling thread to wait until the target thread terminates. |
| 7 | **B** | `findAll()` returns a `List<T>` of all records from the entity table. |
| 8 | **D** | Default Spring Bean scope is **Singleton** (one shared instance per application context). |
| 9 | **A** | A controller method returning `"redirect:/path"` instructs the client browser to make a new request to that URL. |
| 10 | **C** | `th:replace` replaces the host element entirely with the referenced fragment. |

---

## Question 2 — Short Answers (12 Marks)

### 1) Main Architecture Layers in Spring Boot and Their Roles

| Layer | Annotation | Role |
|-------|------------|------|
| **Presentation (Controller)** | `@Controller` | Handles HTTP requests, passes data to view. |
| **Business Logic (Service)** | `@Service` | Contains application/business rules. |
| **Data Access (Repository)** | `@Repository` | Communicates with the database via JPA. |
| **Model (Entity)** | `@Entity` | Represents a database table row as a Java object. |

---

### 2) Use of `RequestDispatcher` Interface

`RequestDispatcher` allows a servlet to **forward** a request to another resource (servlet, JSP, or file) or **include** another resource's output in the response — all within the same server, without a new browser request.

- `dispatcher.forward(req, res)` → transfers full control to the target.
- `dispatcher.include(req, res)` → includes the target's output and then continues.

---

### 3) Ensuring `main()` is the Last Thread to Finish

Call `t.join()` on every worker thread inside `main()`. This blocks `main()` from proceeding until each joined thread has terminated, guaranteeing `main()` finishes last.

```java
t1.join();
t2.join();
// main continues only after both t1 and t2 finish
```

---

### 4) How Synchronization Prevents Race Conditions

When a method/block is marked `synchronized`, the JVM associates it with an object-level **monitor lock**. Only one thread can hold that lock at a time. Other threads must wait in a queue until the lock is released. This serializes access to shared data, so no two threads can read/modify it simultaneously → race condition eliminated.

---

### 5) Use of Proxy Objects in Spring Boot Bean Scopes (6 Marks)

**Problem:** A Singleton bean (e.g., a `@Controller`) is created once at startup. If it needs a Session-scoped or Request-scoped bean injected, that dependency cannot exist at startup (no HTTP session/request exists yet) — causing a DI failure.

**Solution — Proxy:**
- Spring injects a **Proxy** (a fake placeholder object that implements the same interface) into the Singleton at startup instead of the real bean.
- The Proxy stores no real data itself.
- At **runtime**, when a request hits the controller and calls a method on the injected dependency, the Proxy intercepts the call, looks up the **real** instance for the current user's session/request, and delegates the call to it.

**Result:** The Singleton controller always holds one stable proxy reference, while the real underlying bean is dynamically resolved per request/session, avoiding both the startup crash and data leakage between users.

---

## Question 3 — Coding (12 Marks)

### 1) Thymeleaf Template — `average.html`

> Display the average if calculated, or an error message if division by zero occurred.

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<body>
  <h2>Average Result</h2>

  <p th:if="${avg != null}"  th:text="'Average = ' + ${avg}"></p>
  <p th:if="${error != null}" th:text="'Error: ' + ${error}"></p>

</body>
</html>
```

**Key points:**
- Use `th:if="${avg != null}"` to show result only when division succeeded.
- Use `th:if="${error != null}"` to show the error message only when an exception was caught.
- `th:text` renders the model attribute as element text.

---

### 2) Multithreaded Array Search — 5 Threads

**Design:**
- Array size 1000, target = 999.
- Split into 5 ranges of 200 each.
- A shared variable `foundIndex` (initialized to -1) holds the result.
- Use `synchronized` to update `foundIndex` safely.
- Main calls `join()` on all threads, then checks the result.

```java
class Searcher implements Runnable {
    static int[] arr;          // shared array
    static int target = 999;
    static int foundIndex = -1;

    int from, to;
    Searcher(int from, int to) { this.from = from; this.to = to; }

    public synchronized void setFound(int idx) {
        if (foundIndex == -1) foundIndex = idx;
    }

    public void run() {
        for (int i = from; i < to; i++) {
            if (arr[i] == target) { setFound(i); return; }
        }
    }
}

public class Main {
    public static void main(String[] args) throws InterruptedException {
        Searcher.arr = new int[1000];
        // fill array ... Searcher.arr[750] = 999; (example)

        Thread[] threads = new Thread[5];
        for (int i = 0; i < 5; i++)
            threads[i] = new Thread(new Searcher(i * 200, (i + 1) * 200));
        for (Thread t : threads) t.start();
        for (Thread t : threads) t.join();

        if (Searcher.foundIndex != -1)
            System.out.println("Found at index: " + Searcher.foundIndex);
        else
            System.out.println("Element does not exist");
    }
}
```

---

## Question 4 — Spring Data JPA (6 Marks)

> **Given:** `Student` entity with columns `id`, `name`, `grade`.

### Repository

```java
public interface StudentRepository extends JpaRepository<Student, Integer> {

    @Query("SELECT s FROM Student s WHERE s.grade IN :grades")
    List<Student> findByGrades(@Param("grades") List<String> grades);
}
```

### Service

```java
@Service
public class StudentService {
    @Autowired StudentRepository repo;

    public void run() {
        // Insert a fake student
        Student s = new Student();
        s.setName("Ali Hassan");
        s.setGrade("A");
        repo.save(s);

        // Display all A-grade students
        List<Student> topStudents =
            repo.findByGrades(List.of("A-", "A", "A+"));

        for (Student st : topStudents)
            System.out.println(st.getId() + " | " + st.getName() + " | " + st.getGrade());
    }
}
```

**Key points for full marks:**
- `JpaRepository<Student, Integer>` provides `save()` and `findAll()` out of the box.
- Custom `@Query` with `IN :grades` handles multiple grade values in one query.
- `repo.save(entity)` performs INSERT when `id` is null.
