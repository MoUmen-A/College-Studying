# Software Requirements Engineering: Advanced Examination Series
## Exam 01: Foundations of Elicitation, Scope Modeling & SRS Quality
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
Analyze the following requirement from a laboratory inventory management system:
> *"The system should manage all chemical requests quickly and be sufficiently user-friendly so lab technicians do not get confused."*
- **a) Defect Identification (2.5 Marks):** Identify at least three (3) distinct violations of the 9 Quality Characteristics of requirements (cite specific terms like ambiguity, untestability, imprecision).
- **b) Surgical Rewrite (2.5 Marks):** Rewrite this requirement into two (2) separate, atomic, verifiable statements (one functional requirement and one non-functional performance requirement) that satisfy IEEE/ISO standards.

#### Question 2 (5 Marks)
Analyze the following requirement from an e-commerce order processing module:
> *"The checkout module shall calculate state and local sales taxes, discount promo codes, and automatically email receipts, or display an error message if the server is down, unless the user chose guest checkout."*
- **a) Defect Identification (2.5 Marks):** Identify why this statement violates the principles of *Atomicity*, *Completeness*, and *Modifiability*.
- **b) Surgical Rewrite (2.5 Marks):** Decompose and rewrite this compound statement into distinct, properly labeled functional requirements with explicit boundary conditions.

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks, 5 Marks Each)
*Answer the following deep-dive theoretical prompts with structured, professional justifications.*

#### Question 3 (5 Marks)
Contrast **Requirements Validation** with **Requirements Verification** (5 Marks):
- Define both concepts using the classic Boehm distinction (*'building the right product'* vs. *'building the product right'*).
- Provide a concrete real-world scenario where a Software Requirements Specification (SRS) successfully passes all **Verification** checks but utterly **fails Validation** upon release.
- Explain which stakeholders must lead each activity and why.

#### Question 4 (5 Marks)
Analyze the relationship between **Business Problems**, **Business Objectives**, and **Success Metrics** (5 Marks):
- Differentiate these three concepts in terms of timing, purpose, and measurability.
- Using the Chemical Tracking System (CTS) case study:
  - State the core Business Problem.
  - State the corresponding Business Objective.
  - Formulate a precise, quantifiable Success Metric tracked during testing or post-release.

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks, 5 Marks Each)
*Evaluate the operational scenarios below and justify your strategic elicitation choices.*

You are appointed Lead Business Analyst for modernizing an enterprise logistics platform. Evaluate the following elicitation scenarios (10 Marks - 5 Marks each):
1. **Scenario 1 (Observation vs. Interviews):** Warehouse forklift drivers follow complex, undocumented manual staging workflows. When interviewed in conference rooms, they omit crucial steps. Justify why **Job Shadowing / Passive Observation** is superior to interviews for capturing tacit knowledge. Identify two major risks of observation (including the Hawthorne Effect) and how to mitigate them.
2. **Scenario 2 (Facilitated Workshops vs. Surveys):** The executive committee wants to freeze project scope within two weeks, but three department heads (Procurement, Operations, and Finance) hold fiercely conflicting priorities. Compare **Facilitated Requirements Workshops** against **Questionnaires/Surveys**. Explain why a workshop is the only viable path to achieve consensus, and detail three mandatory preparation steps to prevent the workshop from derailing.

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks, 5 Marks Each)
*Construct formal requirements engineering models according to the prompt instructions.*

Construct the following foundational requirements artifacts based on the Chemical Tracking System (CTS) (10 Marks):
1. **Vision Statement Construction (5 Marks):** Draft a formal 6-clause Vision Statement conforming strictly to the industry standard template:
   - *For* [target user]
   - *Who* [statement of need/opportunity]
   - *The* [product name] *is a* [product category]
   - *That* [key capability / compelling benefit]
   - *Unlike* [existing manual/competitive alternative]
   - *Our product* [statement of primary differentiation & compliance advantage]
2. **Event List Classification (5 Marks):** Categorize each of the following system stimuli as either a **User/Business Event**, a **Temporal Event**, or a **Signal Event**, and explain the operational difference:
   - Event A: *"Chemist submits an emergency requisition for sulfuric acid."*
   - Event B: *"The system clock reaches 00:00 on the last day of the fiscal quarter, triggering EPA compliance report generation."*
   - Event C: *"An IoT barcode scanner transmits a 128-bit RFID container tag to the warehouse gateway."*
   - Event D: *"A hazardous temperature threshold sensor in the chemical vault breaches 45°C."*
   - Event E: *"A research scientist requests an audit log of personal chemical exposure history."*

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)
*Carefully read the enterprise engineering scenario and deliver the three technical tasks that follow.*

#### Scenario Context: BioChem Global operates 40 research laboratories across two campuses. Currently, scientists order chemicals manually via paper forms. 
Management discovered that 30% of ordered chemicals duplicate existing stockroom supplies that expire before use, costing \$1.8M annually in hazardous waste disposal. 
Furthermore, federal OSHA and EPA regulations require automated reporting of chemical usage and storage within 24 hours of inspection, which the current manual system cannot support. 
You are tasked with engineering the requirements baseline for the new automated **Chemical Tracking System (CTS)**.

#### Engineering Tasks & Deliverables:
- **Task 1: Scope Boundary Modeling (3 Marks):** Contrast a **Context Diagram** with an **Ecosystem Map** for the CTS. Identify two external entities (terminators) that appear on the Context Diagram and two external systems that must appear on the Ecosystem Map (such as Health & Safety incident databases or corporate ERP).

- **Task 2: Non-Functional Requirements Specification (4 Marks):** Author two (2) rigorous Non-Functional Requirements for CTS: one **Product Requirement** (availability/performance) and one **External Requirement** (regulatory/safety compliance). Ensure both requirements are 100% verifiable and testable.

- **Task 3: Business Rules as Enterprise Assets (3 Marks):** Explain why the EPA's hazardous disposal calculation algorithms must be documented as **Business Rules** stored separately from project functional requirements. What risk arises if these algorithms are hard-coded directly into the CTS functional specification?

