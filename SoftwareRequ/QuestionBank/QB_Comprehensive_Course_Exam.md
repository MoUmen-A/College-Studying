# Question Bank: Comprehensive Course Mock Examination

> **Subject:** Software Requirements Engineering  
> **Chapter:** Comprehensive Course Review (Chapters 1, 2, and 3)  
> **Total Marks:** 50 | **Questions:** 18  
> **Instructions:** Answer all questions. Write in full sentences. Partial marks are awarded for correct reasoning even if the final answer is incomplete.

---

## 🎓 Examinee Strategic Briefing: How to Solve & Critical Pitfalls to Avoid

Before attempting this comprehensive course mock examination, review this master roadmap to guide your problem-solving across all three chapters:

### 1. How to Approach Each Section:
- **Section A (Defect Diagnosis & Surgical Rewrite):**
  - **Identify Multi-Taxonomy Defects:** Look for combinations of weak modals ("should"), subjective adverbs ("quickly"), aesthetic terms ("attractive"), and compound concerns.
  - **Domain & Compliance Mandates:** In library systems, remember the *delete-on-print* digital copyright rule; in hospital systems, remember the *physical smart-card authentication* policy.
  - **Normative Rewrites:** Every rewritten functional requirement must use unique ID `FR-XXX-01`, RFC 2119 `SHALL`, and quantifiable thresholds.
- **Section B (Conceptual Discrimination):**
  - **Validation vs. Verification:** Cite the Standish Group study to explain how bug-free code matching a flawed SRS causes complete commercial failure.
  - **The 4 Requirement Levels:** Clearly distinguish *User Requirements* (what users need) from *Functional Requirements* (what code does), *NFRs* (quality constraints), and *System Requirements* (how architecture is built).
  - **Scope Models:** Articulate why an Ecosystem Map is essential for revealing indirect system dependencies that a Context Diagram hides.
  - **Business Rules:** Explain why embedding enterprise rules in user stories creates severe code maintenance and synchronization disasters.
- **Section C (Elicitation & Technique Strategy):**
  - **Tacit Knowledge:** Recommend **Observation** and explain how habituation overcomes the **Hawthorne Effect**.
  - **Scale vs. Depth:** Select **Surveys** for large global populations and pair with **Focus Groups** for deeper qualitative clarification.
  - **Disputes:** Recommend **Requirements Workshops** and emphasize the mandatory attendance of authorized project sponsors.
  - **Reactive Safety Systems:** Choose **State-Transition Tables** to mathematically guarantee no invalid or unreachable states exist.
- **Section D (Artifact Construction):**
  - **6-Clause Vision Statement:** Strictly adhere to the standard template (*For... Who... The... That... Unlike... Our product...*).
  - **Event Catalog:** Define all 3 categories (Business, Temporal, Signal) with concrete triggers and system reactions.
  - **Quality Inspection Checklist:** Formulate objective diagnostic rules for Completeness, Modifiability, and Feasibility.
- **Section E (Case Study Analysis):**
  - Link sequential renumbering to the destruction of persistent traceability and automated regression testing.
  - Trace the clinic search breakdown to imprecision in natural language.
  - Trace banking regulatory penalties to the failure of internal verification to evaluate external statutory truth.

### 2. Top Cognitive Traps to Avoid:
1. ❌ **Trap 1: Believing 100% Test Pass Rates Guarantee Software Acceptance.** If requirements are incomplete or invalid, verified software is rejected upon delivery.
2. ❌ **Trap 2: Renumbering Requirements.** Renumbering destroys bidirectional traceability and breaks automated test mapping.
3. ❌ **Trap 3: Vague Rewrites.** Never replace an ambiguous word with another ambiguous word; provide measurable numbers, tables, and time thresholds.

---

## SECTION A — Defect Diagnosis & Surgical Rewrite [15 marks | 4 questions]

### Question 1 (3 marks)
Consider the following requirement drafted for a hospital triage workflow:  
*"The medical records software should search patient records quickly and display clinical charts in an attractive visual format."*  
(a) Identify all quality defects by name across the taxonomy learned in Chapters 1 and 3.  
(b) Explain why subjective adverbs ("quickly") and aesthetic descriptions ("attractive") prevent automated software verification.  
(c) Surgically rewrite this statement into two atomic, verifiable requirements (`FR-MED-01` and `NFR-MED-01`) using RFC 2119 `SHALL` syntax and quantifiable thresholds.

### Question 2 (4 marks)
Review this requirement written for the Chemical Tracking System:  
*"Chemist enters an order, the system checks EPA compliance and inventory levels, and notifies the stockroom immediately."*  
(a) Analyze the structural defects of this requirement with respect to **Atomicity**, **Event Types**, and **Subsystem Boundaries**.  
(b) Explain how conflating human business events with automated background validations complicates traceability and unit testing.  
(c) Surgically rewrite this statement into two distinct, atomic functional requirements (`FR-CTS-10` and `FR-CTS-11`).

### Question 3 (4 marks)
A junior analyst drafted the following requirement for an academic library database:  
*"The library document store must be safe, comply with all international copyright standards, and delete files appropriately."*  
(a) Identify the quality defects and explain why generalist software engineers cannot implement "delete files appropriately" without explicit domain knowledge.  
(b) Identify the specific **Domain Requirement** rule governing licensed document deletion established in Chapter 1.  
(c) Surgically rewrite this requirement (`FR-LIB-20`) incorporating the explicit delete-on-print domain mandate from the lecture.

### Question 4 (4 marks)
Review the following draft specification regarding system access:  
*"Requirement 2.1: Clinic staff shall log into the application using their employee ID numbers."*  
*"Requirement 7.4: Clinic staff must authenticate using their physical health authority smart identity card."*  
(a) Identify the quality defect and classify the NFR category of Requirement 7.4.  
(b) What architectural and user-interface conflicts occur if developers implement both requirements simultaneously?  
(c) Surgically rewrite these statements into a single, unified requirement (`NFR-AUTH-01`) that resolves the conflict and adheres to corporate policy.

---

## SECTION B — Conceptual Discrimination [10 marks | 4 questions]

### Question 5 (2.5 marks)
Compare and contrast **Requirements Validation** with **Requirements Verification**. Use the Standish Group study findings to explain why a software project that achieves 100% verification test pass rates can still be an absolute commercial failure.

### Question 6 (2.5 marks)
Differentiate between **User Requirements**, **Functional Requirements**, and **Non-Functional Requirements (NFRs)**. Provide one clear example of each from the Medical Health Care – Patient Management System (MHC-PMS) case study.

### Question 7 (2.5 marks)
Contrast an **Ecosystem Map** with a **Context Diagram**. Why is a Context Diagram insufficient when designing an enterprise system that depends on data from external third-party compliance hubs and legacy databases through intermediate batch processors?

### Question 8 (2.5 marks)
Explain why **Business Rules** must be recorded and cataloged separately from software user stories and functional requirements. What long-term maintenance disaster occurs when business rules are embedded directly inside application code?

---

## SECTION C — Elicitation & Technique Strategy [10 marks | 4 questions]

### Question 9 (2.5 marks)
An analyst needs to uncover undocumented, routine habits and manual shortcuts practiced by laboratory technicians that do not appear in official operating manuals.  
(a) Which elicitation technique is specifically designed to uncover this **tacit knowledge**?  
(b) What psychological phenomenon (the Hawthorne Effect) can distort the data gathered, and how should the analyst mitigate it?

### Question 10 (2.5 marks)
A university project must gather software requirements from 5,000 alumni across 30 countries within a 2-week timeframe.  
(a) Which elicitation technique must be selected and why?  
(b) What are the major inherent weaknesses of this technique regarding requirement clarification?  
(c) What complementary technique should be deployed to follow up on ambiguous findings?

### Question 11 (2.5 marks)
Two executive stakeholders—the Chief Financial Officer and the Chief Medical Officer—vehemently disagree on the mandatory approval hierarchy for expensive clinical purchases.  
(a) Which elicitation technique is best suited to resolve this political impasse and achieve cross-departmental consensus rapidly?  
(b) What critical success factor must be present during this session to prevent total deadlock?

### Question 12 (2.5 marks)
The development team is tasked with building a complex, state-dependent automated chemical reactor that transitions through *Idle*, *Synthesizing*, *Emergency Purge*, and *Maintenance* states.  
(a) Which Requirements Analysis modeling technique must be utilized?  
(b) Why is natural language prose strictly forbidden for specifying complex, safety-critical state transitions?

---

## SECTION D — Artifact Construction [10 marks | 3 questions]

### Question 13 (4 marks)
Construct the complete **Standard 6-Clause Vision Statement** for the **Chemical Tracking System (CTS)** conforming strictly to the formal template and business goals presented in the lecture.

### Question 14 (3 marks)
Construct an **Event Catalog (Event List)** containing three distinct event triggers for the MHC-PMS:  
1. One **Business / User Event**  
2. One **Temporal Event**  
3. One **Signal Event**  
For each entry, define the event trigger and state the system's explicit automated reaction.

### Question 15 (3 marks)
Construct a **Requirements Quality Inspection Checklist** defining the diagnostic rules for verifying:  
(a) Completeness ("no more, no less")  
(b) Modifiability  
(c) Feasibility  
Provide one concrete inspection test question for each.

---

## SECTION E — Case Study Analysis [5 marks | 3 questions]

### Question 16 (1.5 marks)
*Mini-Case A:* An enterprise engineering team sequentially numbered requirements in their SRS as `Req 1` through `Req 300`. Mid-project, twenty requirements were deleted from Section 2, and the analyst renumbered all subsequent requirements from `Req 21` onward. Two weeks later, system integration testing collapsed and traceability was lost.  
(a) What specification activity was violated?  
(b) Explain why renumbering requirements caused catastrophic failure in regression testing.  
(c) What naming convention prevents this failure?

### Question 17 (1.5 marks)
*Mini-Case B:* A hospital clinic deployed a patient scheduling application where developers implemented the search feature by requiring operators to select a specific clinic branch from a drop-down list before querying patient names. When triage nurses attempted to locate an emergency patient who had an appointment at an unknown clinic branch, they had to repeat the search manually across 20 distinct clinics, wasting 15 critical minutes.  
(a) What Requirements Engineering flaw caused this operational failure?  
(b) Contrast the user intention with the developer interpretation that led to this gap.  
(c) State the rule of requirements specification that prevents this communication breakdown.

### Question 18 (2 marks)
*Mini-Case C:* A commercial banking platform was built specifying that interest on enterprise deposits would be compounded monthly. Six months after deployment, federal banking regulators audited the institution, levied an \$8.5 million penalty, and forced the bank to restate its financial reports because federal statutes legally mandate daily compounding for that deposit tier.  
(a) What requirements quality characteristic was violated in the SRS?  
(b) Why did this defect escape internal QA verification testing?  
(c) How does this demonstrate the boundary between Verification and Validation?

---

# GUIDE ANSWERS & MARKING SCHEME

### Question 1 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Weak Modal Verb:* "Should" expresses an optional preference rather than a mandatory requirement.  
  2. *Subjective Adverb:* "Quickly" is unmeasurable and non-verifiable.  
  3. *Subjective Aesthetic Term:* "Attractive visual format" cannot be objectively evaluated with a pass/fail test.  
  4. *Compound Requirement:* Combines back-end data search performance with front-end UI presentation formatting.  
  (b) **Explanation:** Test engineers cannot write deterministic assertions for subjective terms like "quickly" or "attractive". What is attractive to one doctor may be deemed cluttered and illegible by another.  
  (c) **Surgical Rewrite:**  
  - `FR-MED-01:` The system shall allow authorized clinical staff to search patient medical records by National Patient ID, returning matching search results within 1.5 seconds.  
  - `NFR-MED-01:` The user interface shall display clinical charts in tabular and SVG graphical formats conforming strictly to the Hospital UI Design Standard `HDS-v4.2`.  
- **Marking Scheme:**  
  - 1 mark for identifying defects (modal "should", unmeasured "quickly", aesthetic "attractive", compound nature).  
  - 1 mark for explaining testability/verification failure.  
  - 1 mark for decomposing into `FR-MED-01` and `NFR-MED-01` with `SHALL` and measurable criteria.  
- **Common Mistake Warning:** Merging both rewritten requirements into one sentence connected by "and".

### Question 2 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Violation of Atomicity:* Merges user order entry, business rule compliance checking, inventory verification, and stockroom notification into one complex sentence.  
  2. *Conflation of Event Types:* Mixes a human business event ("Chemist enters order") with automated internal system validations and external notifications.  
  3. *Unverifiable Adverb:* "Immediately" is non-verifiable without an explicit latency limit.  
  (b) **Explanation:** Compound requirements obscure traceability. If inventory checking succeeds but stockroom notification fails, the requirement cannot be clearly marked as passed or failed in test management tools.  
  (c) **Surgical Rewrite:**  
  - `FR-CTS-10:` When an order is submitted, the system shall validate the requested chemical container against current EPA regulatory threshold limits and available inventory within 2.0 seconds.  
  - `FR-CTS-11:` Upon successful validation of a chemical request, the system shall automatically transmit an electronic fulfillment notification to the chemical stockroom dispatcher queue.  
- **Marking Scheme:**  
  - 1.5 marks for identifying atomicity, event conflation, and vague adverb "immediately".  
  - 1 mark for explaining traceability and testing complications.  
  - 1.5 marks for two atomic, verifiable requirements (`FR-CTS-10`, `FR-CTS-11`) with `SHALL`.  
- **Common Mistake Warning:** Forgetting to specify the timing threshold or system reaction in the rewritten requirements.

### Question 3 Guide Answer
- **Model Answer:**  
  (a) **Defects & Generalist Gap:** "Safe," "comply with all international copyright standards," and "delete files appropriately" are non-verifiable buzzwords. Software engineers lack specialized knowledge of international intellectual property law and cannot deduce what "appropriately" means without explicit domain specifications.  
  (b) **Specific Domain Requirement Rule:** The lecture explicitly states: *"To comply with international digital copyright legislation, specific classes of imported licensed documents must be automatically deleted on arrival or printed directly to a network server with no local electronic copy saved."*  
  (c) **Surgical Rewrite:**  
  `FR-LIB-20:` The system shall automatically route incoming licensed digital documents marked as copyright-restricted directly to the designated secure network print spooler and permanently purge all local electronic copies and temporary cache files within 5.0 seconds of print completion.  
- **Marking Scheme:**  
  - 1 mark for identifying vague buzzwords and the generalist software engineer domain gap.  
  - 1.5 marks for citing the delete-on-print/no-local-copy domain rule from the lecture.  
  - 1.5 marks for rewrite with ID `FR-LIB-20`, `SHALL`, and explicit automated purge behavior.  
- **Common Mistake Warning:** Writing a generic password authentication requirement instead of the delete-on-print domain mandate.

### Question 4 Guide Answer
- **Model Answer:**  
  (a) **Defects & Taxonomy:** Violates **Consistency** (two requirements describe conflicting authentication mechanisms). Requirement 7.4 is an **Organizational Non-Functional Requirement** (governing employee physical identity authentication standards).  
  (b) **Architectural & UI Conflicts:** If developers implement both, the login screen will display a standard employee ID keyboard input form while another team installs physical smart card reader drivers. Users will be uncertain whether typing an ID is sufficient or if the smart card is mandatory, causing authentication bypasses or login failures.  
  (c) **Surgical Rewrite:**  
  `NFR-AUTH-01:` Clinic staff shall authenticate into the system by inserting their physical health authority smart identity card into the workstation card reader, with the system verifying the card's 8-digit employee identifier within 1.0 second.  
- **Marking Scheme:**  
  - 1 mark for identifying Consistency violation and classifying Req 7.4 as an Organizational NFR.  
  - 1.5 marks for analyzing UI/architectural divergence and security bypass risks.  
  - 1.5 marks for unified rewrite (`NFR-AUTH-01`) enforcing smart card policy with `SHALL`.  
- **Common Mistake Warning:** Classifying physical smart card login as an External Requirement.

### Question 5 Guide Answer
- **Model Answer:**  
  - **Validation ("Building the right product"):** Confirms that requirements accurately capture true stakeholder operational needs, business objectives, and environmental constraints.  
  - **Verification ("Building the product right"):** Confirms that the requirements documents and software deliverables meet formal engineering quality standards, templates, syntactic rules, and testable specifications.  
  - **Why 100% Verification Can Still Equal Failure:** A software team can deliver code that passes 100% of unit and integration test cases with zero bugs because the code perfectly matches the written SRS (100% verified). However, if the SRS omitted essential daily workflows (Standish Group: 12.3% project failures caused by incomplete requirements), or specified an incorrect business rule, the delivered software is completely useless to end-users (failed validation).  
- **Marking Scheme:**  
  - 1 mark for contrasting "right product" vs. "product right".  
  - 1.5 marks for explaining how a bug-free system built to an incorrect/incomplete specification results in complete project failure.  
- **Common Mistake Warning:** Calling verification the customer review process.

### Question 6 Guide Answer
- **Model Answer:**  
  - **User Requirements:** High-level natural language statements describing what tasks users need to accomplish.  
    - *MHC-PMS Example:* "A clinic nurse needs to view all upcoming patient appointments for the day."  
  - **Functional Requirements:** Concrete technical statements of system services, inputs, behaviors, and outputs.  
    - *MHC-PMS Example:* `R-2:` "The system shall automatically generate a daily appointment manifest for each clinic every morning at 06:00."  
  - **Non-Functional Requirements (NFRs):** System-wide constraints on behavioral quality, operational environment, or performance.  
    - *MHC-PMS Example:* "Total downtime during working hours (Mon–Fri, 08:30–17:30) shall not exceed 5 seconds per day."  
- **Marking Scheme:**  
  - 1 mark for defining the three levels.  
  - 1.5 marks (0.5 each) for accurate MHC-PMS examples from the lecture.  
- **Common Mistake Warning:** Giving a non-functional requirement when asked for a functional requirement.

### Question 7 Guide Answer
- **Model Answer:**  
  - **Context Diagram:** A DFD Level 0 diagram that defines the immediate boundary of the system under development, showing direct data/control flows between the central system process bubble and external entities (terminators).  
  - **Ecosystem Map:** An enterprise architectural model depicting all participating systems in the broader solution environment that exchange data or are affected, **including systems that have no direct interface with the new software**.  
  - **Why Context Diagram is Insufficient:** If the new software relies on a central corporate database that receives daily batch updates from third-party regulatory hubs and external vendor catalogs via intermediate message queues, a Context Diagram will only show the central database bubble. It completely obscures the external dependencies, timing constraints, and failure modes of the upstream feeder systems. An Ecosystem Map makes these critical indirect relationships visible.  
- **Marking Scheme:**  
  - 1 mark for defining Context Diagram and Ecosystem Map.  
  - 1.5 marks for explaining how intermediate batch feeds and indirect interfaces create blindspots on a Context Diagram.  
- **Common Mistake Warning:** Stating that an Ecosystem Map shows source code modules.

### Question 8 Guide Answer
- **Model Answer:**  
  - **Definition & Separation:** Business rules are enterprise-level policies, statutory tax codes, regulatory formulas, and operational guidelines that exist independent of any single software system. They must be cataloged in an enterprise repository with unique identifiers (e.g., `BR-TAX-01`).  
  - **Long-Term Maintenance Disaster:** If business rules are embedded directly inside application source code and user stories, when a regulation or corporate policy changes (e.g., a 1% change in VAT tax rate or discount threshold), developers must hunt through hundreds of code files across multiple systems. Some instances are updated while others are missed, causing inconsistent business calculations, accounting discrepancies, and months of costly emergency refactoring.  
- **Marking Scheme:**  
  - 1 mark for defining business rules as enterprise assets.  
  - 1.5 marks for explaining the maintenance disaster (scattered code updates, inconsistencies, accounting errors).  
- **Common Mistake Warning:** Believing business rules belong exclusively inside the SRS functional specification.

### Question 9 Guide Answer
- **Model Answer:**  
  (a) **Elicitation Technique:** **Observation** (passive job shadowing / fly-on-the-wall observation). It captures tacit knowledge—instinctive shortcuts and workarounds that users perform automatically but forget to articulate during interviews.  
  (b) **Hawthorne Effect & Mitigation:**  
  - *Phenomenon:* People unnaturally alter their normal daily behavior when they know they are being observed, rigidly following official manuals and hiding their real shortcuts.  
  - *Mitigation:* The analyst must conduct extended observations over multiple days to let subjects habituate, use unobtrusive observation, and cross-validate observed actions against system transaction audit logs and output artifacts.  
- **Marking Scheme:**  
  - 1 mark for naming Observation and tacit knowledge.  
  - 1 mark for defining the Hawthorne Effect.  
  - 0.5 marks for mitigation strategies (habituation, artifact cross-checking).  
- **Common Mistake Warning:** Suggesting interviews as the best tool to find tacit knowledge.

### Question 10 Guide Answer
- **Model Answer:**  
  (a) **Elicitation Technique:** **Surveys / Questionnaires**. It is the only feasible technique capable of gathering quantitative feedback from 5,000 geographically dispersed users across 30 countries within two weeks at low cost.  
  (b) **Major Inherent Weaknesses:** Inability to ask interactive follow-up questions, inability to clarify ambiguous responses, and typically low response rates.  
  (c) **Complementary Technique:** **Focus Groups** or targeted **Interviews** with representative subsets of respondents to explore surprising statistical trends or ambiguous survey responses.  
- **Marking Scheme:**  
  - 1 mark for selecting Surveys/Questionnaires with justification.  
  - 1 mark for explaining inability to ask follow-up questions and clarify ambiguity.  
  - 0.5 marks for pairing with Focus Groups or Interviews.  
- **Common Mistake Warning:** Proposing one-on-one interviews for all 5,000 alumni.

### Question 11 Guide Answer
- **Model Answer:**  
  (a) **Elicitation Technique:** **Requirements Workshops** (facilitated cross-functional working sessions). It brings opposing stakeholders together in a structured, moderated environment to negotiate trade-offs and achieve alignment rapidly.  
  (b) **Critical Success Factor:** The presence of a **skilled, neutral facilitator** and the mandatory attendance of the **authorized decision-makers (project sponsors)** with the formal authority to make final binding decisions. If key decision-makers are absent, the workshop ends in deadlock.  
- **Marking Scheme:**  
  - 1.5 marks for identifying Requirements Workshops and cross-functional alignment value.  
  - 1 mark for identifying a neutral facilitator and mandatory presence of authorized decision-makers.  
- **Common Mistake Warning:** Recommending Brainstorming; brainstorming does not resolve disputes or establish binding policy.

### Question 12 Guide Answer
- **Model Answer:**  
  (a) **Analysis Modeling Technique:** **State-Transition Diagram (STD)** or **State Table**.  
  (b) **Why Natural Language is Forbidden:** Natural language prose is inherently sequential and ambiguous. In a safety-critical reactor system, prose descriptions easily omit invalid state transitions (e.g., transitioning directly from *Maintenance* to *Synthesizing* without passing through *Idle* self-tests), creating catastrophic safety hazards. State tables provide an exhaustive mathematical matrix of every state against every event, guaranteeing that all valid, invalid, and error transitions are explicitly engineered.  
- **Marking Scheme:**  
  - 1 mark for State-Transition Diagram / State Table.  
  - 1.5 marks for explaining safety risks, omitted transitions, and the exhaustive verification guarantee of state tables.  
- **Common Mistake Warning:** Suggesting a Data Flow Diagram (DFD).

### Question 13 Guide Answer
- **Model Answer:**  
  ```
  +----------------------------------------------------------------------------------------------------+
  |                           CHEMICAL TRACKING SYSTEM VISION STATEMENT                                |
  +----------------------------------------------------------------------------------------------------+
  | For:          Scientists who need to request containers of chemicals,                              |
  | Who:          Need to quickly search inventories and track container usage across labs,           |
  | The:          Chemical Tracking System is an information system                                    |
  | That:         Will provide a single point of access to the chemical stockroom and to vendors,      |
  |               storing the location of every chemical container, quantity remaining, and complete   |
  |               usage history, saving 25% on chemical costs in the first year.                      |
  | Unlike:       Current manual ordering processes,                                                   |
  | Our product:  Will automatically generate all federal and state government compliance reports for  |
  |               chemical storage and hazardous disposal.                                             |
  +----------------------------------------------------------------------------------------------------+
  ```  
- **Marking Scheme:**  
  - 4 marks total: ~0.65 marks per clause correctly completed following the lecture template.  
- **Common Mistake Warning:** Omitting the "Unlike" or "Our product" clauses.

### Question 14 Guide Answer
- **Model Answer:**  
  **MHC-PMS Event Catalog Artifact:**  
  1. **Business / User Event:**  
     - *Trigger:* A clinic receptionist enters a patient's national ID and clicks "Book Appointment".  
     - *System Reaction:* The system verifies doctor availability, creates the appointment record, and displays a confirmation number.  
  2. **Temporal Event:**  
     - *Trigger:* The system clock reaches 06:00 every morning.  
     - *System Reaction:* The system automatically generates a daily appointment manifest for each hospital clinic and prints it to the clinic desk spooler.  
  3. **Signal Event:**  
     - *Trigger:* A clinic nurse scans their physical 8-digit health authority employee badge across an optical/RFID reader.  
     - *System Reaction:* The hardware reader sends an interrupt signal to the terminal software, which authenticates the badge and unlocks the triage screen.  
- **Marking Scheme:**  
  - 1 mark for Business Event (trigger + reaction).  
  - 1 mark for Temporal Event (06:00 manifest trigger + reaction).  
  - 1 mark for Signal Event (badge scan trigger + reaction).  
- **Common Mistake Warning:** Describing a user clicking a button as a temporal event.

### Question 15 Guide Answer
- **Model Answer:**  
  **Requirements Quality Inspection Checklist Artifact:**  
  (a) **Completeness ("No More, No Less"):**  
  - *Inspection Test Question:* Does the requirement explicitly define all inputs, boundary limits, error recovery behaviors, and exception handling paths without including extraneous design constraints or unrequested features?  
  (b) **Modifiability:**  
  - *Inspection Test Question:* Does the requirement carry a persistent, unique alphanumeric identifier, and is it documented atomically in exactly one location in the SRS rather than duplicated across sections?  
  (c) **Feasibility:**  
  - *Inspection Test Question:* Is the requirement technically achievable within the known constraints of the target hardware architecture, network bandwidth, available team competencies, approved budget, and project schedule?  
- **Marking Scheme:**  
  - 1 mark for Completeness rule.  
  - 1 mark for Modifiability rule.  
  - 1 mark for Feasibility rule.  
- **Common Mistake Warning:** Writing subjective questions like "Is the requirement well written?".

### Question 16 Guide Answer
- **Model Answer:**  
  (a) **Specification Activity Violated:** **Uniquely Label Each Requirement** (Activity 3 of Requirements Specification).  
  (b) **Why Renumbering Caused Collapse:** Renumbering destroys **persistent identification**. All downstream assets—test suites, traceability matrices (RTM), architecture documents, and bug tracking tickets—reference requirements by their assigned IDs. When numbers shifted, test scripts designed to test `Req 45` were executed against completely different functionality, causing massive false regression failures and complete loss of traceability.  
  (c) **Naming Convention:** Use stable, hierarchical alphanumeric identifiers with functional prefixes (e.g., `REQ-CHEM-ORD-042`). When a requirement is removed, its identifier is marked as "Obsolete / Retired", and new requirements are appended with new incremental numbers without renumbering existing items.  
- **Marking Scheme:**  
  - 0.5 marks for identifying Uniquely Label Each Requirement.  
  - 0.5 marks for explaining the collapse of persistent traceability links and test mapping.  
  - 0.5 marks for specifying stable alphanumeric prefix conventions and ID retirement.  
- **Common Mistake Warning:** Claiming that renumbering is an acceptable practice.

### Question 17 Guide Answer
- **Model Answer:**  
  (a) **Requirements Flaw:** **Imprecision and Ambiguity** in the specification, combined with a lack of validation between business analysts, users, and developers.  
  (b) **User Intention vs. Developer Interpretation:**  
  - *User Intention:* The user intended to enter a patient name into a single search box and have the system scan all clinics across the hospital network simultaneously.  
  - *Developer Interpretation:* The developer assumed a two-stage input sequence: select a specific clinic dropdown first, then query only the selected clinic's records.  
  (c) **Specification Rule:** The rule of **Unambiguity and Completeness** — requirements must explicitly state the operational scope, inputs, default values, and search domain so that only one single technical interpretation exists.  
- **Marking Scheme:**  
  - 0.5 marks for identifying imprecision and ambiguity.  
  - 0.5 marks for clearly contrasting the multi-clinic intention with the dropdown-per-clinic interpretation.  
  - 0.5 marks for stating the completeness/unambiguity specification rule.  
- **Common Mistake Warning:** Blaming the developer for writing buggy code instead of recognizing that the requirement itself was ambiguous.

### Question 18 Guide Answer
- **Model Answer:**  
  (a) **Quality Characteristic Violated:** **Correctness** (the requirement did not accurately represent an authorized, legally valid capability).  
  (b) **Why Internal QA Tests Failed to Catch It:** Internal QA test cases only verify that the software behaves according to the written SRS. Because the SRS specified monthly compounding, QA authored unit tests expecting monthly calculation and marked them `PASS`. The system was "built right" (verified), but was the "wrong product" (invalid).  
  (c) **Boundary Between Verification and Validation:**  
  - *Verification* confirmed that the code matched the written specification (monthly interest ran without bugs).  
  - *Validation* failed because nobody checked the specification against external statutory banking regulations (daily compounding legal mandate). Validation evaluates correctness against the external world, whereas Verification evaluates consistency against internal documents.  
- **Marking Scheme:**  
  - 0.5 marks for identifying Correctness.  
  - 0.5 marks for explaining why QA pass/fail tests cannot detect specification errors.  
  - 1 mark for explaining the external legal boundary of Validation vs. internal document boundary of Verification.  
- **Common Mistake Warning:** Confusing verification failure with validation failure.

