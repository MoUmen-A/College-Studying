# Question Bank: Chapter 3 — Requirements Validation & Verification

> **Subject:** Software Requirements Engineering  
> **Chapter:** Chapter 3 — Requirements Validation & Verification (Part 1)  
> **Total Marks:** 50 | **Questions:** 18  
> **Instructions:** Answer all questions. Write in full sentences. Partial marks are awarded for correct reasoning even if the final answer is incomplete.

---

## 🎓 Examinee Strategic Briefing: How to Solve & Critical Pitfalls to Avoid

Before attempting this exam, review this mental roadmap to guide your problem-solving and prevent common errors:

### 1. How to Approach Each Section:
- **Section A (Defect Diagnosis & Surgical Rewrite):**
  - **Identify Quality Characteristics:** Name defects using the formal lecture terms: *Ambiguous*, *Incomplete*, *Infeasible*, *Untestable*, *Inconsistent*, or *Unmodifiable*.
  - **Resolve Infeasibility:** If a requirement demands 100% accuracy in noisy environments on IoT chips, rewrite it to a realistic industrial benchmark ($\ge 95\%$ accuracy on 50 pre-defined commands in $\le 60\ \text{dB}$ noise).
  - **Harmonize Contradictions:** Combine conflicting rules (e.g., email vs. mobile SMS) into a unified, consistent requirement using `SHALL`.
- **Section B (Conceptual Discrimination):**
  - **Validation vs. Verification:** Remember: Verification asks *"Is the specification written right?"*; Validation asks *"Is it the right product for the customer and the law?"*.
  - **The Banking Precedent:** Use the monthly vs. daily compounding interest case to prove that syntactically verified requirements can still fail validation completely.
  - **Standish Group 12.3% Statistic:** Memorize the 3 drivers of project collapse: (1) Underestimated budgets, (2) 10x–100x cost of downstream rework, and (3) Customer system rejection.
- **Section C (Elicitation & Technique Strategy):**
  - **Aesthetics are Untestable:** Explain why terms like "visually appealing" cannot produce binary pass/fail test assertions; replace them with UI style guide references.
  - **All High Priority = No Priority:** Explain how un-prioritized requirements force developers to make arbitrary feature cuts during schedule crunches.
  - **"No More, No Less":** "No less" = exhaustive exception and boundary handling; "No more" = avoiding unnecessary gold-plating and premature architectural constraints.
- **Section D (Artifact Construction):**
  - **7 Interpretations of Completeness:** Be prepared to detail: Models, Individual Reqs, Metadata, Repositories, Set of Docs, Individual Spec Docs, and the Baseline.
  - **Quality Inspection Checklist:** Formulate objective diagnostic questions for Unambiguity, Testability, Feasibility, and Modifiability.
  - **Poor SRS Matrix:** Map the 4 impact dimensions: Communication, Cost/Schedule, System Quality, and Traceability/Verification.
- **Section E (Case Study Analysis):**
  - Ground legal and banking audit disasters in **Correctness** and the failure of internal verification to evaluate external regulatory truth.
  - Address copy-paste duplication bugs as **Modifiability** failures.

### 2. Top Cognitive Traps to Avoid:
1. ❌ **Trap 1: Believing Verification Catches Regulatory Errors.** Internal QA only checks code against the written SRS; if the SRS has an illegal rule, the code will pass QA testing and fail legal validation.
2. ❌ **Trap 2: Confusing "Modifiable" with "Editable".** Modifiability does not mean a file is unlocked; it means each requirement appears *atomically once* under a unique ID, allowing single-point maintenance without cross-document contradictions.
3. ❌ **Trap 3: Equating Word Count with Completeness.** Completeness is "no more, no less"; unnecessary prose bloat introduces ambiguity.

---

## SECTION A — Defect Diagnosis & Surgical Rewrite [15 marks | 4 questions]

### Question 1 (3 marks)
Review the following requirement extracted from a retail point-of-sale specification:  
*"The system shall be easy to use and fast for supermarket checkout clerks."*  
(a) Identify the quality characteristic violated based strictly on the lecture taxonomy.  
(b) Explain why words like "easy to use" and "fast" make verification impossible for quality assurance engineers.  
(c) Surgically rewrite this requirement into a rigorous, verifiable requirement (`NFR-POS-01`) using the exact quantifiable metrics and phrasing taught in the lecture.

### Question 2 (4 marks)
An analyst authored the following statement in an e-commerce checkout module:  
*"The system shall calculate sales tax."*  
(a) Name the primary quality characteristic violated by this statement.  
(b) Explain the severe project risks and technical uncertainties developers face when implementing this incomplete statement.  
(c) Surgically rewrite this requirement (`FR-TAX-01`) into a complete specification incorporating inputs, reference tables, regional jurisdictions, and RFC 2119 `SHALL` syntax.

### Question 3 (4 marks)
A technical proposal contains the following requirement for an embedded wearable device:  
*"The system shall translate spoken audio in real-time with 100% accuracy in noisy industrial factory environments running on low-power IoT microcontrollers."*  
(a) Identify the quality characteristic violated by this requirement.  
(b) Analyze the engineering and environmental contradictions that make this requirement unviable.  
(c) Surgically rewrite this requirement (`FR-VOX-01`) into an engineered, feasible specification adhering to realistic industrial voice recognition benchmarks defined in the lecture.

### Question 4 (4 marks)
Review the following excerpts from two different sections of the same Software Requirements Specification (SRS):  
- *Section 3.1.2:* "Email address is mandatory for all user registration."  
- *Section 4.5.1:* "Users may complete registration using only a mobile phone number via SMS verification."  
(a) Identify the quality characteristic violated by this specification set.  
(b) Explain what happens when software developers and database architects implement conflicting requirements in separate modules.  
(c) Surgically rewrite these statements into a single, unified, and consistent requirement (`FR-REG-01`) that harmonizes user identification methods.

---

## SECTION B — Conceptual Discrimination [10 marks | 4 questions]

### Question 5 (2.5 marks)
Compare and contrast **Requirements Validation** ("building the right product") with **Requirements Verification** ("building the product right"). Identify two distinct evaluation activities associated with each discipline.

### Question 6 (2.5 marks)
Explain why a requirement that satisfies **Syntactic Correctness** (e.g., follows the standard template and uses `SHALL`) can still completely fail **Requirements Validation**. Provide an example from the banking domain cited in the lecture.

### Question 7 (2.5 marks)
Contrast the quality attribute **Modifiability** with **Atomicity**. Explain how copy-pasting a security timeout rule across 12 different functional sections violates modifiability and creates severe maintenance defects.

### Question 8 (2.5 marks)
According to the **Standish Group CHAOS Study (1994)**, incomplete requirements account for **12.3% of project failures and budget blowouts**. Detail the three underlying mechanisms through which omitted requirements drive projects into collapse.

---

## SECTION C — Elicitation & Technique Strategy [10 marks | 4 questions]

### Question 9 (2.5 marks)
During the review of an SRS, a QA test lead rejects a requirement stated as: *"The report must be visually appealing and modern."*  
(a) Which quality characteristic is violated?  
(b) Why can a test engineer NOT write a binary pass/fail test case for this requirement?  
(c) How should this requirement be formulated to make it fully testable and verifiable?

### Question 10 (2.5 marks)
A business analyst discovers that an SRS contains 200 functional requirements, all tagged with priority level *"High / Critical"*.  
(a) Which quality characteristic of good requirements is violated?  
(b) What operational chaos occurs during development sprints when requirements lack differentiated prioritization?  
(c) How should requirements be prioritized across release increments?

### Question 11 (2.5 marks)
An engineering team is preparing to baseline the requirements for a medical infusion pump. The project manager wants to skip formal validation reviews to save two weeks on the schedule, claiming: *"We have unit testing and system testing later to catch any problems."* Evaluate the project manager's rationale using the downstream cost-of-rework escalation factor taught in the lecture.

### Question 12 (2.5 marks)
A requirements specification defines normal user transactions in meticulous detail, but completely omits what happens when the network drops, database disk space is exhausted, or invalid characters are entered into form fields.  
(a) Which dimension of requirements quality is missing?  
(b) Explain the concept of "no more, no less" in requirements completeness.

---

## SECTION D — Artifact Construction [10 marks | 3 questions]

### Question 13 (4 marks)
Construct an architectural taxonomy detailing the **Seven Interpretations of "Requirements Completeness"** defined in the lecture. For each interpretation, provide its exact scope and a concrete example of what must be verified.

### Question 14 (3 marks)
Construct a **Requirements Quality Inspection Checklist** containing four foundational verification dimensions: (1) Unambiguity, (2) Testability, (3) Feasibility, and (4) Modifiability. For each dimension, provide one explicit diagnostic verification rule that an inspector must evaluate before approving an SRS requirement.

### Question 15 (3 marks)
Construct a comparative **Consequences of Poor SRS Matrix** mapping four project failure dimensions (**Communication**, **Cost & Schedule**, **System Quality**, and **Traceability / Verification**) to their specific downstream operational manifestations as detailed in the lecture risk analysis.

---

## SECTION E — Case Study Analysis [5 marks | 3 questions]

### Question 16 (1.5 marks)
*Mini-Case A:* A commercial banking platform was built specifying that interest on enterprise deposits would be compounded monthly. Six months after deployment, federal banking regulators audited the institution, levied an \$8.5 million penalty, and forced the bank to restate its financial reports because federal statutes legally mandate daily compounding for that deposit tier.  
(a) What requirements quality characteristic was violated in the SRS?  
(b) Why did this defect escape internal QA verification testing?  
(c) How does this demonstrate the boundary between Verification and Validation?

### Question 17 (1.5 marks)
*Mini-Case B:* A healthcare software startup developed an Electronic Medical Records (EMR) application. During development, developers copy-pasted a session timeout requirement—*"The system shall terminate inactive user sessions after 15 minutes of inactivity"*—into 12 different subsystem specification documents. When hospital security policy mandated changing the timeout to 5 minutes to comply with revised privacy regulations, analysts updated only 10 of the documents.  
(a) What quality characteristic was violated?  
(b) What operational defect manifested in the production system?  
(c) How should the specification have been structured to ensure modifiability?

### Question 18 (2 marks)
*Mini-Case C:* A municipal water utility commissioned a smart billing application. The SRS contained the statement: *"The system shall calculate municipal wastewater utility charges for all residential customer accounts."* Developers delivered a billing engine that billed every house a flat \$45 per month. The water utility refused to accept the software, claiming wastewater charges must be calculated dynamically based on water meter flow volume multiplied by tiered seasonal rates. The development firm demanded full payment, arguing they delivered exactly what was written in the SRS.  
(a) Identify the primary quality defect that caused this contractual dispute.  
(b) Analyze the breakdown between stakeholder intention and delivered functionality.  
(c) State who bears contractual responsibility when an SRS requirement lacks operational completeness.

---

# GUIDE ANSWERS & MARKING SCHEME

### Question 1 Guide Answer
- **Model Answer:**  
  (a) **Quality Characteristic Violated:** **Clear & Unambiguous** (leaves room for subjective interpretation; relies on non-quantifiable adjectives).  
  (b) **Explanation:** Terms like "easy to use" and "fast" have no objective engineering definitions. A test engineer cannot construct a deterministic, repeatable pass/fail test case for "easy" or "fast". One person may consider a 5-minute transaction "fast," while another considers 10 seconds too slow.  
  (c) **Surgical Rewrite:**  
  `NFR-POS-01:` A trained supermarket checkout clerk shall be able to complete a standard customer checkout transaction (consisting of 1 to 20 scanned items) in under 90 seconds on at least 95% of transactions during operational acceptance testing.  
- **Marking Scheme:**  
  - 1 mark for naming Clear & Unambiguous.  
  - 1 mark for explaining non-verifiability and impossibility of designing binary pass/fail test cases.  
  - 1 mark for the exact lecture rewrite (`NFR-POS-01`, trained clerk, under 90 seconds, 95% of transactions).  
- **Common Mistake Warning:** Rewriting as "The system shall process checkouts fast within 30 seconds" without defining the user class ("trained clerk") or statistical percentile ("95% of transactions").

### Question 2 Guide Answer
- **Model Answer:**  
  (a) **Primary Quality Characteristic Violated:** **Completeness** (the requirement states the high-level intent but completely omits necessary details: inputs, tax calculation algorithms, tax rate tables, exemptions, and regional jurisdictions).  
  (b) **Downstream Risks:** Developers are forced to make unguided architectural and business assumptions. They will either hardcode an arbitrary tax percentage, omit county/municipal taxes, or ignore shipping exemptions, leading to financial inaccuracies, legal liability, massive rework during billing audits, and customer overcharging.  
  (c) **Surgical Rewrite:**  
  `FR-TAX-01:` The system shall calculate state and county sales tax for each taxable order line item based on the customer shipping address zip code, applying the active rates published in the State Tax Table (Table 4.1), and display the itemized tax breakdown on the order checkout summary screen.  
- **Marking Scheme:**  
  - 1 mark for identifying Completeness.  
  - 1.5 marks for explaining developer guesswork, tax liabilities, and rework risks.  
  - 1.5 marks for complete rewrite with ID `FR-TAX-01`, `SHALL`, shipping zip code input, State Tax Table 4.1 reference, and itemized display.  
- **Common Mistake Warning:** Writing "The system shall calculate 10% tax" which hardcodes an assumption rather than referencing the authoritative tax table.

### Question 3 Guide Answer
- **Model Answer:**  
  (a) **Quality Characteristic Violated:** **Feasibility** (not technically capable of being implemented within existing technological capabilities, hardware limits, and physical constraints).  
  (b) **Engineering & Environmental Contradictions:** Achieving 100% voice recognition accuracy in real-time is technically impossible even in whisper-quiet laboratories due to dialect variations. Demanding 100% accuracy in **noisy industrial factory environments** running on **low-power IoT microcontrollers** violates physical acoustic constraints and processor memory/compute boundaries.  
  (c) **Surgical Rewrite:**  
  `FR-VOX-01:` The embedded voice recognition subsystem shall recognize a set of 50 pre-defined industrial command phrases with an accuracy of $\ge 95\%$ in operating environments where ambient acoustic noise does not exceed $60\ \text{dB}$.  
- **Marking Scheme:**  
  - 1 mark for identifying Feasibility.  
  - 1.5 marks for explaining acoustic noise limits and IoT processing/memory constraints.  
  - 1.5 marks for rewrite specifying 50 pre-defined commands, $\ge 95\%$ accuracy, and quiet/controlled ambient conditions.  
- **Common Mistake Warning:** Believing that modern AI can easily achieve 100% accuracy on IoT hardware.

### Question 4 Guide Answer
- **Model Answer:**  
  (a) **Quality Characteristic Violated:** **Consistency** (the two requirement statements directly contradict each other regarding mandatory registration credentials).  
  (b) **Consequences of Inconsistency:** The database architect will design the `User` table with an `email_address` column marked as `NOT NULL` (based on Section 3.1.2), while the front-end registration developer will build a UI form allowing users to submit without an email address (based on Section 4.5.1). During integration testing or user registration, the system throws database constraint violation exceptions, crashing the registration workflow.  
  (c) **Surgical Rewrite:**  
  `FR-REG-01:` The user registration subsystem shall require new users to register by providing either a valid email address or an SMS-capable mobile phone number as their primary account identifier, validating the provided identifier via an automated single-use verification token before account activation.  
- **Marking Scheme:**  
  - 1 mark for identifying Consistency.  
  - 1.5 marks for analyzing database schema `NOT NULL` conflicts and integration test crashes.  
  - 1.5 marks for unified, harmonious rewrite (`FR-REG-01`) using `SHALL`.  
- **Common Mistake Warning:** Deleting one requirement entirely without creating a unified, consistent policy statement.

### Question 5 Guide Answer
- **Model Answer:**  
  - **Requirements Validation ("Building the right product"):** Evaluates whether the specified software requirements accurately capture the true desires, business objectives, operational workflows, and real-world needs of the customer and end-users.  
    - *Evaluation Activities:* (1) Customer/user walk-throughs and prototyping sessions; (2) Acceptance criteria reviews against business vision and goals.  
  - **Requirements Verification ("Building the product right"):** Evaluates whether the authored requirements documents conform to formal engineering quality standards, organizational templates, and syntactic rules, ensuring statements are clear, unambiguous, consistent, atomic, and testable.  
    - *Evaluation Activities:* (1) Formal peer inspections of the SRS against IEEE 830 checklists; (2) Authoring pass/fail verification test cases to confirm testability.  
- **Marking Scheme:**  
  - 1 mark for contrasting "right product" (user intent/scope) vs. "product right" (document quality/standards).  
  - 1.5 marks (0.75 each) for two concrete activities for Validation and two for Verification.  
- **Common Mistake Warning:** Inverting the definitions (calling Verification "building the right product").

### Question 6 Guide Answer
- **Model Answer:**  
  - **Explanation:** Syntactic correctness (Verification) merely guarantees that a sentence is well-formed, uses `SHALL`, adheres to document templates, has a unique ID, and is testable. However, a requirement can be grammatically flawless and completely testable, yet be **factually, legally, or conceptually wrong** (Validation failure).  
  - *Lecture Banking Example:* An SRS states: *"The system shall compound savings account interest on a monthly basis on the last calendar day of each month."*  
    - This requirement passes Verification (it is unambiguous, uniquely labeled, and 100% testable via unit tests).  
    - It **fails Validation** completely because statutory banking regulations legally mandate that interest must be compounded daily. The requirement builds the "wrong product" that exposes the bank to millions in regulatory fines.  
- **Marking Scheme:**  
  - 1 mark for explaining that syntactic quality does not guarantee business/legal truth.  
  - 1.5 marks for the banking interest monthly vs. daily compounding regulatory example.  
- **Common Mistake Warning:** Claiming that a verified requirement is always valid.

### Question 7 Guide Answer
- **Model Answer:**  
  - **Modifiability:** A quality attribute of an SRS that ensures it can be updated easily, consistently, and without introducing errors. It requires unique labeling, a logical organizational structure, a comprehensive table of contents, and **no redundancy (each requirement appears exactly once)**.  
  - **Atomicity:** A quality attribute where each individual requirement encapsulates exactly one discrete functional behavior or rule.  
  - **Why Copy-Pasting Causes Severe Defects:** If a session timeout rule is duplicated across 12 different functional sections, when security policies mandate an update (e.g., shortening timeout from 15 min to 5 min), analysts inevitably update some occurrences (e.g., 10 sections) and miss others (2 sections). This introduces immediate **internal inconsistency**, leading developers to implement conflicting timeout timers across different screens and introducing security vulnerabilities.  
- **Marking Scheme:**  
  - 1 mark for defining Modifiability and Atomicity.  
  - 1.5 marks for explaining how copy-pasting breaks single-point maintenance and causes internal contradictions.  
- **Common Mistake Warning:** Believing that repeating a requirement across multiple chapters makes it clearer or reinforces its importance.

### Question 8 Guide Answer
- **Model Answer:**  
  According to the Standish Group CHAOS Study (1994), incomplete requirements directly cause 12.3% of project failures and cost overruns through three distinct mechanisms:  
  1. **Artificially Underestimated Budgets & Schedules:** Initial project cost and duration estimates are calculated based solely on specified features. Because critical operational workflows and error handling were omitted, the initial budget is vastly underfunded, leading to inevitable financial collapse when reality hits.  
  2. **Exponentially Costlier Downstream Rework:** Requirements omitted during early engineering must eventually be built during system integration or after customer deployment. Catching and retrofitting a missed requirement during coding or production costs **10x to 100x more** than specifying it during early requirements engineering.  
  3. **Customer Dissatisfaction & System Rejection:** The software may pass 100% of the test cases written for the specified features, but when end-users attempt daily work, essential operational capabilities are missing, causing stakeholders to reject the delivered system as unfit for purpose.  
- **Marking Scheme:**  
  - 2.5 marks total: ~0.83 marks for each mechanism (Underestimated Budgets, 10x–100x Cost of Rework, Customer Rejection) detailed accurately from the lecture.  
- **Common Mistake Warning:** Stating that the 12.3% statistic refers to coding bugs rather than incomplete requirements.

### Question 9 Guide Answer
- **Model Answer:**  
  (a) **Quality Characteristic Violated:** **Testable / Verifiable** (and Clear & Unambiguous).  
  (b) **Why Test Cases Cannot Be Designed:** Words like "visually appealing" and "modern" are aesthetic, subjective opinions. A QA engineer cannot write an objective, deterministic test assertion that outputs `PASS` or `FAIL`. What looks "modern" to a designer may look unreadable to a data entry operator.  
  (c) **Verifiable Formulation:**  
  `FR-REP-01:` The sales summary report shall display all transaction totals grouped by product category in tabular layout conforming strictly to corporate UI Style Guide v2.1, rendering data table fonts in 11pt Arial with alternating row shading `#F2F2F2`.  
- **Marking Scheme:**  
  - 0.5 marks for identifying Testable / Verifiable.  
  - 1 mark for explaining the impossibility of objective binary pass/fail assertions for aesthetics.  
  - 1 mark for rewriting using an objective corporate UI style guide and explicit tabular layout rules.  
- **Common Mistake Warning:** Rewriting as "The report must be approved by the marketing manager as visually appealing," which defers subjectivity to a person rather than creating an objective technical test.

### Question 10 Guide Answer
- **Model Answer:**  
  (a) **Quality Characteristic Violated:** **Necessary & Prioritized** (every requirement must be prioritized to reflect its business necessity and delivery urgency).  
  (b) **Operational Chaos:** When everything is classified as "Critical / High Priority," nothing is prioritized. Developers are forced to make arbitrary choices about which features to build first. When project deadlines tighten or budgets shrink, developers drop essential foundational architecture in favor of superficial features, and project managers cannot plan phased delivery increments.  
  (c) **Prioritization Staging:** Requirements must be categorized into tiered release increments based on business value, implementation cost, and technical risk:  
  - *Tier 1 (High / MVP):* Mandatory for initial system launch (Sprint 1–2).  
  - *Tier 2 (Medium):* Valuable enhancements scheduled for subsequent releases (Sprint 3–4).  
  - *Tier 3 (Low):* Nice-to-have capabilities deferred to future iterations.  
- **Marking Scheme:**  
  - 0.5 marks for identifying Necessary & Prioritized.  
  - 1 mark for explaining developer unguided choices and inability to manage scope crunches.  
  - 1 mark for describing tiered release increments (Tier 1/High $\rightarrow$ Tier 2/Medium $\rightarrow$ Tier 3/Low).  
- **Common Mistake Warning:** Believing that marking all requirements as "High" ensures developers work faster.

### Question 11 Guide Answer
- **Model Answer:**  
  - **Evaluation:** The project manager's rationale is fatally flawed and violates basic software engineering economics.  
  - **Cost-of-Rework Escalation Factor:** The lecture establishes that discovering and resolving a requirements error during requirements validation costs a baseline of $1\times$. If the requirement defect is allowed to slip into design, coding, system testing, or production, the cost of downstream rework escalates **exponentially by 10x to 100x**.  
  - **Application to Infusion Pump:** For a safety-critical life-support system like an infusion pump, a requirements omission discovered during testing requires scrapping already-written code, re-architecting hardware firmware, and re-submitting for regulatory certification. Skipping two weeks of validation to save time will result in months of downstream testing delays and hundreds of thousands of dollars in rework.  
- **Marking Scheme:**  
  - 1 mark for rejecting the PM's plan with economic justification.  
  - 1.5 marks for explaining the 10x to 100x downstream cost escalation factor from the lecture.  
- **Common Mistake Warning:** Agreeing with the project manager that late testing catches everything with minimal consequence.

### Question 12 Guide Answer
- **Model Answer:**  
  (a) **Missing Dimension:** **Completeness of Individual Requirements** (specifically omitting boundary conditions, exception states, and error handling paths).  
  (b) **"No More, No Less" Principle:**  
  - *"No Less":* A complete requirement must specify not only the "happy path" (normal user input and expected outcome), but also all edge cases, environmental failures (e.g., network disconnects, disk full), invalid inputs, and explicit system recovery responses.  
  - *"No More":* A requirement must avoid unnecessary technical embellishments, extraneous features not requested by users, or prematurely constraining software architecture (avoiding scope bloat and "gold plating").  
- **Marking Scheme:**  
  - 1 mark for naming Completeness of Individual Requirements (error/exception paths).  
  - 1.5 marks for explaining both halves of "no more, no less" (exhaustiveness of conditions vs. avoiding extraneous gold-plating).  
- **Common Mistake Warning:** Assuming "completeness" means writing as much descriptive text as possible.

### Question 13 Guide Answer
- **Model Answer:**  
  **The Seven Interpretations of "Requirements Completeness":**  
  1. **Completeness of Requirements Analysis Models:** Visual diagrams (DFDs, ERDs, State Transition Diagrams) model all operational states, processes, data entities, and transitions without dead ends or missing flows.  
  2. **Completeness of Individual Requirements:** Every single requirement statement specifies all user inputs, algorithmic computations, expected outputs, boundary values, and error-handling conditions.  
  3. **Completeness of Requirement Metadata:** Each requirement record in the requirements management repository has all mandatory attributes filled out (unique ID, priority tier, author, origin/source, version, and status).  
  4. **Completeness of Requirements Repositories:** The central management repository contains all known user classes, use cases, business rules, and product backlog items without missing functional domains.  
  5. **Completeness of the Set of Requirements Documents:** The project possesses the complete suite of necessary documentation artifacts (Vision & Scope Document, Use Case Catalog, SRS, and Data Dictionary).  
  6. **Completeness of Individual Specification Documents:** Every standardized section, subsection, and appendix of the adopted document template (e.g., IEEE 830) is fully completed with no sections left blank or marked "TBD".  
  7. **Completeness of the Requirements Baseline:** The formally frozen set of requirements approved for an upcoming sprint or release contains all necessary capabilities required to proceed to architectural design and implementation.  
- **Marking Scheme:**  
  - 4 marks total: ~0.57 marks per interpretation accurately named and explained with its verification scope.  
- **Common Mistake Warning:** Listing generic qualities like "clear" or "testable" instead of the 7 specific interpretations of Completeness.

### Question 14 Guide Answer
- **Model Answer:**  
  **Requirements Quality Inspection Checklist Artifact:**  
  1. **Dimension 1: Unambiguity**  
     - *Diagnostic Rule:* Does the requirement statement possess exactly one interpretation shared by both business users and developers? Is it completely free of subjective, qualitative adjectives (e.g., "fast," "intuitive," "user-friendly," "robust," "scalable") and weak auxiliary verbs ("should," "might")?  
  2. **Dimension 2: Testability / Verifiability**  
     - *Diagnostic Rule:* Can a QA engineer design a finite, objective, and cost-effective test case (unit test, automated integration test, or inspection) that produces a definitive binary `PASS` or `FAIL` outcome? Does it include quantifiable acceptance metrics?  
  3. **Dimension 3: Feasibility**  
     - *Diagnostic Rule:* Is the capability technologically achievable within the constraints of the target hardware architecture, bandwidth limits, team technical competency, approved budget, and project schedule?  
  4. **Dimension 4: Modifiability**  
     - *Diagnostic Rule:* Is the requirement atomic, assigned a unique, persistent identifier, and documented exactly once in the specification, so that future changes require modifying only one single specification location?  
- **Marking Scheme:**  
  - 3 marks total: 0.75 marks per dimension with an explicit, rigorous diagnostic verification rule.  
- **Common Mistake Warning:** Formulating rules as vague questions (e.g., "Is it good?") rather than verifiable diagnostic criteria.

### Question 15 Guide Answer
- **Model Answer:**  
  **Consequences of Poor SRS Risk Analysis Matrix:**  
  | Impact Dimension | Specific Risk & Downstream Operational Manifestation |
  | :--- | :--- |
  | **1. Communication** | Vague, ambiguous natural language creates an interpretation gap where developers build what they *assume* was intended, resulting in a delivered product that fails to match user mental models. |
  | **2. Cost & Schedule** | Omitted requirements cause artificial underbidding during planning, triggering endless change requests, continuous contractual renegotiations, and 10x–100x rework costs that delay deployment. |
  | **3. System Quality & Defect Density** | Overlooked nonfunctional requirements (concurrency, failover, throughput, encryption) lead to server crashes under peak load, database deadlocks, and severe security breaches in production. |
  | **4. Traceability & Verification** | Non-verifiable specifications prevent QA engineers from authoring objective pass/fail test cases; requirements cannot be mapped to code commits or verified in acceptance test runs. |  
- **Marking Scheme:**  
  - 3 marks total: 0.75 marks per dimension with detailed operational consequences from the lecture.  
- **Common Mistake Warning:** Treating all consequences as simply "losing money" without distinguishing between communication, quality, and traceability failures.

### Question 16 Guide Answer
- **Model Answer:**  
  (a) **Quality Characteristic Violated:** **Correctness** (the requirement did not accurately represent an authorized, legally valid capability).  
  (b) **Why Internal QA Tests Failed to Catch It:** Internal QA test cases only verify that the software behaves according to the written SRS. Because the SRS specified monthly compounding, QA authored unit tests expecting monthly calculation and marked them `PASS`. The system was "built right" (verified), but was the "wrong product" (invalid).  
  (c) **Boundary Between Verification and Validation:**  
  - *Verification* confirmed that the code matched the written specification (monthly interest ran without bugs).  
  - *Validation* failed because nobody checked the specification against external statutory banking regulations (daily compounding legal mandate). Validation evaluates correctness against the external world, whereas Verification evaluates consistency against internal documents.  
- **Marking Scheme:**  
  - 0.5 marks for identifying Correctness.  
  - 0.5 marks for explaining why QA pass/fail tests cannot detect specification errors.  
  - 0.5 marks for explaining the external legal boundary of Validation vs. internal document boundary of Verification.  
- **Common Mistake Warning:** Claiming the developers introduced a bug; the code executed exactly as specified.

### Question 17 Guide Answer
- **Model Answer:**  
  (a) **Quality Characteristic Violated:** **Modifiability** (and **Consistency** once the partial edit occurred).  
  (b) **Operational Production Defect:** Two subsystem modules retained the old 15-minute timeout, while ten modules enforced the new 5-minute timeout. When users navigated from one subsystem to another, their sessions either terminated prematurely or remained open unexpectedly, violating hospital privacy regulations and confusing clinical users.  
  (c) **Modifiable Specification Structure:** The session timeout rule should have been documented **atomically exactly once** in the Security Nonfunctional Requirements section under a unique identifier (e.g., `NFR-SEC-014`). All other subsystem specifications should have simply cross-referenced `NFR-SEC-014`. Modifying the timeout would then require editing exactly one line in the entire SRS.  
- **Marking Scheme:**  
  - 0.5 marks for identifying Modifiability.  
  - 0.5 marks for explaining the mixed-state production bug (some screens 15 min, others 5 min).  
  - 0.5 marks for the single-point atomic definition + cross-referencing structure.  
- **Common Mistake Warning:** Suggesting that the analysts should have remembered to edit all 12 documents, failing to understand that the structural flaw is redundancy.

### Question 18 Guide Answer
- **Model Answer:**  
  (a) **Primary Quality Defect:** **Incompleteness** (and **Ambiguity**). The requirement stated that charges shall be calculated, but completely omitted the pricing model, mathematical formula, meter readings, seasonal rates, and tiered volume thresholds.  
  (b) **Breakdown of Intention vs. Functionality:**  
  - *Utility Intention:* Expected a tiered algorithmic utility formula: $\text{Charge} = \text{Metered Flow} \times \text{Tiered Rate}$.  
  - *Delivered Functionality:* The developer delivered a static flat-rate calculation: $\text{Charge} = \$45$. The developer technically satisfied the literal sentence ("calculated utility charges"), but completely failed customer operational intent.  
  (c) **Contractual Responsibility:** In formal Requirements Engineering, **the author of the requirements specification (the business analyst / contracting entity)** bears primary responsibility for operational omissions. If a specification is approved with missing algorithms, developers are legally protected when delivering any logical interpretation that satisfies the literal text. This is why thorough **Requirements Validation** before baseline sign-off is contractually mandatory.  
- **Marking Scheme:**  
  - 0.5 marks for identifying Incompleteness and Ambiguity.  
  - 0.5 marks for contrasting the tiered flow formula intention with the flat-rate delivery.  
  - 1 mark for analyzing contractual responsibility and the imperative of Validation before sign-off.  
- **Common Mistake Warning:** Blaming developers for being lazy, ignoring the fact that incomplete requirements legally permit arbitrary implementation.

