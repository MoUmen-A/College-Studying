# Exam 02: True/False, Essay & Applied Cases (Analysis & Specification)

> **Subject:** Software Requirements Engineering  
> **Coverage:** Chapter 2 (Requirements Analysis & Specification)  
> **Total Marks:** 50 | **Time Allowed:** 90 Minutes  
> **Instructions:** Answer all questions in full sentences. For True/False questions, you must provide a concise technical justification; correct identification without justification earns only partial credit.

---

## 🎓 Examinee Strategic Briefing: How to Solve & Critical Pitfalls to Avoid

Before attempting this exam, review this mental roadmap to guide your problem-solving and prevent common errors:

### 1. How to Approach Each Section:
- **Section 1 (True / False):**
  - **The "Linear Waterfall" Fallacy:** Requirements development is *never* a one-pass linear conveyor belt; it is fundamentally iterative with constant feedback loops.
  - **Prototypes vs. Models:** Prototypes show *visual workflows*; they cannot detect unreachable states, data anomalies, or deadlocks that formal models (STDs, ERDs, Decision Tables) uncover.
  - **Identifier Persistence:** Renumbering requirements destroys bidirectional traceability and breaks automated test scripts. IDs must persist across the lifecycle.
- **Section 2 (Essays):**
  - **Prioritization Formula:** Remember the 3-dimensional balance: *Business Value ($V$)*, *Implementation Cost ($C$)*, and *Technical Risk ($R$)*.
  - **Reactive Systems:** When describing state transitions, explain why natural language prose causes catastrophic omissions and why State Tables guarantee exhaustive state-event coverage.
  - **Data Dictionary:** Structure your discussion around the exact metadata fields required to eliminate developer interpretation gaps across tiers.
- **Section 3 (Business Goals & Metrics):**
  - Distinguish strategic business targets from feature specifications.
  - When prioritizing, formulate clear decision rules allocating features to *Release 1 (MVP)*, *Release 2*, and *Deferred/Backlog*.
- **Section 4 (Requirements Issues & Subsystem Allocation):**
  - **Subsystem Allocation Triad:** Cleanly separate:
    1. *Hardware:* Physical readers, sensors, actuators, locks.
    2. *Software:* Database queries, validation engines, alert dispatchers.
    3. *Human Roles:* Standard operating procedures, manual credential checks, alarm response.
  - **Data Dictionary Entries:** Must contain: (1) Data Item Name, (2) Data Type/Format, (3) Valid Range/Boundary Limits, (4) Unit of Measure, (5) Optionality/Nullability, and (6) Explicit Error Handling Code.
  - **Business Rules:** Catalog separately using structured propositional logic (`IF... AND... THEN... ELSE...`).

### 2. Top Cognitive Traps to Avoid:
1. ❌ **Trap 1: Confusing Subsystem Allocation with Software Architecture.** Subsystem allocation is *not* front-end vs. back-end; it is *Hardware vs. Software vs. Human Operator Roles*.
2. ❌ **Trap 2: Renumbering Requirements for Document "Neatness".** Renumbering breaks every RTM link and causes automated regression tests to evaluate the wrong functional behaviors.
3. ❌ **Trap 3: Embedding Business Rules directly in User Stories.** Business rules are enterprise assets; embedding them in code or stories creates massive maintenance nightmares when policies change.

---

## SECTION 1 — True or False with Justification [12 marks | 6 questions]

### Question 1 (2 marks)
*Statement:* Requirements Development should be executed as a strict, linear, one-pass waterfall phase to prevent costly rework.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 2 (2 marks)
*Statement:* An interactive UI prototype is a complete substitute for requirements analysis modeling, rendering Data Flow Diagrams and State Tables unnecessary.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 3 (2 marks)
*Statement:* Renumbering requirements sequentially in an SRS (e.g., from `Req 1` to `Req 200`) after an obsolete requirement is deleted is considered an industry best practice for maintaining document neatness.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 4 (2 marks)
*Statement:* Business rules (such as corporate discount formulas or statutory tax calculations) should be embedded directly within individual user stories to maintain tight coupling with functional features.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 5 (2 marks)
*Statement:* A Requirements Traceability Matrix (RTM) is primarily used by developers to write automated unit test scripts without analyst supervision.  
*(State True or False and provide a rigorous technical justification from the lecture).*

### Question 6 (2 marks)
*Statement:* Allocating requirements across subsystems means dividing software modules strictly between front-end UI developers and back-end database administrators.  
*(State True or False and provide a rigorous technical justification from the lecture).*

---

## SECTION 2 — Deep Essay & Analytical Synthesis [14 marks | 3 questions]

### Question 7 (5 marks)
Explain why **Requirements Prioritization** (Activity 4 of Requirements Analysis) is an indispensable engineering discipline. Structure your essay around: (a) the three analytical scoring dimensions that must be balanced, (b) the operational chaos that occurs when all requirements are marked "High Priority", and (c) how an analytical prioritization matrix enables staged iterative release planning.

### Question 8 (5 marks)
Compare and contrast **State-Transition Diagrams (STDs)** with **Data Flow Diagrams (DFDs)**. In your answer, explain what unique system failure modes (such as unreachable states, deadlocks, and unhandled transition conditions) can only be uncovered by an STD, and illustrate why natural language prose fails to specify safety-critical reactive behavior.

### Question 9 (4 marks)
Analyze the technical and organizational role of the **Data Dictionary** (Activity 5 of Requirements Analysis). How does an enterprise Data Dictionary eliminate semantic ambiguity, and what specific components must each entry contain to ensure consistency across front-end developers, back-end engineers, database administrators, and QA testers?

---

## SECTION 3 — Case Study: Business Goals & Metrics [12 marks | 3 questions]

### Scenario Description
A commercial logistics enterprise operates a freight dispatching division with 350 vehicles. Currently, drivers record fuel purchases, border toll receipts, and engine maintenance logs on paper logbooks that are mailed weekly to central accounting. Processing paper logbooks requires 12 full-time accounting clerks, incurs an 8% calculation error rate on fuel tax filings, and delays preventative maintenance by an average of 3 weeks, leading to \$600,000 in premature engine replacements annually. The company has chartered the **Fleet Telematics and Dispatch System (FTDS)**.

### Question 10 (4 marks)
Structure the business foundations for the FTDS project:  
(a) Define the primary **Business Problem** currently burdening logistics operations.  
(b) Formulate two distinct, quantifiable **Business Objectives** for the FTDS investment.  
(c) Define two concrete **Success Metrics** that can be objectively evaluated during post-implementation audits.

### Question 11 (4 marks)
Author a formal, standard **6-Clause Vision Statement** for the Fleet Telematics and Dispatch System conforming strictly to the template taught in Chapter 2 (*For... Who... The... That... Unlike... Our product...*).

### Question 12 (4 marks)
The FTDS steering committee must prioritize 80 requested features against a tight Phase 1 budget.  
(a) Construct an analytical **Requirements Prioritization Framework** defining how the team will score features across the three core lecture dimensions: Business Value, Implementation Cost, and Technical Risk.  
(b) Formulate a decision rule assigning features to: *Release 1 (MVP)*, *Release 2 (Enhancement)*, and *Deferred/Backlog*.

---

## SECTION 4 — Case Study: Requirements Issues & Quality Diagnosis [12 marks | 3 questions]

### Scenario Description
During architectural review of the FTDS draft specification, several requirements are flagged for severe quality defects, lack of subsystem allocation, and missing interface contracts.

### Question 13 (4 marks)
*Draft Requirement 1:*  
*"The telematics device will monitor truck speed, alert dispatchers if speeding occurs, and drivers will drive safely."*  
(a) Identify the architectural analysis defect in this statement according to the **Subsystem Allocation** discipline.  
(b) Explain why mixing hardware sensor capture, software alerting, and human behavior into one narrative sentence cripples engineering contracts.  
(c) Surgically rewrite this statement by decomposing it into three cleanly allocated requirements: Hardware (`REQ-HW-FT-01`), Software (`REQ-SW-FT-01`), and Human Procedural Role (`REQ-OPS-FT-01`).

### Question 14 (4 marks)
*Draft Requirement 2:*  
*"The fuel quantity recorded during refueling must be reasonable and properly formatted."*  
(a) Identify all quality defects by name relative to **Data Dictionary** and **Specification** standards.  
(b) Explain how the lack of a Data Dictionary entry causes conflicting assumptions during database schema design and API payload serialization.  
(c) Surgically construct a formal Data Dictionary entry for `Refuel_Quantity_Liters` defining its data type, valid numerical range, unit of measure, and default error handling.

### Question 15 (4 marks)
*Draft Requirement 3:*  
*"Discount Rule: If a freight customer books lots of shipments, give them our standard preferred shipper discount, unless their billing history is unsatisfactory."*  
(a) Identify all defects by name (focusing on ambiguity, lack of business rule cataloging, and decision logic).  
(b) Explain why business rules must be cataloged in an enterprise repository separate from software user stories.  
(c) Surgically rewrite this rule into a structured propositional logic statement (`BR-LOG-01`) assigning concrete, verifiable volume and credit thresholds.

---

# GUIDE ANSWERS & MARKING SCHEME

### Question 1 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* Requirements Development is **inherently iterative**, not a linear, one-pass waterfall sequence. Elicitation uncovers preliminary user needs, which triggers Analysis modeling; modeling exposes ambiguities, gaps, and logical contradictions that demand immediate further Elicitation. Similarly, formalizing statements during Specification forces precise phrasing that uncovers deeper analysis gaps, and reviewing test cases during Validation reveals missing requirements. Forcing a rigid waterfall process results in building systems based on flawed early assumptions.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for explaining the iterative feedback loops between Elicitation, Analysis, Specification, and Validation.  
- **Common Mistake Warning:** Believing that a waterfall approach prevents rework; it actually delays rework until testing, making it 10x–100x more expensive.

### Question 2 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* UI prototypes make interactive user workflows and visual layout tangible, but they **cannot expose underlying structural, logical, or architectural defects**. Visual analysis models perform distinct, essential functions: State-Transition Diagrams expose unreachable states, deadlock conditions, and unhandled event transitions; Entity-Relationship Diagrams expose data cardinality anomalies and orphaned records; and Decision Tables expose missing conditional logic branches. Prototypes often conceal severe architectural and logical flaws behind attractive visual screens.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for contrasting UI prototypes with the unique structural verification capabilities of STDs, ERDs, and Decision Tables.  
- **Common Mistake Warning:** Answering True, believing that modern UI wireframes replace all backend analysis diagrams.

### Question 3 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* Renumbering requirements destroys **persistent identification**, which is fatal to the entire project lifecycle. Downstream artifacts—such as the Requirements Traceability Matrix (RTM), architectural design components, automated test scripts, defect tracking tickets, and change requests—reference requirements by their exact assigned identifiers. When items are renumbered, all historical links break: test cases evaluate the wrong functional behaviors, and audit trails are corrupted. Industry best practice requires retiring deleted IDs as "Obsolete" and assigning new, unassigned incremental IDs without shifting existing numbers.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for explaining the collapse of persistent traceability, broken test mapping, and the rule of retiring IDs.  
- **Common Mistake Warning:** Answering True, assuming that sequential numbering without gaps is desirable.

### Question 4 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* Business rules (statutory tax policies, corporate pricing discounts, regulatory compliance formulas) are **enterprise-level assets** that exist independently of any individual software application or user story. If embedded directly in code or user stories, when the enterprise business policy changes, developers must manually search through hundreds of code files and user stories across multiple applications, inevitably updating some and missing others. Best practice dictates that business rules must be cataloged in a central enterprise business rules repository, and software requirements should merely cross-reference their persistent identifiers.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for explaining business rules as independent enterprise assets and the maintenance disaster of embedding them in code/stories.  
- **Common Mistake Warning:** Believing that user stories should be completely self-contained with embedded business rules.

### Question 5 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* An RTM is not a coding script; it is a bidirectional governance grid linking business objectives $\rightarrow$ user requirements $\rightarrow$ functional specifications $\rightarrow$ design components $\rightarrow$ code modules $\rightarrow$ test cases. Its primary operational purpose is to ensure **completeness** (confirming no user requirements are orphaned or unbuilt) and to enable the Change Control Board (CCB) to perform **Change Impact Analysis** before approving proposed modifications, identifying exactly which downstream components and test suites are impacted.  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for defining RTM links and its primary role in Change Impact Analysis and completeness verification.  
- **Common Mistake Warning:** Thinking the RTM is only a testing tool.

### Question 6 Guide Answer
- **Model Answer:** **FALSE.**  
  *Justification:* Subsystem Allocation (Activity 8 of Requirements Analysis) does not refer to assigning software tasks to developers. It refers to apportioning requirements across the three fundamental physical and organizational tiers of a complex system: **Hardware** (sensors, locks, physical devices), **Software** (databases, calculation engines, business logic), and **Human Operator Roles** (guards, clerks, manual procedural policies).  
- **Marking Scheme:** 0.5 marks for FALSE; 1.5 marks for explaining allocation across Hardware, Software, and Human Procedural Roles.  
- **Common Mistake Warning:** Confusing subsystem allocation with software architectural partitioning (front-end vs. back-end).

### Question 7 Guide Answer
- **Model Answer:**  
  - **(a) Three Analytical Scoring Dimensions:**  
    1. *Business Value / Customer Benefit:* The commercial revenue, operational cost savings, regulatory necessity, or strategic advantage delivered to users.  
    2. *Implementation Cost / Effort:* The estimated person-hours, technical complexity, license fees, and resource expenditure required to build and test the feature.  
    3. *Technical & Architectural Risk:* The probability of technical failure, unproven third-party APIs, performance bottlenecks, or architectural volatility.  
  - **(b) Operational Chaos of "All High Priority":** When every requirement is tagged as "High/Critical," prioritization is completely destroyed. Developers are left to make unguided, subjective decisions about what to implement first. When schedules compress or budgets shrink, developers drop essential foundational architecture in favor of superficial features, and project managers cannot manage scope trade-offs.  
  - **(c) Staged Release Planning:** By plotting features onto an analytical matrix (Value vs. Cost/Risk), the team assigns high-value/low-cost features to *Release 1 (MVP)* to deliver immediate ROI, schedules high-value/high-risk features into *Release 2*, and defers low-value/high-cost features to future iterations or discards them entirely.  
- **Marking Scheme:**  
  - 1.5 marks for detailing the 3 dimensions (Value, Cost, Risk).  
  - 1.5 marks for explaining the collapse of scope control when all items are "High".  
  - 2 marks for explaining the staged release planning mechanism (MVP vs. subsequent increments).  
- **Common Mistake Warning:** Failing to include the "Technical Risk" dimension in the scoring formula.

### Question 8 Guide Answer
- **Model Answer:**  
  - **Data Flow Diagrams (DFDs):** Model the movement, storage, and transformation of data through sequential processes, depicting system inputs, data stores, external entities, and data outputs. DFDs show *what* data transformations happen, but ignore operational states and timing.  
  - **State-Transition Diagrams (STDs):** Model the dynamic, reactive behavior of a system across discrete operational states in response to internal or external events.  
  - **Unique Failure Modes Uncovered by STDs:**  
    1. *Unreachable / Orphaned States:* States that have outbound transitions but no inbound trigger path.  
    2. *Deadlock States:* Operational states from which there is no valid exit transition.  
    3. *Unhandled Transition Triggers:* Combinations of events and states that lack an explicit reaction (e.g., power loss during data synchronization).  
  - **Why Natural Language Prose Fails:** Natural language is inherently sequential and struggles to represent concurrent, event-driven state changes. Prose descriptions inevitably omit invalid transitions (e.g., attempting to transition directly from *Maintenance* to *Operating* without passing through *Diagnostics*), creating catastrophic safety and logic bugs in reactive systems. State tables provide an exhaustive mathematical matrix guaranteeing that all state-event pairs are explicitly defined.  
- **Marking Scheme:**  
  - 1 mark for defining DFDs (data flow/transformation) vs. STDs (states/reactive behavior).  
  - 2 marks for detailing unreachable states, deadlocks, and unhandled transition combinations.  
  - 2 marks for explaining why natural language fails (sequential bias, omitted transitions) and how state tables guarantee exhaustive coverage.  
- **Common Mistake Warning:** Claiming that DFDs show the sequence of program execution; DFDs show data transformation, not control flow.

### Question 9 Guide Answer
- **Model Answer:**  
  - **Role of the Data Dictionary:** A central repository containing formal, authoritative, and unambiguous definitions of every data element, data structure, schema, and allowable value used throughout the system. It eliminates semantic misunderstandings between business users, analysts, software engineers, and QA testers.  
  - **How it Eliminates Semantic Ambiguity:** Terms like "Order Date" could be interpreted as the moment a user clicks submit, the moment payment clears, or the moment the invoice is generated. A Data Dictionary provides an exact operational and semantic definition agreed upon across all teams.  
  - **Mandatory Components of Each Entry:**  
    1. *Data Element Name:* Persistent, standardized domain identifier.  
    2. *Technical Data Type & Format:* E.g., ISO 8601 UTC timestamp, 32-bit signed integer, string (`CHAR(12)`).  
    3. *Valid Values / Range Limits:* Explicit minimum/maximum numerical boundaries or permitted enumeration values.  
    4. *Optionality & Default Value:* Whether the field is mandatory (`NOT NULL`) or optional, and its default state.  
    5. *Semantic Description & Error Handling:* Plain-language business meaning and the error response triggered if inputs violate valid ranges.  
- **Marking Scheme:**  
  - 1 mark for defining the Data Dictionary's role.  
  - 1 mark for explaining semantic alignment across teams.  
  - 2 marks for detailing at least 4 of the 5 mandatory entry components.  
- **Common Mistake Warning:** Defining data type loosely as "text" or "number" without specifying storage format or range boundaries.

### Question 10 Guide Answer
- **Model Answer:**  
  (a) **Business Problem:** Manual paper logbook reporting causes severe fulfillment latency (weekly mail delays), an 8% calculation error rate on fuel tax filings, and delayed maintenance that results in \$600,000 in premature annual engine replacement expenses.  
  (b) **Business Objectives:**  
  1. Reduce annual fleet engine replacement expenses by 80% within the first year of FTDS operation through automated telematics preventative maintenance alerts.  
  2. Reduce fuel tax filing calculation error rates from 8% to under 0.5% within 6 months of system deployment.  
  (c) **Success Metrics:**  
  1. Automated odometer and engine telemetry transmission shall achieve $\ge 99.8\%$ daily capture reliability across all 350 active vehicles during operational testing.  
  2. Time required for accounting staff to generate quarterly fuel tax audit reports shall decrease from 14 business days to under 4 hours.  
- **Marking Scheme:**  
  - 1 mark for Business Problem.  
  - 1.5 marks for two quantifiable Business Objectives (target percentage + timeframe).  
  - 1.5 marks for two concrete Success Metrics with measurable thresholds.  
- **Common Mistake Warning:** Writing a functional requirement (e.g., "The system shall track fuel") instead of a strategic Business Objective.

### Question 11 Guide Answer
- **Model Answer:**  
  **Vision Statement Artifact — Fleet Telematics and Dispatch System:**  
  - **For** commercial logistics dispatchers and vehicle fleet managers,  
  - **Who** need real-time operational visibility into vehicle telemetry, fuel consumption, and engine diagnostics,  
  - **The** Fleet Telematics and Dispatch System **is an** enterprise vehicle management information system  
  - **That** will provide automated cellular/satellite data capture of truck speed, fuel consumption, GPS location, and diagnostic fault codes, eliminating \$600,000 in premature engine replacements in the first year.  
  - **Unlike** current paper driver logbooks and delayed weekly mail reporting processes,  
  - **Our product** will automatically generate real-time preventative maintenance dispatch orders and produce audited fuel tax compliance filings across all regional transit jurisdictions.  
- **Marking Scheme:**  
  - 4 marks total: ~0.65 marks per clause correctly completed following the 6-clause lecture template.  
- **Common Mistake Warning:** Inverting the "Unlike" and "Our product" clauses.

### Question 12 Guide Answer
- **Model Answer:**  
  (a) **Prioritization Framework:** Each requirement is scored on a 1–5 scale across three dimensions:  
  - *Business Value ($V$):* 1 (Low convenience) to 5 (Direct regulatory compliance / high financial ROI).  
  - *Implementation Cost ($C$):* 1 (Low effort / <40 hrs) to 5 (Extensive architectural refactoring / >300 hrs).  
  - *Technical Risk ($R$):* 1 (Proven standard technology) to 5 (Unproven hardware integration / volatile API).  
  - *Composite Priority Score:* $\text{Score} = \frac{V}{C \times R}$ (features with highest value and lowest cost/risk achieve the highest score).  
  (b) **Decision Rules for Staged Releases:**  
  - *Release 1 (MVP):* Score $\ge 0.5$ (mandatory regulatory features, high-value/low-cost core telematics).  
  - *Release 2 (Enhancement):* High value but high cost/risk ($V \ge 4$, $C \ge 4$). Scheduled after core architecture stabilizes.  
  - *Deferred / Backlog:* Low value ($V \le 2$) or unacceptably high risk ($R = 5$).  
- **Marking Scheme:**  
  - 2 marks for defining the scoring formula across Value, Cost, and Risk.  
  - 2 marks for clear decision rules allocating features to Release 1, Release 2, and Deferred.  
- **Common Mistake Warning:** Setting decision rules solely based on developer preference without balancing value against risk.

### Question 13 Guide Answer
- **Model Answer:**  
  (a) **Architectural Defect:** Violation of **Subsystem Allocation** (Activity 8 of Requirements Analysis). Conflates hardware sensors (speed tracking), software business logic (threshold alerting), and human driver operational responsibilities into a single run-on sentence.  
  (b) **Explanation:** Conflating subsystems creates contractual confusion: hardware suppliers do not know what physical interfaces to build, software developers cannot verify human driving behavior, and testers cannot author deterministic pass/fail tests.  
  (c) **Surgical Subsystem Allocation:**  
  - `REQ-HW-FT-01` *(Hardware):* The onboard telematics gateway shall sample vehicle wheel speed via the vehicle OBD-II/CAN-bus interface at a minimum frequency of 1.0 Hz and transmit telemetry packets over cellular 4G/LTE.  
  - `REQ-SW-FT-01` *(Software):* When received vehicle speed exceeds the posted highway speed limit by $> 10\ \text{km/h}$ for more than 30 consecutive seconds, the central dispatch software shall generate a High-Priority Speed Violation event on the dispatcher console within 5.0 seconds.  
  - `REQ-OPS-FT-01` *(Human Role):* Dispatcher personnel shall verbally contact drivers flagged with active High-Priority Speed Violations within 10 minutes to verify vehicle operational status.  
- **Marking Scheme:**  
  - 1 mark for identifying Subsystem Allocation violation.  
  - 1 mark for explaining hardware vs. software vs. human contractual boundaries.  
  - 2 marks for three properly allocated requirements with explicit IDs (`REQ-HW-FT-01`, `REQ-SW-FT-01`, `REQ-OPS-FT-01`) and `SHALL`.  
- **Common Mistake Warning:** Assigning the human driver's adherence to speed limits to the software subsystem.

### Question 14 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Extreme Ambiguity:* "Reasonable" and "properly formatted" are completely subjective.  
  2. *Missing Schema & Boundaries:* Fails to define data type, precision, minimum/maximum allowable fuel volume, and unit of measure (liters vs. gallons).  
  3. *Untestable:* Test engineers cannot construct boundary value test cases without defined limits.  
  (b) **Explanation:** Without a Data Dictionary, the mobile app developer may record fuel as an integer, the cloud backend as a floating-point number in gallons, and the database as a string, causing conversion errors, database truncation exceptions, and incorrect tax filings.  
  (c) **Data Dictionary Entry Artifact:**  
  - *Data Element Name:* `Refuel_Quantity_Liters`  
  - *Data Type / Format:* Decimal (`DECIMAL(6,2)`)  
  - *Valid Range / Values:* $5.00 \le \text{Volume} \le 1,200.00$  
  - *Unit of Measure:* Liters ($L$)  
  - *Default Value:* `NULL` (Mandatory user input)  
  - *Error Handling:* If input is $< 5.00$ or $> 1,200.00$, the system shall reject the entry with error code `ERR-VOL-OUT-OF-BOUNDS`.  
- **Marking Scheme:**  
  - 1 mark for naming defects (subjective adjectives, missing schema).  
  - 1 mark for explaining cross-system data corruption and payload errors.  
  - 2 marks for complete Data Dictionary entry with data type, range, unit, and error handling.  
- **Common Mistake Warning:** Omitting the decimal precision or defining valid range as "any positive number".

### Question 15 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Vague Conditions:* "Buys lots of shipments" is non-quantifiable.  
  2. *Subjective Logic:* "Unsatisfactory billing history" lacks objective criteria.  
  3. *Uncataloged Business Rule:* The pricing rule is written as an informal user requirement rather than cataloged in an enterprise business rules repository.  
  (b) **Explanation:** Business rules exist independently of specific software systems. If embedded in code or user stories, when the corporate pricing policy changes, developers must hunt through hundreds of code files. When cataloged separately, business rules are updated once at the enterprise level with full traceability to dependent requirements.  
  (c) **Surgical Rewrite (Formal Rule `BR-LOG-01`):**  
  ```
  IF (Customer_Monthly_Shipments >= 50)
     AND (Customer_Days_Sales_Outstanding <= 45)
  THEN Apply 12% Preferred Shipper Freight Discount to Invoice Subtotal;
  ELSE IF (Customer_Days_Sales_Outstanding > 60)
     THEN Flag Account for Credit Hold; Apply 0% Discount;
  ELSE Apply 0% Standard Freight Rate.
  ```  
- **Marking Scheme:**  
  - 1 mark for identifying non-quantifiable conditions ("lots of shipments", "unsatisfactory").  
  - 1.5 marks for explaining business rules as independent enterprise assets.  
  - 1.5 marks for structured formal logic with explicit thresholds (50 shipments, 45 DSO).  
- **Common Mistake Warning:** Writing a functional requirement with `SHALL` instead of formulating the underlying enterprise Business Rule.

