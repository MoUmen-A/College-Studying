# Question Bank: Chapter 2 — Requirements Analysis & Specification

> **Subject:** Software Requirements Engineering  
> **Chapter:** Chapter 2 — Requirements Analysis & Specification  
> **Total Marks:** 50 | **Questions:** 18  
> **Instructions:** Answer all questions. Write in full sentences. Partial marks are awarded for correct reasoning even if the final answer is incomplete.

---

## 🎓 Examinee Strategic Briefing: How to Solve & Critical Pitfalls to Avoid

Before attempting this exam, review this mental roadmap to guide your problem-solving and prevent common errors:

### 1. How to Approach Each Section:
- **Section A (Defect Diagnosis & Surgical Rewrite):**
  - **Decouple Business Logic from Interfaces:** Never combine mathematical algorithms (e.g., interest calculation) with communication protocols (e.g., payment API) in a single requirement.
  - **Apply Subsystem Allocation:** Separate Hardware (readers/locks), Software (databases/logic), and Human Roles (guards/operators).
  - **Formalize Business Rules:** Write business rules using structured propositional logic (`IF... AND... THEN... ELSE...`) with explicit numerical boundaries.
- **Section B (Conceptual Discrimination):**
  - **Iterative Nature:** Emphasize the feedback loops: Analysis exposes gaps $\rightarrow$ Elicitation; Specification forces precision $\rightarrow$ Analysis; Validation uncovers defects $\rightarrow$ Elicitation.
  - **Modeling vs. Prototyping:** Prototypes show UI workflows; formal models (DFDs, ERDs, STDs, Decision Tables) expose logic deadlocks, unreachable states, and cardinality violations.
  - **Interfaces:** Differentiate *Software Interfaces* (application contracts/APIs) from *Communication Interfaces* (transport protocols, encryption, latency limits).
  - **RTM & CCB:** Explain how the RTM's bidirectional links reveal upstream business impacts and downstream code/test impacts during CCB Impact Analysis.
- **Section C (Elicitation & Technique Strategy):**
  - **Prioritization Scoring:** Balance *Business Value*, *Implementation Cost*, and *Technical Risk* to stage features into releases.
  - **State Machines:** Choose State-Transition Diagrams for reactive, state-dependent behavior, explaining why prose leaves transitions unhandled.
  - **Business Rules Assets:** State that business rules belong in an enterprise repository, referenced only by persistent rule IDs (`BR-XXX-01`).
- **Section D (Artifact Construction):**
  - **Data Dictionary:** Populate all 5 mandatory fields: Name, Data Type/Format, Valid Range/Enumeration, Optionality/Default, and Semantic Description/Error Code.
  - **Subsystem Allocation Matrix:** Explicitly provide rows for Hardware, Software, and Human Roles with distinct responsibilities.
  - **Change Impact Checklist:** Include assessment criteria across Schedule, Cost, Technical Architecture, and Quality/Regression Risk.
- **Section E (Case Study Analysis):**
  - Analyze why renumbering requirements destroys persistent traceability and breaks automated testing.
  - Detail why standard templates (IEEE 830) prevent the accidental omission of critical NFRs.

### 2. Top Cognitive Traps to Avoid:
1. ❌ **Trap 1: Renumbering Requirements.** Renumbering is *never* good practice; it breaks traceability matrices and corrupts test suite mappings.
2. ❌ **Trap 2: Allocating Software Tasks to Human Roles.** Allocating requirements means defining operational responsibilities for physical devices, software engines, and human procedures.
3. ❌ **Trap 3: Vague Data Dictionary Ranges.** Never define data types simply as "number" or "text"; specify `DECIMAL(6,2)` or `CHAR(12)` with explicit minimum and maximum boundaries.

---

## SECTION A — Defect Diagnosis & Surgical Rewrite [15 marks | 4 questions]

### Question 1 (3 marks)
Review the following requirement extracted from an online banking system draft specification:  
*"The system should calculate interest accurately and be properly integrated with external payment APIs."*  
(a) Identify all quality defects by name based on the lecture material (focusing on modal verbs, ambiguity, and interface specification).  
(b) Explain why coupling business algorithm calculation with interface integration in a single statement causes downstream engineering failures.  
(c) Surgically rewrite this into two distinct, atomic requirements (`FR-BNK-01` and `FR-BNK-02`) using RFC 2119 `SHALL` syntax.

### Question 2 (4 marks)
An analyst documented the following statement in an enterprise access control specification:  
*"Security guards and cameras will ensure that only authorized employees enter the server room, and an alert will be sent if a badge is invalid."*  
(a) Identify the architectural analysis defect in this statement according to the **Subsystem Allocation** discipline.  
(b) Explain how requirements must be apportioned among hardware, software, and human procedural roles.  
(c) Surgically rewrite this statement by decomposing it into three cleanly allocated requirements: one for Hardware (`REQ-HW-01`), one for Software (`REQ-SW-01`), and one for Human Operator Role (`REQ-OPS-01`).

### Question 3 (4 marks)
Consider the following specification entry for a chemical order submission:  
*"Requirement 4.2.1: The chemical quantity field must be reasonable, not too large, and formatted appropriately."*  
(a) Identify all quality defects by name relative to **Data Dictionary** and **Specification** standards.  
(b) Explain how the absence of a Data Dictionary entry leads to conflicting developer assumptions during database schema creation.  
(c) Surgically construct a formal Data Dictionary entry for `Chemical_Order_Quantity` defining its technical data type, valid range, units of measure, and default error handling.

### Question 4 (4 marks)
A project team drafted the following business rule into a user story:  
*"Discount Rule: If a corporate customer buys lots of chemicals, give them our standard 15% VIP discount, unless their credit rating is bad."*  
(a) Identify all defects by name (focusing on ambiguity, lack of business rule cataloging, and decision logic).  
(b) Explain why business rules must be treated as independent enterprise assets rather than embedded directly into software user stories.  
(c) Surgically rewrite this rule into a formal, unambiguous Decision Table or nested propositional logic statement assigning concrete, verifiable thresholds.

---

## SECTION B — Conceptual Discrimination [10 marks | 4 questions]

### Question 5 (2.5 marks)
Explain why **Requirements Development** is inherently an **iterative process** rather than a linear, one-pass waterfall sequence. Describe the feedback loops between Analysis, Specification, and Validation as presented in the lecture.

### Question 6 (2.5 marks)
Contrast the operational purpose of **Requirements Modeling** with **Requirements Prototyping**. In your answer, explain what unique types of defects visual analysis diagrams (DFD, ERD, State Transition) expose that a UI prototype cannot reveal.

### Question 7 (2.5 marks)
Differentiate between **Software Interfaces** and **Communication Interfaces** within the External Interface Analysis discipline. Provide a concrete example of each from an enterprise client-server application.

### Question 8 (2.5 marks)
Explain the distinction between a **Requirements Traceability Matrix (RTM)** and a **Change Control Board (CCB)**. How does an RTM enable the CCB to perform an effective **Impact Analysis** before approving a proposed requirement modification?

---

## SECTION C — Elicitation & Technique Strategy [10 marks | 4 questions]

### Question 9 (2.5 marks)
A development team receives 120 conflicting feature requests from marketing, sales, and laboratory users for the upcoming product release, but the engineering budget can only accommodate 40 features.  
(a) Which Requirements Analysis activity must the analyst execute?  
(b) What analytical scoring dimensions should the team balance to prioritize these features objectively?  
(c) What artifact should be produced to stage these features into releases?

### Question 10 (2.5 marks)
During the specification phase, an analyst observes that developers frequently invent their own database column names and validation boundaries, resulting in mismatched API payloads between front-end and back-end teams.  
(a) What foundational specification deliverable was omitted?  
(b) What specific components must this deliverable contain to enforce cross-team domain consistency?

### Question 11 (2.5 marks)
An engineering team is designing a safety shutdown mechanism for an automated chemical synthesis reactor. The system transitions between four operational states: *Idle*, *Synthesizing*, *Emergency Purge*, and *Maintenance*.  
(a) Which requirements modeling diagram is best suited to specify the exact conditions under which the system transitions between these states?  
(b) Why is natural language prose inadequate for specifying complex state-dependent reactive behavior?

### Question 12 (2.5 marks)
The corporate legal division modifies the national tax withholding and chemical tariff regulations. Because the software team embedded tax calculations directly inside hundreds of individual UI script files, updating the system requires four months of code refactoring.  
(a) What specification best practice was violated?  
(b) How should business rules be cataloged and maintained across the enterprise?

---

## SECTION D — Artifact Construction [10 marks | 3 questions]

### Question 13 (4 marks)
Construct a formal **Data Dictionary Table Artifact** for three core data elements in a Chemical Management System:  
1. `Container_ID`  
2. `Chemical_Hazard_Class`  
3. `Storage_Temperature_Celsius`  
For each element, specify: (a) Data Type / Format, (b) Valid Range / Permitted Values, (c) Optionality (Mandatory vs. Optional), and (d) Brief Semantic Description.

### Question 14 (3 marks)
Construct a **Subsystem Allocation Specification Matrix** for a **Biometric Smart Access Security Door**, allocating the system's operational requirements across the three essential subsystem tiers: **Hardware**, **Software**, and **Human Operator Roles**, providing at least two explicit responsibilities for each tier.

### Question 15 (3 marks)
Construct a formal **Change Impact Analysis Checklist** comprising four distinct assessment dimensions (Schedule, Cost, Technical Architecture, Quality/Regression) that a Change Control Board (CCB) must evaluate before approving a change to a baselined requirement.

---

## SECTION E — Case Study Analysis [5 marks | 3 questions]

### Question 16 (1.5 marks)
*Mini-Case A:* An enterprise software team labeled requirements in their SRS sequentially as `Req 1`, `Req 2`, `Req 3`... up to `Req 250`. In month four, the client deleted `Req 45` and inserted 10 new features into Section 2. The analyst renumbered all subsequent requirements from 46 to 260. Two weeks later, system integration testing completely collapsed.  
(a) What specification activity was violated?  
(b) Why did renumbering requirements cause catastrophic testing and traceability failure?  
(c) What naming convention should have been used instead?

### Question 17 (1.5 marks)
*Mini-Case B:* A hospital information system was built without adopting standard requirement templates (such as IEEE 830 / ISO 29148). The analysts wrote freeform text documents describing all functional screens. When the system was deployed, it experienced frequent downtime during network switchovers, crashed under 50 concurrent users, and failed international data security audits.  
(a) What critical category of requirements was omitted because a standardized template was not adopted?  
(b) Why does a standard template prevent this oversight?  
(c) Name two specific quality attributes that were overlooked.

### Question 18 (2 marks)
*Mini-Case C:* A mid-sized fintech startup experienced continuous friction between the software development team and business executives. The developers complained: *"The business keeps changing their minds every week,"* while executives complained: *"We asked for simple adjustments and the project is three months late and over budget."* An external audit revealed that changes were communicated verbally during coffee breaks, and no baselines were ever recorded.  
(a) Identify the two Requirements Management practices missing from this organization.  
(b) What organizational governance body must be instituted to resolve this friction?  
(c) Outline the step-by-step workflow required before any proposed modification is implemented into code.

---

# GUIDE ANSWERS & MARKING SCHEME

### Question 1 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Weak Auxiliary Verb:* "Should" denotes an optional guideline rather than a mandatory requirement.  
  2. *Subjective Adverbs:* "Accurately" and "properly" are non-quantifiable and impossible to test objectively.  
  3. *Compound Requirement / Conflation of Concerns:* Combines mathematical business logic (interest calculation) with external interface communications (payment API) in a single statement.  
  (b) **Explanation:** Coupling business logic with interface protocols prevents atomic verification. If the payment API is changed or unavailable, the interest calculation cannot be independently verified or reused.  
  (c) **Surgical Rewrite:**  
  - `FR-BNK-01:` The system shall compute daily compound interest on all savings balances exceeding \$1,000 using official Interest Algorithm `ALG-FIN-2024-B`.  
  - `FR-BNK-02:` The system shall transmit all approved payment transaction payloads to the External Payment Gateway API over TLS 1.3 conforming to Payment Interface Contract `INT-EXT-PAY-v3`.  
- **Marking Scheme:**  
  - 1 mark for identifying defects (modal "should", unmeasured "properly/accurately", compound nature).  
  - 1 mark for explaining the hazard of coupling algorithm logic with interface protocols.  
  - 1 mark for decomposing into two atomic requirements (`FR-BNK-01`, `FR-BNK-02`) using `SHALL`.  
- **Common Mistake Warning:** Retaining words like "properly" in the rewritten requirements instead of referencing explicit interface contracts or algorithms.

### Question 2 Guide Answer
- **Model Answer:**  
  (a) **Architectural Defect:** Violation of **Subsystem Allocation** (Activity 8 of Requirements Analysis). The requirement conflates hardware devices, software processing, and human operator procedures into an undifferentiated narrative sentence.  
  (b) **Explanation of Subsystem Allocation:** Complex systems comprise multiple tiers. Requirements must be explicitly allocated so that hardware engineers know what physical devices to procure/wire, software engineers know what business logic to code, and operations teams know what human standard operating procedures (SOPs) to enforce.  
  (c) **Surgical Decomposition:**  
  - `REQ-HW-01` *(Hardware):* The physical entry portal shall incorporate an optical RFID badge reader and an electromagnetic door strike lock rated for minimum 1,200 lbs holding force.  
  - `REQ-SW-01` *(Software):* Upon receiving badge scan data, the security server software shall validate the employee credential against the Active Directory authorization list within 500 ms and dispatch an audible alert log event if the credential is invalid.  
  - `REQ-OPS-01` *(Human Role):* Security guard personnel shall physically inspect visitor photo IDs and manually authorize temporary access badges for unbadged escort visitors.  
- **Marking Scheme:**  
  - 1 mark for identifying Subsystem Allocation violation.  
  - 1 mark for explaining hardware vs. software vs. human responsibility boundaries.  
  - 2 marks for three properly allocated requirements with explicit IDs (`REQ-HW-01`, `REQ-SW-01`, `REQ-OPS-01`).  
- **Common Mistake Warning:** Allocating the security guard's actions to the software subsystem.

### Question 3 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Extreme Ambiguity:* "Reasonable," "not too large," and "appropriately" are completely subjective.  
  2. *Missing Data Schema:* Omits data type, minimum/maximum numeric bounds, precision, and units of measure.  
  3. *Untestable Boundary Conditions:* Test engineers cannot construct boundary value test cases without defined limits.  
  (b) **Explanation:** Without a central Data Dictionary, front-end developers might define the field as an unrestricted string, back-end developers as a 16-bit integer (max 32,767), and database administrators as a decimal with 2 decimal places, causing data truncation, API payload errors, and system crashes.  
  (c) **Data Dictionary Entry Artifact:**  
  - *Data Element Name:* `Chemical_Order_Quantity`  
  - *Data Type / Format:* Unsigned Integer (`uint32`)  
  - *Valid Range / Values:* $1 \le \text{Quantity} \le 5,000$  
  - *Unit of Measure:* Integer count of standard containers  
  - *Default Value:* 1  
  - *Error Handling:* If input is $\le 0$ or $> 5,000$, the system shall reject the entry with error message `ERR-QTY-OUT-OF-BOUNDS`.  
- **Marking Scheme:**  
  - 1 mark for identifying subjective adjectives and missing schema definitions.  
  - 1 mark for explaining cross-tier developer misalignment.  
  - 2 marks for a complete Data Dictionary entry with data type, range, unit, and error handling.  
- **Common Mistake Warning:** Defining data type simply as "number" without specifying integer vs. float or valid numerical boundaries.

### Question 4 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Vagueness:* "Buys lots of chemicals" is non-quantifiable.  
  2. *Subjectivity:* "Bad credit rating" lacks an objective credit score threshold.  
  3. *Failure to Separate Business Rules:* The rule is written as an informal functional requirement rather than cataloged in a central enterprise business rules repository.  
  (b) **Explanation:** Business rules (pricing formulas, discount matrices, tax codes) exist independently of any individual software system. If embedded in code or user stories, when the corporate discount policy changes, developers must hunt through hundreds of code files. When cataloged separately, business rules are updated once at the enterprise policy level with full traceability to dependent requirements.  
  (c) **Surgical Rewrite (Formal Rule `BR-DISC-01`):**  
  ```
  IF (Customer_Annual_Volume >= $100,000)
     AND (Customer_Credit_Score >= 700)
  THEN Apply 15% VIP Discount to Order Subtotal;
  ELSE IF (Customer_Credit_Score < 700)
     THEN Flag Order for Credit Department Approval; No Discount;
  ELSE Apply 0% Standard Discount.
  ```  
- **Marking Scheme:**  
  - 1 mark for identifying non-quantifiable conditions ("lots of chemicals", "bad credit").  
  - 1.5 marks for explaining business rules as independent enterprise assets.  
  - 1.5 marks for structured formal logic with explicit thresholds (\$100k volume, 700 credit score).  
- **Common Mistake Warning:** Writing a functional requirement with `SHALL` instead of formulating the underlying enterprise Business Rule.

### Question 5 Guide Answer
- **Model Answer:**  
  - **Iterative Nature:** Requirements Development cannot execute as a rigid, one-way waterfall sequence because discovering, analyzing, documenting, and validating requirements are mutually dependent activities:  
    1. Eliciting preliminary needs triggers **Analysis** modeling, which uncovers gaps, ambiguities, and logical contradictions that require immediate further **Elicitation**.  
    2. Documenting requirements during **Specification** forces rigorous phrasing, exposing hidden assumptions that demand deeper **Analysis**.  
    3. Reviewing test cases during **Validation** reveals missing exception workflows and unfeasible constraints, feeding defect reports back into **Elicitation** and **Analysis**.  
- **Marking Scheme:**  
  - 1 mark for refuting the linear waterfall model.  
  - 1.5 marks (0.5 each) for describing the specific feedback loops: Analysis $\rightarrow$ Elicitation, Specification $\rightarrow$ Analysis, and Validation $\rightarrow$ Elicitation.  
- **Common Mistake Warning:** Confusing the iterative lifecycle of Requirements Development with Agile software sprint execution.

### Question 6 Guide Answer
- **Model Answer:**  
  - **Requirements Modeling:** Uses formal visual diagrams (DFDs, ERDs, State Transition Diagrams, Decision Tables) to systematically expose structural contradictions, redundant data paths, missing logical states, and inconsistent transitions across the problem space.  
  - **Requirements Prototyping:** Builds tangible user interface mockups and interactive wireframes to validate user workflows, confirm look-and-feel expectations, and help stakeholders visualize features they cannot articulate.  
  - **Unique Defects Exposed by Modeling:**  
    1. *Deadlock or Unreachable States:* State transition models expose system states from which there is no exit transition (prototypes only show happy-path screens).  
    2. *Data Entity Inconsistencies & Cardinality Violations:* ERDs expose many-to-many relationship anomalies and orphaned data tables.  
    3. *Missing Conditional Logic Branches:* Decision tables reveal unhandled combinations of input variables.  
- **Marking Scheme:**  
  - 1 mark for contrasting visual structural analysis (Modeling) with interactive behavioral validation (Prototyping).  
  - 1.5 marks for explaining specific defects exposed exclusively by models (unreachable states, data relationship anomalies, missing logical branches).  
- **Common Mistake Warning:** Claiming that prototypes replace the need for modeling; prototypes often conceal fatal architectural and logic flaws behind attractive UI screens.

### Question 7 Guide Answer
- **Model Answer:**  
  - **Software Interfaces:** Specify the programmatic data exchange contracts, application programming interfaces (APIs), shared libraries, web services, and database query connections between your software and other external software applications.  
    - *Enterprise Example:* RESTful JSON API endpoint contract connecting the billing system to an external credit card verification service (e.g., Stripe API v3 over HTTPS).  
  - **Communication Interfaces:** Specify the physical and network transport protocols, encryption standards, bandwidth constraints, and transmission mechanics required to move data packets across network boundaries.  
    - *Enterprise Example:* Specifying TLS 1.3 encryption, WebSocket full-duplex protocol over TCP port 443, with a maximum allowable network round-trip packet latency of 150 ms.  
- **Marking Scheme:**  
  - 1 mark for defining Software Interfaces with a software API example.  
  - 1 mark for defining Communication Interfaces with a network protocol/encryption example.  
  - 0.5 marks for contrasting application contracts vs. transport mechanisms.  
- **Common Mistake Warning:** Grouping API data formats and network cables into the same category without distinguishing software contracts from transport mechanics.

### Question 8 Guide Answer
- **Model Answer:**  
  - **Requirements Traceability Matrix (RTM):** A bidirectional grid linking business objectives $\rightarrow$ user requirements $\rightarrow$ functional specifications $\rightarrow$ architectural design components $\rightarrow$ source code modules $\rightarrow$ test cases.  
  - **Change Control Board (CCB):** A formal governance committee composed of project sponsors, lead architects, QA leads, and business analysts responsible for reviewing, evaluating, and approving or rejecting proposed requirement modifications.  
  - **How RTM Enables Impact Analysis:** When a stakeholder requests a modification to requirement `REQ-042`, the CCB queries the RTM. The matrix immediately reveals: (1) which upstream business objectives are affected, (2) which downstream functional requirements must be refactored, (3) which architectural components and database tables must be redesigned, and (4) which regression test suites must be re-run. Without the RTM, impact analysis is pure guesswork.  
- **Marking Scheme:**  
  - 1 mark for defining RTM and CCB.  
  - 1.5 marks for explaining how bidirectional links expose impacted modules, tests, and cost during impact analysis.  
- **Common Mistake Warning:** Assuming the CCB writes the code or that the RTM automatically accepts or rejects changes.

### Question 9 Guide Answer
- **Model Answer:**  
  (a) **Analysis Activity:** **Prioritize Requirements** (Activity 4 of Requirements Analysis).  
  (b) **Analytical Scoring Dimensions:** The team must evaluate and balance three core dimensions for each requirement:  
  1. *Business Value / Customer Benefit* (revenue generation, regulatory necessity, user satisfaction).  
  2. *Implementation Cost / Effort* (developer hours, architectural complexity).  
  3. *Technical & Architectural Risk* (unproven technology, external dependencies, performance bottlenecks).  
  (c) **Staging Deliverable / Artifact:** A **Staged Release Plan** or **Prioritized Requirements Matrix** mapping high-value/low-cost features to Release 1 (MVP) and deferring high-risk/low-value features to subsequent increments.  
- **Marking Scheme:**  
  - 0.5 marks for identifying Prioritize Requirements.  
  - 1.5 marks (0.5 each) for Value, Cost, and Risk dimensions.  
  - 0.5 marks for naming Staged Release Plan / Prioritization Matrix.  
- **Common Mistake Warning:** Suggesting that the project manager simply picks their favorite features or uses "first-come, first-served".

### Question 10 Guide Answer
- **Model Answer:**  
  (a) **Foundational Deliverable Omitted:** The **Data Dictionary** (Activity 5 of Requirements Analysis).  
  (b) **Required Components to Enforce Consistency:**  
  1. *Precise Data Item Name & Semantic Meaning* (domain definition agreed upon across all teams).  
  2. *Technical Data Type & Storage Format* (e.g., ISO 8601 UTC timestamp, 32-bit floating point).  
  3. *Valid Values / Enumerations & Boundary Ranges* (e.g., minimum and maximum thresholds).  
  4. *Nullability & Default Values* (whether the field is mandatory or optional).  
  5. *Composed Data Structures / Schemas* (exact hierarchical payload structures for APIs and database tables).  
- **Marking Scheme:**  
  - 1 mark for naming the Data Dictionary.  
  - 1.5 marks for listing at least 4 required components (name, data type, valid range/values, nullability/composites).  
- **Common Mistake Warning:** Calling the deliverable a "database schema" or "class diagram"; the Data Dictionary is the formal RE asset that defines semantic data items before schemas are generated.

### Question 11 Guide Answer
- **Model Answer:**  
  (a) **Modeling Diagram:** **State-Transition Diagram (STD)** or **State Table**.  
  (b) **Inadequacy of Natural Language:** Natural language prose is inherently sequential and struggles to represent concurrent, event-driven state changes. In complex reactive systems, prose inevitably omits invalid transitions (e.g., attempting to transition directly from *Maintenance* to *Synthesizing* without passing through *Idle* checks). State Transition Tables exhaustively map every state against every possible event, ensuring that forbidden transitions and error states are explicitly handled.  
- **Marking Scheme:**  
  - 1 mark for State-Transition Diagram / State Table.  
  - 1.5 marks for explaining why prose fails (omitted transitions, ambiguity in state-event matrices, inability to detect unreachable states).  
- **Common Mistake Warning:** Suggesting a Data Flow Diagram (DFD); DFDs model data movement across processes, NOT state-dependent reactive behavior.

### Question 12 Guide Answer
- **Model Answer:**  
  (a) **Specification Best Practice Violated:** **Record Business Rules Separately** (Activity 4 of Requirements Specification).  
  (b) **Cataloging & Maintenance Best Practice:** Business rules must be cataloged in an **enterprise-level business rules repository** as independent assets, assigned unique identifiers (e.g., `BR-TAX-014`), and maintained separately from individual application source code and user stories. Software requirements should merely cross-reference the business rule ID, allowing business logic or calculation engine formulas to be modified in one central repository without refactoring application interfaces.  
- **Marking Scheme:**  
  - 1 mark for identifying "Record Business Rules Separately".  
  - 1.5 marks for explaining the enterprise repository, unique rule ID referencing, and decoupling business policy from code.  
- **Common Mistake Warning:** Recommending that business rules be written directly inside the SRS functional requirements.

### Question 13 Guide Answer
- **Model Answer:**  
  **Data Dictionary Table Artifact:**  
  | Element Name | Data Type / Format | Valid Range / Permitted Values | Optionality | Semantic Description |
  | :--- | :--- | :--- | :--- | :--- |
  | `Container_ID` | String (`CHAR(12)`) prefixed with `"CNT-"` | Format: `CNT-[0-9]{8}` (e.g., `CNT-10048291`) | Mandatory | Unique global alphanumeric identifier encoded in optical barcode on physical chemical container. |
  | `Chemical_Hazard_Class` | Enumeration | `{'Flammable', 'Corrosive', 'Toxic', 'Oxidizer', 'Non-Hazardous'}` | Mandatory | Official regulatory hazardous material classification governing storage and disposal protocols. |
  | `Storage_Temperature_Celsius` | Floating Point (`DECIMAL(4,1)`) | $-80.0\ ^\circ\text{C} \le T \le +40.0\ ^\circ\text{C}$ | Optional (Default: $+20.0\ ^\circ\text{C}$) | Mandated environmental storage temperature required to maintain reagent chemical stability. |  
- **Marking Scheme:**  
  - 4 marks total: 1.33 marks per complete, technically rigorous entry containing name, data type, valid range/values, optionality, and semantic description.  
- **Common Mistake Warning:** Leaving out the valid range or specifying data types colloquially as "text" or "number".

### Question 14 Guide Answer
- **Model Answer:**  
  **Subsystem Allocation Specification Matrix — Smart Access Security Door:**  
  | Subsystem Tier | Subsystem Component | Allocated Operational Responsibilities |
  | :--- | :--- | :--- |
  | **Hardware** | Optical/RFID Reader & Magnetic Lock | 1. Capture optical barcode / RFID badge data and transmit raw bitstream to security server via Wiegand interface.<br/>2. Physically energize/de-energize the 1,200 lb electromagnetic door strike upon receiving digital release command. |
  | **Software** | Access Validation Engine & Alert Dispatcher | 1. Query the employee authorization database to verify that badge credentials match the current room access schedule.<br/>2. Log all access attempts with UTC timestamp, and trigger security console alerts if three consecutive unauthorized scans occur within 60 seconds. |
  | **Human Role** | Security Guard / Front Desk Operator | 1. Physically verify photo identification for unbadged visitors and issue temporary visitor escort credentials.<br/>2. Respond physically to emergency security console tamper alerts within 3 minutes of dispatch. |  
- **Marking Scheme:**  
  - 1 mark for Hardware allocation (physical capture, locking).  
  - 1 mark for Software allocation (credential validation, logging/alerts).  
  - 1 mark for Human Role allocation (manual ID check, alarm response).  
- **Common Mistake Warning:** Assigning software database queries to the hardware tier.

### Question 15 Guide Answer
- **Model Answer:**  
  **CCB Change Impact Analysis Checklist Artifact:**  
  1. **Schedule Impact:**  
     - What is the estimated delta in person-hours required to design, code, and test the change?  
     - Does implementing this change delay the approved milestone or critical path delivery date?  
  2. **Cost & Resource Budget Impact:**  
     - What is the total financial cost of the rework across engineering, QA, and documentation?  
     - Does this require procuring additional hardware, software licenses, or specialized consultants?  
  3. **Technical & Architectural Architecture Impact:**  
     - Does the modification alter external software/communication interface contracts or database schemas?  
     - Does the change compromise nonfunctional requirements (e.g., latency, throughput, memory consumption)?  
  4. **Quality & Regression Risk:**  
     - How many dependent requirements, modules, and test cases are impacted in the Traceability Matrix (RTM)?  
     - What is the probability of introducing regression defects into previously verified production features?  
- **Marking Scheme:**  
  - 3 marks total: 0.75 marks per dimension (Schedule, Cost, Architecture, Quality/Risk) with explicit assessment criteria.  
- **Common Mistake Warning:** Evaluating only developer coding time while ignoring regression testing and architectural impact.

### Question 16 Guide Answer
- **Model Answer:**  
  (a) **Specification Activity Violated:** **Uniquely Label Each Requirement** (Activity 3 of Requirements Specification).  
  (b) **Why Renumbering Caused Collapse:** Renumbering destroys **persistent identification**. Test suites, architecture diagrams, traceability matrices, and defect trackers reference requirements by their unique ID. When `Req 45` was deleted and subsequent items were shifted, test cases written for the old `Req 46` were now evaluating the functionality of the old `Req 47`. All bidirectional traceability collapsed, rendering test results meaningless.  
  (c) **Recommended Naming Convention:** Use hierarchical, stable, alphanumeric identifiers incorporating a functional prefix (e.g., `REQ-CHEM-ORD-042` or `FR-PAY-015`). When a requirement is deleted, its identifier is retired/flagged as "Obsolete", and new requirements receive new, unassigned incremental IDs without shifting existing numbers.  
- **Marking Scheme:**  
  - 0.5 marks for identifying Uniquely Label Each Requirement.  
  - 0.5 marks for explaining the collapse of persistent traceability links and test mapping.  
  - 0.5 marks for specifying stable alphanumeric prefix conventions and ID retirement.  
- **Common Mistake Warning:** Believing that renumbering is standard clean-up practice in software documentation.

### Question 17 Guide Answer
- **Model Answer:**  
  (a) **Category Omitted:** **Non-Functional Requirements (NFRs)** and **External Interface Specifications**.  
  (b) **Why Templates Prevent Oversight:** Standard requirements document templates (such as IEEE 830 / ISO 29148) contain pre-structured, mandatory sections dedicated specifically to Performance, Reliability, Availability, Security, Hardware Interfaces, and Error Handling. They act as an exhaustive checklist; an analyst cannot finalize the document without explicitly addressing each quality dimension.  
  (c) **Overlooked Quality Attributes:**  
  1. *Availability / Reliability / Failover* (crashed during network switchovers).  
  2. *Performance / Scalability / Concurrency* (crashed under 50 concurrent users) or *Security / Compliance* (failed data security audits).  
- **Marking Scheme:**  
  - 0.5 marks for identifying Non-Functional Requirements.  
  - 0.5 marks for explaining the template as an exhaustive quality checklist.  
  - 0.5 marks for identifying the two quality attributes from the case.  
- **Common Mistake Warning:** Suggesting that the team simply forgot to write more user stories.

### Question 18 Guide Answer
- **Model Answer:**  
  (a) **Missing Requirements Management Practices:**  
  1. *Establish Baselines & Version Control* (requirements were never frozen or formally versioned).  
  2. *Establish a Formal Change Control Process* (changes were communicated verbally without impact analysis or approval).  
  (b) **Governance Body:** A **Change Control Board (CCB)** must be established, comprising the project sponsor, lead software architect, QA lead, and business analyst.  
  (c) **Step-by-Step Change Workflow:**  
  1. *Change Request Submission:* Stakeholder submits a formal Change Request Form detailing the proposed modification.  
  2. *Impact Analysis:* The business analyst and technical lead use the Traceability Matrix (RTM) to assess impacts on cost, schedule, architecture, and regression risk.  
  3. *CCB Evaluation:* The CCB reviews the impact assessment and formally decides to Approve, Reject, or Defer the request.  
  4. *Baseline Update & Communication:* If approved, the SRS baseline is incremented (e.g., v1.1), the RTM is updated, and revised requirements are dispatched to developers and testers.  
- **Marking Scheme:**  
  - 0.5 marks for identifying Baselines and Change Control.  
  - 0.5 marks for identifying the Change Control Board (CCB).  
  - 1 mark for the 4-step change workflow (Request $\rightarrow$ Impact Analysis $\rightarrow$ CCB Review $\rightarrow$ Baseline Update).  
- **Common Mistake Warning:** Suggesting that developers should simply refuse to talk to executives.

