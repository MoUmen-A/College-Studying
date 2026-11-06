# Software Requirements Engineering: Advanced Examination Series
## Exam 07: Requirements Prioritization, Prototyping & Business Value
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
Analyze the following requirement from a retail e-commerce platform:
> *"The product recommendation engine should show relevant items that customers will like based on their history."*
- **a) Defect Identification (2.5 Marks):** Identify why 'relevant items' and 'that customers will like' are subjective and completely untestable.
- **b) Surgical Rewrite (2.5 Marks):** Rewrite this into an algorithmic functional requirement specifying concrete inputs (past 30 days purchase history, items viewed $\ge 3$ times), collaborative filtering parameters, and output presentation formats.

#### Question 2 (5 Marks)
Analyze the following requirement from a flash-sale inventory engine:
> *"The shopping cart should handle high traffic spikes smoothly without crashing or letting users buy out-of-stock items."*
- **a) Defect Identification (2.5 Marks):** Evaluate the vagueness of 'high traffic spikes smoothly' and the compound nature of cart performance vs. race-condition inventory locks.
- **b) Surgical Rewrite (2.5 Marks):** Formulate two atomic requirements: one specifying concurrent user transaction volume (requests per second) and one defining pessimistic/optimistic inventory locking to prevent overselling.

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks, 5 Marks Each)
*Answer the following deep-dive theoretical prompts with structured, professional justifications.*

#### Question 3 (5 Marks)
The Science of **Requirements Prioritization** (5 Marks):
- Why is requirements prioritization essential in software engineering? Why can an organization not implement all requirements simultaneously?
- Describe the **Analytical Prioritization Framework** that balances:
  1. Business Value to Customers
  2. Business Value to the Organization (Revenue, Compliance)
  3. Implementation Cost
  4. Technical Risk
- Explain how prioritization directly dictates release staging (e.g., Minimum Viable Product [MVP] vs. Release 2 vs. Future Backlog).

#### Question 4 (5 Marks)
Prototyping as an Elicitation, Analysis, and Validation Tool (5 Marks):
- Why do industry experts assert that *'Users usually don't know what they want until they see what they don't want'*?
- Distinguish between a **Low-Fidelity Mockup (Throwaway Prototype)** and a **High-Fidelity Evolutionary Prototype**.
- Explain two distinct risks of showing a high-fidelity prototype to executive stakeholders too early in the requirements lifecycle (e.g., assuming software is already completed, premature focus on aesthetics over business logic).

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks, 5 Marks Each)
*Evaluate the operational scenarios below and justify your strategic elicitation choices.*

Navigating Divergent Stakeholder Needs in Consumer Retail (10 Marks - 5 Marks each):
1. **Focus Groups vs. A/B Testing Data Analysis for UI Enhancements:** A retail company is deciding between a traditional multi-step checkout versus a modern one-page accordion checkout. Compare gathering feedback via an in-person **Focus Group** against analyzing quantitative user behavior via **Document / Usage Log Analysis (A/B testing telemetry)**. Why is observed behavioral telemetry more reliable than focus group opinions for conversion optimization?
2. **Brainstorming for Omnichannel Innovation:** The retailer wants to unify in-store digital kiosks with mobile app shopping. Outline the rules for a successful **Brainstorming Session** with marketing, store managers, and software architects. Explain the golden rule: *'Defer judgment / do not censor ideas during ideation'*, and describe how ideas are subsequently analyzed and pruned.

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks, 5 Marks Each)
*Construct formal requirements engineering models according to the prompt instructions.*

Visual Scope Decomposition for E-Commerce (10 Marks):
1. **Feature Tree Construction (5 Marks):** Design a complete 3-level **Feature Tree** for an E-Commerce Platform under the L1 Category: `Order Management`:
   - Decompose into three L2 Sub-features: `Cart Processing`, `Payment Settlement`, and `Order Fulfillment Tracking`.
   - Under each L2 sub-feature, specify two concrete L3 capabilities (e.g., Promo Code Validation, Multi-Currency Conversion, Real-Time Courier Tracking).
   - Explain why feature trees are the preferred artifact for executive steering committee reviews.
2. **Context Diagram: External Payment & Logistics Interfaces (5 Marks):** Draw a text-based Context Diagram detailing the interactions between `RetailCorp E-Commerce Core` and: `Customer Web/Mobile Browser`, `Payment Gateway (Stripe/PayPal)`, `Enterprise ERP / Warehouse Engine`, and `Third-Party Courier API (FedEx/UPS)`. Identify two data flows in each direction across the boundary.

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)
*Carefully read the enterprise engineering scenario and deliver the three technical tasks that follow.*

#### Scenario Context: MegaRetailer operates 500 physical stores and an online storefront generating \$500M annually. 
During annual Cyber Monday sales, the online platform regularly crashes under 100,000 concurrent shoppers, resulting in estimated lost sales of \$4M per hour. 
Furthermore, retail store managers complain that physical inventory numbers do not sync with the online store, causing online orders to be accepted for items that were already bought by in-store shoppers. 
Management has allocated \$3M to build an integrated real-time **Omnichannel Inventory and Cart Engine**.

#### Engineering Tasks & Deliverables:
- **Task 1: Specifying Concurrency & Scalability NFRs (4 Marks):** Write two verifiable Non-Functional Product Requirements specifying peak transaction throughput (orders processed per second under 100,000 active sessions) and maximum inventory sync latency between retail POS terminals and the cloud database ($\le 500$ ms).

- **Task 2: Prioritizing the MVP Release Backlog (3 Marks):** The marketing department wants AI virtual dressing rooms, while the logistics department demands automated stock reservation locks. Apply prioritization principles to justify which feature belongs in the MVP launch for Cyber Monday and which feature must be deferred.

- **Task 3: Business Rules for Inventory Allocation (3 Marks):** Formulate a formal Business Rule defining how inventory is locked when a customer adds an item to their cart (e.g., temporary 15-minute hold) and what occurs when the reservation timer expires without checkout completion.

