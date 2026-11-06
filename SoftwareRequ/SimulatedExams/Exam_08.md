# Software Requirements Engineering: Advanced Examination Series
## Exam 08: Domain Modeling, Business Algorithms & Safety Constraints
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
Analyze the following requirement from an airline crew scheduling module:
> *"The scheduling system must ensure pilots get enough rest between flights according to FAA regulations and do not work too many hours."*
- **a) Defect Identification (2.5 Marks):** Detail why 'enough rest' and 'too many hours' represent incomplete and legally hazardous requirements.
- **b) Surgical Rewrite (2.5 Marks):** Rewrite this into a deterministic, verifiable requirement citing explicit statutory boundaries (e.g., minimum 10 consecutive hours of rest, maximum 8 flight-duty hours in a 24-hour rolling window).

#### Question 2 (5 Marks)
Analyze the following requirement from a commercial aircraft flight planning module:
> *"The flight planning engine shall calculate fuel consumption accurately based on weather, wind, and aircraft weight."*
- **a) Defect Identification (2.5 Marks):** Why is 'accurately' unverifiable without error tolerance margins? What domain calculation models are missing?
- **b) Surgical Rewrite (2.5 Marks):** Formulate a testable requirement specifying input data sources, domain fuel burn formulas, and acceptable calculation tolerance ($\pm 1.5\%$ of certified dispatch consumption).

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks, 5 Marks Each)
*Answer the following deep-dive theoretical prompts with structured, professional justifications.*

#### Question 3 (5 Marks)
The Anatomy of **Domain Requirements** (5 Marks):
- What are **Domain Requirements** and how do they differ fundamentally from User Requirements?
- Explain why Domain Requirements often reflect:
  1. Fundamental laws of physics or mathematics.
  2. Industry statutory standards (e.g., FAA, ICAO).
  3. Specialized technical jargon.
- Why do software engineers frequently struggle to understand and validate domain requirements? What role does a **Product Champion / Subject Matter Expert (SME)** play in bridging this gap?

#### Question 4 (5 Marks)
Requirements Modeling: **Data Flow Diagrams (DFDs) vs. State-Transition Diagrams (STDs)** (5 Marks):
- Compare DFDs and STDs in requirements analysis:
  - What is the primary modeling perspective of a DFD (processes, data stores, data flows)?
  - What is the primary modeling perspective of an STD (states, transitions, guard conditions, events)?
- Explain why a complex aircraft boarding and flight departure system cannot be modeled adequately with DFDs alone and requires an STD to capture chronological state dependencies.

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks, 5 Marks Each)
*Evaluate the operational scenarios below and justify your strategic elicitation choices.*

Elicitation in Highly Regulated, Mission-Critical Domains (10 Marks - 5 Marks each):
1. **Document Analysis of Regulatory Standards:** Commercial airlines operate under thousands of pages of FAA Federal Aviation Regulations (FARs). Explain why an analyst must perform rigorous **Document Analysis** to extract business rules before holding requirements workshops with chief pilots. What specific requirement traceability errors are prevented by citing regulation clause numbers?
2. **Interviews with Union Representatives vs. Operations Executives:** Airline pilots and flight attendants are represented by labor unions with strict collective bargaining agreements (CBAs). Contrast interviewing airline operations managers (who prioritize scheduling efficiency) with union representatives (who prioritize quality of life and rest rules). How does an analyst manage conflicting stakeholder inputs in a unionized environment?

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks, 5 Marks Each)
*Construct formal requirements engineering models according to the prompt instructions.*

Modeling Complex Aviation Workflows (10 Marks):
1. **Decision Tree Modeling for Flight Delay Triage (5 Marks):** Construct a formal **Decision Tree** for an automated flight delay decision engine:
   - Level 1 Decision Node: Weather severity at destination (Acceptable vs. Below Minimums).
   - Level 2 Decision Node: Aircraft maintenance status (No Faults vs. Minor MEL Deferred vs. Ground Halt).
   - Level 3 Decision Node: Crew duty hours remaining ($> 3$ hours vs. $\le 3$ hours).
   - Define the final dispatch actions: *Cleared for Departure*, *Delay 60 Mins for Re-Crew*, *Divert to Alternate Airport*, *Cancel Flight*. Explain why decision trees prevent missing logic paths in complex software.
2. **Ecosystem Map: Flight Operations Solution Space (5 Marks):** Draw a text-based Ecosystem Map for `AeroPlan Flight Dispatch Engine` showing its data links to: `National Weather Radar Feed`, `FAA Air Traffic Control Telemetry`, `Aircraft Weight & Balance Sensor Network`, `Passenger Ticketing System`, and `Crew Mobile Rostering App`.

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)
*Carefully read the enterprise engineering scenario and deliver the three technical tasks that follow.*

#### Scenario Context: TransGlobal Airways is developing an automated next-generation Flight Dispatch and Fuel Optimization Engine. 
The system must generate optimized flight paths for 800 daily flights, reducing jet fuel consumption while guaranteeing safety compliance. 
The engine must compute aircraft climb, cruise, and descent profiles accounting for high-altitude jetstream winds, aircraft takeoff weight, and airport runway gradients. 
During requirements review, software developers expressed confusion over physics equations relating thrust, drag coefficients, and fuel burn. 
You are tasked with engineering domain specifications and validation criteria.

#### Engineering Tasks & Deliverables:
- **Task 1: Specifying Physics-Based Domain Requirements (4 Marks):** Write a formal domain requirement incorporating the aircraft deceleration and landing rollout calculation, specifying physical inputs (runway friction coefficient, wind component, aircraft landing weight) and referencing certified aerodynamic tables.

- **Task 2: Non-Functional Safety & Redundancy Requirements (3 Marks):** Formulate two verifiable Non-Functional Product Requirements specifying computational latency (flight plan calculated in $\le 10$ seconds) and dual-server hot-standby redundancy ensuring zero lost dispatch records during server failover.

- **Task 3: Defining Validation Test Cases with Product Champions (3 Marks):** Explain how a Lead Business Analyst collaborates with a senior flight dispatcher (**Product Champion**) to design validation test cases that compare the engine's calculated fuel burn against historical black-box telemetry data from actual past flights.

