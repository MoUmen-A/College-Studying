# Software Requirements Engineering: Advanced Examination Series
## Exam 09: External Interfaces, Embedded Subsystems & Safety Verification
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
Analyze the following requirement from an automotive over-the-air (OTA) firmware update system:
> *"The vehicle shall download software updates wirelessly and install them when convenient without bricking the car."*
- **a) Defect Identification (2.5 Marks):** Critique 'when convenient' and 'without bricking the car'. Why are these colloquialisms unacceptable in a safety-critical specification?
- **b) Surgical Rewrite (2.5 Marks):** Rewrite into two verifiable requirements: one defining precise vehicle state prerequisites for installation (e.g., vehicle parked, battery charge $\ge 70\%$, ignition off) and one specifying cryptographic hash verification and atomic rollback upon flash failure.

#### Question 2 (5 Marks)
Analyze the following requirement from a collision avoidance sensor module:
> *"The front radar unit should alert the braking subsystem quickly if an object appears suddenly in front of the vehicle."*
- **a) Defect Identification (2.5 Marks):** Evaluate the vagueness of 'quickly' and 'appears suddenly'.
- **b) Surgical Rewrite (2.5 Marks):** Formulate a deterministic requirement specifying sensor detection distance, time-to-collision threshold, and maximum allowable CAN-bus message transmission latency ($\le 20$ ms).

---

### Section B: Conceptual Discrimination & Theoretical Rationale (10 Marks, 5 Marks Each)
*Answer the following deep-dive theoretical prompts with structured, professional justifications.*

#### Question 3 (5 Marks)
External Interfaces in Systems Engineering: **User vs. Software vs. Hardware vs. Communications** (5 Marks):
- Software applications do not exist in isolation; they connect to the physical world through external interfaces.
- Define and contrast the four major external interface classes:
  1. **User Interfaces (UI)**
  2. **Software Interfaces (APIs / Shared Data)**
  3. **Hardware Interfaces (Sensors, Actuators, Microcontrollers)**
  4. **Communications Interfaces (Protocols, Wireless, Busses)**
- Provide a concrete automotive connected-vehicle example for each of the four interface classes.

#### Question 4 (5 Marks)
The Role of **Acceptance Criteria and Requirements Testability** (5 Marks):
- Why is an untestable requirement considered an engineering defect?
- Explain how the early authoring of **System Test Cases** during the Requirements Analysis phase serves as a powerful validation filter.
- What is meant by the phrase: *'If you cannot write a test case for a requirement, you do not understand the requirement'*?

---

### Section C: Elicitation Technique Strategy & Trade-Off Analysis (10 Marks, 5 Marks Each)
*Evaluate the operational scenarios below and justify your strategic elicitation choices.*

Elicitation in Multi-Disciplinary Hardware/Software Projects (10 Marks - 5 Marks each):
1. **Reverse Engineering / Interface Analysis of Legacy Hardware:** An automotive OEM is integrating a new telematics gateway with a 10-year-old engine control unit (ECU). The original ECU vendor has gone out of business. Explain how an analyst performs **Interface Analysis and Protocol Decoding (Reverse Engineering)** to elicit signal definitions, baud rates, and message timing from physical CAN-bus traces.
2. **Simulated Drive Testing vs. Driver Focus Groups:** To design a heads-up display (HUD) driver alert system, the team wants to understand driver distraction. Compare gathering feedback via a **Focus Group** against observing driver reaction times in an **Instrumented Driving Simulator**. Explain why simulator telemetry reveals unconscious eye-gaze and reaction latencies that focus group participants cannot articulate.

---

### Section D: Artifact Engineering & Scope Modeling (10 Marks, 5 Marks Each)
*Construct formal requirements engineering models according to the prompt instructions.*

Modeling Connected Vehicle Systems (10 Marks):
1. **Context Diagram: Automotive Telematics Gateway (5 Marks):** Design a Context Diagram for the `Telematics Gateway Unit (TGU)`:
   - Central Process: `Telematics Gateway Module`.
   - Four External Terminators: `Cloud Telematics Server (via 5G Cellular)`, `Vehicle In-Cabin Touchscreen (Infotainment)`, `Internal Vehicle CAN-Bus Network`, and `GPS Satellite Constellation`.
   - Specify two data/control flows for each terminator crossing the physical boundary.
2. **Subsystem Requirements Allocation (5 Marks):** An automatic emergency call feature (**eCall**) triggers when an airbag deploys during a crash. Allocate this requirement across:
   - Hardware Subsystem (accelerometers, pyrotechnic sensors, cellular modem).
   - Software Subsystem (crash confirmation algorithm, telemetry packaging, automated voice dispatch).
   - External Infrastructure Subsystem (cellular tower roaming, emergency dispatch operator).

---

### Section E: Comprehensive Real-World Case Study Engineering (10 Marks)
*Carefully read the enterprise engineering scenario and deliver the three technical tasks that follow.*

#### Scenario Context: AutoTech Motors is deploying an Over-The-Air (OTA) firmware update platform across 2 million connected electric vehicles. 
The system must deploy security patches and autonomous driving updates remotely. 
If an update is corrupted or interrupted due to loss of cellular signal, the vehicle must never be left in an un-drivable condition. 
Furthermore, government automotive cybersecurity regulations (ISO/SAE 21434 and UN R156) mandate strict digital signing and cryptographic verification of all firmware images before installation. 
You are the Lead Systems Analyst responsible for the firmware update SRS.

#### Engineering Tasks & Deliverables:
- **Task 1: Specifying Atomic Firmware Installation Requirements (4 Marks):** Write two formal functional requirements specifying the pre-installation cryptographic signature verification process and the atomic A/B dual-partition memory flashing mechanism ensuring instant rollback if boot verification fails.

- **Task 2: Specifying Non-Functional Cybersecurity & Integrity Requirements (3 Marks):** Author two verifiable Non-Functional Product Requirements specifying end-to-end encryption standards (e.g., TLS 1.3 with mutual certificate authentication) and firmware image integrity hash validation using SHA-256.

- **Task 3: Operational State Prerequisites for Safe Installation (3 Marks):** Detail three mandatory environmental and operational guard conditions that the vehicle software must verify *before* initiating a safety-critical ECU firmware update (e.g., transmission in Park, emergency brake engaged, high-voltage battery state of charge $\ge 50\%$, vehicle speed = 0 km/h).

