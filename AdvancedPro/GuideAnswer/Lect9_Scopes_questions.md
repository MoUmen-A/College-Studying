# Lecture 9 — Bean Scopes, Sessions, and Proxies: Question Bank & Guide Answers

## Topic Summary

- **Sessions & State Management:** A session provides private server-side storage per user (browser) to avoid data leakage (e.g., one user seeing another's tasks). Manually, this is done via `HttpSession`.
- **Spring Bean Scopes:** Defines the lifecycle and visibility of a bean. Main scopes include **Singleton** (default, one per app), **Session** (one per user session), and **Request** (one per HTTP request).
- **The Dependency Injection Conflict:** At application startup, there are no active requests or sessions, making it impossible for Spring to directly inject a Session/Request scoped bean into a Singleton Controller.
- **The Proxy Solution:** Spring handles the scope mismatch by injecting a "placeholder" Proxy object. At runtime, the Proxy intercepts calls, dynamically looks up the correct instance for the active thread/user, and delegates the method call.

## Tone analysis

No past exam samples were provided, so the following questions are written using a standard academic tone. Provide past exams in future runs for more accurate tone calibration.

---

# Question Bank

Group order: Multiple choice → Fill-in-the-blank → Short answer → True/False + justify → Application → Compare & contrast → Essay / long answer

---

## Multiple choice (MCQ)

### Q1 — Multiple choice | Bloom's: Remember | Difficulty: Easy | Marks: 2
**Question:**
Which of the following describes the default scope of a Spring Bean (such as a `@Service` or `@Controller`)?

A. Request  
B. Session  
C. Singleton  
D. Prototype  

**Guide answer:**
C

**Key points to include:**
- Singleton is the default scope if nothing is specified.
- Only one instance is created and shared across the entire application.

**Common mistakes to avoid:**
Assuming session is the default because web applications imply user sessions.

### Q2 — Multiple choice | Bloom's: Understand | Difficulty: Medium | Marks: 2
**Question:**
Why does Spring use a Proxy object when injecting a Session-scoped bean into a Singleton Controller?

A. To increase the execution speed and minimize memory overhead during HTTP requests.  
B. To handle the mismatch at startup because no active user session exists when the Controller is initialized.  
C. Because Singleton beans are not allowed to be injected with any dependencies.  
D. To prevent Cross-Site Scripting (XSS) attacks in the user session.  

**Guide answer:**
B

**Key points to include:**
- Controller is created at startup, but Session doesn't exist yet.
- Proxy acts as a placeholder that resolves the real bean at runtime.

**Common mistakes to avoid:**
Selecting A; proxies actually introduce a tiny amount of overhead, not a speed increase.

---

## Fill-in-the-blank

### Q3 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2
**Question:**
When extracting a generic Object from a manual `HttpSession` and casting it to a specific collection (like `List<Task>`), developers use the ____________ annotation to silence compiler complaints regarding type erasure.

**Guide answer:**
`@SuppressWarnings("unchecked")`

**Key points to include:**
- Exact annotation name.

**Common mistakes to avoid:**
Writing `@SuppressWarning` (missing the 's') or just `"unchecked"` without the annotation framework.

### Q4 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2
**Question:**
If data is only useful for the brief moment it takes to load a single page or process a form submission, you should configure the bean with ____________ scope.

**Guide answer:**
Request

**Key points to include:**
- Destroyed right after the HTTP response.

**Common mistakes to avoid:**
Confusing it with Session scope, which persists across multiple requests.

---

## Short answer

### Q5 — Short answer | Bloom's: Understand | Difficulty: Medium | Marks: 5
**Question:**
Explain the mechanism of a Proxy object at runtime when an HTTP request hits a mapped endpoint.

**Guide answer:**
When a request hits the controller and invokes a method on the injected dependency, the call doesn't go to the real object immediately. Instead, it hits the Proxy first. The Proxy intercepts the call, performs a dynamic lookup to find the specific bean instance belonging to the current user's session or request, and then delegates the call to that real instance.

**Key points to include:**
- Interception of the method call.
- Dynamic lookup of the correct user/thread instance.
- Delegation to the real object.

**Common mistakes to avoid:**
Assuming the Proxy creates a new object on every method call (it fetches the existing scoped object).

### Q6 — Short answer | Bloom's: Understand | Difficulty: Easy | Marks: 5
**Question:**
Briefly explain the structural security/data leakage issue that occurs when using a Singleton bean to store a List of user-submitted Tasks.

**Guide answer:**
Because a Singleton creates only one shared instance of the bean for the entire application, any state (like a List of Tasks) saved inside it is shared across all browsers/users. Consequently, a task added by User A is completely visible and modifiable by User B, which is a severe data leakage and privacy issue.

**Key points to include:**
- Singleton means one shared instance.
- Shared state leads to visible data across different users.

**Common mistakes to avoid:**
Blaming the database or the browser interface rather than the application's shared memory state.

---

## True / False + justify

### Q7 — True / False + justify | Bloom's: Understand | Difficulty: Easy | Marks: 3
**Question:**
T/F: In a typical web application, classes containing only application logic and no user-specific data (such as standard Services and Mappers) should be declared with Session scope.

**Guide answer:**
False. If a class contains only logic and no user-specific state, it should be a Singleton (the default). Creating thousands of copies of a pure logic class wastes memory needlessly.

**Key points to include:**
- Logic-only classes do not need private state.
- Singleton saves memory.

**Common mistakes to avoid:**
Believing every layer in a web app must have Request or Session scope to be thread-safe.

### Q8 — True / False + justify | Bloom's: Analyse | Difficulty: Medium | Marks: 3
**Question:**
T/F: When a Session-scoped proxy is injected into a Singleton controller, the Spring Boot application crashes at startup because of a scope mismatch.

**Guide answer:**
False. Spring Boot does not crash in this scenario precisely because it uses a Proxy. The Proxy acts as a temporary empty shell at startup to satisfy the dependency injection requirements, resolving the real object only when a request actually happens.

**Key points to include:**
- Proxies prevent the startup crash.
- Resolves mapping when an active request is available.

**Common mistakes to avoid:**
Stating that the app crashes (which would only happen if proxy modes are configured incorrectly / disabled).

---

## Application (scenario-based)

### Q9 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 8
**Question:**
You are building an e-commerce website. Determine the most appropriate Spring bean scope (Singleton, Session, or Request) for each of the following components, and briefly justify your choice in 1 sentence for each:
1. `TaxCalculatorService`: Computes tax rates based on standard formulas.
2. `ShoppingCart`: Holds the list of items a user intends to buy as they browse different pages.
3. `PaymentErrorLogger`: Gathers validation errors during a single checkout submission to return immediately to the UI.

**Guide answer:**
1. **Singleton:** `TaxCalculatorService` only contains business logic without user-specific state, so one shared instance is memory efficient.
2. **Session:** `ShoppingCart` data needs to be isolated per user and persist across multiple HTTP requests as they navigate the site.
3. **Request:** `PaymentErrorLogger` is only relevant for the duration of that single form submission and should be discarded once the response is sent.

**Key points to include:**
- Correct scopes: Singleton, Session, Request.
- Justifications matching the lifecycle/shared rules.

**Common mistakes to avoid:**
Making the ShoppingCart Singleton (exposing carts to all users) or the Logger Session (keeping old errors around).

---

## Compare & contrast

### Q10 — Compare & contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 8
**Question:**
Compare managing user data manually via `HttpSession` attributes versus using Spring's Session scope. Discuss the developer experience and code cleanliness.

**Guide answer:**
Managing data manually via `HttpSession` requires developers to explicitly interact with the session object (e.g., `session.getAttribute()`, `session.setAttribute()`), handle null checks, and cast objects back to their correct types (often requiring `@SuppressWarnings("unchecked")`). 

In contrast, Spring's Session scope handles this transparently. Developers can inject the session-scoped bean directly into controllers using `@Autowired` and interact with it as a normal Java object. Spring manages the lifecycle, lookup, and background binding, leading to cleaner code devoid of manual HTTP attribute manipulation.

**Key points to include:**
- Manual: requires `getAttribute()`, casting, and potential warnings.
- Spring: uses Dependency Injection, treats session data as regular beans.
- Developer experience: Spring is cleaner and more abstracted.

**Common mistakes to avoid:**
Saying they are functionally different in where data is saved (both save data in server memory per user).

---

## Essay / long answer

### Q11 — Essay / long answer | Bloom's: Evaluate | Difficulty: Hard | Marks: 15
**Question:**
Detail the entire lifecycle of a Spring Boot application dealing with a Singleton Controller that depends on a Session-scoped bean. Outline what happens during component scanning, application startup (the "Crash Point"), the Proxy solution, and what exactly occurs at runtime when a user makes an HTTP request.

**Guide answer:**
**Introduction:** 
In Spring Boot, mismatched scopes (like a Singleton depending on a Session object) pose a unique Dependency Injection challenge that is solved automatically through the use of Proxy patterns.

**Body:** 
1. **Component Scanning & Bean Definition:** At startup, Spring scans for annotations (`@Controller`, `@Service`) and maps out their required scopes and dependencies.
2. **The "Crash Point" at Startup:** As Spring wires dependencies, it attempts to inject the Session-scoped bean into the Singleton Controller. However, since the app is just launching, no user HTTP requests exist, meaning no Session exists yet. Normally, this would cause a failure.
3. **The Proxy Solution:** To resolve this, Spring injects a Proxy (an "empty shell" or interceptor) that implements the same interface as the Session bean. The application successfully finishes starting up with the Controller holding this Proxy.
4. **Runtime Execution:** When an HTTP request finally hits the mapped controller endpoint, the Controller calls a method on what it thinks is the Session bean. The call actually hits the Proxy. The Proxy inspects the incoming thread, identifies the specific user session (e.g., User #42), fetches the actual, real Session bean from server memory, and delegates the method call to it.

**Conclusion:** 
Spring's Proxy mechanism allows developers to seamlessly mix long-lived stateless Singletons with short-lived stateful user data, maintaining architectural cleanliness without sacrificing application stability.

**Key points to include:**
- Startup phase: no active session available.
- Proxy creation: placeholder injected into Controller.
- Runtime phase: interception, dynamic lookup, and delegation.

**Common mistakes to avoid:**
Skipping the interception and delegation steps in the runtime phase.

---

## Study tips

- **Proxy mechanism:** Ensure you can visualize the timeline difference between *Startup* (Proxy creation) and *Runtime* (Proxy delegation).
- **Scope definitions:** Practice translating real-world metaphors (e.g., Singleton = Hotel Front Desk, Session = Guest Room, Request = Room Service Order) into code requirements.

## Coverage gap analysis

- **Covered:** Manual Sessions, Singleton, Session, Request scopes, Startup vs Runtime behaviour, Proxies.
- **Not covered (explicitly testing syntax):** The actual annotations used to declare these scopes in code (e.g., `@Scope("session")` or `@SessionScope`). 
  - *Why it matters:* Required for implementation.
  - *Suggested question type:* Fill-in-the-blank or Short answer on how to annotate a class to be Session-scoped.

---
*Generated from `AdvancedPro/Lect/Lect9-Session_Req_Singleton_Proxy_Vs_Bean_SpringBoot3.md`.*
