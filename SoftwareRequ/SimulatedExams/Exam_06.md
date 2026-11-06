# Software Requirements Engineering: Advanced Examination Series
## Exam 06: Event-Driven Modeling, Requirements Metadata & Change Control
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
Analyze the following requirement from a 911 emergency dispatch system:
> *"When a 911 call is received, the CAD system must dispatch emergency services immediately to the caller's location."*
- **a) Defect Identification (2.5 Marks):** Identify why 'dispatch immediately' is an impossible requirement. What crucial intermediate steps (caller triage, address verification, unit availability check) are omitted, violating *Completeness*?
- **b) Surgical Rewrite (2.5 Marks):** Rewrite into a sequence of atomic, verifiable requirements establishing maximum allowable system latency between call classification and first responder mobile notification.

#### Question 2 (5 Marks)
Analyze the following requirement from a police mobile mapping unit:
> *"The mobile map should display incidents clearly and update frequently without draining the vehicle battery."*
- **a) Defect Identification (2.5 Marks):** Critique 'clearly', 'frequently', and 'without draining the battery'. Why can a QA engineer not write automated tests against this statement?
- **b) Surgical Rewrite (2.5 Marks):** Formulate measurable criteria: specify map rendering resolution, GPS coordinate update frequency (in Hz/seconds), and maximum allowed DC power consumption (in Watts).

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks, 5 Marks Each)
*Answer the following deep-dive theoretical prompts with structured, professional justifications.*

#### Question 3 (5 Marks)
Requirements Metadata: **Uniquely Labeling Requirements & Tracking Attributes** (5 Marks):
- Why do IEEE and ISO requirements engineering standards strictly forbid unnumbered or bullet-point requirements in an SRS?
- What properties must a **Requirement Identifier** possess to withstand deletions, insertions, and reorganizations over a multi-year project?
- Beyond the unique ID and description text, identify and explain five (5) critical **Requirement Attributes (Metadata)** that must be maintained in a modern requirements management tool (e.g., Origin, Priority, Status, Author, Release Number).

#### Question 4 (5 Marks)
Event-Driven Systems Engineering: **User vs. Temporal vs. Signal Events** (5 Marks):
- In requirements analysis, an Event List establishes the system boundary by defining external triggers.
- Define and contrast the three fundamental classes of events:
  1. **User / Business Events**
  2. **Temporal Events**
  3. **Signal / Hardware Events**
- Provide a concrete, real-world emergency dispatch example for each of the three event types and describe the system's corresponding response.

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks, 5 Marks Each)
*Evaluate the operational scenarios below and justify your strategic elicitation choices.*

Elicitation under High-Stress and Life-Critical Constraints (10 Marks - 5 Marks each):
1. **Job Shadowing in Emergency Call Centers:** Emergency 911 operators work under intense psychological pressure. Explain why stopping an operator during a live emergency call to ask elicitation questions violates professional ethics and yields invalid data. Detail how a Business Analyst uses **Silent Audio/Screen Recording combined with Post-Shift Retrospective Inquiries** to elicit operator workflows safely and accurately.
2. **Requirements Workshops for Inter-Agency Emergency Services:** Dispatching a major structure fire requires simultaneous coordination between Police, Fire, Paramedics, and City Water utilities. Explain why holding separate departmental elicitation interviews produces territorial conflicts. Outline a facilitation strategy for a joint inter-agency workshop to establish unified incident command protocols.

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks, 5 Marks Each)
*Construct formal requirements engineering models according to the prompt instructions.*

Modeling Real-Time Emergency Telemetry (10 Marks):
1. **Event List Construction (5 Marks):** Author a comprehensive Event List for the Computer-Aided Dispatch (CAD) containing exactly six (6) distinct events: two User Events, two Temporal Events, and two Signal Events. For each event, document: Event Name, Trigger Mechanism, Source Entity, and Expected System Output.
2. **Change Control Process Workflow (5 Marks):** Construct a flowchart or sequential step-by-step description of a formal **Requirements Change Control Process**:
   - Step 1: Change Request Submission
   - Step 2: Impact Analysis (Technical, Schedule, Cost, Quality)
   - Step 3: Change Control Board (CCB) Review & Decision
   - Step 4: Baseline Update & Configuration Versioning
   - Step 5: Stakeholder Notification & Traceability Update
   Explain why emergency projects fail when changes are agreed upon informally without CCB governance.

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)
*Carefully read the enterprise engineering scenario and deliver the three technical tasks that follow.*

#### Scenario Context: Metropolis City is replacing its legacy dispatch platform with a next-generation CAD system. 
The system must support 100 concurrent 911 call takers, integrate with national cellular automated location data (e911 Phase II GPS), and dispatch Police, Fire, and EMS units across 15 jurisdictions. 
Public safety regulations dictate that system downtime cannot exceed 5 minutes per year (99.999% availability). 
During requirements inspection, analysts discovered that response time definitions differed between Police chiefs (who measure from call arrival to officer on scene) and IT developers (who measure database query latency). 
You are tasked with establishing unambiguous requirements.

#### Engineering Tasks & Deliverables:
- **Task 1: Disambiguating Performance Metrics (4 Marks):** Resolve the conflicting definitions of 'response time' by authoring two distinct, verifiable requirements: one specifying IT system processing and dispatch queuing latency ($\le 2$ seconds) and one specifying automated field unit notification broadcast.

- **Task 2: Specifying 'Five Nines' Availability (3 Marks):** Write a rigorous Non-Functional Product Requirement detailing the 99.999% availability metric, including hardware redundancy, database clustering, and automatic failover within 3 seconds of server hardware failure.

- **Task 3: External Interface Specification (3 Marks):** Detail the external interface requirements between the CAD system and the National Crime Information Center (NCIC) database, specifying query protocol, encrypted payload formatting, and automated retry logic upon connection timeouts.

