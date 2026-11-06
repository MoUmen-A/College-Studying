# Software Requirements Engineering: Comprehensive Guide Answer & Marking Scheme
## Detailed Model Solutions for Exam 01
**Course:** Software Requirements Engineering (CS / SE)  
**Corresponding Exam Paper:** [Exam_01.md](file:///d:/Gam3a/Exam-Creation/SoftwareRequ/SimulatedExams/Exam_01.md)  
**Total Marks:** 50 Marks | **Passing Standard:** 70% | **Full Marks Goal:** 50/50  

---

### Section A: Requirements Defect Analysis & Surgical Rewrite (10 Marks)

#### Solution to Question 1 (5 Marks)
*Grading Scheme: [2.5 Marks] for identifying specific quality characteristic violations; [2.5 Marks] for providing a rigorous, testable, atomic rewrite.*

- **Defect Identification (2.5 Marks):**
  1. *Ambiguity & Subjectivity:* The word "quickly" has no quantifiable engineering meaning.
  2. *Untestability / Non-Verifiability:* "Sufficiently user-friendly" and "do not get confused" cannot be verified with a deterministic pass/fail test.
  3. *Incompleteness:* Fails to specify the required user inputs, error states, and system boundaries.
- **Surgical Rewrite (2.5 Marks):**
  - **`FR-CTS-REQ-001` (Functional):** *"The system shall allow a chemist to submit a chemical requisition by specifying Chemical Name, CAS Number, Required Volume, and Delivery Laboratory."*
  - **`NFR-CTS-PERF-001` (Performance NFR):** *"The system shall process and confirm submission of an in-stock chemical request within 1.5 seconds for 95% of requests under a load of up to 50 concurrent users."*
  - **`NFR-CTS-USAB-001` (Usability NFR):** *"A newly hired lab technician shall be able to complete a standard chemical request within 3 minutes on their first attempt after completing a 15-minute training tutorial."*

---

#### Solution to Question 2 (5 Marks)
*Grading Scheme: [2.5 Marks] for diagnosing defects; [2.5 Marks] for providing decomposed, verifiable requirements.*

- **Defect Identification (2.5 Marks):**
  1. *Violation of Atomicity:* Merges sales tax calculation, promo code validation, receipt emailing, and server error handling into a single run-on sentence.
  2. *Impeded Traceability:* A QA tester cannot verify promo code logic independently from tax calculation.
  3. *Incomplete Error Handling:* "Display an error message if the server is down" fails to specify retry logic, transaction rollbacks, or offline persistence.
- **Surgical Rewrite (2.5 Marks):**
  - **`FR-CHK-TAX-01`:** *"The checkout module shall calculate applicable state and municipal sales taxes based on the destination shipping address zip code retrieved from the State Tax Database."*
  - **`FR-CHK-PROMO-02`:** *"The checkout module shall validate promotional discount codes against active campaign dates and apply approved percentage deductions to eligible line items."*
  - **`FR-CHK-RCPT-03`:** *"Upon receipt of successful payment gateway authorization, the system shall transmit a standardized PDF receipt to the customer's verified email address within 60 seconds."*
  - **`FR-CHK-ERR-04`:** *"If the payment gateway does not respond within 5,000 ms, the system shall terminate the transaction, roll back cart locks, and display message `ERR-NET-504: Payment Service Unavailable`."*

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks)

#### Solution to Question 3 (5 Marks)
*Grading Scheme: [2.5 Marks] for precise theoretical definitions; [2.5 Marks] for applied demonstrations and governance analysis.*

- **Validation vs. Verification Definitions (2 Marks):**
  - **Validation (*Building the right product*):** Confirms that the specified system satisfies the actual operational needs, business goals, and operational context of users and stakeholders.
  - **Verification (*Building the product right*):** Confirms that the requirements documents satisfy internal quality standards, conform to templates, are mathematically consistent, and can be tested.
- **Scenario of Passing Verification but Failing Validation (2 Marks):**
  - An engineering team specifies an automated chemical ordering system that strictly requires users to enter 16-digit chemical inventory serial numbers. The specification is 100% complete, unambiguous, and passes all verification checklists. However, in the physical lab, scientists handle vials labeled only by chemical formulas and common trade names; they have no access to 16-digit serials. The software is verified as defect-free against specs, but **fails validation** because scientists cannot use it.
- **Stakeholder Governance Roles (1 Mark):**
  - Validation must be led by **Business Analysts, Product Owners, and End-Users**.
  - Verification is led by **Software Quality Engineers, Systems Analysts, and Software Architects**.

---

#### Solution to Question 4 (5 Marks)
*Grading Scheme: [2.5 Marks] for core concepts and taxonomy; [2.5 Marks] for applied illustrations and enterprise asset management.*

- **Three-Tier Hierarchy (2 Marks):**
  - **Business Problem:** The operational pain point or market barrier currently experienced (e.g., manual processes, excessive waste).
  - **Business Objective:** The strategic, quantifiable target the enterprise intends to achieve to resolve the problem.
  - **Success Metric:** Concrete measurement tracked during operation to evaluate whether the objective was achieved.
- **Chemical Tracking System (CTS) Application (3 Marks):**
  - **Business Problem:** *"Manual chemical inventory management is inefficient, causing \$1.8M in annual waste from expired, duplicated chemical containers."*
  - **Business Objective:** *"Reduce company chemical purchasing expenses by 25% within the first 12 months of CTS deployment."*
  - **Success Metric:** *"Reduce average time to locate an existing chemical container in local stockrooms to under 5 minutes on 90% of searches, and reduce discarded expired chemicals by 40% year-over-year."*

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks)

#### Solutions to Elicitation Scenarios (5 Marks Each)
*Grading Scheme: [2.5 Marks] for comparative technical justification; [2.5 Marks] for risk analysis and operational mitigation strategies.*

- **Scenario 1: Observation vs. Interviews (5 Marks):**
  - *Superiority of Observation (2.5 Marks):* Forklift operators perform tacit, muscle-memory actions (e.g., verifying pallet integrity, checking manual clearance boards) that they omit during interviews because they take them for granted. Observation captures the true 'As-Is' operational reality.
  - *Risks & Mitigation (2.5 Marks):* 
    1. *Hawthorne Effect:* Workers alter their behavior when watched. Mitigation: Spend extended time on the warehouse floor until workers become accustomed to the analyst; frame the study as evaluating software tools, not worker efficiency.
    2. *Context Misinterpretation:* Analyst assumes a workaround is standard procedure. Mitigation: Pair observation with post-shift debriefing questions (*Contextual Inquiry*).
- **Scenario 2: Facilitated Workshops vs. Surveys (5 Marks):**
  - *Superiority of Workshops (2.5 Marks):* Surveys collect passive, isolated opinions and cannot resolve direct political conflict between department heads. A facilitated workshop forces decision-makers into a single room with a neutral facilitator to negotiate trade-offs in real time.
  - *Three Mandatory Preparation Steps (2.5 Marks):*
    1. *Select Empowered Decision-Makers:* Ensure attendees have actual authority to commit departmental scope.
    2. *Establish Clear Scope Boundaries Ahead of Time:* Distribute draft use cases and agenda 48 hours prior.
    3. *Appoint a Dedicated Scribe:* Separate facilitation from note-taking to capture all decisions and action items.

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks)

#### Solutions to Modeling Prompts (5 Marks Each)
*Grading Scheme: [3 Marks] for structural correctness and clause completeness; [2 Marks] for technical precision and domain relevance.*

- **1. Vision Statement Construction (5 Marks):**
  - **For** research scientists and laboratory technicians
  - **Who** need to locate and requisition chemical containers across campus facilities
  - **The** Chemical Tracking System (CTS) **is an** automated laboratory inventory management platform
  - **That** provides real-time container tracking, stockroom lookup, automated replenishment, and hazardous usage auditing
  - **Unlike** current manual paper ordering forms and fragmented departmental spreadsheets
  - **Our product** automatically generates federal OSHA/EPA environmental compliance reports and reduces chemical purchasing expenses by 25% in the first year.
- **2. Event List Classification (5 Marks):**
  - **Event A (User/Business Event):** Human-initiated action seeking to accomplish an organizational goal.
  - **Event B (Temporal Event):** Triggered automatically by the passage of time or arrival of a scheduled calendar deadline.
  - **Event C (Signal Event):** Triggered by an external hardware device or sensor transmitting a data packet.
  - **Event D (Signal Event):** Triggered by a physical environmental threshold sensor breach.
  - **Event E (User/Business Event):** Human-initiated reporting query.

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)

#### Model Solutions & Evaluation Rubric:
*Grading Scheme: Task 1 [4 Marks], Task 2 [3 Marks], Task 3 [3 Marks].*

- **Task 1: Scope Boundary Modeling (3 Marks):**
  - *Context Diagram vs. Ecosystem Map (1 Mark):* Context diagram shows direct boundary interfaces to the CTS process. Ecosystem map shows the broader solution space, including systems that do not interface directly with CTS but share data or are impacted.
  - *Context Diagram Terminators (1 Mark):* `Chemist`, `Chemical Stockroom Clerk`, `Barcode Scanner`.
  - *Ecosystem Map External Systems (1 Mark):* `Corporate SAP ERP`, `OSHA/EPA Reporting Gateway`, `Health & Safety Incident Database`.
- **Task 2: Non-Functional Requirements Specification (4 Marks):**
  - *Product Requirement (2 Marks):* **`NFR-CTS-AVAIL-01`:** *"The CTS shall maintain 99.8% uptime during laboratory operating hours (Monday–Friday, 07:00–20:00), with scheduled maintenance restricted to weekends."*
  - *External Requirement (2 Marks):* **`NFR-CTS-REG-02`:** *"The system shall encrypt all chemical storage location and hazard records at rest using AES-256 and generate EPA Form SARA-312 manifests conforming to statutory XML schema v4.1."*
- **Task 3: Business Rules as Enterprise Assets (3 Marks):**
  - *Rationale (1.5 Marks):* EPA hazardous classification formulas apply across the entire corporation, not just the CTS project. Treating them as enterprise assets ensures consistent compliance across future lab and shipping systems.
  - *Risk of Hard-Coding (1.5 Marks):* When environmental regulations update toxicity thresholds, hard-coded rules require expensive source code refactoring and re-testing; externalized business rules can be updated via configuration tables without altering software logic.

---

> [!TIP]
> **Full Marks Key:** Always write requirements using the RFC 2119 / IEEE standard keyword **SHALL** for mandatory requirements, provide quantifiable operational numbers (seconds, MB, percentages), and explicitly state what the system must do when an error or network drop occurs.
