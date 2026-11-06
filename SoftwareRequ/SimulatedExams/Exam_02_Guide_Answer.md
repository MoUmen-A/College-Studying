# Software Requirements Engineering: Comprehensive Guide Answer & Marking Scheme
## Detailed Model Solutions for Exam 02
**Course:** Software Requirements Engineering (CS / SE)  
**Corresponding Exam Paper:** [Exam_02.md](file:///d:/Gam3a/Exam-Creation/SoftwareRequ/SimulatedExams/Exam_02.md)  
**Total Marks:** 50 Marks | **Passing Standard:** 70% | **Full Marks Goal:** 50/50  

---

### Section A: Requirements Defect Analysis & Surgical Rewrite (10 Marks)

#### Solution to Question 1 (5 Marks)
*Grading Scheme: [2.5 Marks] for identifying specific quality characteristic violations; [2.5 Marks] for providing a rigorous, testable, atomic rewrite.*

- **Defect Identification (2.5 Marks):**
  1. *Ambiguity:* The word "normally" has no software specification.
  2. *Incompleteness:* "If an error occurs, it will inform the doctor appropriately" fails to define what errors exist, what message is displayed, or what recovery action is taken.
  3. *Untestability:* A test engineer cannot verify whether an arbitrary message is "appropriate".
- **Surgical Rewrite (2.5 Marks):**
  - **`FR-CLINIC-SCHED-01`:** *"The system shall display the selected clinic's daily appointment manifest containing Patient Name, Medical Record Number (MRN), Scheduled Start Time, and Appointment Reason in chronological order."*
  - **`FR-CLINIC-ERR-02`:** *"If the patient appointment database is unreachable after 3 retry attempts (1,000 ms timeout each), the system shall display error banner `ERR-DB-503: Clinic schedule offline. Retrying in 30 seconds...` and log the exception to the audit server."*

---

#### Solution to Question 2 (5 Marks)
*Grading Scheme: [2.5 Marks] for diagnosing defects; [2.5 Marks] for providing decomposed, verifiable requirements.*

- **Defect Identification (2.5 Marks):**
  1. *Infeasibility:* "Zero downtime" is physically and mathematically impossible in distributed networked systems.
  2. *Untestability:* "Extremely reliable" is a marketing slogan, not a measurable software engineering metric.
- **Surgical Rewrite (2.5 Marks):**
  - **`NFR-PMS-AVAIL-01`:** *"The MHC-PMS shall be available to all clinic terminals Monday through Friday between 08:00 and 18:00 with total unscheduled downtime not exceeding 30 seconds per business month (99.98% operational availability)."*
  - **`NFR-PMS-REL-02`:** *"The system shall exhibit a Mean Time Between Failures (MTBF) of at least 720 operating hours during business operation."*

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks)

#### Solution to Question 3 (5 Marks)
*Grading Scheme: [2.5 Marks] for precise theoretical definitions; [2.5 Marks] for applied demonstrations and governance analysis.*

- **Seven Interpretations of Completeness (3 Marks):**
  1. *Individual Requirement Completeness:* Specifies all inputs, valid ranges, output displays, and explicit error handlers.
  2. *Requirements Models Completeness:* State transition diagrams have no orphan states or dead ends; DFDs balance inputs and outputs.
  3. *Requirements Baseline Completeness:* The agreed-upon release package contains all functional and non-functional specifications required to build the release without unstated assumptions.
- **Standish Group CHAOS Study & Economic Impact (2 Marks):**
  - Incomplete requirements cause **12.3% of all project failures and severe cost overruns**.
  - *Economic Reasons:*
    1. *Artificially Low Initial Estimates:* Budgets and schedules are underestimated because omitted requirements were never calculated.
    2. *Cost of Late Rework:* Discovering missing requirements during testing or post-release costs up to 100x more to fix than discovering them during the Analysis phase.

---

#### Solution to Question 4 (5 Marks)
*Grading Scheme: [2.5 Marks] for core concepts and taxonomy; [2.5 Marks] for applied illustrations and enterprise asset management.*

- **Definitions & Differences (2 Marks):**
  - **Functional Requirements:** Statements of system services, input transformations, and behavioral responses.
  - **Non-Functional Requirements:** System-wide quality constraints (speed, uptime, security) governing how well functions execute.
  - **Design Constraints:** Imposed boundary limitations on technology choices (e.g., must run on Linux, must use Oracle DB).
- **Spawning Child Functional Requirements (1.5 Marks):**
  - An NFR stating *"Patient records must be protected against unauthorized access"* directly spawns functional requirements for: (1) Smart-card biometric login screens, (2) Role-based access permission tables, (3) Automated 10-minute session timeouts, and (4) Cryptographic audit logging.
- **Architectural Influence (1.5 Marks):**
  - Functional requirements dictate what individual modules do; NFRs dictate the high-level architecture (e.g., microservices, database replication, caching layers, load balancers).

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks)

#### Solutions to Elicitation Scenarios (5 Marks Each)
*Grading Scheme: [2.5 Marks] for comparative technical justification; [2.5 Marks] for risk analysis and operational mitigation strategies.*

- **Scenario 1: Prototyping vs. Document Analysis (5 Marks):**
  - *Technique Sequence:* Document Analysis must precede Prototyping.
  - *Document Analysis Role (2.5 Marks):* Mine the 800 pages of COBOL manuals to extract complex medical business rules, data schemas, and dosage algorithms that users cannot recall.
  - *Prototyping Role (2.5 Marks):* Once backend logic is extracted, build interactive UI prototypes to validate modernized clinical workflows with younger nurses and physicians who reject terminal-based green-screen interfaces.
- **Scenario 2: Surveys vs. Focus Groups (5 Marks):**
  - *Questionnaires/Surveys (2.5 Marks):* Reaches thousands of citizens across the state inexpensively; provides statistically valid demographic data; however, cannot clarify misunderstandings or ask follow-up questions.
  - *Focus Groups (2.5 Marks):* Small, structured sessions (8-12 participants); uncovers deep emotional perceptions and usability frustrations; however, vulnerable to vocal participant bias and carries high cost per participant.

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks)

#### Solutions to Modeling Prompts (5 Marks Each)
*Grading Scheme: [3 Marks] for structural correctness and clause completeness; [2 Marks] for technical precision and domain relevance.*

- **1. Data Dictionary Construction (5 Marks):**
  - **Data Structure:** `Patient_Appointment_Record`
  - **Composition:** `Patient_ID` + `Clinic_Code` + `Appointment_Timestamp` + `Physician_License_No` + `Appointment_Status`
  - **Data Elements:**
    - `Patient_ID`: 10-digit alphanumeric string; Format: `PAT-[0-9]{7}`; Mandatory.
    - `Clinic_Code`: 3-character enumeration: `[CARD, ONCO, PEDI, NEUR, GENP]`.
    - `Appointment_Timestamp`: ISO 8601 UTC format: `YYYY-MM-DDThh:mm:ssZ`.
    - `Appointment_Status`: Enumerated: `[Scheduled, CheckedIn, InConsultation, Completed, Cancelled, NoShow]`.
  - *Value:* Guarantees that clinical users and database programmers mean the exact same data constraints, preventing runtime truncation errors.
- **2. Feature Tree Decomposition (5 Marks):**
  - **L1 Feature:** `Clinical Consultations`
    - **L2 Sub-Feature 1:** `Appointment Management`
      - **L3 Capability 1.1:** `Clinic Calendar Slot Booking`
      - **L3 Capability 1.2:** `Automated SMS Reminder Dispatch`
    - **L2 Sub-Feature 2:** `Prescription Dispatch`
      - **L3 Capability 2.1:** `Electronic Drug Formulary Lookup`
      - **L3 Capability 2.2:** `Automated Drug-Drug Allergy Interaction Check`

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)

#### Model Solutions & Evaluation Rubric:
*Grading Scheme: Task 1 [4 Marks], Task 2 [3 Marks], Task 3 [3 Marks].*

- **Task 1: Stakeholder Classification (3 Marks):**
  - *Primary Stakeholders:* Clinic receptionists, staff physicians, attending nurses (direct daily hands-on users).
  - *Secondary Stakeholders:* Outpatient clinic patients, hospital billing department, pharmacists.
  - *Key Stakeholders:* Chief Medical Officer, Hospital Legal Compliance Director, IT Director. Ultimate privacy sign-off belongs to the **Hospital Legal Compliance Director**.
- **Task 2: Interface Analysis (3 Marks):**
  - *User Interface (UI):* Touchscreen tablet interface for doctors during rounds; high-contrast desktop portal for receptionists.
  - *Software Interface (API):* RESTful HL7/FHIR API transmitting insured patient eligibility queries to national insurance clearinghouses with 2,000 ms timeout limits.
  - *Hardware Interface:* USB smart-card badge reader communicating over PC/SC protocol for two-factor physician authentication.
- **Task 3: Resolving Specification Inconsistency (4 Marks):**
  - *Conflict Analysis (1.5 Marks):* Unrestricted emergency overrides (R-14) directly violate the 20-patient safety ceiling (R-89).
  - *Reconciled Rule-Based Requirement (2.5 Marks):* **`FR-PMS-OVERRIDE-01`:** *"The system shall permit an attending physician to book an urgent patient beyond the 20-patient clinic limit only upon entering an authorized Emergency Justification Code and submitting two-factor smart-card credentials. The system shall automatically transmit an emergency override notification to the Medical Director within 15 minutes."*

---

> [!TIP]
> **Full Marks Key:** Always write requirements using the RFC 2119 / IEEE standard keyword **SHALL** for mandatory requirements, provide quantifiable operational numbers (seconds, MB, percentages), and explicitly state what the system must do when an error or network drop occurs.
