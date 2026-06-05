# 🎓 Exam Creation & Study Guide Workspace

Welcome to the **Exam-Creation** workspace. This repository is structured to manage lecture content, previous exams, and generated guide answers/question banks for university courses. It serves as an automated hub for creating study aids, aligning closely with course material and previous exams.

Currently, the workspace supports two key subjects:
- **Cybersecurity (CyberSec)**
- **Advanced Programming (AdvancedPro)**

---

## 📂 Repository Structure

The workspace is organized into subject-specific folders and an automated agent instruction set:

```
Exam-Creation/
├── instructions.md           # Instructions/prompt for the AI exam generation agent
├── CyberSec/                 # Cybersecurity course materials
│   ├── Lec/                  # Lecture notes and slides content
│   ├── PrevExam/             # Historical exam papers and midterm files
│   └── GuideAnswer/          # Generated question banks & detailed guide answers
└── AdvancedPro/              # Advanced Programming (Java & Spring Boot) materials
    ├── Lect/                 # Spring Boot & Multithreading lecture markdown notes
    └── PrevExams/            # Placeholder for previous Advanced Programming exams
```

---

## 📄 Core Components

### 🤖 1. AI Agent Instructions ([instructions.md](instructions.md))
The root file [instructions.md](instructions.md) serves as a system prompt for an intelligent exam preparation assistant. It guides the AI agent to:
- **Analyze Inputs:** Extract key concepts, identify previous exam tones, and map cognitive levels to Bloom's taxonomy.
- **Generate 7 Question Types:**
  1. *Multiple Choice (MCQ)* (with realistic distractors)
  2. *Short Answer* (recall/comprehension)
  3. *Application* (scenario-based problem solving)
  4. *Compare & Contrast* (similarities/differences/significance)
  5. *Essay / Long Answer* (synthesis and depth)
  6. *True / False + Justification* (reasoning checks)
  7. *Fill-in-the-blank* (precise terminology)
- **Calibrate Tone:** Match the level of formality, verb preferences (e.g., "define", "explain", "compare"), and language mix (e.g., English technical terms inside Arabic phrasing if present in the lectures).
- **Structure Outputs:** Include the question, a model guide answer, key points for full marks, common student mistakes, difficulty breakdown (~30% Easy, ~40% Medium, ~30% Hard), and a coverage gap analysis.

---

### 🛡️ 2. Cybersecurity (`CyberSec/`)
This module is dedicated to the Cybersecurity curriculum, covering network endpoint security, cryptography, malware, and key management.

* **Lectures ([CyberSec/Lec/](CyberSec/Lec/)):**
  - [CyberMalware.txt](CyberSec/Lec/CyberMalware.txt) – Types of malware, propagation mechanisms, and defense.
  - [Hashfunction.txt](CyberSec/Lec/Hashfunction.txt) – Cryptographic hash functions, properties (one-way, collision resistance), and SHA.
  - [ModernCy\[her](CyberSec/Lec/ModernCy[her) – Modern symmetric and asymmetric cryptography.
  - [NetEndPointSec](CyberSec/Lec/NetEndPointSec) – Network security, firewalls, and endpoint defense.
  - [NetworkSecurityBasics.txt](CyberSec/Lec/NetworkSecurityBasics.txt) – Fundamental security goals (CIA triad) and network attacks.
  - [cyberAttack](CyberSec/Lec/cyberAttack) – Categories and details of cyber attacks.
  - [keymang](CyberSec/Lec/keymang) – Key distribution, KDC, KTC, and symmetric key management.
  - [publicKey](CyberSec/Lec/publicKey) – Public-key infrastructure (PKI), RSA, and X.509 certificates.

* **Previous Exams ([CyberSec/PrevExam/](CyberSec/PrevExam/)):**
  - Past exam scripts from years [23](CyberSec/PrevExam/23) and [25.txt](CyberSec/PrevExam/25.txt).
  - Midterm exams: [midterm_A.pdf](CyberSec/PrevExam/midterm_A.pdf) and [midterm_makeup.pdf](CyberSec/PrevExam/midterm_makeup.pdf).

* **Guide Answers & Question Banks ([CyberSec/GuideAnswer/](CyberSec/GuideAnswer/)):**
  - [Exam_23_Guide_Answers.md](CyberSec/GuideAnswer/Exam_23_Guide_Answers.md) and [Exam_25_Guide_Answers.md](CyberSec/GuideAnswer/Exam_25_Guide_Answers.md) – Step-by-step model solutions for past exam questions.
  - Topic-focused question banks, such as [KeyManagement_Summary_And_Questions.md](CyberSec/GuideAnswer/KeyManagement_Summary_And_Questions.md), [NetEndPointSec_QuestionBank.md](CyberSec/GuideAnswer/NetEndPointSec_QuestionBank.md), and [NetworkBasics_HashFunction_QuestionBank.md](CyberSec/GuideAnswer/NetworkBasics_HashFunction_QuestionBank.md).

---

### 💻 3. Advanced Programming (`AdvancedPro/`)
This module is focused on Java, Spring Boot, Object-Relational Mapping (ORM), and Multithreading.

* **Lectures ([AdvancedPro/Lect/](AdvancedPro/Lect/)):**
  - [Lect6-Spring_Boot_Architecture.md](AdvancedPro/Lect/Lect6-Spring_Boot_Architecture.md) – Overview of Spring Boot structure and runtime flow.
  - [Lect7-IOC_DI_SpringBoot2.md](AdvancedPro/Lect/Lect7-IOC_DI_SpringBoot2.md) – Inversion of Control (IoC) and Dependency Injection (DI) concepts.
  - [Lect9-Session_Req_Singleton_Proxy_Vs_Bean_SpringBoot3.md](AdvancedPro/Lect/Lect9-Session_Req_Singleton_Proxy_Vs_Bean_SpringBoot3.md) – Scopes (Request, Session, Singleton), Proxying, and Bean configurations.
  - [Lect10_Hibernate_ORM_Vs_JPA_Thymleaf_SpringBoot.md](AdvancedPro/Lect/Lect10_Hibernate_ORM_Vs_JPA_Thymleaf_SpringBoot.md) – Object-Relational Mapping with Hibernate vs JPA, and Thymeleaf integration.
  - [Lect11_Scheduler_sleep_yield_join_Priority_MultiThreading1.md](AdvancedPro/Lect/Lect11_Scheduler_sleep_yield_join_Priority_MultiThreading1.md) – Multithreading basics, thread schedulers, thread states, and controls (`sleep`, `yield`, `join`, priority).

* **Previous Exams ([AdvancedPro/PrevExams/](AdvancedPro/PrevExams/)):**
  - *Folder ready for historical exam materials.*

---

## 🛠️ How to Generate Exam Question Banks

If you are using an LLM / AI agent to generate new question banks or solve exams in this workspace, follow these steps:

1. **Provide Context:** Feed the lecture contents (from `CyberSec/Lec/` or `AdvancedPro/Lect/`) and target past exams (from the corresponding `PrevExam/` folder).
2. **Inject the Instructions:** Feed the contents of [instructions.md](instructions.md) as the system prompt or primary prompt instructions.
3. **Execute and Save:** The generated questions, guide answers, and coverage gap analysis should be saved to the appropriate `GuideAnswer/` directory following the naming format: `[Topic]_QuestionBank.md`.
