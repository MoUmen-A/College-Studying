# Exam 01: True/False, Essay & Applied Cases (Foundations & Elicitation)

> **Subject:** Software Requirements Engineering  
> **Coverage:** Chapter 1 (Fundamentals) & Chapter 2 (Requirements Elicitation)  
> **Total Marks:** 50 | **Time Allowed:** 90 Minutes  
> **Instructions:** Answer all questions in full sentences. For True/False questions, you must provide a concise technical justification; correct identification without justification earns only partial credit.

---

## 🎓 Examinee Strategic Briefing: How to Solve & Critical Pitfalls to Avoid

Before attempting this exam, review this mental roadmap to guide your problem-solving and prevent common errors:

### 1. How to Approach Each Section:
- **Section 1 (True / False):**
  - **Look for Universal Absolutes:** Words like "guaranteed", "synonymous", "identical across all", or "always" almost always signal a conceptual flaw.
  - **The NFR Trap:** Always remember that a system can have zero functional bugs and still be 100% useless if it fails an NFR (e.g., latency, safety, uptime).
  - **Taxonomy Boundaries:** Distinguish *Internal Corporate Policies* (Organizational NFRs) from *External Statutory Laws* (External NFRs). Just because an enterprise obeys a statutory law does not make it an organizational requirement!
- **Section 2 (Essays):**
  - When comparing techniques (e.g., Observation vs. Workshops), organize your answer along structured axes: *Objective*, *Knowledge Type (Explicit vs. Tacit)*, *Cost/Effort*, and *Primary Failure Mode*.
  - When analyzing the SDLC Analysis phase, always use the 3-step sequence: *As-Is $\rightarrow$ Improvements $\rightarrow$ To-Be*.
- **Section 3 (Business Goals & Metrics):**
  - **Problem:** State the negative current baseline (financial loss, latency, error rate).
  - **Business Objective:** State the high-level business improvement target (e.g., "Reduce X by Y% within timeframe Z"). *Never* write software features here!
  - **Success Metric:** State a measurable operational criterion tracked during testing/production (e.g., "Order time $\le 10$ minutes on 80% of orders").
  - **Vision Statement:** Strictly write all 6 clauses in order: *For... Who... The... That... Unlike... Our product...*.
- **Section 4 (Requirements Issues & Surgical Rewrites):**
  - **Spot Defects:** Highlight vague adjectives ("fast", "user-friendly", "reasonable", "appropriate") and weak modals ("should", "might").
  - **Rewrite Blueprint:** Always format as: `[ID] The system SHALL [action] [quantifiable metric] [operational context/trigger]`.

### 2. Top Cognitive Traps to Avoid:
1. ❌ **Trap 1: Confusing Tacit Knowledge with the Hawthorne Effect.** Tacit knowledge is unarticulated instinctual skill; the Hawthorne Effect is *deliberate/subconscious behavior change when watched*.
2. ❌ **Trap 2: Confusing Context Diagrams with Ecosystem Maps.** Context diagrams show *direct terminators only*; Ecosystem maps reveal the *entire interconnected landscape including indirect systems*.
3. ❌ **Trap 3: Rewriting with another ambiguous word.** Changing "search fast" to "search very fast within a short time" earns 0 marks for rewrite. Use concrete metrics like "within 1.5 seconds".

---

## SECTION 1 — True or False with Justification [12 marks | 6 questions]

### Question 1 (2 marks)
*Statement:* If a software system satisfies 100% of its documented functional requirements with zero coding defects, it is guaranteed to be acceptable and operational in production.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 2 (2 marks)
*Statement:* Requirements Elicitation and Requirements Development are synonymous terms in Requirements Engineering.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 3 (2 marks)
*Statement:* In the Requirements Engineering taxonomy, a statutory healthcare privacy regulation (such as `HStan-03-2006-priv`) is classified as an Organizational Non-Functional Requirement because the organization must implement it.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 4 (2 marks)
*Statement:* A Context Diagram and an Ecosystem Map represent the exact same system boundary, with the Ecosystem Map merely using different visual icons.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 5 (2 marks)
*Statement:* The Hawthorne Effect describes a situation where users cannot articulate tacit knowledge during an interview because they perform tasks unconsciously.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 6 (2 marks)
*Statement:* In domain requirements engineering, the calibration constant $\frac{9.81\ \text{m/s}^2}{\alpha}$ for train deceleration is a universal physical constant identical across all train classes.  
*(State True or False and provide a rigorous technical justification from the lecture).*

---

## SECTION 2 — Deep Essay & Analytical Synthesis [14 marks | 3 questions]

### Question 7 (5 marks)
Explain the architectural and operational relationships between the three sequential steps of the **Analysis Phase in the SDLC** (As-Is System, Improvements, To-Be System). In your essay, analyze how failing to thoroughly investigate the As-Is system leads to severe budget escalations and user rejection in the To-Be system, citing the Medical Health Care – Patient Management System (MHC-PMS) or Library Information System (LIBSYS).

### Question 8 (5 marks)
Compare and contrast **Passive Observation** and **Requirements Workshops** as elicitation techniques. Structure your comparison across: (a) primary objective, (b) type of knowledge uncovered (explicit vs. tacit), (c) cost and organizational coordination effort, and (d) the primary risk or failure mode of each technique.

### Question 9 (4 marks)
Analyze the role of **Negative Requirements** (explicit exclusions) in functional specifications. Why is defining what the system *shall not do* just as critical as defining what it *shall do*? Illustrate with the LIBSYS copyright/privacy constraints presented in Chapter 1.

---

## SECTION 3 — Case Study: Business Goals & Metrics [12 marks | 3 questions]

### Scenario Description
The regional health network operates a distributed pathology laboratory network. Currently, hospital clinics order specialized chemical reagents and test kits via handwritten requisition forms and faxes. Requisition orders take an average of 4 business days to fulfill, stockouts occur on 18% of routine tests, and \$450,000 worth of perishable reagents expire on shelf annually due to lack of batch traceability. The board has chartered the **Pathology Supply Tracking System (PSTS)** to modernize laboratory inventory and procurement.

### Question 10 (4 marks)
Extract and formally structure the core business foundations for this project:  
(a) State the primary **Business Problem** currently afflicting the health network.  
(b) Formulate two distinct, quantifiable **Business Objectives** for the PSTS project.  
(c) Formulate two concrete **Success Metrics** that can be objectively measured during post-deployment operational acceptance testing.

### Question 11 (4 marks)
Author a formal, standard **6-Clause Vision Statement** for the Pathology Supply Tracking System conforming strictly to the template taught in Chapter 2 (*For... Who... The... That... Unlike... Our product...*).

### Question 12 (4 marks)
Classify the following four stakeholders of the PSTS project into their precise taxonomy (**Primary Stakeholder**, **Secondary Stakeholder**, or **Key Stakeholder**) and justify each:  
1. *Chief Clinical Pathologist (authorizes departmental capital budget)*  
2. *Laboratory Technician (enters daily reagent draw requests at the bench)*  
3. *State Hazardous Bio-Waste Inspector (audits disposal logs annually)*  
4. *Central Hospital Procurement Officer (approves vendor purchase orders)*

---

## SECTION 4 — Case Study: Requirements Issues & Quality Diagnosis [12 marks | 3 questions]

### Scenario Description
During the initial review of the PSTS draft specification, the lead architect flags several problematic requirement statements authored by an entry-level analyst.

### Question 13 (4 marks)
*Draft Requirement 1:*  
*"The software should search laboratory inventory fast and notify technicians if chemicals are low."*  
(a) Identify all quality defects by name based on the lecture standards.  
(b) Explain why each defect undermines verification and testing.  
(c) Surgically rewrite this statement into two atomic, verifiable functional requirements (`FR-PST-01` and `FR-PST-02`) using RFC 2119 `SHALL` syntax and quantifiable thresholds.

### Question 14 (4 marks)
*Draft Requirement 2:*  
*"Technicians can look up reagents across clinics."*  
(a) Diagnose the imprecision and ambiguity hazard in this statement by contrasting the user intention with the developer interpretation (using the clinic search case from Chapter 1).  
(b) Explain the operational failure that occurs if developers implement a single-clinic dropdown instead of a global search.  
(c) Surgically rewrite the requirement (`FR-PST-03`) to eliminate the ambiguity completely.

### Question 15 (4 marks)
*Draft Requirement 3:*  
*"The PSTS system shall be reliable, secure, and conform to all hospital privacy laws with zero downtime."*  
(a) Identify the quality defects in this requirement (distinguish between untestable buzzwords and infeasible constraints).  
(b) Decompose and rewrite this into:  
   - One quantifiable Product NFR (`NFR-PST-01`) governing system availability and downtime threshold based on the lecture's working hours metric.  
   - One External NFR (`NFR-PST-02`) specifying statutory healthcare privacy compliance.

---

# GUIDE ANSWERS & MARKING SCHEME

### Question 1 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* A system can implement 100% of its functional requirements with zero bugs and still fail completely if it violates critical **Non-Functional Requirements (NFRs)**. For example, if a safety-critical flight control system executes mathematically perfect flight calculations (functional correctness) but suffers a 500 ms latency delay (NFR performance failure), the aircraft will crash. Similarly, an enterprise system that is too slow, crashes under load, or violates statutory privacy laws will be rejected by users and regulators despite functional perfection.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for technical justification referencing NFR failure / aircraft latency example.  
- **Common Mistake Warning:** Answering True, believing that functional requirements are all that define software correctness.

### Question 2 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* Requirements Elicitation is only the **first subdiscipline** of Requirements Development. Requirements Development consists of four sequential, iterative subdisciplines: (1) Requirements Elicitation, (2) Requirements Analysis, (3) Requirements Specification, and (4) Requirements Validation & Verification. Therefore, elicitation is a component of development, not its synonym.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for listing the 4 subdisciplines of Requirements Development.  
- **Common Mistake Warning:** Confusing Requirements Development with Requirements Management.

### Question 3 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* Statutory privacy regulations (such as `HStan-03-2006-priv` or GDPR) originate from external legislative, legal, and governmental bodies outside the organization's boundary. According to the NFR taxonomy in Chapter 1, they are classified as **External Requirements**, not Organizational Requirements. Organizational Requirements originate from *internal* corporate policies, internal software lifecycle standards (`XYZCo-SP-STAN-95`), or company-mandated development environments.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for distinguishing External (legislative/statutory) from Organizational (internal corporate policy/standards).  
- **Common Mistake Warning:** Thinking any rule followed by an organization is an "Organizational" requirement.

### Question 4 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* A Context Diagram and an Ecosystem Map have fundamentally different architectural scopes. A Context Diagram shows only the immediate system boundary, depicting direct data and control flows between the central system process and direct external terminators. An Ecosystem Map illustrates the broader enterprise landscape, including **participating systems that have no direct interface with the new product** but exchange data indirectly through intermediary databases, batch feeds, or message brokers.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for explaining direct terminators (Context) vs. direct + indirect participating systems (Ecosystem).  
- **Common Mistake Warning:** Believing an Ecosystem Map is just a graphical redesign of a Context Diagram.

### Question 5 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* The Hawthorne Effect describes the psychological phenomenon where individuals **alter their normal behavior and act unnaturally** (e.g., strictly adhering to official rules and hiding routine shortcuts) simply because they are aware of being actively observed. The inability of users to articulate unconscious habits during an interview is the definition of **tacit knowledge**, not the Hawthorne Effect.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for accurately defining the Hawthorne Effect (behavior modification due to observation) vs. tacit knowledge.  
- **Common Mistake Warning:** Mixing up tacit knowledge with the Hawthorne Effect.

### Question 6 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* While $9.81\ \text{m/s}^2$ is the universal gravitational acceleration constant, the factor $\alpha$ is related to train inertia, weight, and carriage friction. The lecture explicitly specifies that the calibrated values of $\frac{9.81\ \text{m/s}^2}{\alpha}$ are **determined dynamically based on the specific train class**.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for explaining that the ratio is calibrated dynamically per train class.  
- **Common Mistake Warning:** Assuming physical formulas contain only fixed universal constants.

### Question 7 Guide Answer
- **Model Answer:**  
  - **The Three Steps of the Analysis Phase:**  
    1. *Understand the As-Is System:* The analyst thoroughly models existing manual procedures, legacy software workflows, paperwork, and data flows to baseline current performance.  
    2. *Identify Improvements:* The team diagnoses operational pain points, calculation bottlenecks, manual redundancies, data entry errors, and lost business opportunities.  
    3. *Define the To-Be System:* The analyst specifies the target software's required functional capabilities, system integrations, and non-functional quality constraints.  
  - **Consequences of Skipping the As-Is Investigation:** If analysts jump straight to specifying the To-Be system without understanding the As-Is baseline, they miss critical undocumented manual workarounds and operational exceptions that current workers perform daily. When the To-Be system is deployed, it enforces rigid automated workflows that break real-world operations, leading to user rejection, emergency change requests, and 10x–100x cost escalations during production.  
  - *Lecture Case Application:* In MHC-PMS/LIBSYS, failure to analyze how staff currently query records across clinic branches or library collections leads developers to build single-clinic silos that paralyze daily operations.  
- **Marking Scheme:**  
  - 1.5 marks for detailing the 3 steps in exact chronological sequence.  
  - 2 marks for analyzing the failure to investigate As-Is workflows (omitted workarounds, downstream rework, rejection).  
  - 1.5 marks for grounding the analysis in the lecture case studies.  
- **Common Mistake Warning:** Treating the 3 steps as generic SDLC phases (Analysis, Design, Coding) rather than the internal steps of the Analysis Phase.

### Question 8 Guide Answer
- **Model Answer:**  
  | Dimension | Passive Observation | Requirements Workshops |
  | :--- | :--- | :--- |
  | **(a) Primary Objective** | Capture real-world workflows, daily procedures, and baseline tasks as they actually occur in the operational workplace. | Bring cross-functional stakeholders together in an intensive, short-duration session to hammer out scope, resolve conflicts, and reach consensus. |
  | **(b) Knowledge Type** | **Tacit Knowledge:** Uncovers unwritten habits, instinctual workarounds, and subconscious steps that users fail to articulate verbally. | **Explicit & Negotiated Knowledge:** Unearths declared business goals, policy rules, and negotiated feature priorities. |
  | **(c) Cost & Coordination** | Moderate cost; involves low scheduling friction (shadowing one worker), but consumes extensive analyst time. | High cost; requires intensive logistical coordination to bring executives, department heads, and analysts together for days. |
  | **(d) Primary Risk / Failure** | **The Hawthorne Effect:** Workers alter their behavior when watched, following rules unnaturally and concealing true shortcuts. | **Absence of Key Decision-Makers:** If authorized sponsors miss the session, or if facilitation is weak, the workshop degenerates into deadlocks with zero consensus. |  
- **Marking Scheme:** 1.25 marks per dimension (a, b, c, d) accurately evaluated for both techniques. Total = 5 marks.  
- **Common Mistake Warning:** Failing to identify "tacit knowledge" as the core strength of observation.

### Question 9 Guide Answer
- **Model Answer:**  
  - **Role of Negative Requirements:** Functional specifications written in natural language often leave implicit assumptions unstated. Software engineers naturally build what is technologically easiest or most feature-rich unless explicitly constrained. Negative requirements explicitly define system boundaries, legal prohibitions, and security limits by specifying what the system **shall not do**.  
  - **Why Critical:** Negative requirements eliminate developer guesswork, prevent unauthorized feature creep ("gold-plating"), prevent data leaks, and guarantee compliance with statutory privacy and copyright laws.  
  - **LIBSYS Illustrations from Lecture:**  
    1. *Privacy Exclusion:* "The system shall not disclose personal patron records (beyond name and library card ID) to unauthorized staff."  
    2. *Copyright Mandate:* "Specific classes of imported licensed documents shall not be saved as local electronic copies (must be automatically deleted on arrival or printed directly to a network server)."  
- **Marking Scheme:**  
  - 1.5 marks for explaining developer assumptions, boundary definitions, and gold-plating prevention.  
  - 1 mark for compliance/security necessity.  
  - 1.5 marks for citing the LIBSYS patron privacy and delete-on-print copyright rules from Chapter 1.  
- **Common Mistake Warning:** Stating that negative requirements are just non-functional requirements.

### Question 10 Guide Answer
- **Model Answer:**  
  (a) **Business Problem:** Manual handwritten requisition and fax ordering causes severe operational delays (4-day fulfillment), high routine test stockout rates (18%), and massive financial waste (\$450,000 annual loss from expired, untracked reagent stock).  
  (b) **Business Objectives:**  
  1. Reduce annual expired reagent waste expenses by 75% within the first year of PSTS deployment.  
  2. Reduce average requisition order fulfillment latency from 4 business days to under 24 hours within 6 months of system launch.  
  (c) **Success Metrics:**  
  1. Average reagent draw request processing time shall be $\le 5$ minutes on at least 90% of submitted orders during operational testing.  
  2. Reagent container inventory tracking accuracy shall achieve $\ge 99.5\%$ automated reconciliation against physical stock during monthly audits.  
- **Marking Scheme:**  
  - 1 mark for Business Problem.  
  - 1.5 marks for two quantifiable Business Objectives (target percentage + timeframe).  
  - 1.5 marks for two concrete Success Metrics with measurable thresholds.  
- **Common Mistake Warning:** Writing a functional requirement with `SHALL` when asked for a Business Objective.

### Question 11 Guide Answer
- **Model Answer:**  
  **Vision Statement Artifact — Pathology Supply Tracking System:**  
  - **For** clinical pathologists and laboratory technicians who need to request and track diagnostic chemical reagents,  
  - **Who** require rapid reagent fulfillment without testing stockouts or expired container delays,  
  - **The** Pathology Supply Tracking System **is an** enterprise laboratory inventory and procurement information system  
  - **That** will provide a single centralized portal to clinic stockrooms and external reagent vendors, storing real-time batch locations, remaining volumes, and complete usage history, cutting expired chemical losses by 75% in the first year.  
  - **Unlike** current manual handwritten paper forms and fax ordering processes,  
  - **Our product** will automatically track expiration thresholds, trigger automated vendor replenishments, and generate statutory hazardous waste disposal manifests for health inspection compliance.  
- **Marking Scheme:**  
  - 4 marks total: ~0.65 marks per clause correctly completed following the 6-clause lecture template.  
- **Common Mistake Warning:** Omitting the "Unlike" or "Our product" clauses.

### Question 12 Guide Answer
- **Model Answer:**  
  1. *Chief Clinical Pathologist:* **Key Stakeholder.** Holds departmental capital budget authority and makes final binding decisions regarding system procurement, business objectives, and project authorization.  
  2. *Laboratory Technician:* **Primary Stakeholder.** Interacts directly with the software on a daily, hands-on basis at the laboratory bench to order and log reagents.  
  3. *State Hazardous Bio-Waste Inspector:* **Secondary Stakeholder.** Does not use the software daily, but is indirectly affected by the system's outputs, consuming annual compliance audit logs and disposal manifests.  
  4. *Central Hospital Procurement Officer:* **Primary / Key Stakeholder.** Directly operates the purchasing approval screens (Primary) and executes corporate financial contracts with chemical vendors (Key/Decision-maker).  
- **Marking Scheme:** 1 mark per stakeholder correctly categorized with concise justification. Total = 4 marks.  
- **Common Mistake Warning:** Classifying the State Inspector as a Key Stakeholder because they have regulatory power. Key stakeholders are project financial sponsors/decision-makers.

### Question 13 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Weak Auxiliary Verb:* "Should" expresses an optional guideline rather than a mandatory contractual requirement.  
  2. *Subjective Adverb:* "Fast" is unquantified and cannot be objectively verified.  
  3. *Vague Condition:* "If chemicals are low" omits the reorder threshold value, units of measure, and target inventory formula.  
  4. *Compound Concern:* Combines inventory querying with automated alert dispatching in one clause.  
  (b) **Explanation:** Test engineers cannot write binary pass/fail test assertions for "fast". Developers do not know what inventory percentage constitutes "low", resulting in missed reorders and stockouts.  
  (c) **Surgical Rewrite:**  
  - `FR-PST-01:` The system shall allow authenticated laboratory staff to search reagent inventory across all regional pathology stockrooms by chemical name or CAS registry number, returning results within 1.5 seconds.  
  - `FR-PST-02:` When the remaining volume of any reagent container falls below 15% of its rated capacity, the system shall automatically generate a low-stock alert notification to the stockroom technician queue within 60 seconds.  
- **Marking Scheme:**  
  - 1 mark for naming defects (weak modal "should", unmeasured "fast", vague threshold).  
  - 1 mark for explaining verification/testing impossibility.  
  - 2 marks for decomposing into `FR-PST-01` and `FR-PST-02` with `SHALL` and measurable limits.  
- **Common Mistake Warning:** Keeping both behaviors in a single sentence using "and".

### Question 14 Guide Answer
- **Model Answer:**  
  (a) **Hazard of Imprecision & Ambiguity:**  
  - *User Intention:* The technician types a reagent name once into a global search bar, expecting the software to search across all hospital clinics and central depots simultaneously to locate emergency supplies.  
  - *Developer Interpretation:* The developer builds a single-clinic dropdown search interface where the technician must select a specific clinic from a list first, searching only that clinic's local stock.  
  (b) **Operational Failure:** If an emergency patient requires a rare antidote or biopsy reagent whose location is unknown, the technician must manually repeat the search 20+ times across individual clinic dropdowns, wasting critical minutes and potentially endangering patient survival.  
  (c) **Surgical Rewrite:**  
  `FR-PST-03:` The system shall provide a global inventory search function allowing laboratory staff to query available reagent containers across all regional hospital clinics and storage depots simultaneously using a single search query.  
- **Marking Scheme:**  
  - 1.5 marks for contrasting the global search intention with the dropdown-per-clinic interpretation.  
  - 1 mark for analyzing the emergency operational failure.  
  - 1.5 marks for atomic, unambiguous rewrite (`FR-PST-03`) using `SHALL`.  
- **Common Mistake Warning:** Blaming the user for not knowing which clinic to search.

### Question 15 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Untestable Quality Buzzwords:* "Reliable" and "secure" are subjective adjectives lacking verification criteria.  
  2. *Infeasible Constraint:* "Zero downtime" is physically and technologically impossible in enterprise software engineering (hardware fails, networks disconnect, maintenance requires reboots).  
  3. *Unspecified Compliance Standards:* "Conform to all hospital privacy laws" omits the statutory regulatory code.  
  (b) **Surgical Decomposition:**  
  - `NFR-PST-01` *(Product NFR - Availability):* The PSTS system shall be operational and accessible Monday through Friday between 08:00 and 18:00, with total unplanned downtime not exceeding 5 seconds per working day.  
  - `NFR-PST-02` *(External NFR - Statutory Privacy):* The system shall enforce patient confidentiality and specimen record encryption in transit and at rest in strict compliance with statutory healthcare privacy standard `HStan-03-2006-priv`.  
- **Marking Scheme:**  
  - 1 mark for identifying untestable buzzwords, infeasible "zero downtime", and missing statutory names.  
  - 1.5 marks for `NFR-PST-01` specifying availability hours and $\le 5$ seconds downtime/day.  
  - 1.5 marks for `NFR-PST-02` specifying `HStan-03-2006-priv` and encryption.  
- **Common Mistake Warning:** Rewriting "zero downtime" as "99.999% uptime" without defining working hours or operational windows.

