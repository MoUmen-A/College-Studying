# CSE2001 - Software Engineering
## Simulated Exam 3: Real-time Software Engineering & Processes/Requirements
**Course:** CSE2001  
**Time Allowed:** 2 Hours  
**Total Marks:** 50 Marks  

---

### Section A: Complete the Statements (10 Marks, 2 Marks Each)
*Fill in the missing terms in the statements below. Do not write full sentences, just provide the correct term or phrase.*

1. A real-time system is a software system where correct functioning depends not only on the results produced, but also on the __________ at which those results are produced.
2. In a __________ real-time system, operation is degraded if results are not produced according to timing requirements, but the system does not fail completely.
3. Stimuli that occur at predictable, regular time intervals (such as polling a temperature sensor every 50ms) are called __________ stimuli.
4. In a general real-time software architecture, the processes responsible for gathering data from hardware inputs and buffering it are called __________ processes.
5. The real-time design process activity that involves calculating and analyzing timing constraints, deadlines, and execution frequencies is called __________.

---

### Section B: Short Answer & Explanations (15 Marks, 5 Marks Each)
*Answer the following questions concisely. Ensure you cover all parts of the question.*

1. Explain why a simple sequential programming loop (e.g., a single loop polling all inputs in sequence) is usually not sufficient for a complex real-time system. Describe the process-based architecture that is used instead.
2. List five (5) distinct characteristics of embedded real-time systems that differentiate them from ordinary desktop applications.
3. Explain the difference between "functional requirements" and "domain requirements". Provide one (1) example of a domain requirement for an embedded software system controlling a passenger train's braking mechanism.

---

### Section C: Differences and Comparisons (10 Marks, 5 Marks Each)
*Provide clear, structured comparisons for the following concepts. Using tables is recommended.*

1. Differentiate between "Periodic stimuli" and "Aperiodic stimuli" across three (3) points of comparison: predictability of arrival, typical hardware trigger mechanism, and a concrete example for each.
2. Differentiate between "Hard real-time systems" and "Soft real-time systems" by comparing:
   * The definition of correctness in each system.
   * The direct consequence of missing a single timing deadline.
   * A practical example of each type of system.

---

### Section D: Case Study and Scenario-Based Modeling (15 Marks)
*Read the scenario below and answer the tasks that follow.*

**Scenario:**  
A home security company is designing an embedded alarm system called "SecureHome". The system consists of motion sensors, window contact sensors, a siren actuator, and a keypad controller. 
* When the system is initialized, it is in an `Idle` state. 
* When the user enters the arming code on the keypad, the system transitions to the `Armed` state. 
* If any sensor detects movement or a window opening while armed, the system enters a `Delay` state, starting a 30-second countdown timer. 
* If the user enters a valid PIN on the keypad during this 30-second delay, the system transitions back to the `Idle` state. 
* If the 30-second timer expires before a valid PIN is entered, the system enters the `Siren Active` state, sounding the siren.
* At any time, if the user presses the red "Emergency" panic button on the keypad, the system immediately enters the `Siren Active` state. 
* From the `Siren Active` state, entering the administrator PIN transitions the system back to `Idle`.

#### Tasks:
1. **State Machine Modeling (7 Marks):** Draw a UML State Diagram describing the states, transitions, actions, and trigger events for the "SecureHome" system.
2. **Real-time Classification (4 Marks):** Classify the "SecureHome" system as either hard real-time or soft real-time. Provide a clear justification for your classification based on the consequences of timing failures.
3. **Stimuli Identification (4 Marks):** Identify and describe one (1) periodic stimulus and one (1) aperiodic stimulus that this security system must handle, explaining how they map to the physical hardware inputs.
