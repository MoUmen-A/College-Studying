# Question Bank: Chapter 1 — Fundamentals of Software Requirements Engineering

> **Subject:** Software Requirements Engineering  
> **Chapter:** Chapter 1 — Fundamentals of Software Requirements Engineering  
> **Total Marks:** 50 | **Questions:** 18  
> **Instructions:** Answer all questions. Write in full sentences. Partial marks are awarded for correct reasoning even if the final answer is incomplete.

---

## 🎓 Examinee Strategic Briefing: How to Solve & Critical Pitfalls to Avoid

Before attempting this exam, review this mental roadmap to guide your problem-solving and prevent common errors:

### 1. How to Approach Each Section:
- **Section A (Defect Diagnosis & Surgical Rewrite):**
  - **Scan for Subjective Fluff:** Words like "fast", "easily", "user-friendly", and "modern" are non-quantifiable and impossible to verify with binary pass/fail test cases.
  - **Check Modal Verbs:** "Should" denotes an optional suggestion; RFC 2119 requires **`SHALL`** for mandatory requirements.
  - **Enforce Atomicity:** Break compound sentences that mix UI style, security, and functional logic into distinct, numbered statements.
  - **Rewrite Formula:** Always use: `[FR-XXX-01] The system SHALL [action] [verifiable criteria / quantifiable metric] [scope/conditions]`.
- **Section B (Conceptual Discrimination):**
  - **User vs. Functional Reqs:** User requirements state what the customer needs to accomplish; functional requirements state what the software must execute.
  - **Completeness vs. Consistency:** Completeness means no missing features/exceptions; consistency means no internal contradictions. A document can be 100% consistent yet fatally incomplete!
  - **NFR Life-Critical Impact:** Remember the flight control example: 100% mathematically correct calculations delivered 500 ms late will crash an aircraft.
- **Section C (Elicitation & Technique Strategy):**
  - **The 3 Analysis Steps:** Always follow the exact SDLC order: (1) Understand As-Is $\rightarrow$ (2) Identify Improvements $\rightarrow$ (3) Define To-Be.
  - **Domain Constraints:** Recognize that legal mandates (like digital copyright delete-on-print) cannot be discovered through user interviews; they require studying statutory codes.
- **Section D (Artifact Construction):**
  - **NFR Taxonomy:** Carefully classify requirements into Product (uptime/speed), Organizational (corporate standards/smart-cards), and External (laws/regulations).
  - **Domain Physics:** Ensure the train deceleration formulas ($D_{\text{train}}$ and $D_{\text{gradient}}$) define all variables and note that $\alpha$ depends dynamically on train class.
- **Section E (Case Study Analysis):**
  - In the clinic search case, clearly contrast the **user intention** (query all clinics simultaneously) with the **developer interpretation** (dropdown menu per clinic branch).

### 2. Top Cognitive Traps to Avoid:
1. ❌ **Trap 1: Classifying External Statutory Laws as Organizational Requirements.** Privacy laws (GDPR, `HStan-03-2006-priv`) are *External NFRs*; internal company coding rules are *Organizational NFRs*.
2. ❌ **Trap 2: Rewriting "fast" as "very fast".** Always replace qualitative adjectives with measurable numbers (e.g., "within 2.0 seconds").
3. ❌ **Trap 3: Believing Domain Requirements are only about UI.** Domain requirements include physical laws (braking friction) and formal industry protocols (Z39.50).

---

## SECTION A — Defect Diagnosis & Surgical Rewrite [15 marks | 4 questions]

### Question 1 (3 marks)
Consider the following requirement extracted from a draft specification for the Medical Health Care – Patient Management System (MHC-PMS):  
*"The system should search clinic appointments fast and easily for doctors."*  
(a) Identify all quality defects by name based on the lecture material.  
(b) Explain why each identified issue is a defect in Requirements Engineering.  
(c) Surgically rewrite this requirement into a rigorous functional requirement complying with RFC 2119 syntax (`SHALL`), assigned a unique identifier `FR-MHC-01`, with unambiguous, verifiable behavior.

### Question 2 (4 marks)
Consider the following requirement statement for the Library Information System (LIBSYS):  
*"The document viewer shall be user-friendly, modern, and allow users to read retrieved materials directly in the document store while automatically preventing unauthorized access."*  
(a) Identify all quality defects by name.  
(b) Explain why each defect undermines verification and implementation.  
(c) Surgically rewrite this statement into two atomic, verifiable requirements (`FR-LIB-01` and `FR-LIB-02`).

### Question 3 (4 marks)
Consider the following natural language requirement from a clinic appointment subsystem:  
*"A user shall be able to search clinic appointments."*  
(a) Analyze the hazard of imprecision and ambiguity in this requirement by explaining the conflicting interpretations between the user's mental model and the developer's technical implementation as described in the lecture.  
(b) Identify the quality hallmarks violated.  
(c) Surgically rewrite the requirement (`FR-MHC-02`) to resolve the interpretation gap completely.

### Question 4 (4 marks)
Consider the following draft requirement for a high-speed passenger train safety sub-system:  
*"The train system shall calculate automatic braking deceleration accurately whenever track conditions change."*  
(a) Identify the category of requirement this should belong to according to the lecture taxonomy, and name its defect.  
(b) Explain what happens when generalist software engineers attempt to implement this requirement without explicit domain formulation.  
(c) Surgically rewrite this requirement (`FR-TRN-01`) incorporating the exact mathematical domain formula and parameters specified in the lecture.

---

## SECTION B — Conceptual Discrimination [10 marks | 4 questions]

### Question 5 (2.5 marks)
Explain the distinction between **User Requirements** and **Functional Requirements**. In your explanation, illustrate how a single high-level user requirement for LIBSYS or MHC-PMS decomposes into a concrete functional requirement.

### Question 6 (2.5 marks)
Compare and contrast **Completeness** and **Consistency** as the two fundamental quality rules of functional specifications. What are the specific project hazards when a specification is consistent but incomplete?

### Question 7 (2.5 marks)
Explain why a failure in a **Non-Functional Requirement (NFR)** can render an entire software system completely useless even when 100% of its functional requirements execute with total correctness. Support your reasoning with the safety-critical system example cited in the lecture.

### Question 8 (2.5 marks)
Differentiate between **Organizational Requirements** and **External Requirements** within the NFR taxonomy. Provide one concrete example of each from the LIBSYS or MHC-PMS lecture case studies to substantiate the boundary between internal enterprise governance and external compliance.

---

## SECTION C — Elicitation & Technique Strategy [10 marks | 4 questions]

### Question 9 (2.5 marks)
The hospital board decides to modernize its legacy manual patient scheduling process into the computerized MHC-PMS. During the **Analysis Phase**, the business analyst must execute the three core sequential steps outlined in the SDLC framework. Identify these three steps in chronological order and describe the specific outcome of each step for the MHC-PMS project.

### Question 10 (2.5 marks)
During the requirements discovery phase for LIBSYS, users request the ability to print licensed research articles. However, external international copyright legislation imposes stringent constraints. Identify the requirement class this constraint falls under, explain why general user interview techniques fail to uncover such requirements, and state which stakeholder or information source must be investigated.

### Question 11 (2.5 marks)
A development team is tasked with implementing the user authentication interface for the MHC-PMS. The clinical director states: *"Our doctors cannot waste 30 seconds typing passwords between emergency consultations."*  
(a) Which category of NFR does this constraint represent?  
(b) What organizational policy solution is specified in the lecture to satisfy this operational constraint while preserving security?  
(c) What artifact or physical token is required?

### Question 12 (2.5 marks)
Software requirements often must define not only what the system shall do, but also explicit exclusions (negative requirements: what the system should *not* do). Using the LIBSYS case study from the lecture, identify an explicit negative privacy or interface requirement and explain why documenting negative boundaries is essential for developer guidance.

---

## SECTION D — Artifact Construction [10 marks | 3 questions]

### Question 13 (3.5 marks)
Construct a complete **Requirements Classification Table** mapping the following four real-world requirements to their precise taxonomy category (**Functional Requirement**, **Product NFR**, **Organizational NFR**, **External NFR**, or **Domain Requirement**) based strictly on the lecture:  
1. *"The system shall automatically generate a daily appointment manifest for each clinic every morning at 06:00."*  
2. *"Total downtime during working hours (Mon–Fri, 08:30–17:30) shall not exceed 5 seconds per day."*  
3. *"Software development lifecycle and deliverables must strictly conform to internal corporate standard XYZCo-SP-STAN-95."*  
4. *"All search interfaces across external databases must conform strictly to the international Z39.50 standard."*

### Question 14 (3.5 marks)
Construct a formal technical specification for the **Train Protection System Deceleration Domain Requirement**. Your artifact must include:  
(a) The formal algebraic equations for total train deceleration ($D_{\text{train}}$) and gradient deceleration ($D_{\text{gradient}}$) using standard mathematical notation.  
(b) Definition of all variables ($D_{\text{control}}$, $D_{\text{gradient}}$, $\alpha$, gravitational constant).  
(c) The dynamic dependency factor governing $\frac{9.81\ \text{m/s}^2}{\alpha}$.

### Question 15 (3 marks)
Draft three formal, uniquely identified Functional Requirements (`FR-LIB-10`, `FR-LIB-11`, and `FR-LIB-12`) for the **Library Information System (LIBSYS)** that specify database searching capabilities, built-in document viewing, and order tracking, conforming strictly to the baseline behavior described in the lecture.

---

## SECTION E — Case Study Analysis [5 marks | 3 questions]

### Question 16 (1.5 marks)
*Mini-Case A:* An engineering team built an electronic document retrieval subsystem for an academic library. Upon delivery, the university's legal counsel halted system deployment because student terminals downloaded licensed research monographs directly onto USB drives and local temporary directories without restriction.  
(a) What category of requirement was overlooked?  
(b) What specific operational mandate from the lecture was violated?  
(c) How should the system have been engineered to remain compliant?

### Question 17 (1.5 marks)
*Mini-Case B:* The MHC-PMS was deployed across a metropolitan hospital network. On Monday morning at 08:35, the system went offline for 45 seconds due to a database lock contention, forcing outpatient triage desks to halt admissions. The project manager claimed: *"A 45-second glitch in enterprise software is completely normal and acceptable."*  
(a) Evaluate the project manager's claim against the explicit Product NFR defined in the lecture.  
(b) State the exact availability requirement and allowable downtime threshold.  
(c) What architectural consequence arises from this stringent threshold?

### Question 18 (2 marks)
*Mini-Case C:* A hospital clinic deployed a patient scheduling application where developers implemented the search feature by requiring operators to select a specific clinic branch from a drop-down list before querying patient names. When triage nurses attempted to locate an emergency patient who had an appointment at an unknown clinic branch, they had to repeat the search manually across 20 distinct clinics, wasting 15 critical minutes.  
(a) What underlying Requirements Engineering flaw caused this operational failure?  
(b) Contrast the user intention with the developer interpretation that led to this gap.  
(c) State the rule of requirements specification that prevents this communication breakdown.

---

# GUIDE ANSWERS & MARKING SCHEME

### Question 1 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Ambiguity / Subjective Adjectives:* Terms "fast" and "easily" are non-quantifiable and open to subjective interpretation.  
  2. *Imprecision / Weak Modal Verb:* Use of the weak auxiliary verb "should" instead of mandatory RFC 2119 keywords ("shall").  
  3. *Missing Scope & Boundary:* It does not specify whether the search queries a single clinic or all clinics across the hospital network simultaneously.  
  (b) **Explanation:** Subjective words like "fast" and "easily" cannot be tested or verified; an engineer cannot design a binary pass/fail test case for "easy". "Should" creates contractual ambiguity regarding whether the capability is optional or mandatory.  
  (c) **Surgical Rewrite:**  
  `FR-MHC-01:` The system shall allow authorized clinical staff to search appointment schedules across all hospital clinics simultaneously by patient name or national identity number, returning matching records within 2.0 seconds.  
- **Marking Scheme:**  
  - 1 mark for naming defects correctly (ambiguity/non-verifiable terms, weak modal).  
  - 1 mark for explaining why they undermine testing/verification.  
  - 1 mark for correct RFC 2119 rewrite with ID `FR-MHC-01`, `SHALL`, and quantifiable/verifiable scope.  
- **Common Mistake Warning:** Students frequently rewrite the requirement using phrases like "shall be very fast" which retains the non-verifiable defect instead of introducing a measurable constraint.

### Question 2 Guide Answer
- **Model Answer:**  
  (a) **Defects Identified:**  
  1. *Non-Atomic (Compound Requirement):* Combines UI design ("user-friendly, modern"), functional viewing capabilities, and security access control into a single clause.  
  2. *Untestable Quality Buzzwords:* "User-friendly" and "modern" are subjective and lack objective verification criteria.  
  3. *Vague Security Constraint:* "Automatically preventing unauthorized access" fails to define the authentication mechanism or authorization roles.  
  (b) **Explanation:** Compound requirements prevent independent verification, tracking, and prioritization. If the viewer works but security fails, the requirement status cannot be cleanly reported as implemented or verified.  
  (c) **Surgical Rewrite:**  
  - `FR-LIB-01:` The system shall provide built-in document viewers allowing authenticated users to read retrieved materials directly in the document store without launching external client applications.  
  - `FR-LIB-02:` The document viewer shall display retrieved materials only to users holding an active patron session, terminating document display immediately upon session expiration.  
- **Marking Scheme:**  
  - 1.5 marks for identifying compound structure and untestable adjectives ("user-friendly", "modern").  
  - 1 mark for explaining verification/tracking consequences.  
  - 1.5 marks for decomposing into two atomic, verifiable requirements (`FR-LIB-01` and `FR-LIB-02`) with `SHALL`.  
- **Common Mistake Warning:** Students often keep both concerns in a single sentence connected by "and also", failing the atomicity requirement.

### Question 3 Guide Answer
- **Model Answer:**  
  (a) **Hazard of Imprecision & Interpretation Gap:**  
  - *User Intention:* The user types a patient name once, expecting the system to automatically query all hospital clinics simultaneously to locate the patient's booking.  
  - *Developer Interpretation:* The developer builds a single-clinic search where the user must first select a specific clinic from a drop-down menu, and then search only within that selected clinic's database.  
  - *Resulting Hazard:* Severe operational failure; searching for a patient whose booking clinic is unknown requires repeated, error-prone manual searches across 20+ individual clinic databases.  
  (b) **Quality Hallmarks Violated:** Violates **Completeness** (the search scope and inputs/outputs are omitted) and **Unambiguity** (allows two distinct, contradictory technical implementations).  
  (c) **Surgical Rewrite:**  
  `FR-MHC-02:` The system shall provide a global appointment search function allowing clinical staff to query patient appointment schedules across all hospital clinics simultaneously using patient name or unique patient identifier.  
- **Marking Scheme:**  
  - 1.5 marks for contrasting the user intention (all clinics) with developer interpretation (dropdown per clinic).  
  - 1 mark for naming Completeness and Unambiguity.  
  - 1.5 marks for writing `FR-MHC-02` resolving the multi-clinic scope with `SHALL`.  
- **Common Mistake Warning:** Confusing "imprecision" with "functional error"; the developer implemented the code logically, but the ambiguity in natural language caused the divergence.

### Question 4 Guide Answer
- **Model Answer:**  
  (a) **Requirement Class & Defect:** This is a **Domain Requirement** (originating from the application domain's physical and safety laws). Its defect is extreme **imprecision and non-verifiability** ("accurately whenever track conditions change" provides no mathematical definition or tolerance).  
  (b) **Consequences for Generalist Engineers:** Software engineers lack specialized physics/railway engineering knowledge. Without explicit mathematical formulas and parameter definitions, generalist engineers cannot deduce train inertia, track gradient resistance, or class-specific deceleration constants, resulting in unsafe braking software.  
  (c) **Surgical Rewrite:**  
  `FR-TRN-01:` The automatic train protection subsystem shall compute the automatic braking deceleration $D_{\text{train}}$ in $\text{m/s}^2$ as:  
  $$D_{\text{train}} = D_{\text{control}} + D_{\text{gradient}}$$  
  where $D_{\text{gradient}} = 9.81\ \text{m/s}^2 + \frac{\text{compensated gradient}}{\alpha}$, and the calibration constant $\frac{9.81\ \text{m/s}^2}{\alpha}$ shall be resolved dynamically from the onboard configuration based on the train class.  
- **Marking Scheme:**  
  - 1 mark for identifying Domain Requirement and non-verifiability.  
  - 1 mark for explaining the generalist software engineer vs. domain expert gap.  
  - 2 marks for complete mathematical formula with variables defined and ID `FR-TRN-01`.  
- **Common Mistake Warning:** Omitting the sub-formula for $D_{\text{gradient}}$ or failing to define the parameter $\alpha$ as train-class dependent.

### Question 5 Guide Answer
- **Model Answer:**  
  - **User Requirements:** High-level natural language statements supplemented with informal diagrams that describe the operational tasks and services users expect the system to provide, written from the customer's problem-domain viewpoint.  
  - **Functional Requirements:** Concrete technical specifications detailing what the software must do, system inputs, processing behaviors, outputs, and explicit system reactions under specific conditions.  
  - *Example from Lecture:*  
    - *User Requirement (LIBSYS):* "Users need an easy way to find articles in the library collections."  
    - *Functional Requirement Decomposition (`FR-1`):* "The user shall be able to search either all initial database collections or select an arbitrary subset."  
- **Marking Scheme:**  
  - 1 mark for defining User Requirements.  
  - 1 mark for defining Functional Requirements.  
  - 0.5 marks for an accurate decomposition example from the lecture text.  
- **Common Mistake Warning:** Stating that user requirements are non-functional while functional requirements are technical. Both describe functional capabilities, but at different abstraction levels.

### Question 6 Guide Answer
- **Model Answer:**  
  - **Completeness:** All services, operational scenarios, inputs, constraints, boundary conditions, and exception behaviors required by users are explicitly defined in the specification.  
  - **Consistency:** Requirements do not contradict one another; descriptions of system behavior, terminology, and constraints are harmonious across the entire specification.  
  - *Hazards of a Consistent but Incomplete Specification:* A specification may be 100% internally consistent (no statements contradict each other), but if key operational scenarios (e.g., error recovery, zero-result search, network timeout) are omitted, developers will make unguided assumptions, resulting in major downstream defects, budget blowouts, and user rejection upon delivery.  
- **Marking Scheme:**  
  - 1 mark for defining Completeness.  
  - 1 mark for defining Consistency.  
  - 0.5 marks for explaining the hazard of consistent but incomplete requirements.  
- **Common Mistake Warning:** Thinking consistency guarantees completeness; a document with just one single requirement is perfectly consistent, yet catastrophically incomplete.

### Question 7 Guide Answer
- **Model Answer:**  
  - **Reasoning:** Non-Functional Requirements (NFRs) act as system-wide constraints on behavior, architecture, performance, and safety. While functional requirements dictate *what* the system does, NFRs dictate *how well* or *under what operational boundaries* it does it. If an NFR is violated, the operational utility of the software collapses entirely.  
  - *Lecture Example:* An aircraft flight control system. If the system executes its flight calculations with 100% mathematical accuracy (functional correctness), but takes 500 ms longer than the hard real-time latency threshold (NFR failure), the control surfaces cannot respond in time, and the aircraft will crash.  
- **Marking Scheme:**  
  - 1.5 marks for theoretical explanation of NFRs as system-wide behavioral constraints.  
  - 1 mark for citing the aircraft flight control latency crash example from the lecture.  
- **Common Mistake Warning:** Believing that functional bugs are always more critical than NFR bugs.

### Question 8 Guide Answer
- **Model Answer:**  
  - **Organizational Requirements:** NFRs that stem from organizational policies, internal corporate standards, employee procedures, implementation language standards, and development methodologies.  
    - *Lecture Example:* In LIBSYS, "Software development lifecycle and deliverables must strictly conform to internal corporate standard XYZCo-SP-STAN-95" or in MHC-PMS, "Clinic staff must authenticate using their physical health authority smart identity card."  
  - **External Requirements:** NFRs that arise from factors outside the organization and its development boundary, such as legislative mandates, statutory privacy acts, regulatory safety standards, and interoperability mandates.  
    - *Lecture Example:* In MHC-PMS, "System must strictly enforce patient data confidentiality according to statutory healthcare privacy code HStan-03-2006-priv."  
- **Marking Scheme:**  
  - 1 mark for distinguishing internal corporate governance from external legal/regulatory forces.  
  - 1.5 marks (0.75 each) for citing correct examples from the lecture table (e.g., `XYZCo-SP-STAN-95` vs. `HStan-03-2006-priv`).  
- **Common Mistake Warning:** Classifying statutory privacy laws (like HIPAA/GDPR or `HStan-03-2006-priv`) as organizational requirements because the organization implements them.

### Question 9 Guide Answer
- **Model Answer:**  
  The three foundational steps of the **Analysis Phase** in the SDLC:  
  1. **Understand the Existing Situation (As-Is System):** Study the current manual paper appointment ledgers, clinic desk phone procedures, and data bottlenecks to establish a baseline of current performance.  
  2. **Identify Improvements:** Uncover pain points, redundancies, double-booking errors, long patient wait times, and high administrative costs in the current process.  
  3. **Define New System Requirements (To-Be System):** Document the concrete functional services, multi-clinic appointment search features, and availability constraints required in the computerized MHC-PMS.  
- **Marking Scheme:**  
  - 1.5 marks for listing the 3 steps in exact chronological order (As-Is $\rightarrow$ Improvements $\rightarrow$ To-Be).  
  - 1 mark for grounding each step in the MHC-PMS context.  
- **Common Mistake Warning:** Swapping the order or describing the steps as "Requirements, Design, Coding" (which are SDLC phases, not the Analysis steps).

### Question 10 Guide Answer
- **Model Answer:**  
  - **Requirement Class:** **Domain Requirement** (specifically derived from external legal copyright legislation governing digital library operations).  
  - **Why General User Interviews Fail:** End-users (students, library patrons) and librarians are focused on immediate convenience (e.g., downloading PDFs, saving to flash drives). They are unaware of technical licensing restrictions, liability penalties, and statutory copyright mandates.  
  - **Information Sources / Stakeholders:** Legal counsel, international digital copyright statutes, licensed database contracts, and published digital rights management protocols.  
- **Marking Scheme:**  
  - 1 mark for identifying Domain Requirement (Legal/Copyright).  
  - 1 mark for explaining why end-user interviews do not reveal legal/statutory constraints.  
  - 0.5 marks for naming legal counsel / copyright statutes as the required source.  
- **Common Mistake Warning:** Labeling copyright constraints as "User Requirements".

### Question 11 Guide Answer
- **Model Answer:**  
  (a) **NFR Category:** **Organizational Requirement** (governing employee authentication policy and workplace operational procedure).  
  (b) **Organizational Policy Solution:** The hospital enforces a rapid physical smart-card login policy rather than keyboard password entry.  
  (c) **Physical Token / Artifact:** Each staff member operates the system by inserting or tapping their physical **8-digit health authority employee smart identity badge**.  
- **Marking Scheme:**  
  - 1 mark for identifying Organizational Requirement.  
  - 1 mark for describing the smart card policy solution.  
  - 0.5 marks for identifying the 8-digit health authority badge token.  
- **Common Mistake Warning:** Calling smart card authentication a "Product Requirement".

### Question 12 Guide Answer
- **Model Answer:**  
  - **Negative Requirement from LIBSYS:** "System shall not disclose personal patron records (beyond name and library card ID) to unauthorized staff" or "Specific classes of imported licensed documents shall not be saved as local electronic copies."  
  - **Why Documenting Negative Requirements is Essential:** Natural language specifications often assume common sense, but software developers build what is technologically straightforward unless constrained. Explicitly documenting what the system *shall not do* establishes explicit boundaries, prevents security/privacy leaks, and eliminates unauthorized features that developers might otherwise implement.  
- **Marking Scheme:**  
  - 1 mark for stating an explicit negative requirement from the lecture text.  
  - 1.5 marks for explaining how negative boundaries prevent security violations and constrain developer assumptions.  
- **Common Mistake Warning:** Believing requirements can only specify positive features.

### Question 13 Guide Answer
- **Model Answer:**  
  | # | Requirement Statement | Exact Taxonomy Category |
  | :--- | :--- | :--- |
  | 1 | *"The system shall automatically generate a daily appointment manifest for each clinic every morning at 06:00."* | **Functional Requirement** |
  | 2 | *"Total downtime during working hours (Mon–Fri, 08:30–17:30) shall not exceed 5 seconds per day."* | **Product Non-Functional Requirement** |
  | 3 | *"Software development lifecycle and deliverables must strictly conform to internal corporate standard XYZCo-SP-STAN-95."* | **Organizational Non-Functional Requirement** |
  | 4 | *"All search interfaces across external databases must conform strictly to the international Z39.50 standard."* | **Domain Requirement** |  
- **Marking Scheme:**  
  - 1 mark each for items 1, 2, and 4 (3 marks total).  
  - 0.5 marks for item 3. Total = 3.5 marks.  
- **Common Mistake Warning:** Labeling Z39.50 as a generic functional requirement rather than recognizing standard protocols as Domain Requirements.

### Question 14 Guide Answer
- **Model Answer:**  
  **Technical Specification Artifact — Train Protection Braking Deceleration:**  
  (a) **Mathematical Formulas:**  
  $$D_{\text{train}} = D_{\text{control}} + D_{\text{gradient}}$$  
  $$D_{\text{gradient}} = 9.81\ \text{m/s}^2 + \frac{\text{compensated gradient}}{\alpha}$$  
  (b) **Variable Definitions:**  
  - $D_{\text{train}}$: Total calculated automatic deceleration rate of the train ($\text{m/s}^2$).  
  - $D_{\text{control}}$: Deceleration rate commanded by the train braking control system ($\text{m/s}^2$).  
  - $D_{\text{gradient}}$: Additional deceleration or acceleration component caused by track incline/gravity ($\text{m/s}^2$).  
  - $9.81\ \text{m/s}^2$: Acceleration due to Earth's gravity ($g$).  
  - $\text{compensated gradient}$: The effective slope/incline of the railway track section.  
  - $\alpha$: Factor related to the mass and inertial characteristics of the train.  
  (c) **Dynamic Dependency Factor:**  
  The calibrated value of $\frac{9.81\ \text{m/s}^2}{\alpha}$ is not a fixed universal constant; it is **determined dynamically based on the specific train class** (weight, carriage count, and braking mechanism).  
- **Marking Scheme:**  
  - 1.5 marks for accurate LaTeX algebraic equations.  
  - 1 mark for definitions of all 5 variables/constants.  
  - 1 mark for identifying dynamic dependence on train class.  
- **Common Mistake Warning:** Forgetting to state that $D_{\text{gradient}}$ incorporates track slope and that $\alpha$ depends on the train class.

### Question 15 Guide Answer
- **Model Answer:**  
  - `FR-LIB-10:` The system shall allow users to search either all initial library database collections or select an arbitrary subset of collections for querying.  
  - `FR-LIB-11:` The system shall provide built-in document viewers allowing users to read retrieved materials directly within the document store without downloading local copies.  
  - `FR-LIB-12:` Every processed order shall be allocated a unique alphanumeric `ORDER_ID`, which the system shall allow the user to copy to permanent account storage.  
- **Marking Scheme:**  
  - 1 mark per requirement (unique ID, RFC 2119 `SHALL`, accurate LIBSYS functionality from lecture). Total = 3 marks.  
- **Common Mistake Warning:** Using informal terms like "Users can search..." instead of normative syntax "The system shall allow users to search...".

### Question 16 Guide Answer
- **Model Answer:**  
  (a) **Requirement Category Overlooked:** **Domain Requirement** (specifically digital copyright compliance law).  
  (b) **Operational Mandate Violated:** The lecture specifies: *"To comply with international digital copyright legislation, specific classes of imported licensed documents must be automatically deleted on arrival or printed directly to a network server with no local electronic copy saved."*  
  (c) **Correct Engineering Solution:** The system should have implemented an automated background daemon that routes downloaded licensed documents directly to a secure network spooler for physical printing and executes immediate deletion from local RAM/disk cache.  
- **Marking Scheme:**  
  - 0.5 marks for identifying Domain Requirement.  
  - 0.5 marks for citing the delete-on-print/no-local-copy mandate.  
  - 0.5 marks for describing the delete-on-print background daemon solution.  
- **Common Mistake Warning:** Suggesting user login screens as the fix, missing the mandatory delete-on-arrival/direct-print domain rule.

### Question 17 Guide Answer
- **Model Answer:**  
  (a) **Evaluation:** The project manager's claim is completely false and violates the specification.  
  (b) **Exact Product NFR & Threshold:** The lecture explicitly defines the MHC-PMS Product Requirement: *"The system shall be available Mon–Fri, 08:30–17:30. Total downtime during working hours shall not exceed 5 seconds per day."* The 45-second outage exceeded the daily budget by 800%.  
  (c) **Architectural Consequence:** To satisfy an extreme availability constraint of $\le 5$ seconds downtime/day, the software architecture must incorporate high-availability clustering, instant database failover, and active-active redundancy rather than standard monolithic database setups.  
- **Marking Scheme:**  
  - 0.5 marks for rejecting the PM's claim.  
  - 0.5 marks for stating the exact 5 seconds/day threshold during 08:30–17:30.  
  - 0.5 marks for explaining architectural implications (clustering/failover).  
- **Common Mistake Warning:** Citing generic "99.9% uptime" rather than the exact lecture metric of "$\le 5$ seconds per day between 08:30 and 17:30".

### Question 18 Guide Answer
- **Model Answer:**  
  (a) **Underlying Flaw:** **Imprecision and Ambiguity** in the specification, combined with a lack of validation between business analysts, users, and developers.  
  (b) **User Intention vs. Developer Interpretation:**  
  - *User Intention:* The user intended to enter a patient name into a single search box and have the system scan all clinics across the hospital network simultaneously.  
  - *Developer Interpretation:* The developer assumed a two-stage input sequence: select a specific clinic dropdown first, then query only the selected clinic's records.  
  (c) **Specification Rule:** The rule of **Unambiguity and Completeness** — requirements must explicitly state the operational scope, inputs, default values, and search domain so that only one single technical interpretation exists.  
- **Marking Scheme:**  
  - 0.5 marks for identifying imprecision and ambiguity.  
  - 1 mark for clearly contrasting the multi-clinic intention with the dropdown-per-clinic interpretation.  
  - 0.5 marks for stating the completeness/unambiguity specification rule.  
- **Common Mistake Warning:** Blaming the developer for writing buggy code instead of recognizing that the requirement itself was ambiguous.

