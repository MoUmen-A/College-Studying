# CSE2001 - Software Engineering
## Simulated Exam 2: Guide Answer & Marking Scheme

---

### Section A: Complete the Statements (10 Marks, 2 Marks Each)

1. **absence**  
   *(Ref: [AllContent.txt:600](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#600) - "Testing can reveal the presence of errors, not their absence.")*
2. **validation**  
   *(Ref: [AllContent.txt:622-627](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L622-627) - "Verification: Are we building the product right?... Validation: Are we building the right product?")*
3. **Assertion**  
   *(Ref: [AllContent.txt:701-706](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L701-706) - "Setup... Call... Assertion...")*
4. **Availability**  
   *(Ref: [AllContent.txt:874-883](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L874-883) - "Confidentiality, Integrity, Availability...")*
5. **confidentiality**  
   *(Ref: [AllContent.txt:875-877](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L875-877) - "Confidentiality: Information must not be disclosed... Attacker reads patient records.")*

---

### Section B: Short Answer & Explanations (15 Marks, 5 Marks Each)

#### 1. Contrast "Development testing" and "Release testing" (5 Marks)
*Award up to 5 marks based on covering all three required comparison points. (Ref: [AllContent.txt:746-750](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L746-750))*
* **Performing team (1.5 Marks):** Development testing is conducted by the software developers themselves. Release testing is conducted by a separate, independent testing team.
* **Primary goals (2 Marks):** Development testing is defect testing, aiming to find bugs and break code. Release testing is validation testing, aiming to prove to the supplier/client that the software is complete, fits requirements, and is ready for external use.
* **Implementation details (1.5 Marks):** Developers have access to source code and use implementation knowledge (white-box/structural testing). Release testers usually do not inspect source code and test from specifications (black-box testing).

#### 2. Test-Driven Development (TDD) process and benefits (5 Marks)
*Award 2.5 marks for process explanation and 2.5 marks for three correct benefits. (Ref: [AllContent.txt:731-741](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L731-741))*
* **TDD Process Cycle:**
  1. Identify a small chunk of functionality to implement.
  2. Write an automated test for it *before* writing any implementation code.
  3. Run all tests (the new test fails because the code is missing).
  4. Write the implementation code.
  5. Rerun all tests, ensuring the new code passes.
  6. Move to the next functionality increment.
* **Benefits (Choose any three):**
  * **Code coverage:** Every code segment written has at least one associated test.
  * **Regression testing:** An automated suite of regression tests builds up incrementally.
  * **Simplified debugging:** When a test fails, the bug is almost certainly in the newly written code.
  * **System documentation:** The test code acts as a functional specification showing what the program should do.

#### 3. Operational Security: Human/Social aspect and balance (5 Marks)
*Award 2.5 marks for explaining the human/social aspect, and 2.5 marks for the balance discussion. (Ref: [AllContent.txt:888-898](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L888-898))*
* **Human/Social issue:** Operational security concerns human behavior. Users often bypass security features (e.g., sharing passwords, leaving sessions logged in) because doing so makes their jobs easier. It is a human factor rather than a software defect.
* **Balance:** Security must balance technical protection with system usability and effectiveness. If controls are too restrictive, users will actively subvert them to remain productive, resulting in a less secure system in practice.

---

### Section C: Differences and Comparisons (10 Marks, 5 Marks Each)

#### 1. Software Inspections vs Software Testing (5 Marks)
*Award up to 5 marks based on clarity and correctness of the comparison. (Ref: [AllContent.txt:641-655](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L641-655))*

| Point of Comparison | Software Inspections (Static) | Software Testing (Dynamic) |
| :--- | :--- | :--- |
| **Execution requirements** | Does not require running the code. | Requires executing the software with test inputs. |
| **Development artifacts** | Can be applied to incomplete code, UML models, requirements, database designs. | Can only be applied to runnable code/systems. |
| **Verified characteristics** | Strong at verifying quality attributes like standard compliance, portability, maintainability. | Strong at verifying non-functional attributes (e.g., performance) and customer usability. |

#### 2. Security Assurance Strategies (5 Marks)
*Award 1.5 marks for each strategy's explanation and example, plus 0.5 bonus for formatting. (Ref: [AllContent.txt:949-963](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L949-963))*
* **Vulnerability avoidance:** Designing the system so that security vulnerabilities do not exist.
  * *Example:* Having no external connection to a server (external attacks become impossible).
* **Attack detection and elimination:** Detecting and neutralizing active attacks before they can exploit vulnerabilities.
  * *Example:* Implementing a firewall or running real-time virus scanner monitors.
* **Exposure limitation and recovery:** Designing systems to limit damage and quickly restore assets in the event of a successful attack.
  * *Example:* Having regular automated offline backup databases and data restoration processes.

---

### Section D: Case Study and Scenario-Based Modeling (15 Marks)

#### 1. Security Classification (5 Marks)
*Award 2.5 marks for the dimension, and 2.5 marks for the threat classification. (Ref: [AllContent.txt:878-881](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L878-881) & [L933-937](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L933-937))*
* **a) Security Dimension:** **Integrity**.
  * *Justification:* Integrity requires that information is not damaged, corrupted, or altered in an unauthorized manner. Changing lab test results violates integrity.
* **b) Threat Type:** **Modification**.
  * *Justification:* Under IIMF, modification is when an attacker tampers with a system asset (alters or destroys a record), which directly applies to changing existing lab results in the database.

#### 2. Equivalence Partitioning Test Design (5 Marks)
*Award 1.25 marks for each partition listed with its corresponding test values. (Ref: [AllContent.txt:710-715](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L710-715))*
1. **Valid Partition (1 to 120 inclusive):**
   * *Representative Test Values:* `25` (middle), `1` (lower boundary), `120` (upper boundary).
2. **Invalid Partition - Too Low (< 1):**
   * *Representative Test Values:* `0` (boundary), `-5` (negative value).
3. **Invalid Partition - Too High (> 120):**
   * *Representative Test Values:* `121` (boundary), `200` (extreme value).
4. **Invalid Partition - Non-Integer:**
   * *Representative Test Values:* `22.5` (decimal), `abc` (text).

#### 3. Scenario Testing (5 Marks)
*Award 2 marks for the explanation, and 3 marks for the scenario description. (Ref: [AllContent.txt:754-756](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L754-756))*
* **Explanation:** Scenario testing is a validation technique where a typical usage flow through the system is sketched out, and a test case is derived to exercise multiple related features in sequence rather than testing them in isolation.
* **Usage Scenario Sketch:**
  * *Scenario:* "A patient logs into HealthNet, navigates to the 'Lab Results' section, downloads the PDF file for their recent blood test, reviews it, goes to the profile page to update their current weight value, clicks save, and securely logs out of the portal."
  * *This tests:* Authentication, authorization/access control, file downloading, profile modification, database updating, and session termination in one sequential flow.
