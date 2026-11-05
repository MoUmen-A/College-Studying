# CSE2001 - Software Engineering
## Simulated Exam 4: Comprehensive Final Exam (All Chapters)
**Course:** CSE2001  
**Time Allowed:** 3 Hours  
**Total Marks:** 50 Marks  

---

### Section A: Complete the Statements (10 Marks, 2 Marks Each)
*Fill in the missing terms in the statements below. Do not write full sentences, just provide the correct term or phrase.*

1. According to the SEI capability maturity approach, the maturity level where process management procedures and strategies are formally defined, documented, and utilized is called __________.
2. While functional requirements specify what the system services must do, non-functional requirements constrain the system or development process and often apply to the __________.
3. In software user testing, the stage where customers test a custom software system to decide whether it is ready to be accepted and deployed is called __________ testing.
4. Under security engineering terminology, a __________ represents an inherent weakness in a system that could potentially be exploited by an attacker to cause damage.
5. In a process-oriented real-time architecture, the process component that executes the decision-making logic and computes the system response is called the __________.

---

### Section B: Short Answer & Explanations (15 Marks, 5 Marks Each)
*Answer the following questions concisely. Ensure you cover all parts of the question.*

1. Contrast the **Spiral Model** and the **V-Model**. Explain how each model differs in its approach to managing risk, handling changing requirements, and planning testing activities.
2. In requirements engineering, explain why final requirements documents are often a compromise. Detail the three-step change management process used to handle requirement changes during development.
3. Security is considered a prerequisite for software dependability. Explain how an application security compromise directly affects the following four dependability properties: **Reliability, Availability, Safety,** and **Resilience**.

---

### Section C: Differences and Comparisons (10 Marks, 5 Marks Each)
*Provide clear, structured comparisons for the following concepts. Using tables is recommended.*

1. Differentiate between **Validation Testing** and **Defect Testing** in terms of:
   * The primary objective of each testing goal.
   * What a "successful test case" signifies in each context.
2. Differentiate between the three levels of system security: **Infrastructure security, Application security,** and **Operational security**. For each, define the focus area and identify which level is primarily a software engineering responsibility.

---

### Section D: Case Study and Scenario-Based Modeling (15 Marks)
*Read the scenario below and answer the tasks that follow.*

**Scenario:**  
A tech firm is developing a "SmartTemp" Connected Thermostat System. 
* **Homeowners** use a mobile app to log in, view current indoor temperatures, adjust the target temperature, and set heating/cooling schedules. 
* The **Thermostat Controller** (an embedded device in the house) periodically polls its physical temperature sensor, processes this data, and sends control signals to a heating/cooling **Actuator** to maintain the target temperature. It also sends status telemetry to a central database. 
* **System Administrators** log in to configure user profiles, register new thermostat devices, and generate monthly energy efficiency reports.
* A security analyst has flagged that an **Attacker** might attempt a Denial of Service (DoS) attack to disrupt system communication and turn off heating during winter, or attempt to read and intercept sensitive user profile information over the network. 

#### Tasks:
1. **Use Case Modeling (5 Marks):** Sketch out the Use Case Diagram for the "SmartTemp" system, showing the actors (Homeowners, Administrators, Thermostat Controller, Actuators) and their primary interactions.
2. **Security & Misuse Modeling (5 Marks):** Draw a Misuse Case Diagram showing how an Attacker threatens the system's standard operations and identify what security controls (e.g., CAPTCHA, SSL/TLS encryption, WAF/Rate Limiting) mitigate these threats.
3. **Behavioral Sequence Modeling (5 Marks):** Draw a Sequence Diagram illustrating the message sequence when a Homeowner adjusts the target temperature on the mobile app, showing the interaction between the Homeowner, Mobile App, Central Controller, and Database.
