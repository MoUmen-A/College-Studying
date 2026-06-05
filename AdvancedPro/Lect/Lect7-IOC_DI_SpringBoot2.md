# Lect7-IOC DI SpringBoot2

## Page 1

CCS2304 – Advanced
Programming Applications
Lecture 7


## Page 2

SpringBoot Core Concepts
- Inversion of Control (IoC)
- Dependency Injection (DI)
- @Component, @Service, @Controller
- Constructor injection
- Application properties
- @Configuration


## Page 3

Inversion of Control (IoC)
- Framework controls object creation
- Developer focuses on logic
- Loose coupling


## Page 4

Inversion of Control (IoC)
What problem does IoC solve?
In traditional programming,your code controls
everything:
- You create objects
- You decide when they’re created
- You decide which class depends on which
- You manage their lifecycle
This leads to:
- Tight coupling
- Hard-to-change code
- Hard-to-test code


## Page 5

Inversion of Control (IoC)
What’s wrong here?
Traditional code:
public class OrderService {
private PaymentService paymentService = new PaymentService();
public void placeOrder() {
paymentService.pay();
}
}


## Page 6

Inversion of Control (IoC)
IoC means The control of object creation and dependency management is
moved outside your code
Instead of “I create what I need”
You say: “I declare what I need”
And something else provides it.
With IoC (Spring):
public class OrderService {
private PaymentService paymentService;
public OrderService(PaymentService paymentService) {
this.paymentService = paymentService;
}
}


## Page 7

Who controls things now?
- The Spring IoC Container.
–Creates objects (beans)
–Wires dependencies
–Manages lifecycle
–Decides when and how objects exist
Inversion of Control (IoC)


## Page 8

Dependency Injection (DI)
What is a dependency?
- Any object a class needs to do its job. Example
student class can contain course object.
What is a dependency injection?
- Dependencies are provided (injected) into a
class instead of the class creating them itself
- DI is one implementation of IoC


## Page 9

SpringBoot Annotations
Annotations in Spring Boot are metadata that provide
instructions to the Spring framework at runtime or compile time
Annotations allow developers to configure applications directly
in Java code
- Reduces XML-based configuration
- Improves code readability and maintainability
- Enables auto-configuration
- Simplifies dependency injection
- Speeds up application development


## Page 10

SpringBoot Annotations
@SpringBootApplication Annotation
- Used to mark the main class of a Spring Boot application
Example:


## Page 11

SpringBoot Annotations
@Component Annotation
- Marks a class as a generic Spring-managed object (bean)
- Spring automatically detects and registers it during
component scanning
- When Spring starts:
- It scans the project
- Finds @Component
- Creates an object
- Stores it in Application Context
- Example:


## Page 12

Reminder: Spring Boot Architecture


## Page 13

SpringBoot Annotations
@Service Annotation
- Used in the service layer to define business logic and
improve code readability
- Example:


## Page 14

SpringBoot Annotations
@Repository Annotation
- Used in the DAO layer to interact with the database.
- Automatically translates database -related exceptions
into Spring exceptions.
- Example:


## Page 15

Controllers in Spring
- @Controller
–used with HTML View
- @RestController
–used with JSON
- URL mappings


## Page 16

SpringBoot Application
The most common and efficient method to create a Spring Boot project is byusing the web-
based Spring Initializertool https://start.spring.io/ and importing the generated project in your IDE


## Page 17

- Lect7Application class is the starting point of Spring
- Runs with embedded Tomcat
- No need to install server
Project Structure


## Page 18

Simple Task Planner Project: Form
task-form.html


## Page 19

Simple Task Planner Project: Model
- Task is a simple entity class (POJO)
- Note no annotations here so it will NOT be managed by Spring
- This is a simple class used to hold and transfer data between Spring layers
- Then, how is the object created??


## Page 20

- Model is a Spring-provided
interface that acts as a
container for your data
- What is
“@ModelAttribute”?
- Spring creates the object on
the fly and fills it with form
data
- The object creation is the
responsibility of SpringMVC
and NOT Spring IoC
Container
- Then, will we ever need to
annotate the Task class?
Simple Task Planner Project: Controller


## Page 21

Simple Task Planner Project
- When to annotate an entity class?
– when it becomes something more than a simple data
container
For example, if it becomes a database entity
- If we add @Component to Task, what happens?
– Spring will create ONE shared instance
– This is WRONG for user data
– Leads to data corruption between requests


## Page 22

Simple Task Planner Project: Controller
- This class acts as a servlet
controller
- The controller contacts the
service layer
- calling doGet() through link
“/new” will output the
previous input form
- calling the doPost() will use
the service class and output
the result page with an
appropriate message
- calling default doGet() will
output all created tasks


## Page 23

Simple Task Planner Project: Service
- This service class is only
focused on business logic
- This service class provides
logic for adding a new
task, getting all created
tasks, and calculating
urgency
- The service class can call
Model classes (Task, and
TaskValidator) to perform
the required logic
- The “TaskValidator” acts
as a utility class for the
“Task” Entity


## Page 24

Simple Task Planner Project: Model
- TaskValidator is a simple utility class the validates user input
- It’s managed by Spring (Spring bean) through the @Component
- Spring creates only 1 bean of this class and injects (uses) it
whenever required by other classes


## Page 25

Simple Task Planner Project: Output
result.html


## Page 26

Simple Task Planner Project: Output
task-form.html


## Page 27

Application Properties
- “application.properties” file is where we
control how the application behaves without
changing the code
- Spring Boot automatically reads it when the
app starts


## Page 28

Simple Task Planner Project:
Application Properties
We can:
- Change server settings
– server.port=8081
- Change Thymeleaf properties
– spring.thymeleaf.cache=false
- Configure databases
– spring.datasource.url=jdbc:mysql://localhost:3306/test
– spring.datasource.username=root
– spring.datasource.password=1234


## Page 29

Simple Task Planner Project: Maven
- The created project will automatically include
all Spring dependencies
- However, we still need to add Thymeleaf
dependency

