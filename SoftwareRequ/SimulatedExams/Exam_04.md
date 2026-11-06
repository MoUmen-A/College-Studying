# Software Requirements Engineering: Advanced Examination Series
## Exam 04: Feasibility Analysis, Business Rules & Specification Standards
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
Analyze the following requirement from a mobile banking funds transfer module:
> *"The app should transfer money to other accounts immediately without errors and provide high-level bank-grade security."*
- **a) Defect Identification (2.5 Marks):** Evaluate the terms 'immediately' and 'bank-grade security'. Why are these subjective, unverifiable buzzwords?
- **b) Surgical Rewrite (2.5 Marks):** Rewrite this into two distinct, measurable specifications: an end-to-end transaction latency requirement and an encryption/authentication security requirement citing industry standards (e.g., TLS 1.3, AES-256).

#### Question 2 (5 Marks)
Analyze the following requirement from an automated loan approval engine:
> *"If the applicant has a good credit score and reasonable income, approve the loan, unless they have too much existing debt."*
- **a) Defect Identification (2.5 Marks):** Identify the defects related to *Imprecision*, *Incompleteness*, and *Lack of Deterministic Logic*.
- **b) Surgical Rewrite (2.5 Marks):** Formulate a deterministic requirement referencing explicit numerical thresholds (credit score, debt-to-income ratio) or an external credit policy rule table.

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks, 5 Marks Each)
*Answer the following deep-dive theoretical prompts with structured, professional justifications.*

#### Question 3 (5 Marks)
Requirements Analysis Activity: **Feasibility Analysis and Risk Assessment** (5 Marks):
- What is the primary objective of analyzing requirement feasibility during the Analysis phase?
- Explain three distinct types of feasibility an analyst must evaluate: Technical Feasibility, Economic/Cost Feasibility, and Operational/Schedule Feasibility.
- If a high-priority business requirement is discovered to be technically unfeasible or cost-prohibitive, what two strategic options does the Business Analyst have to resolve the dilemma?

#### Question 4 (5 Marks)
Enterprise Asset Management: **Business Rules vs. Functional Requirements** (5 Marks):
- Define what constitutes a **Business Rule** (policies, government regulations, tax laws, computational algorithms).
- Why do modern software engineering standards demand that Business Rules be recorded and cataloged in an enterprise repository separate from project-level SRS documents?
- Explain how traceability links bridge business rules to the functional requirements that enforce them.

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks, 5 Marks Each)
*Evaluate the operational scenarios below and justify your strategic elicitation choices.*

Strategic Selection of Elicitation Techniques under Regulatory and Global Constraints (10 Marks - 5 Marks each):
1. **Document Analysis vs. Stakeholder Interviews for Financial Compliance:** A multinational bank must comply with the Basel III international capital accord and national anti-money laundering (AML) laws. Explain why **Document Analysis** of legal statutes and regulatory codes is mandatory *before* interviewing bank compliance executives. What happens if an analyst conducts interviews without prior document analysis?
2. **Interface Analysis for Third-Party API Integration:** The mobile wallet must interface with 15 external payment networks (Visa, Mastercard, SWIFT, local ACH). Explain the methodology of **Interface Analysis**. What data parameters, protocol contracts, error codes, and service-level agreements (SLAs) must be analyzed to prevent production integration failure?

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks, 5 Marks Each)
*Construct formal requirements engineering models according to the prompt instructions.*

Modeling Financial Architecture and Logic (10 Marks):
1. **Decision Table Construction for Credit Decisioning (5 Marks):** Construct a formal **Decision Table** for an instant overdraft protection service based on three conditions:
   - Condition 1: Account age > 6 months (True/False)
   - Condition 2: Monthly direct deposit $\ge$ \$2,000 (True/False)
   - Condition 3: Negative balance occurrences in last 90 days = 0 (True/False)
   Define the resultant actions: *Approve Overdraft Limit \$500*, *Approve Overdraft Limit \$250*, *Decline Request*. Explain why decision tables are superior to natural language for complex conditional requirements.
2. **Ecosystem Map Modeling (5 Marks):** Draw a text-based architectural **Ecosystem Map** for ApexPay Mobile Gateway showing how the Central Gateway interconnects with: User Mobile Apps, Core Banking Mainframe, Fraud Detection AI Engine, National Clearinghouse, and SMS Notification Gateway. Trace one end-to-end data flow through the ecosystem.

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)
*Carefully read the enterprise engineering scenario and deliver the three technical tasks that follow.*

#### Scenario Context: ApexPay is launching a cross-border micro-remittance platform allowing migrant workers in North America to send funds to families in Southeast Asia. 
The system must handle currency conversion, comply with international anti-terrorist financing rules, and guarantee transaction settlement within 5 seconds. 
During initial requirements reviews, backend engineers wanted to discard customer-facing transaction dispute features to meet the launch date, while the legal team insisted that dispute mechanisms are a mandatory statutory requirement. 
You are the Lead Business Analyst responsible for establishing the specification baseline.

#### Engineering Tasks & Deliverables:
- **Task 1: Requirements Prioritization Matrix (4 Marks):** Using an analytical prioritization framework (evaluating Business Value, Implementation Cost, and Regulatory Risk), explain how you would resolve the dispute between backend engineers and the legal team regarding dispute workflows.

- **Task 2: Non-Functional Security & Performance Requirements (3 Marks):** Write two formal NFRs for ApexPay: one specifying cryptographic standards for data-in-transit across public networks, and one specifying transaction latency and concurrency under peak holiday remittance volume.

- **Task 3: External Interface Requirements (3 Marks):** Specify the technical requirements for the external interface between ApexPay and the Foreign Exchange (FX) Rate Provider API, addressing update frequency, network timeout handling, and stale rate fallback logic.

