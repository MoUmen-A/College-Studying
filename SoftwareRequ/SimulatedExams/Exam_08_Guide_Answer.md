# Software Requirements Engineering: Comprehensive Guide Answer & Marking Scheme
## Detailed Model Solutions for Exam 08
**Course:** Software Requirements Engineering (CS / SE)  
**Corresponding Exam Paper:** [Exam_08.md](file:///d:/Gam3a/Exam-Creation/SoftwareRequ/SimulatedExams/Exam_08.md)  
**Total Marks:** 50 Marks | **Passing Standard:** 70% | **Full Marks Goal:** 50/50  

---

### Section A: Requirements Defect Analysis & Surgical Rewrite (10 Marks)

#### Solution to Question 1 (5 Marks)
*Grading Scheme: [2.5 Marks] for identifying specific quality characteristic violations; [2.5 Marks] for providing a rigorous, testable, atomic rewrite.*

- **Defect Identification (2.5 Marks):**
  1. *Ambiguity & Lack of Quantification:* Words like 'instantly', 'safely', 'accurately', or 'intuitive' have no measurable engineering definition.
  2. *Untestability:* QA test engineers cannot author deterministic pass/fail tests against qualitative adjectives.
  3. *Incompleteness:* Omits operational prerequisites, server load conditions, and deterministic exception handling.
- **Surgical Rewrite (2.5 Marks):**
  - Formulate atomic requirements using the RFC 2119 keyword **SHALL**.
  - Specify quantitative thresholds: response time $\le 1.5$ seconds under 95th percentile load, explicit user inputs, and deterministic UI feedback states.

---

#### Solution to Question 2 (5 Marks)
*Grading Scheme: [2.5 Marks] for diagnosing defects; [2.5 Marks] for providing decomposed, verifiable requirements.*

- **Defect Identification (2.5 Marks):**
  1. *Violation of Atomicity:* Merging multiple unrelated functions into a single compound statement prevents independent verification.
  2. *Impeded Traceability:* Makes it impossible to trace individual capabilities back to specific user stories or forward to test cases.
  3. *Unhandled Boundary Conditions:* Vague conditional clauses ('unless the system is busy') omit concrete system fallback behaviors.
- **Surgical Rewrite (2.5 Marks):**
  - Decompose the compound statement into discrete, uniquely labeled functional specifications (`FR-01`, `FR-02`), each specifying a single operational action with clear inputs and failure recovery modes.

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks)

#### Solution to Question 3 (5 Marks)
*Grading Scheme: [2.5 Marks] for precise theoretical definitions; [2.5 Marks] for applied demonstrations and governance analysis.*

- **Core Theoretical Contrast (2.5 Marks):**
  - Differentiate the concepts using formal engineering standards (e.g., Boehm's duality: Validation confirms customer utility; Verification confirms specification rigor).
  - Explain why an artifact can be technically flawless in verification while completely missing the business objective in validation.
- **Operational Application & Governance (2.5 Marks):**
  - Detail the specific inspection techniques (peer reviews, inspections, static analysis, traceability matrices) used by QA and Systems Analysts to verify requirements against standard templates.
  - Explain the stakeholder sign-off protocols required for formal validation.

---

#### Solution to Question 4 (5 Marks)
*Grading Scheme: [2.5 Marks] for core concepts and taxonomy; [2.5 Marks] for applied illustrations and enterprise asset management.*

- **Theoretical Architecture & Taxonomy (2.5 Marks):**
  - Clearly delineate the boundaries between functional capabilities, quality attributes (NFRs), and operational/business constraints.
  - Explain how non-functional constraints (e.g., security, performance, regulatory compliance) directly influence the software architecture.
- **Enterprise Asset Management (2.5 Marks):**
  - Detail why business rules, mathematical formulas, and legal statutes must be managed as enterprise-level assets independent of individual project life cycles, ensuring long-term institutional consistency.

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks)

#### Solutions to Elicitation Scenarios (5 Marks Each)
*Grading Scheme: [2.5 Marks] for comparative technical justification; [2.5 Marks] for risk analysis and operational mitigation strategies.*

- **Scenario 1 Strategy (5 Marks):**
  - Contrast the candidate elicitation techniques based on domain constraints, stakeholder availability, and operational risks.
  - Justify why passive observation or structured prototyping excels when stakeholders have difficulty articulating unconscious operational habits.
  - Detail concrete risk mitigations (e.g., preventing the Hawthorne Effect, managing prototype scope creep).
- **Scenario 2 Strategy (5 Marks):**
  - Contrast collaborative elicitation (Workshops, Brainstorming) against broadcast elicitation (Surveys, Document Analysis).
  - Explain why conflicting political priorities between departmental heads require face-to-face facilitation with neutral moderation.
  - List the mandatory procedural prerequisites for successful session execution.

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks)

#### Solutions to Modeling Prompts (5 Marks Each)
*Grading Scheme: [3 Marks] for structural correctness and clause completeness; [2 Marks] for technical precision and domain relevance.*

- **Artifact 1 Construction (5 Marks):**
  - Author the requested model (Vision Statement, Context Diagram, Decision Table, State Diagram, or Data Dictionary) conforming strictly to formal requirements engineering standards.
  - Ensure all clauses, entities, data flows, and state transitions are explicitly labeled with zero colloquial language.
- **Artifact 2 Construction (5 Marks):**
  - Model the technical scope boundary by cleanly separating the internal system from external terminators.
  - Accurately categorize stimuli (User vs. Temporal vs. Signal Events) or map requirements across subsystem boundaries (Software, Hardware, Human).

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)

#### Model Solutions & Evaluation Rubric:
*Grading Scheme: Task 1 [4 Marks], Task 2 [3 Marks], Task 3 [3 Marks].*

- **Task 1: Functional / Safety Specification (4 Marks):**
  - Formulate two atomic, unambiguous requirements with unique persistent labels (`FR-01`, `FR-02`).
  - Specify concrete inputs, operational stimuli, exact response actions, and deterministic failure recovery paths.
- **Task 2: Non-Functional Quality Metrics (3 Marks):**
  - Specify two verifiable Non-Functional Product Requirements with quantifiable metrics (e.g., 99.9% availability, latency percentiles, MTBF, cryptographic standards).
- **Task 3: Architecture Allocation & Traceability (3 Marks):**
  - Apportion responsibilities across software, hardware, and human procedures, or establish bidirectional traceability linking business objectives to validation test cases.

---

> [!TIP]
> **Full Marks Key:** Always write requirements using the RFC 2119 / IEEE standard keyword **SHALL** for mandatory requirements, provide quantifiable operational numbers (seconds, MB, percentages), and explicitly state what the system must do when an error or network drop occurs.
