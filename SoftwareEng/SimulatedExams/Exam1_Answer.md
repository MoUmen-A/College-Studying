# CSE2001 - Software Engineering
## Simulated Exam 1: Guide Answer & Marking Scheme

---

### Section A: Complete the Statements (10 Marks, 2 Marks Each)

1. **activities**  
   *(Ref: [AllContent.txt:L68]( /SoftwareEng/Lec/AllContent.txt#L68) - "Software process: a structured set of activities...")*
2. **agile**  
   *(Ref: [AllContent.txt:L76-77]( /SoftwareEng/Lec/AllContent.txt#L76-77) - "Plan-driven: Activities are planned in advance. Agile: Planning is incremental...")*
3. **software discovery**  
   *(Ref: [AllContent.txt:L166]( /SoftwareEng/Lec/AllContent.txt#L166) - "Software discovery and evaluation: Search for existing reusable systems...")*
4. **customers / end users**  
   *(Ref: [AllContent.txt:L430-432]( /SoftwareEng/Lec/AllContent.txt#L430-432) - "User requirements... Written for: Customers/end users.")*
5. **Change analysis and costing**  
   *(Ref: [AllContent.txt:L482-484]( /SoftwareEng/Lec/AllContent.txt#L482-484) - "1. Problem analysis and change specification -> 2. Change analysis and costing...")*

---

### Section B: Short Answer & Explanations (15 Marks, 5 Marks Each)

#### 1. Why throw-away prototypes should be discarded rather than delivered as a production system (5 Marks)
*Award 1.5 marks for each valid reason listed, up to a maximum of 5 marks. (Ref: [AllContent.txt:L246-249]( /SoftwareEng/Lec/AllContent.txt#L246-249))*
* **Reason 1:** They cannot be tuned easily to meet non-functional requirements such as reliability, security, performance, or storage.
* **Reason 2:** They are usually undocumented, which makes long-term maintenance impossible.
* **Reason 3:** Their structure is degraded due to rapid change during development, leaving a poor and unmaintainable system architecture.
* **Reason 4:** They may not meet organizational quality standards (e.g., coding standards).

#### 2. Definition and importance of traceability in requirements management (5 Marks)
*Award 2 marks for the definition, and 3 marks for explaining why it is essential. (Ref: [AllContent.txt:L466-468]( /SoftwareEng/Lec/AllContent.txt#L466-468) & [L499-501]( /SoftwareEng/Lec/AllContent.txt#L499-501))*
* **Definition (2 Marks):** Traceability is the recording and tracking of relationships (links) between individual requirements, and between requirements and design/implementation elements.
* **Importance (3 Marks):** Traceability is essential to assess the impact and costing of proposed requirements changes. It allows engineers to trace which other requirements and software components depend on the changed requirement, ensuring that no dependent features are broken and that the cost of change is fully understood before implementation.

#### 3. Three stages in the process improvement cycle (5 Marks)
*Award 1 mark for listing the stages, and 1.3 marks for explaining each stage. (Ref: [AllContent.txt:L283-287]( /SoftwareEng/Lec/AllContent.txt#L283-287))*
1. **Process measurement (1.6 Marks):** Measure attributes of the current process or product (e.g., time taken, resources required, number of defects) to establish a baseline and assess future improvements.
2. **Process analysis (1.7 Marks):** Assess the current process, map out process workflows, and identify weaknesses, bottlenecks, or inefficiencies.
3. **Process change (1.7 Marks):** Propose and introduce changes to the process to address the identified weaknesses, and then collect metric data again to measure the impact.

---

### Section C: Differences and Comparisons (10 Marks, 5 Marks Each)

#### 1. Plan-driven vs Agile processes (5 Marks)
*Award up to 5 marks based on the completeness and clarity of the comparison table. (Ref: [AllContent.txt:L76-83]( /SoftwareEng/Lec/AllContent.txt#L76-83))*

| Point of Comparison | Plan-driven process | Agile process |
| :--- | :--- | :--- |
| **Planning approach** | Activities are planned in advance. | Planning is incremental and flexible. |
| **Progress measurement** | Measured against the original plan. | Measured through working increments and feedback. |
| **Suitability** | Best when requirements are stable and well-understood. | Best when requirements are unclear or changing. |

#### 2. Incremental Development vs Incremental Delivery (5 Marks)
*Award 2.5 marks for part (a) and 2.5 marks for part (b). (Ref: [AllContent.txt:L257-263]( /SoftwareEng/Lec/AllContent.txt#L257-263))*
* **a) Evaluation & Evaluators:**
  * **Incremental Development:** Increments are evaluated before moving to the next. The evaluation is typically performed by a *customer proxy* or internal project manager.
  * **Incremental Delivery:** Each increment is deployed to production. The evaluation is performed by *real end-users* in their practical, daily working environment.
* **b) Main Deployment Goal:**
  * **Incremental Development:** The goal is to build, test, and iterate on versions internally to develop the software step-by-step.
  * **Incremental Delivery:** The goal is to deploy usable software versions directly to customers early so they can gain business value immediately.

---

### Section D: Case Study and Scenario-Based Modeling (15 Marks)

#### 1. Model Recommendation & Justification (5 Marks)
*Award 2 marks for model name, and 1.5 marks for each justification. (Ref: [AllContent.txt:L112-120]( /SoftwareEng/Lec/AllContent.txt#L112-120), [L160-163]( /SoftwareEng/Lec/AllContent.txt#L160-163))*
* **Recommended Model:** Integration and configuration / Reuse-oriented software engineering.
* **Justifications:**
  1. QuickBuy wants to purchase an existing Commercial Off-The-Shelf (COTS) inventory system instead of writing it from scratch.
  2. QuickBuy wants to minimize the risk of developing a customized system from scratch and has already identified three candidate packages to evaluate.

#### 2. Five Stages of the Reuse-oriented Process (5 Marks)
*Award 1 mark for each stage listed with correct context. (Ref: [AllContent.txt:L164-171]( /SoftwareEng/Lec/AllContent.txt#L164-171))*
1. **Requirements specification:** QuickBuy defines the required system functions and constraints for inventory and supplier management.
2. **Software discovery and evaluation:** QuickBuy searches for and evaluates existing systems (the 3 candidate COTS packages) to see if they fit.
3. **Requirements refinement:** QuickBuy modifies/refines its requirements to align with the capabilities of the selected COTS system.
4. **Application system configuration:** QuickBuy configures the COTS system features to match its business workflows.
5. **Component adaptation and integration:** QuickBuy adapts components and integrates the COTS software with its existing web-based point-of-sale system.

#### 3. Evaluation (5 Marks)
*Award 2.5 marks for a valid advantage and 2.5 marks for a valid disadvantage. (Ref: [AllContent.txt:L172-177]( /SoftwareEng/Lec/AllContent.txt#L172-177))*
* **Major Advantage:** Reduced cost and risk since less software is developed from scratch, and faster delivery because they are using already-tested existing components.
* **Major Disadvantage:** Inevitable requirements compromises (the COTS system may not fit all of QuickBuy's exact business needs), and loss of control over the future evolution of the reused component.
