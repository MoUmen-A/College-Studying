# Question Bank: Chapter 2 — Requirements Elicitation

> **Subject:** Software Requirements Engineering  
> **Chapter:** Chapter 2 — Requirements Elicitation  
> **Total Marks:** 50 | **Questions:** 18  
> **Instructions:** Answer all questions. Write in full sentences. Partial marks are awarded for correct reasoning even if the final answer is incomplete.

---

## 🎓 Examinee Strategic Briefing: How to Solve & Critical Pitfalls to Avoid

Before attempting this exam, review this mental roadmap to guide your problem-solving and prevent common errors:

### 1. How to Approach Each Section:
- **Section A (Defect Diagnosis & Surgical Rewrite):**
  - **Differentiate Business Goals from Features:** If a prompt asks for a Business Objective, *never* write "The system shall display a button". Write: "Reduce X by Y% within timeframe Z".
  - **Disentangle Conflated Events:** If a sentence mixes human actions, hardware signals, and database checks, decompose it into atomic requirements.
- **Section B (Conceptual Discrimination):**
  - **Development vs. Management:** Development *builds* the baseline (Elicitation $\rightarrow$ Analysis $\rightarrow$ Specification $\rightarrow$ V&V); Management *controls and traces* changes to the baseline (CCB, RTM, Baselines, Issue Tracking).
  - **Context Diagram vs. Ecosystem Map:** Context Diagrams show direct terminators only; Ecosystem Maps show all interacting systems across the enterprise, including indirect systems with no direct API interface.
  - **Stakeholder Taxonomy:**
    - *Primary:* Hands-on daily operators (e.g., Chemists, Clerks).
    - *Secondary:* Indirectly affected stakeholders/auditors (e.g., IT auditors, EPA regulators).
    - *Key:* Executive sponsors and budget decision-makers (e.g., VP of R&D).
- **Section C (Elicitation & Technique Strategy):**
  - **Tacit Knowledge:** Uncovered exclusively through **Observation**; be sure to address the **Hawthorne Effect** and how habituation mitigates it.
  - **Dispute Resolution:** Always recommend **Requirements Workshops** with authorized decision-makers, not Brainstorming.
  - **Large Dispersed Populations:** Choose **Surveys/Questionnaires**, and pair with Focus Groups to resolve ambiguities.
- **Section D (Artifact Construction):**
  - **6-Clause Vision Statement:** Strictly memorize the formula: *For... Who... The... That... Unlike... Our product...*.
  - **Event Catalog:** Define the 3 types clearly: *Business* (human), *Temporal* (time/schedule), *Signal* (hardware sensor).
  - **Feature Tree:** Strictly structure into 3 hierarchical tiers: L1 Group $\rightarrow$ L2 Sub-Feature $\rightarrow$ L3 Detail.
- **Section E (Case Study Analysis):**
  - Explain why Brainstorming cannot replace formal Analysis, and why overlooking Secondary Stakeholders causes compliance shutdowns.

### 2. Top Cognitive Traps to Avoid:
1. ❌ **Trap 1: Writing a Functional Requirement when asked for a Success Metric.** Success metrics measure operational outcomes (e.g., "Order time $\le 10$ minutes on 80% of orders").
2. ❌ **Trap 2: Classifying Regulators as Key Stakeholders.** Key stakeholders are internal budget sponsors/funders; regulators are Secondary Stakeholders.
3. ❌ **Trap 3: Omitting the "Unlike" Clause in Vision Statements.** The "Unlike" and "Our product" clauses define competitive differentiation and cannot be skipped.

---

## SECTION A — Defect Diagnosis & Surgical Rewrite [15 marks | 4 questions]

### Question 1 (3 marks)
Consider the following statement drafted by a junior analyst for the Chemical Tracking System (CTS):  
*"The system should make ordering chemicals faster for scientists so they don't waste time."*  
(a) Identify all quality defects by name based on the lecture material.  
(b) Explain why mixing vague user goals with non-verifiable statements harms project execution.  
(c) Surgically rewrite this into a measurable Business Objective and an associated Success Metric complying with the metrics established in the lecture.

### Question 2 (4 marks)
Consider the following requirement statement extracted from a laboratory safety specification:  
*"Chemist places an order, the system checks EPA rules, and the container barcode is scanned quickly without delay."*  
(a) Identify the structural defects and category confusions in this statement based on scope and event taxonomy.  
(b) Explain why combining business events, signal events, and quality adjectives into a single requirement impairs software verification.  
(c) Surgically rewrite this statement into two distinct, atomic functional requirements (`FR-CTS-01` and `FR-CTS-02`) using RFC 2119 `SHALL` keywords.

### Question 3 (4 marks)
An analyst wrote the following vision statement for the Chemical Tracking System:  
*"Our system is an online software that allows employees to manage chemical containers and saves money compared to our old paper spreadsheets."*  
(a) Identify all defects in this statement relative to the standard 6-part Vision Statement template taught in the lecture.  
(b) Explain why an unstructured vision statement leads to scope creep and misaligned executive expectations.  
(c) Surgically rewrite this statement using the complete, standard 6-clause Vision Statement template (*For... Who... The... That... Unlike... Our product...*).

### Question 4 (4 marks)
Review the following requirement drafted for hazardous chemical disposal compliance:  
*"The software shall handle all government reports appropriately whenever toxic waste is moved."*  
(a) Identify all quality defects by name (focusing on ambiguity, completeness, and event triggers).  
(b) Explain what specific information a developer needs from the Event List and external regulatory terminators to implement this feature.  
(c) Surgically rewrite this requirement (`FR-CTS-03`) into a precise, verifiable functional requirement specifying the regulatory body and timing trigger.

---

## SECTION B — Conceptual Discrimination [10 marks | 4 questions]

### Question 5 (2.5 marks)
Differentiate between **Requirements Development** and **Requirements Management** within the overall Requirements Engineering discipline. Identify the four core sequential subdisciplines that constitute Requirements Development.

### Question 6 (2.5 marks)
Compare and contrast a **Business Problem / Opportunity** with a **Business Objective**, and explain how a **Success Metric** bridges the objective to verifiable post-release performance. Illustrate using the Chemical Tracking System example from the lecture.

### Question 7 (2.5 marks)
Contrast a **Context Diagram** with an **Ecosystem Map**. Explain under what enterprise architectural circumstances an Ecosystem Map provides critical information that a Context Diagram completely omits.

### Question 8 (2.5 marks)
Explain the distinction between **Primary**, **Secondary**, and **Key Stakeholders**. Using the Chemical Tracking System project described in the lecture, classify the Chemist, the IT Compliance Auditor, and the VP of Research & Development into their appropriate stakeholder categories and justify each.

---

## SECTION C — Elicitation & Technique Strategy [10 marks | 4 questions]

### Question 9 (2.5 marks)
A business analyst discovers that experienced laboratory technicians have unwritten routines and manual workarounds for tracking perishable reagents that do not appear in any standard operating procedure. Which elicitation technique is most effective for uncovering this "tacit knowledge," what psychological phenomenon must the analyst mitigate during its execution, and how?

### Question 10 (2.5 marks)
A software project must elicit requirements from 2,500 field engineers spread across 14 global branch offices under a strict 3-week deadline.  
(a) Which elicitation technique should the analyst select and why?  
(b) What are the major inherent limitations of this technique regarding requirement clarification?  
(c) What complementary technique should be paired with it to resolve ambiguities?

### Question 11 (2.5 marks)
During the early scoping of the Chemical Tracking System, departmental heads from R&D, Procurement, and Environmental Safety are in deep disagreement over who approves chemical purchase orders. The project schedule is tight.  
(a) Which elicitation technique is best suited to break departmental silos and achieve consensus rapidly?  
(b) What operational risk can cause this technique to fail completely?

### Question 12 (2.5 marks)
The development team must implement a novel chemical hazard search interface that scientists find difficult to describe conceptually.  
(a) Which elicitation technique is recommended to make requirements tangible when users say "I don't know what I want until I see it"?  
(b) What common user misconception or hazard must the analyst manage when presenting this deliverable?

---

## SECTION D — Artifact Construction [10 marks | 3 questions]

### Question 13 (4 marks)
Construct a formal **6-Clause Vision Statement** for the **Chemical Tracking System (CTS)** conforming strictly to the standardized template and baseline details provided in the lecture.

### Question 14 (3 marks)
Construct an **Event Catalog (Event List)** for the Chemical Tracking System by defining the three event categories described in the lecture (**Business / User Event**, **Temporal Event**, and **Signal Event**) and providing one exact, real-world trigger from the CTS project for each category.

### Question 15 (3 marks)
Construct a **3-Level Feature Tree** for the Chemical Tracking System containing the root system and at least three distinct L1 Feature Groups (Order Chemicals, Health & Safety, Inventory Management), including their respective L2 sub-features and L3 detailed features as detailed in the lecture.

---

## SECTION E — Case Study Analysis [5 marks | 3 questions]

### Question 16 (1.5 marks)
*Mini-Case A:* An enterprise IT team developed a chemical inventory database based solely on interviews with laboratory scientists. After deployment, the system was shut down by state inspectors because the hazardous waste manifests did not comply with Environmental Protection Agency (EPA) filing formats, and the central purchasing system never received billing transaction feeds.  
(a) What category of stakeholders did the team fail to consult?  
(b) Which scope representation artifact would have exposed the missing interfaces to regulatory bodies and enterprise billing?  
(c) How does this artifact prevent this omission?

### Question 17 (1.5 marks)
*Mini-Case B:* A business analyst conducted a single 4-hour brainstorming session with a team of 12 chemists to finalize system specifications. At the end of the session, the analyst documented 80 unrelated feature ideas and immediately handed them to developers as the final requirements baseline. Six months later, the project ran out of budget with half of the core ordering workflows unbuilt.  
(a) What fundamental mistake did the analyst make regarding the role of Brainstorming in the Requirements Development lifecycle?  
(b) What subsequent subdiscipline was omitted before handing work to developers?  
(c) What artifact should have been used to prioritize features against budget?

### Question 18 (2 marks)
*Mini-Case C:* During a user observation study at a commercial chemical depot, an analyst shadowed an order clerk for two days. The clerk operated with 100% adherence to documented safety manuals and completed every data entry field meticulously. However, once the software was deployed in production, error rates spiked by 40% because clerks routinely bypassed five validation screens to meet shipment quotas.  
(a) What psychological effect distorted the elicitation observations?  
(b) Why did the observation fail to capture true operational reality?  
(c) What elicitation technique should have been combined with observation to detect this discrepancy beforehand?

---

# GUIDE ANSWERS & MARKING SCHEME

### Question 1 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Weak Auxiliary Verb:* Use of "should" creates contractual ambiguity regarding necessity.  
  2. *Subjective Adjectives:* "Faster" is unquantified; it cannot be verified.  
  3. *Unverifiable Justification:* "So they don't waste time" is an emotional rationale rather than a measurable business outcome.  
  (b) **Explanation:** Mixing vague aspirations into functional specifications prevents test engineers from creating binary pass/fail verification tests and deprives managers of quantifiable performance tracking.  
  (c) **Surgical Rewrite:**  
  - *Business Objective:* Reduce chemical purchasing expenses by 25% within the first year of operation.  
  - *Success Metric:* Reduce average time spent ordering chemicals to 10 minutes or less on 80% of orders during operational acceptance testing.  
- **Marking Scheme:**  
  - 1 mark for identifying defects (weak modal "should", unmeasured "faster", vague rationale).  
  - 1 mark for explaining verification/measurement failure.  
  - 1 mark for writing the exact Business Objective and Success Metric from the lecture.  
- **Common Mistake Warning:** Students often rewrite the success metric as a functional requirement using "The system shall be 10 minutes faster", missing the target percentage (80% of orders).

### Question 2 Guide Answer
- **Model Answer:**  
  (a) **Defects & Taxonomy Confusions:**  
  1. *Conflation of Distinct Event Types:* Combines a human Business Event ("Chemist places order"), a business rule check ("checks EPA rules"), and an external hardware Signal Event ("barcode is scanned") into a single run-on sentence.  
  2. *Vague Quality Terminology:* "Quickly without delay" is non-verifiable and subjective.  
  3. *Missing Subject/System Boundary:* Does not clearly identify what the software does versus what external hardware/users do.  
  (b) **Explanation:** A requirement must be atomic and verifiable. Conflating hardware signals with user actions prevents independent testing and fails to define system responsibilities.  
  (c) **Surgical Rewrite:**  
  - `FR-CTS-01:` When a chemist submits a chemical request, the system shall validate the requested container against current EPA regulatory threshold limits before routing the request to procurement.  
  - `FR-CTS-02:` Upon receiving a barcode scan event from an optical container scanner, the system shall resolve the container ID and update its inventory status within 1.0 second.  
- **Marking Scheme:**  
  - 1.5 marks for identifying conflation of event types and subjective terms ("quickly without delay").  
  - 1 mark for explaining atomicity and verification failure.  
  - 1.5 marks for two atomic, verifiable requirements (`FR-CTS-01`, `FR-CTS-02`) with RFC 2119 `SHALL`.  
- **Common Mistake Warning:** Merging both actions into one requirement connected with "and", which violates atomicity.

### Question 3 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:** The draft is an informal, colloquial sentence that omits 4 of the 6 essential clauses of the standard Vision Statement template. It lacks the target customer description, the product category definition, key capabilities/benefits, and explicit differentiation against current manual methods.  
  (b) **Explanation:** An informal vision statement fails to define the product boundary. Without explicit differentiation and stated business value, team members make divergent assumptions, resulting in unconstrained scope creep and misaligned executive sponsorship.  
  (c) **Surgical Rewrite (Standard 6-Clause Template):**  
  - **For** scientists who need to request containers of chemicals,  
  - **Who** require rapid access to laboratory reagents without compliance delays,  
  - **The** Chemical Tracking System **is an** information system  
  - **That** will provide a single point of access to the chemical stockroom and to vendors, storing the location of every chemical container, quantity remaining, and complete usage history, saving 25% on chemical costs in the first year.  
  - **Unlike** current manual ordering processes,  
  - **Our product** will automatically generate all federal and state government compliance reports for chemical storage and hazardous disposal.  
- **Marking Scheme:**  
  - 1 mark for naming missing template elements.  
  - 1 mark for explaining scope creep and boundary ambiguity.  
  - 2 marks for complete 6-clause vision statement following the exact lecture template.  
- **Common Mistake Warning:** Skipping the "Unlike" or "Our product" clauses, which define differentiation and competitive advantage.

### Question 4 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Extreme Ambiguity:* "Handle... appropriately" is completely untestable and subjective; it does not specify what actions are performed.  
  2. *Incomplete Event Trigger:* "Whenever toxic waste is moved" does not define whether the trigger is a physical sensor, a database update, or a time-based reporting schedule.  
  3. *Unspecified Regulations:* "All government reports" omits the regulatory authorities (EPA, OSHA).  
  (b) **Required Information:** The developer needs: (1) the specific regulatory agencies governing the report (OSHA and EPA), (2) the exact reporting cadence or trigger event from the Event List (temporal quarterly generation or transaction-driven manifest), and (3) the data schema of the compliance report.  
  (c) **Surgical Rewrite:**  
  `FR-CTS-03:` When a hazardous container is marked for disposal, the system shall automatically generate the mandated Environmental Protection Agency (EPA) Hazardous Waste Manifest form and transmit it electronically to the Health & Safety Department.  
- **Marking Scheme:**  
  - 1 mark for identifying defects (ambiguity of "appropriately", unmeasured trigger).  
  - 1 mark for specifying regulatory agencies (EPA/OSHA) and event triggers.  
  - 2 marks for atomic, verifiable functional requirement with ID `FR-CTS-03` and `SHALL`.  
- **Common Mistake Warning:** Writing "The system shall generate EPA reports quickly" which introduces another non-verifiable adverb.

### Question 5 Guide Answer
- **Model Answer:**  
  - **Requirements Development:** The process of discovering, analyzing, specifying, modeling, and verifying requirements to establish the initial baseline. It encompasses:  
    1. *Requirements Elicitation* (discovering stakeholder needs)  
    2. *Requirements Analysis* (refining, decomposing, and modeling)  
    3. *Requirements Specification* (formal documentation in SRS)  
    4. *Requirements Validation & Verification* (checking correctness and quality).  
  - **Requirements Management:** The ongoing discipline of managing the requirements baseline after approval. It includes change control, impact analysis, version control, requirements traceability (RTM), and status/issue tracking.  
- **Marking Scheme:**  
  - 1 mark for distinguishing Development (creating baseline) from Management (controlling changes/traceability).  
  - 1.5 marks for listing the 4 subdisciplines of Requirements Development in correct order.  
- **Common Mistake Warning:** Treating Elicitation and Development as synonyms; Elicitation is only the first subdiscipline of Development.

### Question 6 Guide Answer
- **Model Answer:**  
  - **Business Problem / Opportunity:** The operational pain point, inefficiency, or commercial opportunity that justifies initiating the software project.  
    - *CTS Example:* "Managing chemical inventories manually costs too much and results in discarded, expired inventory."  
  - **Business Objective:** A concrete, quantified organizational goal that the business expects to achieve by deploying the system.  
    - *CTS Example:* "Reduce chemical purchasing expenses by 25% within the first year of operation."  
  - **Success Metric:** A measurable operational indicator tracked during testing or production to determine whether the objective was met.  
    - *CTS Example:* "Reduce average time spent ordering chemicals to 10 minutes or less on 80% of orders."  
- **Marking Scheme:**  
  - 1 mark for distinguishing Problem (pain point) from Objective (strategic goal).  
  - 0.5 marks for defining Success Metric as the measurable proof of objective achievement.  
  - 1 mark for providing the exact CTS examples from the lecture for all three concepts.  
- **Common Mistake Warning:** Writing a functional requirement (e.g., "The system shall display a chemical catalog") when asked for a Business Objective.

### Question 7 Guide Answer
- **Model Answer:**  
  - **Context Diagram:** A DFD Level 0 diagram that defines the immediate boundary of the system under development, showing direct data/control flows between the central system process bubble and external entities (terminators).  
  - **Ecosystem Map:** A broader enterprise model illustrating all participating systems within the organizational environment that exchange data or are affected by the solution, **including systems that have no direct interface with the new software**.  
  - **Circumstance where Ecosystem Map is Critical:** When the product interacts with systems indirectly via intermediary databases, enterprise service buses, or compliance hubs (e.g., a secondary inventory database that receives daily batch extracts from a vendor system). A Context Diagram hides these indirect dependencies, whereas an Ecosystem Map prevents integration blindspots across the enterprise landscape.  
- **Marking Scheme:**  
  - 1 mark for defining Context Diagram (immediate boundary, direct terminators).  
  - 1 mark for defining Ecosystem Map (entire enterprise system landscape).  
  - 0.5 marks for explaining the indirect interface advantage.  
- **Common Mistake Warning:** Stating that an Ecosystem Map is just a more detailed Context Diagram; its key differentiator is showing indirect and non-interfacing dependent systems.

### Question 8 Guide Answer
- **Model Answer:**  
  - **Primary Stakeholders:** Hands-on end-users who interact directly with the software on a day-to-day basis.  
    - *CTS Classification:* **Chemists** and **Stockroom Clerks** (they directly enter orders and scan containers).  
  - **Secondary Stakeholders:** Individuals or organizations indirectly affected by the inputs, outputs, or enterprise consequences of the system without daily operational interaction.  
    - *CTS Classification:* **IT Compliance Auditors** and **Regulatory Bodies (EPA/OSHA)** (they consume compliance reports or audit security logs).  
  - **Key Stakeholders:** Decision-makers, financial sponsors, and executive leaders who hold budget authority and define strategic priorities.  
    - *CTS Classification:* **VP of Research & Development** and **Chief Chemist** (they authorize project funding and approve project success criteria).  
- **Marking Scheme:**  
  - 1 mark for defining the three categories.  
  - 1.5 marks (0.5 each) for correctly classifying Chemist (Primary), IT Auditor (Secondary), and VP of R&D (Key) with justification.  
- **Common Mistake Warning:** Classifying the VP of R&D as a Primary Stakeholder because they are "important".

### Question 9 Guide Answer
- **Model Answer:**  
  - **Elicitation Technique:** **Observation** (job shadowing / fly-on-the-wall observation).  
  - **Why Effective:** Uncovers "tacit knowledge" (actions users perform instinctively but fail to articulate during interviews because they take them for granted).  
  - **Psychological Phenomenon to Mitigate:** The **Hawthorne Effect** (individuals alter their normal behavior, following official procedures rigidly, simply because they know they are being observed).  
  - **Mitigation Strategy:** The analyst must spend extended time in the environment to build rapport, utilize unobtrusive/passive observation techniques, and corroborate observations with artifact/document analysis.  
- **Marking Scheme:**  
  - 1 mark for naming Observation and tacit knowledge.  
  - 1 mark for identifying and explaining the Hawthorne Effect.  
  - 0.5 marks for the mitigation approach.  
- **Common Mistake Warning:** Recommending Interviews to uncover tacit knowledge; interviews only uncover conscious, articulated knowledge.

### Question 10 Guide Answer
- **Model Answer:**  
  (a) **Technique & Justification:** **Surveys / Questionnaires**. It is the only cost-effective technique capable of gathering quantitative feedback from 2,500 geographically dispersed users across multiple time zones within 3 weeks.  
  (b) **Major Inherent Limitations:** Low response rates; questions must be closed-ended or simple; and most critically, **inability to ask interactive follow-up questions** or clarify ambiguous responses.  
  (c) **Complementary Technique:** **Focus Groups** or **Interviews** with a small, representative sample of respondents to drill down into trends and ambiguous responses revealed by the survey data.  
- **Marking Scheme:**  
  - 1 mark for selecting Surveys/Questionnaires with geographical/scale justification.  
  - 1 mark for identifying inability to ask follow-up questions and low flexibility.  
  - 0.5 marks for pairing with Focus Groups or Interviews.  
- **Common Mistake Warning:** Suggesting Requirements Workshops for 2,500 users.

### Question 11 Guide Answer
- **Model Answer:**  
  (a) **Technique:** **Requirements Workshops** (Facilitated collaborative work sessions). It gathers cross-functional stakeholders (R&D, Procurement, Environmental Safety) in an intensive, moderated environment to hammer out requirements and align conflicting interests rapidly.  
  (b) **Operational Risk:** If **key decision-makers** (sponsors, department heads with final authority) fail to attend, or if the workshop lacks a neutral, skilled facilitator, the session degenerates into stalemates, resulting in zero consensus and wasted project expense.  
- **Marking Scheme:**  
  - 1.5 marks for selecting Requirements Workshops and explaining consensus generation.  
  - 1 mark for identifying the absence of key decision-makers / poor facilitation as the fatal risk.  
- **Common Mistake Warning:** Proposing Brainstorming; brainstorming generates ideas uncensored, it does NOT resolve political deadlocks or establish formal consensus.

### Question 12 Guide Answer
- **Model Answer:**  
  (a) **Technique:** **Prototyping** (wireframes, interactive mockups, proof-of-concept UI). It makes requirements tangible, allowing users to interact with visual workflows and uncover unspoken expectations by discovering what they do *not* want.  
  (b) **User Hazard / Misconception:** Users frequently **mistake a prototype for finished, working software**, assuming that because the UI looks complete, the underlying system is almost ready for production. This causes unrealistic schedule expectations and resistance when architectural backend engineering requires substantial time.  
- **Marking Scheme:**  
  - 1 mark for selecting Prototyping and explaining its tangible feedback value.  
  - 1.5 marks for explaining the misconception that the prototype is finished code.  
- **Common Mistake Warning:** Suggesting Document Analysis when users cannot conceptualize what they want.

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
  - 4 marks total: ~0.65 marks per clause correctly completed following the lecture text.  
- **Common Mistake Warning:** Inverting the "Unlike" and "Our product" clauses.

### Question 14 Guide Answer
- **Model Answer:**  
  **Event Catalog (Event List) Artifact:**  
  1. **User / Business Events:**  
     - *Definition:* An action initiated by a human stakeholder to accomplish a business task.  
     - *CTS Example:* *"Chemist places a chemical request"* or *"Stockroom clerk logs receipt of a shipment."*  
  2. **Temporal Events:**  
     - *Definition:* An event triggered automatically by the arrival of a predetermined time, date, or elapsed interval.  
     - *CTS Example:* *"Time to generate quarterly EPA hazardous waste report arrives"* or *"Daily inventory reorder cycle at 18:00."*  
  3. **Signal Events:**  
     - *Definition:* An event received from external hardware devices, sensors, or automated communication interfaces.  
     - *CTS Example:* *"Chemical container barcode is scanned by optical scanner."*  
- **Marking Scheme:**  
  - 1 mark for Business Event definition + CTS example.  
  - 1 mark for Temporal Event definition + CTS example.  
  - 1 mark for Signal Event definition + CTS example.  
- **Common Mistake Warning:** Confusing a temporal event with a user action (e.g., claiming a user clicking "Run Report" on Monday is a temporal event).

### Question 15 Guide Answer
- **Model Answer:**  
  **Feature Tree Artifact — Chemical Tracking System:**  
  - **L1 Feature Group 1: Order Chemicals**  
    - **L2 Sub-Feature:** Preferred Vendors  
      - **L3 Detailed Feature:** Vendor Catalog Search  
      - **L3 Detailed Feature:** Local Lab Inventory Search  
      - **L3 Detailed Feature:** Direct Vendor Inquiry  
  - **L1 Feature Group 2: Health & Safety**  
    - **L2 Sub-Feature:** Compliance Reporting  
      - **L3 Detailed Feature:** OSHA Safety Data Sheets (SDS) Generation  
      - **L3 Detailed Feature:** EPA Hazardous Chemical Reporting  
  - **L1 Feature Group 3: Inventory Management**  
    - **L2 Sub-Feature:** Container Tracking  
      - **L3 Detailed Feature:** Bar Code Scanning  
      - **L3 Detailed Feature:** Auto-Reordering Threshold Notification  
- **Marking Scheme:**  
  - 1 mark per complete branch (L1 $\rightarrow$ L2 $\rightarrow$ L3) derived from lecture text. Total = 3 marks.  
- **Common Mistake Warning:** Failing to maintain 3 distinct hierarchical levels (L1, L2, L3).

### Question 16 Guide Answer
- **Model Answer:**  
  (a) **Stakeholder Category Omitted:** **Secondary Stakeholders** (specifically regulatory compliance officers, the Health & Safety department, and enterprise IT billing teams).  
  (b) **Scope Representation Artifact:** The **Ecosystem Map** or **Context Diagram**.  
  (c) **How the Artifact Prevents Omission:** An Ecosystem Map explicitly maps all external enterprise systems, regulatory entities, and data interfaces (such as the EPA compliance hub and enterprise billing). By visually laying out all interacting entities before development, integration and reporting gaps are immediately exposed.  
- **Marking Scheme:**  
  - 0.5 marks for identifying Secondary Stakeholders.  
  - 0.5 marks for naming Ecosystem Map / Context Diagram.  
  - 0.5 marks for explaining boundary visualization.  
- **Common Mistake Warning:** Suggesting interviews with scientists would have fixed this; scientists do not know EPA filing specs.

### Question 17 Guide Answer
- **Model Answer:**  
  (a) **Fundamental Mistake:** The analyst mistook **Brainstorming** for a complete requirements elicitation and analysis process. Brainstorming is designed solely for unconstrained idea generation; its outputs are raw, unvetted, and unprioritized.  
  (b) **Subdiscipline Omitted:** **Requirements Analysis** (specifically feasibility analysis, modeling, and analytical prioritization).  
  (c) **Prioritization Artifact:** An analytical **Requirements Prioritization Matrix** (scoring features by business value vs. implementation cost and technical risk) or a **Feature Tree** mapped to release increments.  
- **Marking Scheme:**  
  - 0.5 marks for explaining the misuse of Brainstorming.  
  - 0.5 marks for naming Requirements Analysis.  
  - 0.5 marks for naming the Prioritization Matrix / Feature Tree.  
- **Common Mistake Warning:** Stating that the analyst should have used a survey instead.

### Question 18 Guide Answer
- **Model Answer:**  
  (a) **Psychological Effect:** The **Hawthorne Effect** — people alter their behavior and perform unnaturally when they are aware of being actively monitored.  
  (b) **Why Observation Failed:** The clerk followed procedures strictly while observed, masking the true operational shortcuts and bypasses used during unmonitored peak volume hours.  
  (c) **Complementary Technique:** **Document & Interface Analysis** (analyzing actual transaction audit logs and exception error histories) or anonymous **Interviews/Questionnaires** regarding operational pain points during peak hours.  
- **Marking Scheme:**  
  - 0.5 marks for naming the Hawthorne Effect.  
  - 0.5 marks for explaining the artificial adherence to rules during observation.  
  - 1 mark for recommending Document/Log Analysis or anonymous inquiry.  
- **Common Mistake Warning:** Blaming the observer for asking too many questions, missing the psychological effect.

