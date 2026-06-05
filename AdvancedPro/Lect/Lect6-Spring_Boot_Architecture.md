# CCS2304 – Advanced Programming Applications

## CCS2304 – Advanced Programming Applications

- Lecture 6


## Servlets Pros and Cons

- Solved the problem of dynamic web pages
- Powerful tools
- Exposed developers to too much low-level work


## Problems with Servlets

- Too much boilerplate code


- Example: Every servlet had to deal with:
- protected void doGet(HttpServletRequest request,
- HttpServletResponse response)
- throws ServletException, IOException {
- }
- Even for the simplest tasks


## Problems with Servlets

- Manual object creation caused
  - Tight coupling
  - Hard to replace implementations
  - Hard to test
  - No lifecycle management
  - Every servlet controlled everything.


- Example:
- OrderService service = new OrderService();


## Problems with Servlets

- Servlets often:
  - Read parameters
  - Contain business logic
  - Generate HTML
  - Manage database access
  - All in one class
- This violates Separation of Concerns


## Need for a Framework

- A framework is a reusable software platform that provides structure, rules, and common functionality so developers can focus on business logic.
- Standardized architecture
- Better separation of concerns
- Simpler configuration


## Framework vs Library

- Library
- You call the library
- You control the flow
- Framework
- The framework calls your code
- You plug into its structure
- This is called Inversion of Control (IoC)


## What is Spring?

- Enterprise Java framework
- Manages application objects
- Promotes clean architecture


## What is SpringBoot

- A Java framework built on top of Spring
- Simplifies application development
- Eliminates boilerplate code with auto-configuration
- Comes with an embedded server
- Supports web apps, REST APIs, microservices, security and seamless cloud deployment


## SpringBoot with Web Module

## Spring Boot Architecture

## Spring Boot Architecture

- Client Layer
- This represents the external system or user that interacts with the application by sending HTTPS requests.


## Spring Boot Architecture

- Controller Layer (Presentation Layer)
- Handles incoming HTTP requests from the client.
- Processes the request and sends a response.
- Delegates business logic processing to the Service Layer.


## Spring Boot Architecture

- Service Layer (Business Logic Layer)
- Contains business logic and service classes.
- Communicates with the Repository Layer to fetch or update data.
- Uses Dependency Injection to get required repository services.


## Spring Boot Architecture

- Repository Layer (Data Access Layer)
- Handles CRUD (Create, Read, Update, Delete) operations on the database.
- Extends Spring Data JPA or other persistence mechanisms.


## Spring Boot Architecture

- Model Layer (Entity Layer)
- Represents database entities and domain models.
- Maps to tables in the database using JPA/Spring Data.


## Spring Boot Architecture

- Database Layer
- The actual database that stores application data.
- Spring Boot interacts with it through JPA/Spring Data.


## Request Flow in Spring Boot

- Client  Controller  Service  Repository  Database  Response
- A Client makes an HTTPS request (GET/POST/PUT/DELETE).
- The request is handled by the Controller, which is mapped to the corresponding route.
- If business logic is required, the Controller calls the Service Layer.
- The Service Layer processes the logic and interacts with the Repository Layer to retrieve or modify data in the Database.
- The data is mapped using JPA with the corresponding Model/Entity class.
- The response is sent back to the client. If using Spring MVC with JSP, a JSP page may be returned as the response if no errors occur.


## Spring Boot Project Structure

- Main application class
- Controller packages
- Resources and templates


## Spring Boot Sample

## A Step Back: What is a “Bean”?

- The word “bean” means different things in different contexts
- We must separate between:
  - JavaBean
  - Spring Bean
  - POJO


## POJO

- Plain Old Java Object
- A simple Java class
- No restrictions
- No framework dependencies


- Example:
- public class User {
- private String name;
- private int age;
- public User(String name, int age) {
- this.name = name;
- }
- }


## POJO

- Most Java classes should be POJOs, why?
  - Easy to understand
  - Easy to test
  - Framework-independent
  - Long-lived and reusable


## JavaBean

- It’s a POJO that follows strict conventions:
  - Public no-argument constructor
  - Private fields
  - Public getters and setters
  - Serializable (often expected)


## JavaBean

- Why JavaBeans existed?
- Introduce a standard, reusable software component
- Allow tools to
  - discover properties automatically
  - Bind data easily


- Example:
- public class UserBean implements Serializable {
- private String name;
- public UserBean() {  }
- public String getName() {
- return name;
- }
- public void setName(String name) {
- this.name = name;
- }
- }


## Spring Bean

- A Spring Bean is any object that is created, managed, and injected by the Spring
- Can be a POJO
- Can be a JavaBean
- Or neither
- What makes it a Spring Bean is who manages it, not its structure.


## Spring Bean

- A Spring Bean is an object whose lifecycle is managed by the Spring IoC container
- For each Spring Bean, the container:
- Creates it
- Injects dependencies
- Manages lifecycle
- Applies AOP (transactions, security)
- Destroys it when needed


## POJO vs JavaBean vs Spring Bean

- A POJO is a simple Java object
- A JavaBean is a POJO that follows specific conventions
- A Spring Bean is any object managed by the Spring container, regardless of its structure.

