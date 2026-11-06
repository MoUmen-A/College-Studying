# Exam 04: True/False, Essay & Applied Cases (Comprehensive Final)

> **Subject:** Software Requirements Engineering  
> **Coverage:** Comprehensive Final Examination (Chapters 1, 2, and 3)  
> **Total Marks:** 50 | **Time Allowed:** 90 Minutes  
> **Instructions:** Answer all questions in full sentences. For True/False questions, you must provide a concise technical justification; correct identification without justification earns only partial credit.

---

## 🎓 Examinee Strategic Briefing: How to Solve & Critical Pitfalls to Avoid

Before attempting this comprehensive final examination, review this master roadmap to guide your problem-solving across all three chapters:

### 1. How to Approach Each Section:
- **Section 1 (True / False):**
  - **Domain Requirements:** Can be functional (computations like train deceleration formulas) or non-functional (standards like Z39.50). Programming language constraints are *Organizational*, not Domain!
  - **Dispute Resolution:** Brainstorming *generates* ideas; only *Requirements Workshops* with authorized decision-makers resolve disputes and lock scope.
  - **Baselines & Change:** Baselining does *not* freeze software forever; it forces changes to pass through formal CCB Impact Analysis.
- **Section 2 (Essays):**
  - **The 4 Requirement Levels:** Trace a capability seamlessly:
    1. *User Level:* High-level natural language user goal.
    2. *Functional Level:* Concrete system behavior with `SHALL`.
    3. *NFR Level:* System-wide quality constraint (performance, availability, security).
    4. *System Level:* Technical engineering specification (protocols, hardware interfaces, database schemas).
  - **Development vs. Management:** Clearly contrast creating the baseline (Development: 4 subdisciplines) with controlling changes and maintaining integrity after approval (Management: CCB, Baselines, RTM, Status Tracking).
  - **Imprecision Breakdown:** Analyze the clinic search case: contrast the multi-clinic simultaneous intention with the single-clinic dropdown interpretation.
- **Section 3 (Business Goals & Metrics):**
  - Extract the **Business Problem** directly from operational delays, expired inventory, and financial waste.
  - Maintain the strict 6-clause structure in the **Vision Statement**.
  - Categorize events accurately: *Business* (human initiates), *Temporal* (time/schedule triggers), *Signal* (hardware sensor triggers).
- **Section 4 (Requirements Issues & Subsystem Allocation):**
  - **Subsystem Allocation:** Cleanly apportion responsibilities among Hardware (sensors/loggers), Software (logic/alerting), and Human Roles (nurses/operators).
  - **Consistent Authentication:** Identify Organizational NFR standards (e.g., physical smart-card identity tokens).

### 2. Top Cognitive Traps to Avoid:
1. ❌ **Trap 1: Conflating Functional and System Requirements.** Functional specs say *what the software does*; System specs say *how the technical architecture and interfaces are engineered*.
2. ❌ **Trap 2: Confusing Hardware Signals with User Events.** A sensor reading or barcode scan is a *Signal Event*; a user clicking a button is a *Business Event*.
3. ❌ **Trap 3: Vague Rewrites.** In blood bank or life-critical systems, never use "dangerously low"; state exact numerical units (e.g., "$< 20$ units of O-negative blood").

---

## SECTION 1 — True or False with Justification [12 marks | 6 questions]

### Question 1 (2 marks)
*Statement:* Domain requirements are always non-functional constraints that restrict the programming language used by developers.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 2 (2 marks)
*Statement:* Brainstorming is the most effective elicitation technique for resolving contentious departmental disputes and locking down final scope commitments.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 3 (2 marks)
*Statement:* In a secure building access control system, requirements must be apportioned among software, hardware, and human procedural roles to prevent contractual ambiguity.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 4 (2 marks)
*Statement:* A Software Requirements Specification (SRS) is considered complete as long as every individual functional requirement contains inputs, calculations, and expected outputs.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 5 (2 marks)
*Statement:* In Requirements Management, once an approved requirements baseline is established, no changes can ever be made to the software system.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 6 (2 marks)
*Statement:* According to the Standish Group study, discovering an omitted requirement during user acceptance testing or post-deployment costs 10x to 100x more than discovering it during requirements validation.  
*(State True or False and provide a rigorous technical justification from the lecture).*

---

## SECTION 2 — Deep Essay & Analytical Synthesis [14 marks | 3 questions]

### Question 7 (5 marks)
Explain how the **Four Requirement Perspectives/Levels** (User Requirements, Functional Requirements, Non-Functional Requirements, and System Requirements) interrelate throughout the software engineering lifecycle. In your essay, trace a single real-world clinical capability from the Medical Health Care – Patient Management System (MHC-PMS) across all four levels, demonstrating how high-level user goals decompose into technical specifications and architectural constraints.

### Question 8 (5 marks)
Compare and contrast **Requirements Management** with **Requirements Development**. In your essay, structure an analytical comparison examining: (a) the primary objective of each, (b) the four core subdisciplines of Requirements Development, (c) the four primary governance disciplines of Requirements Management, and (d) how the Change Control Board (CCB) utilizes the Requirements Traceability Matrix (RTM) to perform Change Impact Analysis.

### Question 9 (4 marks)
Analyze the hazard of **Imprecision and Ambiguity** in requirements engineering. Using the famous *"Search clinic appointments"* case study from Chapter 1, contrast the user's mental model with the developer's technical implementation, explain the operational disaster that resulted, and formulate the requirements engineering rule that prevents this breakdown.

---

## SECTION 3 — Case Study: Business Goals & Metrics [12 marks | 3 questions]

### Scenario Description
A large municipal university hospital operates a central blood bank serving 12 trauma centers. Currently, cross-matching requests and emergency blood unit reservations are communicated via phone calls and paper slips. Emergency blood delivery experiences an average delay of 75 minutes, 14% of reserved red blood cell units expire unused due to lack of real-time cold-chain visibility, and hospital billing fails to capture \$320,000 annually in transfusion consumables. The hospital board has commissioned the **Smart Blood Bank Management System (SBBMS)**.

### Question 10 (4 marks)
Extract and formally structure the core business foundations for the SBBMS project:  
(a) Define the primary **Business Problem** currently endangering emergency patient trauma care.  
(b) Formulate two distinct, quantifiable **Business Objectives** for the SBBMS investment.  
(c) Define two concrete **Success Metrics** that can be evaluated during post-implementation operational testing.

### Question 11 (4 marks)
Author a formal, standard **6-Clause Vision Statement** for the Smart Blood Bank Management System conforming strictly to the template taught in Chapter 2 (*For... Who... The... That... Unlike... Our product...*).

### Question 12 (4 marks)
Construct an **Event Catalog (Event List)** for the SBBMS by defining the three event categories described in the lecture (**Business / User Event**, **Temporal Event**, and **Signal Event**) and providing one exact, real-world trigger from the SBBMS project for each category.

---

## SECTION 4 — Case Study: Requirements Issues & Quality Diagnosis [12 marks | 3 questions]

### Scenario Description
During the final verification audit of the draft SBBMS specification, the quality assurance lead flags three high-risk requirements statements for remediation.

### Question 13 (4 marks)
*Audit Statement 1:*  
*"The blood bank software shall be fast, reliable, user-friendly, and alert staff immediately if blood supply is dangerously low."*  
(a) Identify all quality defects by name based on the 9 Quality Characteristics taxonomy.  
(b) Explain why mixing subjective adjectives with unmeasured alerts prevents automated QA verification.  
(c) Surgically rewrite this statement into two atomic, verifiable requirements (`FR-BLD-01` and `NFR-BLD-01`) using RFC 2119 `SHALL` syntax and quantifiable thresholds.

### Question 14 (4 marks)
*Audit Statement 2:*  
*"Requirement 3.2: Staff shall log in using their username and password."*  
*"Requirement 8.5: Staff must authenticate using their physical health authority smart identity card."*  
(a) Identify the quality characteristic violated by these conflicting requirements.  
(b) Classify Requirement 8.5 into its precise NFR taxonomy category (Product, Organizational, or External) and justify your classification.  
(c) Surgically rewrite these statements into a single, unified, and consistent requirement (`NFR-AUTH-BLD-01`).

### Question 15 (4 marks)
*Audit Statement 3:*  
*"The system shall track blood bags, check temperature sensors, and nurses will transfuse patients according to protocol."*  
(a) Identify the architectural analysis defect in this statement according to the **Subsystem Allocation** discipline.  
(b) Explain how conflating hardware sensor telemetry, software database tracking, and human clinical procedures undermines project accountability.  
(c) Surgically decompose this statement into three cleanly allocated requirements: Hardware (`REQ-HW-BLD-01`), Software (`REQ-SW-BLD-01`), and Human Procedural Role (`REQ-OPS-BLD-01`).

---

# GUIDE ANSWERS & MARKING SCHEME

### Question 1 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* Domain requirements are derived directly from the application domain's fundamental operational physics, mathematics, or industry standards. They are **not restricted to non-functional constraints**; they can be **functional requirements** specifying complex domain calculations (such as the train automatic deceleration equation $D_{\text{train}} = D_{\text{control}} + D_{\text{gradient}}$) or non-functional constraints (such as conforming to the international Z39.50 library standard protocol or digital copyright delete-on-print mandates). Furthermore, language constraints are Organizational NFRs, not Domain Requirements.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for explaining that domain requirements can be functional (formulas) or non-functional (protocols), citing the train deceleration formula or Z39.50.  
- **Common Mistake Warning:** Thinking domain requirements only constrain programming tools.

### Question 2 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* Brainstorming is an unconstrained, uncensored ideation technique used during early project inception to generate creative possibilities across multidisciplinary groups. It explicitly suspends criticism and evaluation. It is **completely ineffective for resolving contentious disputes or locking down scope**. The technique specifically designed for cross-departmental alignment, conflict resolution, and locking down scope under tight deadlines is the **Requirements Workshop** (facilitated collaborative work sessions led by a neutral moderator and attended by authorized decision-makers).  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for contrasting unconstrained ideation (Brainstorming) with structured consensus negotiation (Requirements Workshops).  
- **Common Mistake Warning:** Answering True, confusing creative idea generation with dispute resolution.

### Question 3 Guide Answer
- **Model Answer:** **TRUE.**  
  *Justification:* Subsystem Allocation (Activity 8 of Requirements Analysis) dictates that complex systems comprising multiple subcomponents must allocate requirements across **Hardware** (optical badge readers, electronic locks), **Software** (credential validation databases, alert dispatchers), and **Human Operator Roles** (guards verifying physical photo IDs). If requirements are not apportioned cleanly, hardware vendors, software engineers, and facility staff have overlapping or omitted responsibilities, creating severe contractual disputes.  
- **Marking Scheme:** 1 mark for TRUE; 1 mark for explaining hardware vs. software vs. human procedural boundaries.  
- **Common Mistake Warning:** Believing allocation only applies to software architectural layers.

### Question 4 Guide Answer
- **Model Answer:**  
  *Justification:* Completeness operates across **Seven distinct interpretations**, and individual requirement completeness is only one level. A specification can have perfectly complete individual statements (specifying inputs, calculations, and outputs), but if entire models (DFDs, STDs), requirement metadata, requirements repositories, standardized document sections (IEEE 830), or the baseline set are missing, the overall specification is fatally incomplete.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for citing the 7 interpretations of completeness and explaining system/document-level completeness.  
- **Common Mistake Warning:** Believing completeness begins and ends at the sentence level.

### Question 5 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* In Requirements Management, establishing a baseline does not freeze the system permanently against all changes. Software systems operate in dynamic business and regulatory environments where change is inevitable. Establishing a baseline simply means that **uncontrolled, informal changes are prohibited**. Any proposed change must pass through a formal **Change Control Process**, where a Change Control Board (CCB) conducts Change Impact Analysis (assessing cost, schedule, architecture, and regression risks using the RTM) and formally approves or rejects the modification, incrementing the baseline version if approved.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for explaining formal change control, CCB impact analysis, and version incrementation.  
- **Common Mistake Warning:** Believing that baselining means software can never be updated.

### Question 6 Guide Answer
- **Model Answer:** **TRUE.**  
  *Justification:* The lecture and the Standish Group study explicitly emphasize the exponential cost-of-rework escalation factor: discovering and fixing an omitted requirement during early requirements engineering costs a baseline of $1\times$, whereas discovering and retrofitting that same requirement during coding, system testing, or production costs **10x to 100x more**.  
- **Marking Scheme:** 1 mark for TRUE; 1 mark for explaining the 10x to 100x exponential rework cost escalation factor.  
- **Common Mistake Warning:** Assuming testing rework costs are minor.

### Question 7 Guide Answer
- **Model Answer:**  
  - **The Four Requirement Perspectives/Levels:**  
    1. *User Requirements:* High-level statements in natural language and diagrams describing what operational tasks users need to accomplish from their business perspective.  
    2. *Functional Requirements:* Detailed technical statements of system services, inputs, behaviors, outputs, and explicit negative constraints.  
    3. *Non-Functional Requirements (NFRs):* System-wide behavioral and architectural constraints on performance, availability, security, and compliance.  
    4. *System Requirements:* Detailed engineering specifications defining how the software and hardware architecture must be engineered and integrated.  
  - **Tracing a Single Capability across All Four Levels (MHC-PMS):**  
    - *User Requirement:* "Clinic doctors need rapid, secure access to daily patient appointment lists without wasting time typing passwords between consultations."  
    - *Functional Requirement (`FR-MHC-02`):* "The system shall automatically generate a daily appointment manifest for each clinic every morning at 06:00 and display real-time clinic schedules upon user query."  
    - *Non-Functional Requirement (`NFR-MHC-01`):* "Clinic staff shall authenticate using their physical health authority smart identity card (Organizational NFR), and system downtime during working hours (08:30–17:30) shall not exceed 5 seconds per day (Product NFR)."  
    - *System Requirement:* "Workstation terminals shall interface with ISO 7816 smart card readers via PC/SC USB drivers, authenticating the 8-digit badge token against LDAP active directory over TLS 1.3 within 500 ms."  
- **Marking Scheme:**  
  - 2 marks for defining the 4 levels.  
  - 3 marks for tracing a coherent capability from MHC-PMS across all 4 levels (0.75 marks per level).  
- **Common Mistake Warning:** Mixing up Functional Requirements with System Requirements.

### Question 8 Guide Answer
- **Model Answer:**  
  - **(a) Primary Objectives:**  
    - *Requirements Development:* Discovering, analyzing, formalizing, modeling, and verifying the initial approved requirements baseline.  
    - *Requirements Management:* Controlling, maintaining, tracking, and tracing the requirements baseline after approval throughout the project lifecycle.  
  - **(b) Four Subdisciplines of Development:** (1) Requirements Elicitation, (2) Requirements Analysis, (3) Requirements Specification, and (4) Requirements Validation & Verification.  
  - **(c) Four Disciplines of Management:** (1) Change Control & Impact Analysis, (2) Version Control & Baselines, (3) Requirements Traceability Matrix (RTM), and (4) Status & Issue Tracking.  
  - **(d) CCB Impact Analysis using RTM:** When a change request is submitted, the Change Control Board (CCB) inspects the bidirectional links in the RTM. The matrix immediately reveals: (1) which business objectives are affected, (2) which dependent functional requirements must be modified, (3) which architectural components and code modules require refactoring, and (4) which regression test suites must be executed. This allows the CCB to calculate exact schedule delays, financial costs, and regression risks before approving a change.  
- **Marking Scheme:**  
  - 1 mark for (a) contrasting Development vs. Management objectives.  
  - 1 mark for (b) 4 subdisciplines of Development.  
  - 1 mark for (c) 4 disciplines of Management.  
  - 2 marks for (d) explaining CCB impact analysis via bidirectional RTM links.  
- **Common Mistake Warning:** Describing RTM as a simple checklist without bidirectional links.

### Question 9 Guide Answer
- **Model Answer:**  
  - **The Imprecision Hazard:** Ambiguous natural language specifications allow stakeholders to hold completely different interpretations while mistakenly believing they are in agreement.  
  - **MHC-PMS Case Study Breakdown:**  
    - *Written Requirement:* "A user shall be able to search clinic appointments."  
    - *User Mental Model:* The triage nurse or doctor enters a patient name into a single search box once, expecting the system to scan all clinics across the regional hospital network simultaneously to locate the patient's record.  
    - *Developer Implementation:* The developer builds a two-step search where the operator must first select a specific clinic branch from a drop-down list, and then search only within that single clinic's records.  
    - *Operational Disaster:* When an emergency patient arrives whose clinic booking is unknown, nurses must repeat the manual search 20+ times across individual clinic dropdowns, wasting 15 critical minutes and delaying emergency medical triage.  
  - **Requirements Engineering Rule:** Specifications must satisfy **Unambiguity and Completeness** — every requirement must state the exact operational scope, default search domains, inputs, outputs, and exception behaviors so that exactly one single technical interpretation exists.  
- **Marking Scheme:**  
  - 1 mark for defining the imprecision/ambiguity gap.  
  - 2 marks for contrasting user intention (global search) with developer interpretation (dropdown per clinic).  
  - 1 mark for the emergency triage operational disaster.  
  - 1 mark for the Unambiguity and Completeness rule.  
- **Common Mistake Warning:** Blaming the developer for writing bad code rather than identifying the ambiguous requirement.

### Question 10 Guide Answer
- **Model Answer:**  
  (a) **Business Problem:** Severe operational delays in emergency trauma delivery (75-minute wait), high expired blood waste rate (14% annual loss), and \$320,000 in unbilled transfusion consumables due to manual phone/paper workflows and zero real-time inventory visibility.  
  (b) **Business Objectives:**  
  1. Reduce emergency blood unit delivery latency from 75 minutes to under 20 minutes within 6 months of SBBMS deployment.  
  2. Reduce expired blood unit waste from 14% to under 2% within the first year of operation, capturing \$320,000 in unbilled consumables.  
  (c) **Success Metrics:**  
  1. Automated cross-matching query and reservation processing time shall be $\le 60$ seconds on at least 95% of emergency trauma requests during acceptance testing.  
  2. RFID temperature and location telemetry capture accuracy shall achieve $\ge 99.9\%$ across all active blood storage transport coolers.  
- **Marking Scheme:**  
  - 1 mark for Business Problem.  
  - 1.5 marks for two quantifiable Business Objectives (target percentage + timeframe).  
  - 1.5 marks for two concrete Success Metrics with measurable thresholds.  
- **Common Mistake Warning:** Writing a functional requirement with `SHALL` instead of formulating a strategic Business Objective.

### Question 11 Guide Answer
- **Model Answer:**  
  **Vision Statement Artifact — Smart Blood Bank Management System:**  
  - **For** hospital trauma surgeons, emergency triage nurses, and blood bank inventory technicians,  
  - **Who** require instantaneous cross-matching verification and emergency blood supply dispatch without testing delays,  
  - **The** Smart Blood Bank Management System **is an** enterprise clinical inventory and cold-chain tracking information system  
  - **That** will provide centralized real-time visibility into blood unit availability, automated cross-match reservations, and RFID temperature tracking across all 12 regional trauma centers, cutting emergency delivery times to under 20 minutes and eliminating 14% expired unit waste.  
  - **Unlike** current manual paper slips and telephone ordering processes,  
  - **Our product** will provide automated blood expiration alerting, biometric transfusion verification, and seamless electronic medical record billing integration.  
- **Marking Scheme:**  
  - 4 marks total: ~0.65 marks per clause correctly completed following the 6-clause lecture template.  
- **Common Mistake Warning:** Omitting the "Unlike" or "Our product" clauses.

### Question 12 Guide Answer
- **Model Answer:**  
  **SBBMS Event Catalog Artifact:**  
  1. **Business / User Event:**  
     - *Trigger:* A trauma center physician submits an emergency request for 4 units of O-negative blood via the clinical terminal.  
     - *System Reaction:* The system instantly checks real-time regional stock, reserves the nearest available units, and generates a priority courier dispatch order.  
  2. **Temporal Event:**  
     - *Trigger:* The system clock reaches 06:00 every morning.  
     - *System Reaction:* The system automatically generates a daily blood unit expiration manifest across all hospital cold-storage vaults, flagging units within 48 hours of expiration for immediate cross-distribution.  
  3. **Signal Event:**  
     - *Trigger:* An RFID cold-chain temperature sensor in a transit cooler detects a temperature exceeding $+6.0\ ^\circ\text{C}$.  
     - *System Reaction:* The sensor hardware transmits an interrupt packet to the monitoring server, which triggers an audible alarm and flashes a Critical Cold-Chain Violation on the dispatcher console within 2.0 seconds.  
- **Marking Scheme:**  
  - 1 mark for Business Event (trigger + reaction).  
  - 1.5 marks for Temporal Event (06:00 manifest trigger + reaction).  
  - 1.5 marks for Signal Event (RFID temperature sensor trigger + reaction).  
- **Common Mistake Warning:** Confusing a hardware sensor signal with a business user event.

### Question 13 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Untestable Quality Buzzwords:* "Fast," "reliable," and "user-friendly" are subjective and non-verifiable.  
  2. *Unmeasured Adverbs & Thresholds:* "Immediately" lacks a latency limit, and "dangerously low" omits the numeric reserve threshold.  
  3. *Compound Statement:* Conflates UI usability, system reliability, inventory querying, and alert dispatching into one clause.  
  (b) **Explanation:** A test engineer cannot construct a binary pass/fail test for "dangerously low". Developers will arbitrarily pick a number (e.g., 5 bags vs. 50 bags), leading to missed stockout warnings during major trauma disasters.  
  (c) **Surgical Rewrite:**  
  - `FR-BLD-01:` When the total available inventory of O-negative blood units across all central vaults falls below 20 units, the system shall automatically dispatch a Priority 1 Low-Stock Alert to the blood bank supervisor console and SMS gateway within 15 seconds.  
  - `NFR-BLD-01:` The blood inventory database shall be accessible Monday through Sunday, 24 hours a day, with total unplanned downtime not exceeding 5 seconds per calendar month during active trauma shifts.  
- **Marking Scheme:**  
  - 1 mark for naming defects (buzzwords, unmeasured thresholds, compound structure).  
  - 1 mark for explaining verification failure and arbitrary developer guessing.  
  - 2 marks for decomposing into `FR-BLD-01` and `NFR-BLD-01` with `SHALL` and measurable limits.  
- **Common Mistake Warning:** Keeping both functional and availability concerns in one requirement.

### Question 14 Guide Answer
- **Model Answer:**  
  (a) **Quality Characteristic Violated:** **Consistency** (Requirement 3.2 and Requirement 8.5 describe contradictory, mutually exclusive user authentication mechanisms).  
  (b) **Classification & Justification:** Requirement 8.5 is an **Organizational Non-Functional Requirement**. It specifies an internal organizational policy and operational standard regarding how hospital employees authenticate into institutional workstations using physical identity tokens.  
  (c) **Surgical Rewrite:**  
  `NFR-AUTH-BLD-01:` Clinical blood bank staff shall authenticate into the system by inserting their physical health authority smart identity card into the workstation terminal reader, with the system verifying the card's 8-digit healthcare authority employee badge number within 1.0 second.  
- **Marking Scheme:**  
  - 1 mark for identifying Consistency violation.  
  - 1.5 marks for classifying Req 8.5 as Organizational NFR with policy justification.  
  - 1.5 marks for unified rewrite (`NFR-AUTH-BLD-01`) enforcing the smart identity card standard using `SHALL`.  
- **Common Mistake Warning:** Classifying physical smart card authentication as an External Requirement.

### Question 15 Guide Answer
- **Model Answer:**  
  (a) **Architectural Analysis Defect:** Violation of **Subsystem Allocation** (Activity 8 of Requirements Analysis). It improperly merges hardware sensor telemetry, software inventory management, and human clinical procedures into an undifferentiated narrative sentence.  
  (b) **Explanation:** Blurring subsystems creates project failure: hardware engineers do not know what sensor specifications to buy, software developers cannot control nurse behavior, and QA testers cannot write automated test cases for human compliance.  
  (c) **Surgical Subsystem Allocation:**  
  - `REQ-HW-BLD-01` *(Hardware):* Each blood transit cooler shall incorporate an internal digital temperature datalogger that samples internal thermal conditions every 60 seconds across the range of $+1.0\ ^\circ\text{C}$ to $+10.0\ ^\circ\text{C}$ with $\pm 0.2\ ^\circ\text{C}$ accuracy.  
  - `REQ-SW-BLD-01` *(Software):* Upon receiving cooler telemetry via Bluetooth/cellular gateway, the blood management software shall record the temperature log and flag any blood bag exposed to temperatures $> +6.0\ ^\circ\text{C}$ for $> 30$ cumulative minutes as "Spoiled / Quarantine" within 3.0 seconds.  
  - `REQ-OPS-BLD-01` *(Human Role):* Transfusion nurses shall scan the patient ID wristband and verify patient blood group compatibility on the mobile bedside scanner prior to initiating blood transfusion.  
- **Marking Scheme:**  
  - 1 mark for identifying Subsystem Allocation violation.  
  - 1 mark for explaining hardware vs. software vs. human accountability boundaries.  
  - 2 marks for three properly allocated requirements with explicit IDs (`REQ-HW-BLD-01`, `REQ-SW-BLD-01`, `REQ-OPS-BLD-01`) and `SHALL`.  
- **Common Mistake Warning:** Assigning the nurse's clinical verification to the software subsystem.

