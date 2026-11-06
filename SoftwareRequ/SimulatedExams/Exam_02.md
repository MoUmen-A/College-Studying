# Software Requirements Engineering: Advanced Examination Series
## Exam 02: Analysis Modeling, Data Dictionaries & Completeness Dimensions
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
Analyze the following requirement from a clinical scheduling module:
> *"The MHC-PMS shall display patient appointment schedules normally, but if an error occurs, it will inform the doctor appropriately."*
- **a) Defect Identification (2.5 Marks):** Detail why this requirement fails the tests of *Unambiguity*, *Completeness*, and *Verifiability*. What does 'normally' or 'appropriately' mean to a test engineer?
- **b) Surgical Rewrite (2.5 Marks):** Rewrite this into a complete, testable functional requirement specifying exact inputs, display outputs, and deterministic error handling.

#### Question 2 (5 Marks)
Analyze the following requirement from a pharmaceutical dispensing interface:
> *"The system should be extremely reliable and have zero downtime during peak hospital hours."*
- **a) Defect Identification (2.5 Marks):** Evaluate this statement against the quality criteria of *Feasibility* and *Testability*. Why is 'zero downtime' an engineering trap?
- **b) Surgical Rewrite (2.5 Marks):** Rewrite this into a verifiable Non-Functional Product Requirement utilizing MTBF (Mean Time Between Failures), allowed downtime thresholds, and scheduled operational windows.

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks, 5 Marks Each)
*Answer the following deep-dive theoretical prompts with structured, professional justifications.*

#### Question 3 (5 Marks)
Deep-Dive into the **Seven Interpretations of Requirements Completeness** (5 Marks):
- In requirements engineering literature, 'completeness' is not a monolithic term. Explain what completeness means at the level of:
  1. An individual functional requirement.
  2. The Requirements Analysis Models (e.g., State Diagrams, DFDs).
  3. The Requirements Baseline.
- Cite the findings of the **Standish Group CHAOS Study** regarding incomplete requirements (percentage of failure/overruns) and explain the two economic reasons why omissions cause project collapse.

#### Question 4 (5 Marks)
Differentiate **Functional Requirements**, **Non-Functional Requirements (NFRs)**, and **Design Constraints** (5 Marks):
- Provide clear definitions of each category.
- Explain why a single NFR (e.g., HIPAA patient data privacy) inevitably spawns multiple child functional requirements.
- Contrast how NFRs influence overall system architecture versus how functional requirements dictate component behavior.

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks, 5 Marks Each)
*Evaluate the operational scenarios below and justify your strategic elicitation choices.*

Analyze the tactical trade-offs in requirement gathering (10 Marks - 5 Marks each):
1. **Technique Comparison (Prototyping vs. Document Analysis):** A regional healthcare authority contracts your team to replace a 25-year-old COBOL patient record system. The original developers retired, but 800 pages of user manuals and batch script specifications exist. Contrast using **Document Analysis** against **Interactive UI Prototyping**. In which phase of analysis should each technique be deployed to maximize efficiency?
2. **Surveys vs. Focus Groups for Public Healthcare:** The hospital wants feedback on an outpatient mobile portal from 50,000 diverse citizens across the state. Compare **Questionnaires/Surveys** against **Focus Groups**. Evaluate both techniques based on: sample representativeness, ability to ask follow-up questions, cost per participant, and risk of moderator bias.

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks, 5 Marks Each)
*Construct formal requirements engineering models according to the prompt instructions.*

Develop requirements engineering models for the Medical Health Care – Patient Management System (MHC-PMS) (10 Marks):
1. **Data Dictionary Construction (5 Marks):** Construct a formal Data Dictionary entry for `Patient_Appointment_Record`. Define its logical composition, sub-elements (e.g., `Patient_ID`, `Clinic_Code`, `Appointment_Timestamp`, `Status`), data types, and valid range/enumeration constraints. Explain how a data dictionary eliminates semantic ambiguity between clinical staff and database developers.
2. **Feature Tree Decomposition (5 Marks):** Design a 3-level **Feature Tree** (L1, L2, L3) for the MHC-PMS feature category `Clinical Consultations`. Decompose this L1 feature into two L2 sub-features (e.g., `Appointment Management` and `Prescription Dispatch`), and break down each L2 feature into two specific L3 functional capabilities.

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)
*Carefully read the enterprise engineering scenario and deliver the three technical tasks that follow.*

#### Scenario Context: St. Jude Regional Medical Center is commissioning the MHC-PMS to coordinate 12 specialized outpatient clinics. 
Doctors demand instant access to patient medical histories, but the hospital compliance board mandates strict adherence to statutory health privacy regulations (HStan-03-2006-priv). 
During early elicitation, junior analysts reported that clinic receptionists, head surgeons, and pharmacists have irreconcilable expectations regarding appointment overbooking and emergency overrides. 
You are tasked with engineering the requirements baseline and resolving stakeholder conflict.

#### Engineering Tasks & Deliverables:
- **Task 1: Stakeholder Classification & Governance (3 Marks):** Classify the clinic receptionists, head surgeons, hospital compliance officers, and external patients into **Primary**, **Secondary**, and **Key Stakeholders**. Who has ultimate sign-off authority on privacy constraints?

- **Task 2: Interface Analysis (3 Marks):** Analyze the external interfaces for MHC-PMS across three distinct categories: **User Interfaces (UI)**, **Software Interfaces (APIs)** to external national insurance databases, and **Hardware Interfaces** to hospital smart identity card readers.

- **Task 3: Resolving Specification Inconsistency (4 Marks):** Requirement R-14 states: *'Any physician may override clinic appointment caps to admit an urgent patient.'* Requirement R-89 states: *'Clinic schedules must never exceed 20 patients per session to prevent medical malpractice fatigue.'* Analyze this conflict against the quality characteristic of **Consistency** and formulate a reconciled, rule-based requirement.

