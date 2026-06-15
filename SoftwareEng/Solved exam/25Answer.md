# CSE2001 - Software Engineering Final Exam Solutions
**Date of Exam:** 21/6/2025  
**Course Curriculum Reference:** [AllContent.txt](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt)

---

## Part 1: Multiple Choice Questions (MCQs)

### Question 1:
How does the Spiral Model address requirement engineering throughout the software lifecycle?
- a) All requirements are fully defined and frozen at the very beginning of the project.
- **b) Requirements are incrementally refined and re-evaluated during each iteration.**
- c) Requirement engineering is primarily a post-development activity to document features.
- d) It focuses solely on technical requirements, ignoring user needs.

**Answer:** **b**  
**Explanation (Ref: [AllContent.txt:L304-307](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L304-307)):** The Spiral Model is an iterative, risk-driven process model. Unlike the Waterfall model which freezes requirements early, each loop of the spiral involves identifying goals, analyzing risks, and incrementally refining and re-evaluating requirements based on prototype feedback.

---

### Question 2:
In the context of software testing, which technique focuses on testing the internal structure, design, and implementation of the software?
- **a) White-box Testing**
- b) Black-box Testing
- c) Acceptance Testing
- d) Regression Testing

**Answer:** **a**  
**Explanation (Ref: [AllContent.txt:L29-30](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L29-30)):** White-box testing (also called structural testing) uses knowledge of the program's code, structure, design, and implementation to design test cases, contrasting with Black-box testing which relies solely on requirements.

---

### Question 3:
Which of the following best describes a 'hard real-time' system?
- a) A system where missing a deadline degrades performance but is tolerable.
- **b) A system where missing a deadline results in catastrophic system failure.**
- c) A system that responds quickly to user input, but not necessarily within strict time constraints.
- d) A system that requires frequent updates to its software.

**Answer:** **b**  
**Explanation (Ref: [AllContent.txt:L1049-1050](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L1049-1050)):** By definition, in a hard real-time system, the correctness of the system depends not only on the logical result but also on the time it is delivered. Missing a timing deadline leads to total and potentially catastrophic failure of the system.

---

### Question 4:
Which of the following is a characteristic of the Incremental Model?
- a) All requirements are gathered and documented at the beginning.
- b) It is best suited for projects with well-understood and stable requirements.
- **c) A working version of the system is produced quickly and then evolved.**
- d) It minimizes customer feedback during development.

**Answer:** **c**  
**Explanation (Ref: [AllContent.txt:L104-108](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L104-108)):** In the incremental model, development is broken down into multiple increments. The basic core requirements are implemented first, yielding a working version of the system quickly, which is subsequently evolved and expanded in later stages.

---

### Question 5:
Which type of stimulus in a real-time system occurs at unpredictable intervals?
- a) Periodic Stimuli
- b) Deterministic Stimuli
- c) Continuous Stimuli
- **d) Aperiodic Stimuli**

**Answer:** **d**  
**Explanation (Ref: [AllContent.txt:L1064-1066](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L1064-1066)):** Aperiodic stimuli occur irregularly and unpredictably, usually triggered by external events in the environment (e.g., interrupts or emergency overrides), unlike periodic stimuli which occur at set intervals.

---

## Part 2: Scenario-Based Questions

### Scenario A: Autonomous Traffic Light Control System

#### a) Classification & Justification
- **Classification:** **Hard Real-time System**
- **Justification:** According to the scenario, *"A delay of even a few seconds in reaction time could lead to gridlock or serious accidents."* In a hard real-time system, missing a deadline results in catastrophic failure (collisions, safety hazard, loss of life). In contrast, soft real-time systems only experience degraded performance when deadlines are missed. Because this system is safety-critical and failure to respond in time leads to physical harm, it is a hard real-time system.

#### b) Stimuli Identification
- **Periodic Stimulus:** The regular polling of inductive loop sensors in the road (e.g., every 50ms) to read vehicle speeds and count presence, or continuous frame-by-frame feed analysis from the cameras.
- **Aperiodic Stimulus:** The sudden detection of an emergency vehicle siren, or an emergency manual override signal from traffic authority dispatchers, which happens at unpredictable intervals.

#### c) Responsiveness
- **Responsiveness** is the system's ability to receive an environmental input (stimulus) and complete the execution of the corresponding logic to control the output (actuator) within a strict, guaranteed timing deadline (Ref: [AllContent.txt:L1040-1043](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L1040-1043)).
- In this specific traffic control system, responsiveness represents how quickly the system processes video streams showing an approaching car or an emergency siren, computes the updated timing schedule, and changes the traffic signals to prevent accidents.

---

### Scenario B: Online Course Platform

#### a) Recommended Model & Justification
- **Recommended Model:** **Incremental Development Model**
- **Justification:**
  1. **Quick Initial Feedback:** The scenario specifies that the university wants to *"prioritize quick initial deployment to gather user feedback"*. The Incremental model allows rapid release of a core version (with basic listing and enrollment) to gather feedback, which then informs subsequent builds.
  2. **Evolving & Flexible Scope:** The university anticipates adding complex, interactive features (live discussion, analytics) in *"future phases based on pilot program feedback and emerging technologies."* The Incremental model is designed to handle changing requirements, allowing specification, development, and validation to interleave (Ref: [AllContent.txt:L104-108](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L104-108)).

#### b) Flow Diagram for the Incremental Process Model
```mermaid
flowchart TD
    Start([Start Project]) --> Req[1. Define Outline Requirements]
    Req --> Inc1[Increment 1: Core Platform<br>- Course Listing<br>- Student Enrollment<br>- Basic Content Delivery]
    Inc1 --> Deploy1[Deploy & Gather User/Pilot Feedback]
    Deploy1 --> ReqRef1[Refine Requirements for next phase]
    ReqRef1 --> Inc2[Increment 2: Interactive Features<br>- Live Discussions<br>- Collaborative Assignments]
    Inc2 --> Deploy2[Deploy & Gather Feedback]
    Deploy2 --> ReqRef2[Refine Requirements for advanced features]
    ReqRef2 --> Inc3[Increment 3: Advanced Modules<br>- Grading Modules<br>- Analytics]
    Inc3 --> Final[Final Platform Release]
```

#### c) Evaluation of the Alternative Model (Waterfall Model)
- **Why Waterfall is Less Appropriate:**
  1. **Inflexibility to Change:** Waterfall is a linear, sequential plan-driven model (Ref: [AllContent.txt:L130-133](file:///d:/Gam3a/Exam-Creation/SoftwareEng/Lec/AllContent.txt#L130-133)). All requirements must be finalized at the start. Since the university needs to adapt based on feedback and emerging educational technologies, any changes under Waterfall would require expensive rework.
  2. **No Early Working System:** Under Waterfall, the platform would not be delivered or seen by users until the very end of the cycle (after all coding and testing of all features is complete). This directly conflicts with the goal of a quick initial pilot deployment to gather feedback.

---

## Part 3: Behavioral & Security Modeling

### A. Misuse Case Diagram (Online Public Event Ticket Sales System)

This misuse case diagram shows how an Attacker (Misuser) threatens standard ticket operations and how the system uses security controls to mitigate these threats.

```mermaid
flowchart LR
    %% Actors
    Customer([Customer])
    Attacker([Attacker / Bot])

    subgraph System Boundary: Event Ticket Sales System
        %% Legitimate Use Cases
        UC_Browse((Browse Events))
        UC_Select((Select Seats))
        UC_Purchase((Purchase Tickets))
        UC_Receive((Receive Digital Tickets))

        %% Misuse Cases (Threats)
        MC_DDoS((Disrupt System - DDoS)):::misuse
        MC_Bots((Manipulate Allocations - Bot Buying)):::misuse
        MC_Steal((Steal Payment Details)):::misuse
        MC_Intercept((Intercept Digital Tickets)):::misuse

        %% Security Use Cases (Controls)
        SC_WAF((Rate Limiting & WAF)):::security
        SC_Captcha((CAPTCHA & Bot Detection)):::security
        SC_Encrypt((PCI-DSS & SSL/TLS Encryption)):::security
        SC_Sign((Digital Signing & MFA)):::security
    end

    %% Legitimate Actor Links
    Customer --- UC_Browse
    Customer --- UC_Select
    Customer --- UC_Purchase
    Customer --- UC_Receive

    %% Attacker Links
    Attacker --- MC_DDoS
    Attacker --- MC_Bots
    Attacker --- MC_Steal
    Attacker --- MC_Intercept

    %% Threat Relations
    MC_DDoS -.->|<<threaten>>| UC_Browse
    MC_DDoS -.->|<<threaten>>| UC_Purchase
    MC_Bots -.->|<<threaten>>| UC_Select
    MC_Bots -.->|<<threaten>>| UC_Purchase
    MC_Steal -.->|<<threaten>>| UC_Purchase
    MC_Intercept -.->|<<threaten>>| UC_Receive

    %% Mitigation Relations
    SC_WAF -.->|<<mitigate>>| MC_DDoS
    SC_Captcha -.->|<<mitigate>>| MC_Bots
    SC_Encrypt -.->|<<mitigate>>| MC_Steal
    SC_Sign -.->|<<mitigate>>| MC_Intercept

    classDef misuse fill:#ffcccc,stroke:#ff0000,stroke-width:2px;
    classDef security fill:#ccffcc,stroke:#00aa00,stroke-width:2px;
```

---

### B. State Machine Diagram (Automatic Washing Machine)

This state machine models the washing cycles, including the ability to transition to a `Paused` state at any point before completion, and resume where it left off.

```mermaid
stateDiagram-v2
    [*] --> Ready
    Ready --> Filling : Press Start (Select Program)
    
    Filling --> Washing : Water Level Sufficient
    Washing --> Draining1 : Wash Cycle Complete
    Draining1 --> Rinsing : Water Level Empty
    Rinsing --> Draining2 : Rinse Cycle Complete
    Draining2 --> Spinning : Rinse Water Empty
    Spinning --> Finished : Spin Cycle Complete
    Finished --> Ready : Open Door & Retrieve Clothes

    %% Pausing mechanism from all active states
    Filling --> Paused : Press Pause / Open Door
    Washing --> Paused : Press Pause / Open Door
    Draining1 --> Paused : Press Pause / Open Door
    Rinsing --> Paused : Press Pause / Open Door
    Draining2 --> Paused : Press Pause / Open Door
    Spinning --> Paused : Press Pause / Open Door

    Paused --> Filling : Press Start / Resume (Fill water)
    Paused --> Washing : Press Start / Resume (Wash)
    Paused --> Draining1 : Press Start / Resume (Drain dirty water)
    Paused --> Rinsing : Press Start / Resume (Rinse)
    Paused --> Draining2 : Press Start / Resume (Drain rinse water)
    Paused --> Spinning : Press Start / Resume (Spin)
```

---

## Part 4: Comprehensive UML System Specification (HASS)

### 1. Use Case Diagram
Shows the relationships between Patients, Medical Staff, Doctors, Administrators, and the HASS system.

```mermaid
flowchart LR
    %% Actors
    Patient([Patient])
    Staff([Medical Staff])
    Doctor([Doctor])
    Admin([Administrator])
    EmailSys([Email/SMS Gateway])

    subgraph HASS Boundary
        %% Patient Use Cases
        UC_Reg((Register Account))
        UC_Log((Login))
        UC_Search((Search Appointments))
        UC_Book((Book Appointment))
        UC_ViewAppt((View Upcoming Appts))
        UC_Resched((Reschedule Appt))
        UC_Cancel((Cancel Appt))

        %% Staff Use Cases
        UC_ViewCal((View Doctor's Calendar))
        UC_BookBehalf((Book on behalf of Patient))
        UC_Checkin((Check-in Patient))
        UC_UpdatePat((Update Patient Details))
        UC_Notes((Record Visit Notes))

        %% Doctor Use Cases
        UC_ViewDocSchedule((View Personal Schedule))

        %% Admin Use Cases
        UC_ManageDoc((Manage Doctor Profiles))
        UC_ConfigService((Configure Services))
        UC_ConfigHours((Configure Operating Hours))
        UC_Reports((Generate Reports))
    end

    %% Patient Connections
    Patient --- UC_Reg
    Patient --- UC_Log
    Patient --- UC_Search
    Patient --- UC_Book
    Patient --- UC_ViewAppt
    Patient --- UC_Resched
    Patient --- UC_Cancel

    %% Staff Connections
    Staff --- UC_Log
    Staff --- UC_ViewCal
    Staff --- UC_BookBehalf
    Staff --- UC_Checkin
    Staff --- UC_UpdatePat
    Staff --- UC_Notes

    %% Doctor Connections
    Doctor --- UC_Log
    Doctor --- UC_ViewDocSchedule

    %% Admin Connections
    Admin --- UC_Log
    Admin --- UC_ManageDoc
    Admin --- UC_ConfigService
    Admin --- UC_ConfigHours
    Admin --- UC_Reports

    %% Gateway Connections (Secondary Actor)
    UC_Book -.->|<<extend>>| EmailSys
    UC_Resched -.->|<<extend>>| EmailSys
```

---

### 2. Sequence Diagram (Patient Booking an Appointment)
Shows the sequential flow of messages during a successful appointment booking.

```mermaid
sequenceDiagram
    autonumber
    actor Patient
    participant Portal as Web/Mobile UI
    participant Ctrl as HASS Controller
    participant DB as Appointment Database
    actor Gateway as Email/SMS Gateway

    Patient->>Portal: searchAppointments(doctor, specialty, date)
    Portal->>Ctrl: getAvailableSlots(doctor, specialty, date)
    Ctrl->>DB: querySlots(doctor, date)
    DB-->>Ctrl: return availableSlots
    Ctrl-->>Portal: displaySlots(availableSlots)
    Portal-->>Patient: show slot grid

    Patient->>Portal: selectSlotAndBook(slotId)
    Portal->>Ctrl: bookAppointment(patientId, slotId)
    Ctrl->>DB: createAppointmentRecord(patientId, slotId, status="Booked")
    DB-->>Ctrl: bookingSuccess(appointmentId)
    
    par Send Notification
        Ctrl->>Gateway: sendNotification(patientContactInfo, "Your appointment is confirmed.")
        Gateway-->>Patient: SMS/Email Delivered
    end

    Ctrl-->>Portal: confirmBooking(appointmentId)
    Portal-->>Patient: show booking confirmation screen
```

---

### 3. Class Diagram
Describes the object structure, attributes, methods, and relationships of the HASS classes.

```mermaid
classDiagram
    class User {
        <<Abstract>>
        +int userId
        +string name
        +string email
        +string phone
        +string password
        +login() bool
        +logout() bool
    }

    class Patient {
        +string dateOfBirth
        +string address
        +register() bool
        +searchSlots(specialty, date) List
        +bookAppointment(slotId) Appointment
        +rescheduleAppointment(appointmentId, newDate) bool
        +cancelAppointment(appointmentId) bool
    }

    class MedicalStaff {
        +int staffId
        +string department
        +viewDoctorCalendar(doctorId) List
        +bookForPatient(patientId, slotId) Appointment
        +checkInPatient(appointmentId) bool
        +updatePatientDetails(patientId, details) bool
        +recordVisitNotes(patientId, notes) bool
    }

    class Doctor {
        +int doctorId
        +string specialty
        +string clinicRoom
        +viewSchedule() List
        +viewPatientDetails(patientId) Patient
    }

    class Administrator {
        +int adminId
        +manageDoctorProfile(doctorId, profile) bool
        +configureServices(serviceId, config) bool
        +setOperatingHours(clinicId, hours) bool
        +generateReport(reportType) Report
    }

    class Appointment {
        +int appointmentId
        +int patientId
        +int doctorId
        +dateTime appointmentTime
        +string status
        +updateStatus(newStatus) bool
        +reschedule(newTime) bool
    }

    class DoctorProfile {
        +int doctorId
        +string specialty
        +string bio
        +List availabilityCalendar
        +updateAvailability(calendar) bool
    }

    class ClinicService {
        +int serviceId
        +string name
        +string department
        +int durationMinutes
    }

    class Report {
        +int reportId
        +string type
        +dateTime dateGenerated
        +string content
        +generate() bool
    }

    %% Inheritance
    User <|-- Patient
    User <|-- MedicalStaff
    User <|-- Doctor
    User <|-- Administrator

    %% Associations
    Patient "1" --> "0..*" Appointment : books
    Doctor "1" --> "0..*" Appointment : conducts
    MedicalStaff "1" --> "0..*" Appointment : manages
    Administrator "1" --> "0..*" Report : generates
    Administrator "1" --> "0..*" DoctorProfile : configures
    Administrator "1" --> "0..*" ClinicService : configures
    Doctor "1" --> "1" DoctorProfile : possesses
```
