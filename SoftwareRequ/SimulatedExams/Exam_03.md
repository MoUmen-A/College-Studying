# Software Requirements Engineering: Advanced Examination Series
## Exam 03: Requirements Management, Traceability & Non-Functional Taxonomy
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
Analyze the following requirement from a university library database system (LIBSYS):
> *"The search engine shall retrieve documents almost instantaneously and provide intuitive navigation."*
- **a) Defect Identification (2.5 Marks):** Detail why 'almost instantaneously' and 'intuitive navigation' destroy requirement testability. What metric should replace them?
- **b) Surgical Rewrite (2.5 Marks):** Rewrite this into two verifiable requirements: one specifying search query latency under 95th percentile server load, and one specifying UI navigational click depth.

#### Question 2 (5 Marks)
Analyze the following requirement from a student course registration module:
> *"Students can register for courses, pay tuition, drop classes during add/drop week, and the system should also prevent registration if prerequisites are missing."*
- **a) Defect Identification (2.5 Marks):** Explain why bundling multiple disparate actions violates *Atomicity* and impedes *Requirements Traceability*.
- **b) Surgical Rewrite (2.5 Marks):** Deconstruct this into atomic, uniquely labeled functional requirements with prerequisite business rule validation.

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks, 5 Marks Each)
*Answer the following deep-dive theoretical prompts with structured, professional justifications.*

#### Question 3 (5 Marks)
Evaluate the Three-Tier **Non-Functional Requirements (NFR) Classification** (5 Marks):
- Explain the classification established by Ian Sommerville:
  1. **Product Requirements**
  2. **Organizational Requirements**
  3. **External Requirements**
- Classify each of the following real-world requirements into one of the three categories and justify your classification:
  - Requirement A: *"All delivered source code and technical manuals must strictly conform to XYZCo-SP-STAN-95."*
  - Requirement B: *"The system shall maintain 99.95% uptime during final exam week."*
  - Requirement C: *"The system shall comply with GDPR Article 17 regarding the student's Right to be Forgotten."*

#### Question 4 (5 Marks)
The Role of **Requirements Traceability** in Systems Engineering (5 Marks):
- Define what a **Requirements Traceability Matrix (RTM)** is.
- Distinguish between **Forward Traceability** (from requirements to code/test cases) and **Backward Traceability** (from requirements back to stakeholder origins and business objectives).
- Explain how an RTM prevents 'Gold Plating' (developers adding unauthorized features) and facilitates **Change Impact Analysis** when a requirement is modified.

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks, 5 Marks Each)
*Evaluate the operational scenarios below and justify your strategic elicitation choices.*

Compare Elicitation Frameworks under Resource and Time Constraints (10 Marks - 5 Marks each):
1. **Brainstorming vs. Focus Groups:** An EdTech startup wants to design an innovative AI tutoring feature for high school students. Contrast conducting a **Brainstorming Session** with internal software developers and teachers versus hosting a **Focus Group** with high school students. Explain how moderator behavior must differ between the two techniques to avoid suppressing ideas.
2. **Requirements Workshops vs. One-on-One Interviews:** A university plans to merge the legacy databases of the Registrar, Financial Aid, and Housing departments. Explain why holding isolated one-on-one interviews with each department head will result in contradictory requirements. Detail how a 2-day cross-functional **Requirements Workshop** resolves these cross-boundary dependencies.

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks, 5 Marks Each)
*Construct formal requirements engineering models according to the prompt instructions.*

Engineering Scope Models for the University Digital Library (LIBSYS) (10 Marks):
1. **Context Diagram Design (5 Marks):** Model the scope boundary of LIBSYS by specifying:
   - The central system process.
   - Four (4) distinct external entities (terminators), including human actors, external database systems, and hardware devices.
   - For each entity, specify the input and output data/control flows crossing the system boundary.
2. **Domain Requirement Specification (5 Marks):** In LIBSYS, digital copyright law mandates that certain licensed research journals cannot be stored permanently on client machines. Formulate a formal **Domain Requirement** specifying the technical constraints (e.g., automatic delete-on-print, ephemeral memory viewing) and explain why domain requirements are often difficult for generalist software engineers to understand.

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)
*Carefully read the enterprise engineering scenario and deliver the three technical tasks that follow.*

#### Scenario Context: Apex University is replacing its 20-year-old student information system with 'EduPortal.' 
During peak registration on the first day of the semester, 25,000 students attempt to log in simultaneously within a 10-minute window, causing server crashes in the legacy system. 
Furthermore, academic deans complain that students bypass course prerequisites due to batch processing delays in transcript updates. 
The university board mandates that EduPortal must integrate with legacy state financial aid databases while supporting modern mobile responsive design.

#### Engineering Tasks & Deliverables:
- **Task 1: Non-Functional Performance & Scalability Modeling (4 Marks):** Formulate two verifiable, quantifiable Non-Functional Product Requirements that specify concurrency capacity, maximum transaction response time, and failover behavior during the 25,000-student registration spike.

- **Task 2: Business Rule Separation (3 Marks):** The rule determining prerequisite eligibility involves checking minimum passing grades, major standing, and prerequisite waivers signed by department heads. Document this as an enterprise **Business Rule** separate from the registration user story, and explain the architectural benefit.

- **Task 3: Subsystem Requirements Allocation (3 Marks):** Allocate system responsibilities for online course registration across: (a) Software Application Subsystem, (b) Database/Hardware Infrastructure, and (c) Human Procedural Subsystem (Registrar staff).

