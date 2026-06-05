# CCS2304 – Advanced Programming Applications

## CCS2304 – Advanced Programming Applications

- Lecture 9


- 0


## Task Web Application

- Recall last lecture’s project?
- We learned that beans with @Service annotation are created and managed by Spring
- Spring creates only one bean of @Service class and shares it throughout the application
- Consequently, only one Task ArrayList gets created and shared amongst all users


- 1


## Task Web Application

- if a user created a task, another user (browser) could see that created task
- Current issues:
  - Data leakage between users
  - Not realistic for real applications
  - Security issue
- How can we fix it?


- 2


## Sessions

- We need a way to store data per user
- Answer: use Sessions
- What is a session?
  - In layman’s terms: a session is a way for a website to remember you while you are using it
  - Formally: a session is a private storage space on the server for each user


- 3


## Sessions

- Session properties:
  - Allows the server to remember data for each user
  - One session is created per browser (user)
  - Stored on the server
  - Identified by a session ID
- In short:
  - User A → Session A → Tasks A
  - User B → Session B → Tasks B


- 4


## Rewriting Task Application

- Previous Service						Updated Service














- 5


## Rewriting Task Application

- 6


- TASKS_KEY string variable is the label for tasks in the session to differentiate it from other variables saved in the session
- @suppressWarnings(“unchecked”) annotation is used to tell the compiler, "I know what I'm doing, please stop complaining about type safety here."
- Session. getAttribute(TASKS_KEY) returns the list using the string label
- Session.setAttribute(TASKS_KEY,tasks) set the variable with the label TASKS_KEY and the value is the object tasks (Arraylist)


## Why use @suppressWarning

- The Session Retrieval: session.getAttribute(TASKS_KEY) returns a generic Object.
- The Problem: Java doesn't know for sure if that Object is a List<Task>. It could be a String, an integer, or a list of objects.
- The Cast: When the code does (List<Task>), it’s telling the compiler: "Trust me, I know I put a List of Tasks in here earlier."
- The Warning: Because of "Type Erasure" in Java, the compiler can't verify the contents of the list at runtime, so it throws a warning. The @SuppressWarnings("unchecked") is used here to silence that warning.


- 7


## Rewriting Task Application

- Previous Controller


- 8


## Rewriting Task Application

- Updated Controller






- 9


## Updated Task Application

- In the updated task application, we utilized sessions manually
  - we used HttpSession object
  - we manually added the list to the session
  - we were able to create a separate list for each user
- Spring can also manage this using scopes


- 10


## Bean Scopes in SpringBoot

- Recall.. What is a SpringBean?
  - an object created and controlled by Spring
  - used across controllers, services, …etc.
- How long does this object live??


- 11


## Bean Scope

- The scope of a bean is its lifecycle and visibility
- Think of a Scope as the "Lifetime and Sharing Rules" for an object
- In plain English: A scope answers the question: "How many of these objects should I create, and who is allowed to share them?“
- Scope answers the questions:
  - when is the bean created?
  - how long does it live?
  - who can access it?
- Main scopes in Spring
  - Singleton (default)
  - Request
  - Session
- Let’s first take a step back and review what happens in springboot startup


- 12


## Understanding Main Scopes

- Let’s take a metaphorical example about running a hotel:
- Singleton Scope (The Front Desk): There is only one front desk for the whole hotel. Every guest who walks in talks to the exact same desk. It stays there from the moment the hotel opens until it closes.
- Session Scope (The Guest's Room): Each guest gets their own room. As long as they are "checked in" (their session), that room belongs to them. Other guests can't see what's inside it.
- Request Scope (The Room Service Order): When a guest calls for a coffee, that "order" object is created. Once the coffee is delivered and the guest is happy, the order is thrown away. It only exists for that one specific interaction.


- 13


## Why do we need it?

- To Save Memory (Singleton): Most of your code (like a Service that calculates taxes) doesn't hold data; it just performs actions. You don't need 1,000 copies of a "TaxCalculator." One copy is enough for the whole app to share.
- To Keep Data Private (Session/Request): You don't want User A's "Shopping Cart" to show up in User B's browser. Scopes tell Spring: "Give this object to User A and a different one to User B."


- 14


## When to use Singleton?

- Use Singleton (Default - You do nothing)
- 90% of the time.
- Use for: Database connections, Services, Controllers, and Mappers.
- Rule: If the class just contains logic and no "user-specific" data, leave it as a Singleton.


- 15


## Bean Scope – Singleton

- Only ONE instance of the bean is created and shared across the entire application


- Open browser: /count
- Refresh multiple times
- Output:
- Count: 1Count: 2Count: 3
- Same object is reused
- State is shared across all users
- What happens if multiple users access this?
  - Counter will continue Count: 4 for new user


- 16


## When to use Session ?

- Use for: "Who is logged in?", "What is in their cart?", "What is their preferred language?"
- Rule: If the data needs to follow the user from page to page, use Session.


- 17


## Bean Scope – Session

- One object per user session shared across multiple requests of same user


- Open browser: /count and open another browser / incognito window, then refresh multiple times
- Output:
- User 1: Count 1  Count 2  Count 3User 2: Count 1  Count 2  Count 3
- A new object is created for each user


- An issue happens when a singleton bean (e.g., controller) injects a session scoped bean
  - Singleton is created once at startup, request doesn’t exist yet
- Spring uses a placeholder object to handle different instances automatically.
  - The placeholder object is called a proxy
- Spring injects a proxy object into the controller
  - The proxy looks like CounterService
  - Spring fetches the real instance per request


- 18


## Springboot startup

- Let’s take an online shopping website as an example:
- Component Scanning: Spring looks for @Service, @Controller, and @Component.
- Bean Definition: Spring creates a map of all your beans and their Scopes.
- Dependency Injection (The Crash Point): Spring tries to "wire" them together.
  - The Conflict: It sees your Controller needs a shopping Cart (Session).
  - The Logic: Spring says, "I'm starting the app now, but there is no user logged in! I can't create a 'Session' yet."
- The Proxy Solution: Instead of failing, Spring creates a Proxy class (a "fake" version of your bean) and plugs that into the Controller.
- Context Ready: The app is now running, but the Controller is holding a bunch of "empty shells" (Proxies).


- 19


## Springboot runtime

- The Request Hits: A user sends an HTTP request.
- The Controller Call: The Controller calls a method on the Cart.
- The Proxy Interception: The call doesn't go to a real object; it hits the Proxy first.
- The Dynamic Lookup: The Proxy looks at the current thread and says: "Aha! This is User #42. Let me find their specific Session bean."
- Delegation: The Proxy forwards the call to the real instance.


- 20


## When to use Request

- Use for: Tracking a specific error that happened during a single button click, or logging how long one specific page took to load.
- Rule: If the data is only useful for the 0.5 seconds it takes to load a page, use Request.


- 21


## Bean Scope – Request

- New object created for each HTTP request and destroyed after response


- Open browser: /count and refresh multiple times
- Output:
- Count: 1Count: 1Count: 1
- A new object is created for each request


- Same issue happens when a singleton bean (e.g., controller) injects a request scoped bean
  - Singleton is created once at startup, request doesn’t exist yet
- Spring injects a proxy object into the controller
  - The proxy looks like CounterService
  - Spring fetches the real instance per request


- 22


## Why do we do this?

- If we didn't have Session Scope, we would have to do what you saw in your first code snippet: manually grabbing things from HttpSession.
- Spring Scopes allow you to write "clean" Java code without constantly digging into the underlying web session objects.


- 23


## Exercise

- Which scope to use for each of the following?
- A service contains business logic with no user-specific data
  - Singleton
- A controller processes a form submission that acts as a simple calculator
  - Request
- A website’s shopping cart
  - Session
- A user fills a multi-step form and data must persist between steps
  - Session
- A validation object is created only to validate input in one request and then discarded
  - Request
- A global counter that keeps track of total number of visitors to the website
  - Singleton


- 24

