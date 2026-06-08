# Exam 25-26 — Guide Answers

---

## Question 1 — MCQ Answers (10 Marks)

| # | Answer | Key Reason |
|---|--------|-----------|
| 1 | **C** | `return "redirect:/target"` sends a new HTTP response to the client telling the browser to navigate to the new URL → browser URL changes. |
| 2 | **D** | The `name` attribute of an `<input>` element is what the browser submits as the form field key. `id` is only for DOM selection. |
| 3 | **B** | JPA is part of the **Java EE** (Enterprise Edition) platform. |
| 4 | **D** | Spring Data JPA repositories handle SELECT, UPDATE, DELETE (and INSERT via `save()`). |
| 5 | **A** | `th:insert` inserts a fragment's content inside the host element. (`th:replace` replaces the entire host element.) |
| 6 | **B** | `@Scope("request")` limits the bean lifecycle to a single HTTP request. |
| 7 | **A** | `sleep(ms)` pauses the thread for a specified time period. `join()` waits for another thread to finish; `wait()` releases a monitor lock. |
| 8 | **Threads execute one at a time (serially).** | The `synchronized` keyword ensures only one thread enters `increment()` at a time → `x` and `y` are always equal and incremented atomically. The output will always be `x == y`. |
| 9 | **D** | Default Spring Bean scope is **Singleton**. `@Component`, `@Service`, `@Controller`, `@Repository`, `@Entity` (managed by Spring context) all default to singleton. |
| 10 | **A** | The **Service layer** (or Model/Service) is responsible for business logic. The Controller handles HTTP routing and the View handles presentation. |

---

## Question 2 — Short Answers (12 Marks)

### 1) Three Advantages of Spring Boot/Thymeleaf over Java Servlets/JSP

1. **Auto-configuration:** Spring Boot auto-configures components (embedded Tomcat, data source) — no `web.xml` or manual servlet registration needed.
2. **Dependency Injection (IoC):** Spring manages object creation and wiring automatically, reducing boilerplate and coupling.
3. **Thymeleaf natural templates:** Thymeleaf HTML files render correctly in a browser without a running server (unlike JSP which requires compilation), and the syntax is cleaner and type-safe with model binding.

---

### 2) Three Differences: JavaBean vs Spring Bean

| Feature | JavaBean | Spring Bean |
|---------|----------|------------|
| **Managed by** | Developer (created with `new`) | Spring IoC Container |
| **Lifecycle** | Created/destroyed by the developer | Managed by Spring (singleton by default, scoped) |
| **Convention required** | Must have no-arg constructor, private fields, getters/setters, implement `Serializable` | No strict convention — any class annotated with `@Component`, `@Service`, etc. |

---

### 3) How Synchronization Prevents Race Conditions

A `synchronized` block/method acquires a **monitor lock** on an object before executing. Only one thread holds the lock at a time; all others wait. This enforces **mutual exclusion** — no two threads can simultaneously read/write the shared resource. When the lock is released, the next waiting thread proceeds with a consistent state, eliminating race conditions.

---

### 4) Why Override `run()` but NOT Call It Directly

- **Override `run()`:** This method defines the **task** to execute. Java requires us to override it to specify what the thread should do; the `Runnable` interface provides only this one method.
- **Never call `run()` directly:** Calling `run()` on a Runnable or Thread executes it as a **regular method call in the current thread** — no new thread is created. To actually launch a new thread, you must call `t.start()`, which registers with the JVM and causes the JVM to call `run()` in the new thread's context automatically.

---

## Question 3 — Coding (10 Marks)

### 1) Spring Boot Controller + Student Class

> Given the Thymeleaf template that binds `name` and `level`, and displays the count of level-1 students.

**Student Model:**

```java
public class Student {
    private String name;
    private int level;
    // getters & setters
}
```

**Controller:**

```java
@Controller
public class StudentController {
    private List<Student> students = new ArrayList<>();

    @GetMapping("/form")
    public String showForm(Model model) {
        model.addAttribute("student", new Student());
        return "student-form";
    }

    @PostMapping("/register")
    public String register(@ModelAttribute Student student, Model model) {
        students.add(student);
        long firstCount = students.stream()
                            .filter(s -> s.getLevel() == 1)
                            .count();
        model.addAttribute("firstCount", firstCount);
        return "result";
    }
}
```

**Key points:**
- `@GetMapping("/form")` adds an empty `Student` to model so `th:object` has a target.
- `@ModelAttribute` binds the form fields (`name`, `level`) directly into the `Student` object.
- Count level-1 students and pass to `result.html` as `firstCount`.

---

### 2) Multithreaded Min/Max — 2 Threads → `d = max - min`

**Design:** Thread 1 finds max, Thread 2 finds min. Main uses `join()` on both, then computes `d = max - min`.

```java
class MaxFinder implements Runnable {
    int[] arr; static int max = Integer.MIN_VALUE;
    MaxFinder(int[] a) { arr = a; }
    public void run() {
        for (int v : arr) if (v > max) max = v;
    }
}

class MinFinder implements Runnable {
    int[] arr; static int min = Integer.MAX_VALUE;
    MinFinder(int[] a) { arr = a; }
    public void run() {
        for (int v : arr) if (v < min) min = v;
    }
}

public class Main {
    public static void main(String[] args) throws InterruptedException {
        int[] arr = new int[1000];
        // fill arr with values...

        Thread t1 = new Thread(new MaxFinder(arr));
        Thread t2 = new Thread(new MinFinder(arr));
        t1.start(); t2.start();
        t1.join();  t2.join();

        int d = MaxFinder.max - MinFinder.min;
        System.out.println("d = " + d);
    }
}
```

**Key points:**
- `join()` ensures both threads complete before the main thread reads the results.
- `Integer.MIN_VALUE` as the initial `max` and `Integer.MAX_VALUE` as the initial `min` handle any array content correctly.

---

## Question 4 — Spring Data JPA (8 Marks)

> **Given:** `Player` entity with fields: `id`, `name`, `team`, `position`.

### 1. Repository Interface

```java
public interface PlayerRepository extends JpaRepository<Player, Integer> {

    // 2. Custom delete by team
    void deleteByTeam(String team);

    // 3. Custom find by team + position IN list
    @Query("SELECT p FROM Player p WHERE p.team = :team AND p.position IN :positions")
    List<Player> findByTeamAndPositions(@Param("team") String team,
                                        @Param("positions") List<String> positions);
}
```

### 2. Service / Usage

```java
@Service
public class PlayerService {
    @Autowired PlayerRepository repo;

    public void run() {
        // 1. Insert a player
        Player p = new Player();
        p.setName("Mohamed Salah");
        p.setTeam("Egypt");
        p.setPosition("RW");
        repo.save(p);

        // 2. Delete all Angola players
        repo.deleteByTeam("Angola");

        // 3. Display Egypt GK or RW players
        List<Player> result =
            repo.findByTeamAndPositions("Egypt", List.of("GK", "RW"));
        result.forEach(pl ->
            System.out.println(pl.getName() + " | " + pl.getPosition()));
    }
}
```

**Key points for full marks:**
- `deleteByTeam(String team)` → Spring Data derives the DELETE query from the method name automatically.
- Custom `@Query` with `AND p.position IN :positions` handles the OR logic for positions in a single query.
- `repo.save(entity)` → INSERT when `id` is null, UPDATE when `id` exists.
