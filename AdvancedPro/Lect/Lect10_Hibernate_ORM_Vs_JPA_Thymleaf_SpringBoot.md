# CCS2304 – Advanced Programming Applications

## CCS2304 – Advanced Programming Applications

- Lecture 10: Spring Data JPA


## Introduction

- Spring Data Java Persistence API (JPA) is a framework that simplifies database access in Spring Boot applications by providing an abstraction layer over the JPA.
- It enables seamless integration with relational databases using Object-Relational Mapping (ORM), eliminating the need for boilerplate SQL queries.


## Advantage of JPA

- With Spring Data JPA, developers no longer need to:
  - Manually write DAO implementations.
  - Manage EntityManager directly.
  - Write repetitive CRUD queries


## Key Features of Spring Data JPA

- Repository Abstraction: Spring Data JPA provides interfaces like JpaRepository to perform CRUD operations without writing SQL queries.
- Query Methods: We can define methods like findByName() or findByAgeGreaterThan() and Spring automatically generates the query.
- Pagination and Sorting: Supports pagination and sorting using built-in methods like findAll(Pageable pageable).
- Custom Queries: Allows writing custom queries using @Query annotation (JPQL or native SQL).


## Hibernate vs JPA

- JPA (Java Persistence API) is a specification or a set of rules. It is just a document (an interface) that describes how Java objects should be mapped to database tables. It doesn't actually "do" any of the database operations.
- Hibernate is an implementation (an Object-Relational Mapping framework). It is the actual engine that contains the code to generate SQL, connect to the database, and move data.


## Why do we use both in Spring Boot?

- Spring Boot uses Spring Data JPA. This is a layer on top of both JPA and Hibernate.
  - Spring Data JPA: Provides the JpaRepository interface you are using.
  - JPA: Provides the standard annotations like @Id and @ManyToOne.
  - Hibernate: Sits at the bottom, doing the actual work of turning your Java commands into SQL.


## How to use JPA

- Add the Dependencies
- Configure the Connection
- Create an Entity
- The Repository Interface


## Add the Dependencies

- In your pom.xml, you need two primary dependencies: the Spring Data JPA starter and the driver for your specific database (e.g., MySQL, PostgreSQL, or H2 for testing).


## Configure the Connection

- You do not need to write Java code to connect to the database. Instead, you can provide the connection credentials in the `src/main/resources/application.properties` file.
- The property `spring.jpa.hibernate.ddl-auto=update` allows hibernate to create the tables based on your entity classes if they do not already exist. If the tables are present, this setting ensures that they remain synchronized with the entity classes.


## Create an Entity

- An Entity is a simple Java class that represents a table in your database. You use @Entity to tell Spring to map this class to a table.
- An entity class is also by default a singleton class


## The Repository Interface

- In Spring Data JPA, you don't usually implement the repository; you define an interface that extends JpaRepository. Spring will generate the database queries for you automatically.


## Project Example

- So let’s consider a web project:
  - That has three entity classes: student, department, and courses, and their three Repository Interfaces.
- But let’s review how the database relationship works
  - The courses can have more than one student, and a student can register for more than one course (many-to-many)
  - The department has many students and courses(one to many)
- But how does the JPA handle those relationships?
- Can I make a join between two classes in JPA?


## Project entity classes

- @id is the primary key. Every class marked with @Entity must have exactly one
- @GeneratedValue(strategy = GenerationType.IDENTITY) is autoincrement instruction
- @OneToMany(mappedBy = "department") refers to the variable name inside the Student class.


## Project entity classes

- @ManyToOne Equivalent to a foreign key  in sql
- @joincolumn(name=“department_id”) This is where you name the physical column in the database.
- @ManyToMany(mappedBy = "courses") This is the "Mirror" side of the student-course relationship.


## The @ManyToOne & @JoinColumn

- This is the most common annotation in database design. It represents the actual Foreign Key column.
- @ManyToOne: This tells JPA that many records in the current table (e.g., Students) can point to one record in the parent table (e.g., Department).
- @JoinColumn(name = "department_id"): This is where you name the physical column in the database.
  - In your SQL database, the student table will now have a column named department_id.
  - This column stores the ID of the department the student belongs to.
- The "Owner" Rule: In a One-to-Many relationship, the "Many" side is always the owner. That is why the @JoinColumn lives here and not in the Department class.


## Project entity classes

- @joinTable(…) is where the bridge is created that links the two entities, students and courses.
  - name = "student_courses” tells JPA the name of the third table it must create. In a many-to-many relationship, you cannot store the data in the Student table or the Course table alone. You need this "Join Table" to act as a link.
  - joinColumns = @JoinColumn(name = "student_id") refers to the ID of the Owner (the class you are currently writing in). Since this code is inside your Student class, it creates a column named student_id that references the Primary Key of the Student table.
  - inverseJoinColumns = @JoinColumn(name = "course_id") refers to the ID of the other side of the relationship. In this case, it creates a column called course_id that points to the Primary Key of the Course table.


## Why do we only put this in the Student class?

- In JPA, every relationship needs an Owner and a Subscriber (the inverse side).By putting @JoinTable in the Student class, you make Student the owner.
- By putting mappedBy = "courses" in the Course class, you tell the course: "I don't own the bridge table; the Student class does. If you need to find out which students are in a course, look at the bridge table described over there."


## Repository interfaces

- The first parameter tells the Repository who it's managing (The Entity), and the second parameter tells it the Primary Key type.


## When are the tables created?

- The tables are created immediately after the application starts, but before it becomes "Ready" to accept web requests.
- If the tables do not exist in your database, Hibernate follows a specific "Startup Lifecycle" to build them.
- The table names in the database have the same names as defined in the entity Class










## The Startup Lifecycle

- Bean Initialization: Spring starts setting up your Repositories and Services.
- Entity Scanning: Hibernate scans your project for any class marked with @Entity. It reads your @Id, @Column, and relationship annotations (@ManyToOne, etc.).
- Schema Generation: Hibernate connects to the database (using the credentials in application.properties).
- DDL Execution: If spring.jpa.hibernate.ddl-auto is set to update or create, Hibernate sends CREATE TABLE commands to the database.
- Application Ready: Only after the tables are successfully created does Spring finish starting up and say "Started Application in X seconds."


## Project service class

- This is a similar service to previous lectures
- The difference here is using Repository built-in functions such as findall() and deleteById(id)


## The most common JpaRepository methods

- 1. The save() Function
- The save() method is unique because it is "smart"—it performs either an INSERT or an UPDATE depending on whether the object already has an ID.


| Java Action | Internal JPA Logic | SQL Generated | Database Result |
| --- | --- | --- | --- |
| save(newStudent) | ID is null | INSERT INTO student (name, dept_id) VALUES (?, ?) | A new row is created. |
| save(existingStudent) | ID is 5 | UPDATE student SET name = ?, dept_id = ? WHERE id = 5 | The existing row is modified. |


## The most common JpaRepository methods

- 2. The findAll() Function
- This is the most common "Read" operation. It fetches every single record from the table and converts them into Java objects.


| Java Action | Internal JPA Logic | SQL Generated | Java Return Type |
| --- | --- | --- | --- |
| findById(id) | Get one specific row by its Primary Key. | SELECT * FROM table WHERE id = ? | Optional<T> |
| findAll() | Get every row in the table. | SELECT * FROM table | List<T> |
| findAllById(ids) | Get multiple rows (pass a list of IDs). | SELECT * FROM table WHERE id IN (?,?,?) | List<T> |


## The most common JpaRepository methods

- 3. The delete Functions
- There are a few ways to remove data. The most common is deleteById().


| Java Action | Internal JPA Logic | SQL Generated |
| --- | --- | --- |
| repo.deleteById(5L) | Find by ID then Remove | DELETE FROM student WHERE id = 5 |
| repo.delete(studentObject) | Remove specific object | DELETE FROM student WHERE id = ? |
| repo.deleteAll() | Truncate the table | DELETE FROM student |


## Thymeleaf templates



- Department-summary.html


## Thymeleaf templates

- department-summary.html




- Where university/students/delete/{id}: This is the Path Template. It matches the @PostMapping inside your Java Controller exactly.
- (id=${student.id}): This is the Parameter Mapping.
  - It looks at the current student object in the loop.
  - It takes the value of student.id (e.g., 5).
  - It replaces the {id} placeholder in the path with that value.
- .


- /


## Project Controller



## public String deleteStudent(@PathVariable Long id)

- @PostMapping("/students/delete/{id}")
  - {id}: This is a Path Variable. The curly braces tell Spring: "The value at the end of the URL is dynamic. It will change depending on which student the user wants to delete."
    - Example URL: localhost:8080/students/delete/5 (This would delete the student with ID 5).
- @PathVariable Long id
  - This annotation is the "Handshake." It takes the value from the {id} in the URL and converts it into a Java Long variable named id that you can use inside the function.


## public String deleteStudent(@PathVariable Long id)

- us.deleteStudent(id);
  - This line calls your Service Layer
  - The Service then calls the Repository's built-in deleteById(id) method
  - As we discussed before, the Repository will then generate the SQL command: DELETE FROM student WHERE id = ?
- return "redirect:/university/departments/summary";
  - This is a Redirect to GetMapping with that link, not a simple View name.


## Thymeleaf templates



- Student-list.html


## Thymeleaf templates

- Include an if condition inside the th:each loop to check if the department is null; if it is, output 'No Department.'




- Student-list.html


## Thymeleaf templates

- Add-student.html




- The values available are loaded from the database tables department and courses


## Thymeleaf templates

- add-student.html




- Th: object means that thymeleaf will use the object student within this form
- Th:field=*{name} is equivalent to writing this line <input type="text" name="name" id="name" th:value="${student.name}" />

