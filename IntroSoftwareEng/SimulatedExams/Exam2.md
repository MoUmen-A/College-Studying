# CSE2001 - Software Engineering
## Simulated Exam 2: Software Testing & Security Engineering
**Course:** CSE2001  
**Time Allowed:** 2 Hours  
**Total Marks:** 50 Marks  

---

### Section A: Complete the Statements (10 Marks, 2 Marks Each)
*Fill in the missing terms in the statements below. Do not write full sentences, just provide the correct term or phrase.*

1. Program testing is intended to show that a program does what it should do, but testing can only reveal the presence of errors, not their __________.
2. While verification asks "Are we building the product right?", __________ asks "Are we building the right product?" to confirm the software meets customer needs.
3. In automated unit testing, the three parts of a test case structure are: 1. Setup, 2. Call, and 3. __________.
4. The three dimensions of security engineering (often abbreviated as the CIA triad) are: Confidentiality, Integrity, and __________.
5. An interception threat (e.g., an attacker reading a patient's private medical database records) is an attack on the security dimension of __________.

---

### Section B: Short Answer & Explanations (15 Marks, 5 Marks Each)
*Answer the following questions concisely. Ensure you cover all parts of the question.*

1. Contrast "Development testing" and "Release testing" in terms of:
   * The team/person performing the tests.
   * The primary goals of the testing phase.
   * The knowledge and access to implementation details.
2. Explain the process of Test-Driven Development (TDD). List the incremental cycle steps and name three (3) distinct benefits that TDD provides to developers.
3. Explain why "Operational Security" is considered a human and social issue rather than a purely technical software engineering problem. How should security protection be balanced with system effectiveness?

---

### Section C: Differences and Comparisons (10 Marks, 5 Marks Each)
*Provide clear, structured comparisons for the following concepts. Using tables is recommended.*

1. Differentiate between "Software Inspections" and "Software Testing" across three (3) points of comparison: execution requirements, stage of development/artifacts they can be applied to, and the types of characteristics (functional vs. non-functional) they can verify.
2. Differentiate between the three (3) security assurance strategies: "Vulnerability avoidance," "Attack detection and elimination," and "Exposure limitation and recovery." Provide a brief definition and one (1) concrete example for each.

---

### Section D: Case Study and Scenario-Based Modeling (15 Marks)
*Read the scenario below and answer the tasks that follow.*

**Scenario:**  
A local clinic is launching an online patient portal called "HealthNet." Patients use this application to view their medical history, read lab reports, and input their basic health metrics (e.g., weight, age). The portal connects to a central database over the internet. Security is a major concern, as medical data is highly private and sensitive. Additionally, the development team must ensure the software undergoes thorough testing before it is rolled out.

#### Tasks:
1. **Security Classification (5 Marks):** Suppose an attacker attempts to alter a patient's lab result in the database. Classify this specific attack in terms of:
   a) The security dimension compromised.
   b) The threat type (using the IIMF threat classification).
   Justify your classifications based on definitions from security engineering.
2. **Test Case Selection (5 Marks):** The age entry input field on the health metrics page only accepts integer values between 1 and 120 (inclusive). Show how you would apply **partition testing** to design test cases for this field. Identify the equivalence partitions (valid and invalid) and suggest representative test values for each partition.
3. **Scenario Testing (5 Marks):** HealthNet needs to undergo release testing. Explain what scenario-based testing means in this context and sketch one (1) brief, realistic usage scenario that could be used to derive tests.
