# Exam 03: True/False, Essay & Applied Cases (Validation & Verification)

> **Subject:** Software Requirements Engineering  
> **Coverage:** Chapter 3 (Requirements Validation & Verification - Part 1)  
> **Total Marks:** 50 | **Time Allowed:** 90 Minutes  
> **Instructions:** Answer all questions in full sentences. For True/False questions, you must provide a concise technical justification; correct identification without justification earns only partial credit.

---

## 🎓 Examinee Strategic Briefing: How to Solve & Critical Pitfalls to Avoid

Before attempting this exam, review this mental roadmap to guide your problem-solving and prevent common errors:

### 1. How to Approach Each Section:
- **Section 1 (True / False):**
  - **The Validation vs. Verification Mnemonic:**
    - *Validation = Right Product?* (Did we build what the customer and law actually require in the real world?)
    - *Verification = Product Right?* (Did we build the specification correctly according to engineering quality standards and templates?)
  - **The "Syntax-Trap":** A requirement can be grammatically flawless and 100% testable, yet be legally or commercially wrong (e.g., monthly vs. daily compounding interest).
  - **Cost Escalation Economics:** Late rework is *never* cheap; the cost of fixing requirements errors escalates **10x to 100x** downstream.
- **Section 2 (Essays):**
  - **7 Interpretations of Completeness:** Be ready to cite completeness beyond sentence-level (Models, Individual Reqs, Metadata, Repositories, Set of Docs, Individual Spec Docs, Baseline).
  - **"No More, No Less":** "No less" = all inputs, limits, error handling covered; "No more" = no unnecessary gold-plating or premature architectural constraints.
  - **Modifiability vs. Duplication:** Explain why copy-pasting across documents causes partial updates and internal contradictions.
- **Section 3 (Business Goals & Metrics):**
  - Anchor the **Business Problem** in the case's real-world costs and operational failures.
  - Connect **Business Objectives** to strategic targets and **Success Metrics** to measurable testing assertions.
  - Ground your evaluation of omitted workflows in the **Standish Group 12.3% project failure rate**.
- **Section 4 (Requirements Issues & Quality Diagnosis):**
  - **Unambiguous Rewrites:** Replace words like "intuitive" or "user-friendly" with measurable user performance criteria (e.g., "A trained user shall complete checkout in under 90 seconds on 95% of transactions").
  - **Inconsistency Resolution:** When two requirements contradict (e.g., email mandatory vs. phone only), do not delete one arbitrarily; write a unified, harmonious requirement covering both authorized paths.

### 2. Top Cognitive Traps to Avoid:
1. ❌ **Trap 1: Inverting Validation and Verification.** Verification is internal document/syntax checking; Validation is real-world customer/regulatory truth checking.
2. ❌ **Trap 2: Assuming Passing QA Tests Means Valid Software.** Bug-free code that fulfills an incorrect or incomplete SRS will pass 100% of internal verification tests but be rejected by customers.
3. ❌ **Trap 3: Copy-Pasting Requirements for "Convenience".** Duplication violates Modifiability. Always define an NFR atomically once (e.g., `NFR-SEC-014`) and cross-reference it.

---

## SECTION 1 — True or False with Justification [12 marks | 6 questions]

### Question 1 (2 marks)
*Statement:* Requirements Verification is the process of confirming that the software system satisfies the real-world operational needs and business goals of the customer ("building the right product").  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 2 (2 marks)
*Statement:* A requirement that contains zero grammatical errors, uses RFC 2119 `SHALL`, has a unique persistent identifier, and can be verified by automated unit tests is guaranteed to pass Requirements Validation.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 3 (2 marks)
*Statement:* According to the Standish Group CHAOS Study (1994), incomplete requirements are the primary root cause of 12.3% of all software project failures and cost overruns.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 4 (2 marks)
*Statement:* In Requirements Engineering, "completeness" means writing as much descriptive prose as possible to cover every conceivable future feature an organization might ever build.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 5 (2 marks)
*Statement:* Duplicating an identical security session timeout requirement across multiple subsystem documents in an SRS improves modifiability because developers in each subsystem can find it easily.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 6 (2 marks)
*Statement:* The downstream cost of fixing an undiscovered requirements error during coding, system testing, or production is roughly equal to fixing it during early requirements validation, because the rework involves the same logic.  
*(State True or False and provide a rigorous technical justification from the lecture).*

---

## SECTION 2 — Deep Essay & Analytical Synthesis [14 marks | 3 questions]

### Question 7 (5 marks)
Explain the foundational distinction between **Requirements Validation** and **Requirements Verification**. In your essay, structure a comparative matrix analyzing: (a) the philosophical definition of each ("right product" vs. "product right"), (b) the primary target of evaluation, (c) two specific engineering activities associated with each, and (d) why a system that passes 100% of internal QA verification tests can still be an absolute commercial failure.

### Question 8 (5 marks)
Analyze the **Nine Essential Quality Characteristics of Good Requirements** presented in Chapter 3. Select four characteristics from this taxonomy (**Completeness**, **Testability**, **Feasibility**, and **Consistency**) and explain: (a) the formal definition of each, (b) the downstream project disaster that occurs when each is violated, and (c) an illustrative contrast between a flawed requirement and its surgically corrected counterpart.

### Question 9 (4 marks)
Synthesize the **Seven Interpretations of "Requirements Completeness"** taught in the lecture. Why is evaluating completeness at the single requirement level (e.g., inputs, calculations, error paths) insufficient to guarantee completeness across the overall system baseline, and what specific deliverables must be audited across the documentation set?

---

## SECTION 3 — Case Study: Business Goals & Metrics [12 marks | 3 questions]

### Scenario Description
A regional commercial airline operates an online ticket booking and seat reservation engine. During peak holiday flash sales, the booking portal crashes repeatedly, customer credit cards are charged twice for single bookings due to session race conditions, and refund processing takes 21 business days. In a recent customer satisfaction survey, the airline scored in the bottom 10th percentile, and the Department of Transportation fined the airline \$1.2 million for unfulfilled passenger cancellation statutory rights. The board has approved the **Next-Gen Passenger Reservation Engine (NPRE)** modernization project.

### Question 10 (4 marks)
Structure the business foundations for the NPRE project:  
(a) Define the primary **Business Problem** currently damaging the airline's market reputation and financial standing.  
(b) Formulate two distinct, quantifiable **Business Objectives** for the NPRE investment.  
(c) Define two concrete **Success Metrics** that can be objectively measured during post-deployment operational acceptance testing.

### Question 11 (4 marks)
Author a formal, standard **6-Clause Vision Statement** for the Next-Gen Passenger Reservation Engine conforming strictly to the template taught in Chapter 2 (*For... Who... The... That... Unlike... Our product...*).

### Question 12 (4 marks)
The NPRE business analyst presents a project scope document that completely omits customer refund processing and luggage cancellation workflows. When challenged by QA, the analyst replies: *"We are focusing on the booking happy-path first; missing features can easily be added in post-release maintenance."*  
(a) Evaluate the analyst's claim using the **Standish Group CHAOS Study** findings.  
(b) Explain the **three specific mechanisms** through which omitted requirements drive software projects into financial and operational collapse.

---

## SECTION 4 — Case Study: Requirements Issues & Quality Diagnosis [12 marks | 3 questions]

### Scenario Description
During a formal quality audit of the draft NPRE Software Requirements Specification (SRS), the lead verification engineer uncovers several high-risk statements that violate core quality characteristics.

### Question 13 (4 marks)
*Audit Finding 1 (Payment Module):*  
*"The booking engine shall process payments quickly and provide an intuitive, user-friendly checkout experience."*  
(a) Identify the quality characteristics violated based on Chapter 3 standards.  
(b) Explain why subjective adjectives ("intuitive", "user-friendly") make it impossible for test engineers to design objective pass/fail test assertions.  
(c) Surgically rewrite this requirement into two atomic, verifiable requirements: one Functional (`FR-PAY-01`) and one Product NFR (`NFR-PAY-01`) using quantifiable thresholds.

### Question 14 (4 marks)
*Audit Finding 2 (Tax & Surcharge Calculation):*  
*"The system shall calculate aviation taxes and airport fuel surcharges for passenger itineraries."*  
(a) Name the primary quality characteristic violated by this statement.  
(b) Analyze the specific financial, architectural, and legal risks developers face when forced to implement this incomplete requirement.  
(c) Surgically rewrite this statement (`FR-TAX-NPRE-01`) into a complete requirement specifying inputs, jurisdiction tables, currency handling, and error conditions.

### Question 15 (4 marks)
*Audit Finding 3 (Inconsistency & Architectural Contradiction):*  
- *Section 2.4.1:* "All passenger reservations must be guaranteed by a registered email address for electronic ticket issuance."  
- *Section 5.1.3:* "Passengers booking walk-up airport counter flights may complete ticketing using only an SMS mobile number without an email."  
(a) Identify the quality characteristic violated by this specification pair.  
(b) Explain the software database and integration defect that manifests when back-end engineers and kiosk developers implement these conflicting rules.  
(c) Surgically rewrite these statements into a single, unified requirement (`FR-RES-01`) that harmonizes identity validation.

---

# GUIDE ANSWERS & MARKING SCHEME

### Question 1 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* Confirming that a system satisfies the real-world operational needs, business goals, and customer desires ("building the right product") is the definition of **Requirements Validation**. Requirements Verification is focused on "building the product right"—confirming that the authored requirements documents satisfy formal engineering standards, organizational templates, and syntactic rules, and that the code conforms to the written specification.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for correctly defining Validation ("right product") vs. Verification ("product right").  
- **Common Mistake Warning:** Inverting the definitions of Validation and Verification.

### Question 2 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* A requirement can be grammatically flawless, uniquely labeled, RFC 2119 compliant, and pass 100% of automated unit verification tests, yet be **factually, legally, or conceptually wrong** (Validation failure). As illustrated in the lecture's banking case: specifying that savings interest is compounded monthly passes Verification (it is unambiguous, testable, and coded without bugs), but fails Validation completely because banking regulations legally mandate daily compounding. Verification evaluates consistency against internal documents; Validation evaluates correctness against the external operational world and business truth.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for explaining that syntactic perfection does not guarantee business/legal truth, citing the monthly vs. daily interest example.  
- **Common Mistake Warning:** Answering True, assuming that passing unit tests means the requirement is valid.

### Question 3 Guide Answer
- **Model Answer:** **TRUE.**  
  *Justification:* The 1994 Standish Group CHAOS Study explicitly established that incomplete requirements are the direct root cause of **12.3% of software project failures and budget overruns**, making them one of the single largest drivers of software project collapse.  
- **Marking Scheme:** 1 mark for TRUE; 1 mark for citing the Standish Group study's findings on incomplete requirements as a primary driver of project failure.  
- **Common Mistake Warning:** Thinking the 12.3% refers to programming syntax bugs.

### Question 4 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* In Requirements Engineering, completeness is governed by the principle of **"no more, no less"**. A complete requirement must specify all necessary functional inputs, boundary conditions, expected outputs, and error handling ("no less"), while strictly avoiding extraneous descriptions, unrequested features, or unnecessary architectural constraints ("no more") that cause scope creep and gold-plating. Writing massive volumes of descriptive prose introduces ambiguity and unneeded complexity.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for defining "no more, no less" (exhaustiveness of conditions vs. avoiding scope bloat/gold-plating).  
- **Common Mistake Warning:** Confusing narrative verbosity with engineering completeness.

### Question 5 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* Duplicating requirements across multiple sections directly **violates Modifiability** and destroys document maintainability. Modifiability requires **atomicity (each requirement appears exactly once)**. If a timeout rule is copy-pasted across multiple documents, when the policy changes (e.g., from 15 minutes to 5 minutes), analysts inevitably update some occurrences and miss others. This introduces immediate internal contradictions, causing developers to build mismatched timeout timers across different screens and creating severe security vulnerabilities. Best practice is to define the rule once under a unique ID (`NFR-SEC-014`) and cross-reference it.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for explaining how copy-pasting causes partial edits, internal contradictions, and violates atomicity.  
- **Common Mistake Warning:** Thinking redundancy helps developers find information faster.

### Question 6 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* The cost of resolving requirements errors escalates **exponentially by 10x to 100x** as the software progresses through the lifecycle. Fixing an omission during requirements validation costs a baseline of $1\times$ (editing a specification document). Fixing that same omission during coding or system testing requires rewriting code, modifying database schemas, refactoring APIs, and re-running test suites. Fixing it after production deployment can cost millions in data patching, regulatory fines, customer compensation, and emergency hotfixes.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for explaining the 10x to 100x exponential cost-of-rework escalation factor.  
- **Common Mistake Warning:** Assuming that bug fixes cost the same regardless of project phase.

### Question 7 Guide Answer
- **Model Answer:**  
  - **Comparative Matrix:**  
    | Evaluation Dimension | Requirements Validation | Requirements Verification |
    | :--- | :--- | :--- |
    | **(a) Philosophical Definition** | **"Building the right product"**: Confirms requirements accurately reflect real user needs, business goals, and operational truth. | **"Building the product right"**: Confirms requirements documents meet formal quality criteria, templates, and syntactic rules. |
    | **(b) Target of Evaluation** | Customer desires, business workflows, operational environment, and regulatory truth. | Requirements documents (SRS), models, and conformity of code to written specifications. |
    | **(c) Two Specific Activities** | 1. User walkthroughs & prototype reviews.<br/>2. Customer acceptance criteria validation against business goals. | 1. Formal peer inspection of SRS against IEEE 830 checklist.<br/>2. Authoring pass/fail automated verification test cases. |  
  - **(d) Why 100% Verification Test Pass Rate Can Still Equal Commercial Failure:** Internal QA test cases only verify that the software behaves according to the written SRS. If the SRS specified the wrong business algorithm, omitted essential operational exception workflows, or solved the wrong business problem, developers can write bug-free code that passes 100% of test runs. However, when deployed, the system is rejected by users because it fails to perform their actual daily work (Validation failure).  
- **Marking Scheme:**  
  - 1 mark for (a) Right product vs. product right.  
  - 1 mark for (b) Real-world truth vs. document standards.  
  - 1 mark for (c) Two concrete activities for each.  
  - 2 marks for (d) Explaining how bug-free code matching a flawed SRS causes commercial failure.  
- **Common Mistake Warning:** Calling user acceptance testing a verification activity.

### Question 8 Guide Answer
- **Model Answer:**  
  - **1. Completeness:**  
    - *Definition:* Specifies all functional capabilities, user inputs, outputs, environmental states, error responses, and boundary values ("no more, no less").  
    - *Downstream Disaster:* 12.3% project failures (Standish Group); developer guesswork, missed error handling, unbudgeted scope, and 10x–100x rework.  
    - *Contrast:* ❌ "Calculate sales tax." $\rightarrow$ ✅ "Calculate state and county sales tax based on shipping zip code using State Tax Table 4.1."  
  - **2. Testability / Verifiability:**  
    - *Definition:* Objective, cost-effective test cases (inspection, unit tests, automated tests) can definitively prove the software passes or fails.  
    - *Downstream Disaster:* QA engineers cannot write pass/fail assertions; disputes between developers and clients over subjective interpretations.  
    - *Contrast:* ❌ "The report shall be visually appealing and modern." $\rightarrow$ ✅ "The report shall display sales totals in tabular layout conforming to UI Style Guide v2.1 in 11pt Arial."  
  - **3. Feasibility:**  
    - *Definition:* Capable of being implemented within system constraints, technological capabilities, team skills, budget, and schedule.  
    - *Downstream Disaster:* Project cancellation after consuming millions attempting to build physically or technologically impossible capabilities.  
    - *Contrast:* ❌ "Translate speech with 100% accuracy in noisy industrial environments on low-power IoT chips." $\rightarrow$ ✅ "Recognize 50 pre-defined voice commands with $\ge 95\%$ accuracy in quiet environments ($\le 60\ \text{dB}$)."  
  - **4. Consistency:**  
    - *Definition:* Individual requirements do not conflict with or contradict other requirements, business rules, or external standards.  
    - *Downstream Disaster:* Architectural divergence, database constraint exceptions (e.g., `NOT NULL` violations), and system integration crashes.  
    - *Contrast:* ❌ Section 3: "Email mandatory" vs. Section 5: "Phone only allowed" $\rightarrow$ ✅ "User shall register using either email or mobile number, verified via single-use SMS token."  
- **Marking Scheme:** 1.25 marks per quality characteristic (definition, disaster, contrast example). Total = 5 marks.  
- **Common Mistake Warning:** Giving only definitions without analyzing the downstream disaster or contrast example.

### Question 9 Guide Answer
- **Model Answer:**  
  - **The Seven Interpretations of Requirements Completeness:**  
    1. *Completeness of Requirements Analysis Models:* Diagrams (DFDs, ERDs, State models) depict all operational states, entities, and transitions without dead ends.  
    2. *Completeness of Individual Requirements:* Each requirement specifies inputs, algorithms, outputs, boundary limits, and error handling.  
    3. *Completeness of Requirement Metadata:* Every requirement record has mandatory attributes populated (unique ID, author, origin, priority, status).  
    4. *Completeness of Requirements Repositories:* The central repository captures all known user classes, use cases, and product backlog items.  
    5. *Completeness of the Set of Requirements Documents:* All foundational deliverables (Vision & Scope, Use Case Catalog, SRS, Data Dictionary) exist.  
    6. *Completeness of Individual Specification Documents:* Every standardized section of the adopted template (IEEE 830) is completed without blank/TBD sections.  
    7. *Completeness of the Requirements Baseline:* The formally frozen set approved for a release contains everything needed to proceed to design.  
  - **Why Single-Level Completeness is Insufficient:** An individual requirement can be 100% complete internally (e.g., specifying inputs, outputs, and formulas), but if entire use cases, external interface definitions, data dictionary entries, or document template sections are missing from the documentation set, the overall software architecture will be flawed and un-integrable.  
- **Marking Scheme:**  
  - 2.5 marks for accurately identifying at least 5 of the 7 interpretations.  
  - 1.5 marks for explaining why single-requirement completeness fails to guarantee baseline/system integrity.  
- **Common Mistake Warning:** Listing generic qualities like "correct" or "unambiguous" instead of the 7 interpretations of completeness.

### Question 10 Guide Answer
- **Model Answer:**  
  (a) **Business Problem:** Severe operational bottlenecks during peak sales (repeated portal crashes, duplicate credit card charges from race conditions), 21-day refund delays, bottom 10th percentile customer satisfaction, and \$1.2 million in Department of Transportation statutory non-compliance fines.  
  (b) **Business Objectives:**  
  1. Reduce customer refund processing cycle time from 21 business days to under 24 hours within 3 months of NPRE deployment.  
  2. Achieve 100% compliance with Department of Transportation passenger rights statutes, eliminating statutory regulatory penalties within the first year.  
  (c) **Success Metrics:**  
  1. The booking engine shall maintain peak transaction processing with zero duplicate charge errors across 50,000 concurrent booking sessions during holiday flash sales.  
  2. Customer satisfaction rating for online booking and cancellation workflows shall improve to $\ge 85\%$ within 6 months post-launch.  
- **Marking Scheme:**  
  - 1 mark for Business Problem.  
  - 1.5 marks for two quantifiable Business Objectives (target percentage + timeframe).  
  - 1.5 marks for two concrete Success Metrics with measurable thresholds.  
- **Common Mistake Warning:** Writing a functional requirement with `SHALL` instead of formulating a strategic Business Objective.

### Question 11 Guide Answer
- **Model Answer:**  
  **Vision Statement Artifact — Next-Gen Passenger Reservation Engine:**  
  - **For** commercial airline passengers and customer reservation agents,  
  - **Who** require instantaneous, error-free flight booking, seat selection, and immediate cancellation processing,  
  - **The** Next-Gen Passenger Reservation Engine **is an** enterprise cloud booking and ticketing information system  
  - **That** will provide high-concurrency ticket reservation, real-time seat inventory locking, automated credit card reconciliation, and sub-24-hour refund processing, eliminating \$1.2 million in annual regulatory non-compliance penalties.  
  - **Unlike** current legacy booking portals that suffer from duplicate charge race conditions and multi-week refund delays,  
  - **Our product** will provide automated passenger rights compliance tracking, active-active server redundancy, and seamless mobile self-service rebooking.  
- **Marking Scheme:**  
  - 4 marks total: ~0.65 marks per clause correctly completed following the 6-clause lecture template.  
- **Common Mistake Warning:** Omitting the "Unlike" or "Our product" clauses.

### Question 12 Guide Answer
- **Model Answer:**  
  (a) **Evaluation:** The analyst's claim is completely reckless and economically fatal. Incomplete requirements are the single direct cause of 12.3% of project failures (Standish Group). Postponing essential operational workflows (like refunds and cancellations) to post-release maintenance guarantees budget blowouts and customer outrage.  
  (b) **Three Specific Mechanisms of Project Collapse:**  
  1. *Artificially Underestimated Budgets & Schedules:* Initial project estimates are calculated based solely on specified happy-path features. Because complex refund workflows were omitted, the project is vastly underfunded and under-resourced, leading to inevitable financial collapse when reality hits.  
  2. *Exponentially Costlier Downstream Rework (10x–100x):* Retrofitting omitted refund logic after database schemas, payment gateway integrations, and front-end UIs are coded costs 10x to 100x more than specifying them during early requirements engineering.  
  3. *Customer Dissatisfaction & System Rejection:* The booking engine may pass 100% of test cases written for flight purchasing, but when passengers attempt cancellations, the lack of functionality triggers viral complaints, chargebacks, and legal regulatory shutdowns.  
- **Marking Scheme:**  
  - 1 mark for rejecting the analyst's claim using the Standish Group study.  
  - 3 marks (1 mark each) for detailing the three collapse mechanisms (Underestimated Budgets, 10x–100x Cost Escalation, System Rejection).  
- **Common Mistake Warning:** Attributing the failure to coding syntax bugs rather than requirements omissions.

### Question 13 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Untestable Quality Buzzwords:* "Intuitive" and "user-friendly" are subjective opinions; no objective pass/fail criteria exist.  
  2. *Unmeasured Performance Adverb:* "Quickly" has no quantifiable time threshold.  
  3. *Conflation of Concerns:* Combines back-end transaction processing latency with front-end UI usability in a single statement.  
  (b) **Explanation:** A QA engineer cannot write a deterministic unit or integration test assertion that evaluates whether a checkout screen is "intuitive". What is intuitive to an experienced traveler may be confusing to a first-time booker.  
  (c) **Surgical Rewrite:**  
  - `FR-PAY-01:` When a passenger confirms payment, the reservation engine shall securely submit the credit card token to the payment gateway and display the confirmed booking receipt within 2.5 seconds.  
  - `NFR-PAY-01:` A first-time passenger shall be able to navigate from flight selection to payment confirmation in under 4 minutes on at least 90% of unassisted booking sessions during operational usability testing.  
- **Marking Scheme:**  
  - 1 mark for naming defects (subjective buzzwords, unmeasured adverb, compound concern).  
  - 1 mark for explaining the impossibility of objective pass/fail assertions.  
  - 2 marks for decomposing into `FR-PAY-01` and `NFR-PAY-01` with `SHALL` and measurable metrics.  
- **Common Mistake Warning:** Rewriting "user-friendly" as "must look good and modern".

### Question 14 Guide Answer
- **Model Answer:**  
  (a) **Primary Quality Characteristic Violated:** **Completeness** (omits all necessary calculation inputs, tax rates, airport fee schedules, currency conversion, and exemption rules).  
  (b) **Downstream Risks:** Developers are forced to guess how taxes are computed. They will hardcode an arbitrary tax percentage, omit regional airport facility charges, or fail to handle multi-leg international itineraries. This results in severe under-collection of passenger taxes, millions in regulatory audit penalties, and massive code refactoring during billing reconciliations.  
  (c) **Surgical Rewrite:**  
  `FR-TAX-NPRE-01:` The system shall calculate aviation passenger taxes, security fees, and fuel surcharges for each ticketed flight segment based on departure and destination airport codes, referencing the active International Air Transport Association (IATA) Tax Matrix (Table 3.2), and display the itemized tax breakdown in the selected booking currency prior to payment confirmation.  
- **Marking Scheme:**  
  - 1 mark for identifying Completeness.  
  - 1.5 marks for explaining developer guesswork, regulatory penalties, and billing refactoring risks.  
  - 1.5 marks for complete rewrite with ID `FR-TAX-NPRE-01`, `SHALL`, airport code inputs, IATA Tax Matrix reference, and itemized display.  
- **Common Mistake Warning:** Writing "The system shall calculate 15% tax" which hardcodes an assumption instead of referencing authoritative fee tables.

### Question 15 Guide Answer
- **Model Answer:**  
  (a) **Quality Characteristic Violated:** **Consistency** (the two requirement statements directly contradict each other regarding mandatory registration credentials).  
  (b) **Database & Integration Manifestation:** The database architect will design the `Passenger_Profile` table with an `email_address` column defined as `NOT NULL` (based on Section 2.4.1). When an airport kiosk counter developer submits a walk-up reservation with only a mobile phone number (based on Section 5.1.3), the database throws a database constraint violation exception, crashing the kiosk application at the departure gate.  
  (c) **Surgical Rewrite:**  
  `FR-RES-01:` The reservation subsystem shall require passengers to provide either a valid email address or an SMS-capable mobile telephone number as their mandatory contact identifier, and shall dispatch electronic ticketing confirmations via the provided contact channel within 30 seconds of payment clearance.  
- **Marking Scheme:**  
  - 1 mark for identifying Consistency.  
  - 1.5 marks for explaining database `NOT NULL` constraint violations and kiosk application crashes.  
  - 1.5 marks for unified, consistent rewrite (`FR-RES-01`) using `SHALL`.  
- **Common Mistake Warning:** Simply deleting Section 5.1.3 without creating a unified policy.

