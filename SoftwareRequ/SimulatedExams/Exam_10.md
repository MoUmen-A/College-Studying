# Software Requirements Engineering: Advanced Examination Series
## Exam 10: Requirements Recovery, Quality Audits & Enterprise Governance
**Course:** Software Requirements Engineering (CS / SE)  
**Curriculum Alignment:** Karl Wiegers & Joy Beatty (*Software Requirements* 3rd Ed.) & Ian Sommerville (*Software Engineering*)  
**Allowed Time:** 2 Hours | **Total Marks:** 50 Marks  
**Pedagogical Style:** Applied Problem-Solving, Surgical Defect Rewrites, Artifact Modeling & Case Engineering (Non-MCQ)  

---

> [!IMPORTANT]
> **Instructions to Candidates:**
> 1. This examination is designed to test **deep conceptual understanding, architectural reasoning, and professional specification skills**, not rote recall.
> 2. In **Section A**, you must explicitly identify the violated quality characteristics using formal engineering terminology and provide complete, testable rewrites.
> 3. In **Section D**, all models, vision statements, and tables must conform strictly to industry standards.
> 4. Ensure all formulated requirements in **Section E** are atomic, uniquely labeled, and verifiable with clear pass/fail criteria.

---

### Section A: Requirements Defect Analysis & Surgical Rewrite (10 Marks, 5 Marks Each)
*Analyze the flawed requirement statements below. For each prompt, diagnose all quality violations and provide an unambiguous, testable rewrite.*

#### Question 1 (5 Marks)
Analyze the following requirement from a troubled core banking modernization project:
> *"The new ledger must replace the old mainframe accounting ledger and perform all standard daily reconciliation without failing."*
- **a) Defect Identification (2.5 Marks):** Critique 'all standard daily reconciliation' and 'without failing'. Why is referencing an undefined legacy system without explicit formulas a fatal flaw?
- **b) Surgical Rewrite (2.5 Marks):** Rewrite into two unambiguous requirements specifying automated end-of-day trial balance reconciliation rules and deterministic ledger discrepancy exception routing.

#### Question 2 (5 Marks)
Analyze the following requirement from a bank teller customer onboarding workstation:
> *"The teller workstation should load customer profiles very quickly and provide easy navigation across customer accounts, loans, and credit cards."*
- **a) Defect Identification (2.5 Marks):** Detail why 'very quickly' and 'easy navigation' cannot be certified by independent auditors.
- **b) Surgical Rewrite (2.5 Marks):** Formulate verifiable metrics: specify profile retrieval response time ($\le 1.2$ seconds for 99% of requests) and single-click tab navigation between linked customer financial products.

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks, 5 Marks Each)
*Answer the following deep-dive theoretical prompts with structured, professional justifications.*

#### Question 3 (5 Marks)
Requirements Engineering Quality Audit: **The 9 Characteristics Checklist** (5 Marks):
- You are hired as an external auditor to evaluate an enterprise SRS that caused a 6-month project stall.
- Select five (5) of the Nine Quality Characteristics of Requirements:
  1. *Unambiguous*
  2. *Complete*
  3. *Verifiable*
  4. *Consistent*
  5. *Modifiable*
- For each selected characteristic, describe the specific inspection test or analytical technique an auditor uses to determine whether an SRS passes or fails.

#### Question 4 (5 Marks)
Consequences of a Defective SRS on the **Software Testing Lifecycle** (5 Marks):
- Explain why a defective, ambiguous, or incomplete SRS cripples the Quality Assurance (QA) team before a single line of code is written.
- How does an untestable requirement directly lead to subjective arguments between developers and QA testers during User Acceptance Testing (UAT)?
- Describe how defective requirements cause massive cost explosions according to the **Cost of Change Curve** (relative cost of fixing a requirements error during requirements vs. coding vs. production).

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks, 5 Marks Each)
*Evaluate the operational scenarios below and justify your strategic elicitation choices.*

Project Turnaround Strategy and Legacy Knowledge Extraction (10 Marks - 5 Marks each):
1. **Document Analysis of 30-Year-Old COBOL Code vs. Interviews with Retiring Developers:** A bank's core accounting rules reside in 2 million lines of undocumented COBOL mainframe code. The last three senior programmers plan to retire in four months. Contrast performing **Automated Code and Data Schema Analysis** against conducting **Structured Knowledge Transfer Interviews** with the retiring engineers. How should the analyst synthesize both techniques to extract critical accounting algorithms?
2. **Establishing Product Champions for Conflicting Business Divisions:** The Commercial Lending, Retail Banking, and Wealth Management divisions are fighting over customer data ownership in the new core banking system. Explain the concept of a **Product Champion** (Karl Wiegers). How does selecting an empowered Product Champion from each division eliminate stalemate and provide authoritative decision-making for the requirements team?

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks, 5 Marks Each)
*Construct formal requirements engineering models according to the prompt instructions.*

Constructing Traceability and Governance Artifacts (10 Marks):
1. **Requirements Traceability Matrix (RTM) Design (5 Marks):** Design a complete, professional RTM table template for a financial transaction module with columns:
   - `Business Objective ID`
   - `User Requirement / Use Case ID`
   - `Functional Requirement ID (SRS)`
   - `Software Architecture Component`
   - `System Test Case ID`
   Populate the matrix with a realistic banking transfer record from end to end. Explain how this table proves 100% test coverage to banking regulators.
2. **Context Diagram: Core Banking Engine Boundaries (5 Marks):** Model the scope boundary for `NextGen Core Banking Engine` by identifying its central process and its data/control interfaces with: `ATM Network Switch`, `Online Banking Web/Mobile Server`, `Central Bank Clearinghouse (Fedwire)`, and `Internal Risk Management Database`. Specify two bidirectional flows for each entity.

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)
*Carefully read the enterprise engineering scenario and deliver the three technical tasks that follow.*

#### Scenario Context: National Commercial Bank launched a \$20M project to replace its legacy 1980s core banking platform. 
Fourteen months into development, the project is halted. An independent audit reveals that the 400-page SRS document was written entirely in vague natural language, lacked a Data Dictionary, contained over 50 contradictory requirements between savings and checking workflows, and had no traceability to test cases. 
Developers built what they assumed was needed, resulting in an accounting balance discrepancy of \$12M during initial pilot integration. 
You are brought in as Principal Requirements Engineer to execute a complete requirements turnaround.

#### Engineering Tasks & Deliverables:
- **Task 1: Requirements Recovery & Quality Refactoring (4 Marks):** Outline a 4-step recovery action plan to audit, disambiguate, and rewrite the defective SRS. Explain how you will establish a formal **Data Dictionary** to unify accounting terminology across banking teams.

- **Task 2: Establishing a Rigorous Change Control Process (3 Marks):** Detail the structure and authority of the newly formed **Change Control Board (CCB)**. Specify the mandatory impact analysis criteria (financial, architectural, regulatory, and schedule) required before any future change to the requirements baseline is approved.

- **Task 3: Re-Baselining and Validation Sign-Off (3 Marks):** Explain how you will validate the newly refactored requirements set with executive business sponsors and chief risk officers to achieve an approved, legally binding **Requirements Baseline** before allowing development to resume.

