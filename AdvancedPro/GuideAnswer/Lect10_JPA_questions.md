# Lecture 10 — Spring Data JPA: Question Bank & Guide Answers

## Topic Summary

- **Overview:** Spring Data JPA provides a repository abstraction over the JPA/Hibernate stack to simplify CRUD and queries, eliminating boilerplate SQL.
- **Startup Lifecycle:** Hibernate scans entities, connects to DB, handles schema generation (`ddl-auto`), and makes the app ready.
- **Thymeleaf Integration:** Forms use `th:object` / `th:field` for bi-directional binding, and controllers use `@PathVariable` to capture URL arguments.

### 1. Comparison: JPA vs Hibernate vs Spring Data JPA

| Framework/API | Role | Description |
|---|---|---|
| **JPA** | Specification (API) | A set of rules/interfaces (`@Entity`, `@Id`, `@ManyToOne`) describing how objects map to tables. It doesn't perform DB operations. |
| **Hibernate** | Implementation (Engine) | The concrete ORM framework that generates SQL, manages sessions, and moves data to/from the database. |
| **Spring Data JPA** | Abstraction Layer | Sits on top of JPA/Hibernate, auto-generating repository implementations (like `JpaRepository`) and query methods. |

### 2. Understanding Table: Entity Relationships & Mapping

| Concept / Annotation | Definition & Usage | Example / Note |
|---|---|---|
| `@Entity` & `@Id` | Marks a class as a database table and defines its Primary Key. | Default is a singleton class; PK uses `@GeneratedValue(strategy=GenerationType.IDENTITY)`. |
| `@ManyToOne` (Owner) | "Many" records point to "One" parent. Holds the Foreign Key. | Student has `@ManyToOne` and `@JoinColumn(name="department_id")`. |
| `@OneToMany` (Inverse) | The "One" side listing the "Many". Does not own the FK. | Department has `@OneToMany(mappedBy="department")`. |
| `@ManyToMany` (Owner) | Uses a bridge table for M:N relations. | Student defines `@JoinTable(name="student_courses", joinColumns=..., inverseJoinColumns=...)`. |
| `mappedBy` | Tells the inverse side: "Look at the owner side for the mapping." | Used in `Course` for M:N: `@ManyToMany(mappedBy="courses")`. |

### 3. Understanding Table: JpaRepository Core Methods

| Java Action | Internal Logic / Action | Typical Generated SQL |
|---|---|---|
| `save(newObj)` | Detects ID is null (new record). | `INSERT INTO table (var) VALUES (?)` |
| `save(existingObj)`| Detects ID is present (existing record). | `UPDATE table SET var=? WHERE id=?` |
| `findAll()` | Fetches every row in the table. | `SELECT * FROM table` |
| `findById(id)` | Fetches a specific row by its PK. | `SELECT * FROM table WHERE id=?` |
| `deleteById(id)` | Removes the specific row by its PK. | `DELETE FROM table WHERE id=?` |

## Tone analysis

No past exam samples were provided, so the following questions use a neutral academic exam tone (direct verbs such as "explain", "compare", "apply") with reasonable default mark allocations.

---

# Question Bank

Group order: Multiple choice → Fill-in-the-blank → Short answer → True/False + justify → Application → Compare & contrast → Essay

---

## Multiple choice (MCQ)

### Q1 — Multiple choice | Bloom's: Remember | Difficulty: Easy | Marks: 2
**Question:**
Which statement best describes the relationship between JPA and Hibernate?

A. JPA is an implementation, Hibernate is the specification.

B. Hibernate is an implementation of the JPA specification.

C. JPA and Hibernate are independent frameworks with no relation.

D. Hibernate replaces JPA in Spring Data.

**Guide answer:**
B

**Key points to include:**
- JPA = specification; Hibernate = implementation.
- Hibernate implements JPA annotations and runtime behavior.

**Common mistakes to avoid:**
Choosing A or D (reversing spec vs implementation).

### Q2 — Multiple choice | Bloom's: Understand | Difficulty: Medium | Marks: 2
**Question:**
Which annotation and placement correctly make Student the owner of a many-to-many relationship with Course?

A. In `Course`: `@ManyToMany` with `mappedBy="courses"`

B. In `Student`: `@ManyToMany` and `@JoinTable(name="student_courses", joinColumns=@JoinColumn(name="student_id"), inverseJoinColumns=@JoinColumn(name="course_id"))`

C. In `Student`: `@OneToMany` with `@JoinColumn("course_id")`

D. In `Course`: `@JoinTable(...)` only

**Guide answer:**
B

**Key points to include:**
- Owner side defines `@JoinTable`.
- `joinColumns` refer to owner (`student_id`), `inverseJoinColumns` to other side (`course_id`).

**Common mistakes to avoid:**
Confusing `mappedBy` (inverse) with the owner; using `@OneToMany` for many-to-many.

---

## Fill-in-the-blank

### Q3 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2
**Question:**
The JPA annotation used to mark a Java class as a persistent entity is __________.

**Guide answer:**
`@Entity`

**Key points to include:**
- Exact annotation name.
- Placed on the entity class.

**Common mistakes to avoid:**
Writing `@Table` instead of `@Entity`.

### Q4 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2
**Question:**
To let Hibernate automatically create or update database tables based on entity classes, set `spring.jpa.hibernate.ddl-auto` to __________ in `application.properties`.

**Guide answer:**
`update` (or `create`)

**Key points to include:**
- `update` keeps schema in sync; `create` recreates tables.
- Default alternatives: `none`, `validate`, `create-drop`.

**Common mistakes to avoid:**
Thinking this is a Spring Boot property unrelated to Hibernate.

---

## Short answer

### Q5 — Short answer | Bloom's: Understand | Difficulty: Easy | Marks: 5
**Question:**
Briefly explain what `save()` does in `JpaRepository` and how it decides between INSERT and UPDATE.

**Guide answer:**
`save()` persists an entity; if the entity's ID is null (or not present), JPA treats it as new and issues an INSERT; if the entity has a non-null ID that exists in the database, JPA issues an UPDATE. Thus `save()` acts as insert-or-update depending on identity.

**Key points to include:**
- ID-null ⇒ insert; ID-present ⇒ update.
- `save()` delegates to the persistence context / entity manager.

**Common mistakes to avoid:**
Saying `save()` always performs only INSERT or only UPDATE.

### Q6 — Short answer | Bloom's: Understand | Difficulty: Medium | Marks: 5
**Question:**
What is the "owner" side of a JPA relationship and why does it matter?

**Guide answer:**
The owner side is the entity that owns the database foreign-key or join table mapping (where `@JoinColumn` or `@JoinTable` is declared). It matters because changes to the relationship (persisting/updating links) are only reflected in the database when performed on the owner side; the inverse side (with `mappedBy`) is read-only in terms of database mapping.

**Key points to include:**
- Owner contains `@JoinColumn` / `@JoinTable`.
- Only owner updates propagate DB mapping changes.
- `mappedBy` indicates inverse side and points to owner field name.

**Common mistakes to avoid:**
Assuming both sides are symmetrical for DB column creation.

---

## True / False + justify

### Q7 — True / False + justify | Bloom's: Understand | Difficulty: Easy | Marks: 3
**Question:**
T/F: `@OneToMany` must always include a `@JoinColumn` on the same side to create the foreign key column.

**Guide answer:**
False. In a one-to-many / many-to-one pair, the foreign key column belongs to the many side (owner), which typically uses `@ManyToOne` with `@JoinColumn`. The `@OneToMany` side is usually the inverse and uses `mappedBy` instead.

**Key points to include:**
- Many side is owner; `@JoinColumn` normally on many side.
- `@OneToMany(mappedBy=...)` is common.

**Common mistakes to avoid:**
Putting `@JoinColumn` on the inverse side and expecting it to be authoritative.

### Q8 — True / False + justify | Bloom's: Understand | Difficulty: Medium | Marks: 3
**Question:**
T/F: Setting `spring.jpa.hibernate.ddl-auto=update` in production guarantees zero data loss during schema changes.

**Guide answer:**
False. `update` attempts to modify schema non-destructively, but it may not handle complex migrations safely; for production it's recommended to use controlled migrations (Flyway, Liquibase) and backups.

**Key points to include:**
- `update` is convenient but not a replacement for migration tools.
- Risk: incompatible field changes, data loss in some cases.

**Common mistakes to avoid:**
Assuming `update` is a safe automated migration strategy for production.

---

## Application (scenario-based)

### Q9 — Application | Bloom's: Apply / Analyse | Difficulty: Medium | Marks: 8
**Question:**
You have `Student` entities loaded with `department = null` for some records. You render a Thymeleaf `student-list.html` using `th:each` over students and want to show the department name or "No Department" when null. Write the Thymeleaf expression to display either the department name or "No Department".

**Guide answer:**
Use a conditional expression inside the template, for example:

```html
<span th:text="${student.department != null} ? ${student.department.name} : 'No Department'">Department</span>
```

Or using Thymeleaf `th:if`/`th:unless`:

```html
<span th:if="${student.department != null}" th:text="${student.department.name}"></span>
<span th:unless="${student.department != null}">No Department</span>
```

**Key points to include:**
- Use `th:text` with conditional or `th:if`/`th:unless`.
- Correctly access `student.department.name` when not null.

**Common mistakes to avoid:**
Trying to access `student.department.name` directly without null check (causes NPE-like rendering issues).

### Q10 — Application (multi-part) | Bloom's: Apply / Analyse | Difficulty: Hard | Marks: 12
**(a)** Describe how you would model a many-to-many relationship between `Student` and `Course` in JPA, including annotations and the join table. (Marks: 6)

**(b)** Give a short code snippet for the `Student` side showing annotations. (Marks: 4)

**(c)** Explain how to fetch all students enrolled in a given course id using a `JpaRepository` method or JPQL. (Marks: 2)

**Guide answer:**
**(a)** Use `@ManyToMany` on the owner side and `@JoinTable` to declare the bridge table; `mappedBy` on inverse side. Choose owner (e.g., Student) to define `@JoinTable(name="student_courses", joinColumns=@JoinColumn(name="student_id"), inverseJoinColumns=@JoinColumn(name="course_id"))`.

**(b)** Example snippet:

```java
@Entity
public class Student {
  @Id @GeneratedValue(strategy=GenerationType.IDENTITY)
  private Long id;
  private String name;

  @ManyToMany
  @JoinTable(
    name = "student_courses",
    joinColumns = @JoinColumn(name = "student_id"),
    inverseJoinColumns = @JoinColumn(name = "course_id")
  )
  private Set<Course> courses = new HashSet<>();
}
```

**(c)** Use a repository method on `Course` or `StudentRepo`:
- JPQL: `@Query("SELECT s FROM Student s JOIN s.courses c WHERE c.id = :courseId") List<Student> findByCourseId(@Param("courseId") Long courseId);`
- Or load Course and call `course.getStudents()` if relationship is bidirectional and fetched appropriately.

**Key points to include:**
- Owner side defines `@JoinTable`.
- Snippet must show `@ManyToMany` + `@JoinTable`.
- Use JPQL join or repository method to fetch students by course id.

**Common mistakes to avoid:**
Defining duplicate join table on both sides, or forgetting `mappedBy` on inverse side.

---

## Compare & contrast

### Q11 — Compare & contrast | Bloom's: Analyse / Evaluate | Difficulty: Medium | Marks: 8
**Question:**
Compare `@ManyToOne` with `@OneToMany` in JPA: describe which side is the owner, where the foreign key lives, typical annotations used, and one example use-case for each.

**Guide answer:**
- Owner: `@ManyToOne` is the owner side; `@OneToMany` is typically the inverse (use `mappedBy`).
- Foreign key: stored on the many side (table with `@ManyToOne`), e.g., `student.department_id`.
- Annotations: owner uses `@ManyToOne` + `@JoinColumn`; inverse uses `@OneToMany(mappedBy="...")`.
- Use-cases: `@ManyToOne` example—Student → Department; `@OneToMany` example—Department listing students.

**Key points to include:**
- Owner vs inverse; DB column location.
- Practical example mapping.

**Common mistakes to avoid:**
Thinking `@OneToMany` creates the FK column in the referenced table automatically.

### Q12 — Compare & contrast | Bloom's: Analyse / Evaluate | Difficulty: Hard | Marks: 8
**Question:**
Contrast `spring.jpa.hibernate.ddl-auto = update` with a migration tool approach (Flyway/Liquibase). List advantages and risks of each and recommend when to use each approach.

**Guide answer:**
- `ddl-auto=update`: Advantage—automatic and convenient during development; quick schema alignment. Risk—may not handle complex migrations safely, can be unpredictable in production, potential for data loss. Use in development or prototyping.
- Migration tools (Flyway/Liquibase): Advantage—explicit, versioned migrations, repeatable and auditable; safe for production changes. Risk—requires writing migration scripts and ops discipline. Recommended approach for staging/production with CI/CD.

**Key points to include:**
- Safety and reproducibility are primary differences.
- Production → use migration tools; development → `update` acceptable.

**Common mistakes to avoid:**
Assuming `update` handles all schema-change scenarios safely.

---

## Essay / long answer

### Q13 — Essay / long answer | Bloom's: Evaluate / Create | Difficulty: Hard | Marks: 15
**Question:**
Explain the role of the repository abstraction in Spring Data JPA. Discuss how repository method derivation works, when to use custom `@Query`, and trade-offs between using generated finder methods and custom queries. Structure your answer with an introduction, body, and conclusion.

**Guide answer:**
**Introduction:** The repository abstraction (`JpaRepository` and related interfaces) provides a high-level programming model that encapsulates common persistence operations and reduces boilerplate DAO code.

**Body:**
- Method derivation: Spring Data analyzes method names (e.g., `findByNameAndAgeGreaterThan`) to derive queries automatically based on property names and operators. This enables rapid development for common patterns.
- When to use custom `@Query`: Use `@Query` for complex joins, performance-critical queries, queries using database-specific features, or when method name derivation becomes unreadable or insufficient.
- Trade-offs: Derived methods are concise and readable for simple queries but can grow verbose or ambiguous for complex logic. `@Query` gives explicit control and potentially optimized SQL/JPQL but increases coupling to query text and possibly database-specific behavior. Maintainability and performance considerations determine the choice.

**Conclusion:** Use repository derivation for straightforward queries to speed development and readability; adopt `@Query` (or a custom repository implementation) when complexity, performance, or clarity demands explicit query control.

**Key points to include:**
- Purpose of repository abstraction.
- How method derivation maps to queries.
- Criteria for custom `@Query`.
- Trade-offs: readability, maintainability, performance.

**Common mistakes to avoid:**
Overusing `@Query` for trivial lookups; over-relying on derived names that become unreadable.

---

## Study tips

- Revisit owner/inverse rules for relationships (owner defines `@JoinColumn`/`@JoinTable`): many exam mistakes come from mixing up where the FK or join table is declared.
- Practice small hands-on examples with H2: create the `Student`/`Department`/`Course` entities and run the app to inspect generated tables and join table contents.
- Learn safe schema change practices: understand what `ddl-auto=update` does and when to switch to migration tools (Flyway/Liquibase) for production.

## Coverage gap analysis

- Covered: entity annotations, relationship ownership, `JpaRepository` basics, `save()` semantics, `ddl-auto`, Thymeleaf binds, controller path variables.
- Not covered (explicitly in questions): detailed `@Column` options (nullable, length), transaction boundaries (`@Transactional`) — Why testable: important for persistence correctness and concurrency; Suggested question type: Short answer or Application.
- Not covered (explicitly): Fetch types (`LAZY` vs `EAGER`) and N+1 query problem — Why testable: impacts performance and mapping decisions; Suggested question type: Compare & contrast or Application.

---

*Generated from `AdvancedPro/Lect/Lect10_Hibernate_ORM_Vs_JPA_Thymleaf_SpringBoot.md`.*
