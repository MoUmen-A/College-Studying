# Software Requirements Engineering: Advanced Examination Series
## Exam 05: Subsystem Allocation, Iterative Analysis & Verification Methods
**Course:** Software Requirements Engineering (CS / SE)  
**Curriculum Alignment:** Karl Wiegers & Joy Beatty (*Software Requirements* 3rd Ed.) & Ian Sommerville (*Software Engineering*)  
**Allowed Time:** 2 Hours | **Total Marks:** 50 Marks  
**Pedagogical Style:** Applied Problem-Solving, Surgical Defect Rewrites, Artifact Modeling & Case Engineering (Non-MCQ)  

---

> [!IMPORTANT]
> **Instructions to Candidates:**
> 1. This examination is designed to test **deep conceptual understanding, architectural reasoning, and professional specification skills**, not rote recall.
> 2. In **Section A**, you must explicitly identify the violated quality characteristics using formal engineering terminology and provide complete, testable rewrites.
> 3. In **Section D**, all models, vision statements, and tables must conform strictly to industry standards.
> 4. Ensure all formulated requirements in **Section E** are atomic, uniquely labeled, and verifiable with clear pass/fail criteria.

---

### Section A: Requirements Defect Analysis & Surgical Rewrite (10 Marks, 5 Marks Each)
*Analyze the flawed requirement statements below. For each prompt, diagnose all quality violations and provide an unambiguous, testable rewrite.*

#### Question 1 (5 Marks)
Analyze the following requirement for an autonomous mobile robot (AMR) navigation module:
> *"The robot shall detect obstacles in its path and stop safely before hitting anything."*
- **a) Defect Identification (2.5 Marks):** Why is 'stop safely before hitting anything' an incomplete, untestable specification? What physical and temporal parameters are missing?
- **b) Surgical Rewrite (2.5 Marks):** Rewrite this into a verifiable, deterministic safety requirement incorporating sensor range, maximum travel velocity, deceleration rates, and minimum safety stopping buffer distance.

#### Question 2 (5 Marks)
Analyze the following requirement from a warehouse fleet dispatch dashboard:
> *"The dashboard should update robot positions in real-time and provide alerts if robots experience low battery or breakdown."*
- **a) Defect Identification (2.5 Marks):** Identify why 'real-time' is ambiguous and evaluate the lack of atomic criteria for 'low battery' and 'breakdown'.
- **b) Surgical Rewrite (2.5 Marks):** Rewrite into two distinct requirements: one quantifying UI telemetry refresh latency and one defining explicit telemetry alert thresholds.

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks, 5 Marks Each)
*Answer the following deep-dive theoretical prompts with structured, professional justifications.*

#### Question 3 (5 Marks)
The Iterative Nature of **Requirements Development** (5 Marks):
- Many novice software engineers believe Requirements Engineering is a linear, one-pass waterfall phase (Elicit $ightarrow$ Analyze $ightarrow$ Specify $ightarrow$ Validate). 
- Explain why Requirements Development is fundamentally **iterative** and cyclic.
- Detail how the process of **visual modeling** during Analysis uncovers hidden gaps that force analysts back into Elicitation.
- Describe how writing test cases during Validation reveals specification defects that prompt re-analysis.

#### Question 4 (5 Marks)
Requirements Allocation: **Software vs. Hardware vs. Human Procedures** (5 Marks):
- What is **Subsystem Allocation** in complex systems engineering?
- Why is it disastrous to treat an entire multi-disciplinary product as pure software?
- Using a Smart Warehouse Access & Safety System, illustrate how a high-level safety requirement (*'Prevent unauthorized human entry into active robotic picking aisles'*) is apportioned among:
  1. Hardware components.
  2. Software algorithms.
  3. Human operational procedures.

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks, 5 Marks Each)
*Evaluate the operational scenarios below and justify your strategic elicitation choices.*

Selecting Elicitation Methods in Safety-Critical and IoT Environments (10 Marks - 5 Marks each):
1. **Prototyping vs. Mathematical Simulation:** Warehouse managers cannot visualize how 50 autonomous robots will navigate warehouse intersections without gridlock. Compare developing a **Throwaway Physical Prototype** versus building a **Computer Simulation Model**. Explain why simulation is superior for validating concurrency and throughput requirements before hardware procurement.
2. **Focus Groups vs. Contextual Job Observation for Warehouse Operators:** Warehouse picking staff are accustomed to manual clipboards and express fear that robotics will eliminate their jobs. Explain why conducting a standard Focus Group will likely yield defensive, unreliable feedback. Contrast this with **Contextual Inquiry / Observation** and explain how an analyst builds psychological safety to uncover true operational bottlenecks.

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks, 5 Marks Each)
*Construct formal requirements engineering models according to the prompt instructions.*

State Modeling and Boundary Specification for Robotics (10 Marks):
1. **State-Transition Diagram Specification (5 Marks):** Describe the operational states and transitions for an Autonomous Mobile Robot (AMR) using a textual state table:
   - States: `Idle / Charging`, `Dispatched / Navigating`, `Picking Payload`, `Obstacle Paused`, `Emergency E-Stop`.
   - Specify the stimuli/events that trigger transitions between these states (e.g., *Dispatch Command Received*, *Proximity Sensor Breach*, *Obstacle Cleared*, *Manual E-Stop Pressed*).
   - Explain why state models are indispensable for verifying system completeness and preventing unhandled operational deadlocks.
2. **Context Diagram for Warehouse Management Gateway (5 Marks):** Define the scope boundary for the Central Fleet Controller by detailing:
   - Central System: `Fleet Management Server`.
   - Four External Terminators: `Autonomous Robot Fleet`, `Warehouse Management System (WMS)`, `Human Floor Supervisor Console`, and `Automated Fire Alarm Network`.
   - Data flows connecting each terminator to the server.

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)
*Carefully read the enterprise engineering scenario and deliver the three technical tasks that follow.*

#### Scenario Context: RoboLogistics Inc. is engineering a turnkey robotic automated fulfillment warehouse for a major retailer. 
The facility houses 100 autonomous picking robots navigating a 500,000 sq ft grid alongside 200 human warehouse workers. 
The system must fulfill 5,000 customer orders per hour. 
During requirements verification, the safety audit board found that requirements for handling Wi-Fi network dropouts were completely missing from the SRS, creating severe physical collision risks if robots lose central communications. 
You are tasked with engineering safety requirements and system specifications.

#### Engineering Tasks & Deliverables:
- **Task 1: Specifying Fail-Safe Behavioral Requirements (4 Marks):** Formulate two verifiable functional safety requirements specifying the autonomous behavior of an individual robot when central Wi-Fi communication is lost for more than 500 milliseconds. Address stopping distance, audio/visual beacons, and collision avoidance.

- **Task 2: Non-Functional Availability & Reliability Metrics (3 Marks):** Author two quantifiable Non-Functional Product Requirements specifying fleet uptime availability ($\ge 99.9\%$) and Mean Time Between Failures (MTBF) for robot hardware components.

- **Task 3: Requirements Traceability for Safety Certification (3 Marks):** Design an excerpt of a **Requirements Traceability Matrix (RTM)** demonstrating how the high-level business requirement *'Zero Human Injuries'* traces forward into a specific functional safety requirement, an allocated hardware safety sensor, and a formal safety acceptance test case.

