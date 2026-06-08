# 🎓 Exam Creation & Study Guide Workspace

Welcome to the **Exam-Creation** workspace. This repository is structured to manage lecture content, previous exams, and generated guide answers/question banks for university courses. It serves as an automated hub for creating study aids, aligning closely with course material and previous exams.

Currently, the workspace supports two key subjects:
- **Cybersecurity (CyberSec)**
- **Advanced Programming Applications (AdvancedPro)**

---

## 📂 Repository Structure

The workspace is organized into subject-specific folders and custom agent instruction sets:

```
Exam-Creation/
├── CyberSec/                 # Cybersecurity course materials
│   ├── Lec/                  # Lecture notes and slides content
│   ├── PrevExam/             # Historical exam papers and midterm files
│   ├── GuideAnswer/          # Generated question banks & detailed guide answers
│   └── Cyberinstructions.md  # Instructions/prompt for the Cybersecurity AI agent
└── AdvancedPro/              # Advanced Programming (Java & Spring Boot) materials
    ├── Lect/                 # Spring Boot, Servlets, JDBC, and Multithreading notes
    ├── PrevExams/            # Past exams (25.md, 25-26.md) rewritten to Spring Boot & Thymeleaf
    ├── AI-QestionBank/       # Generated Spring Boot & Multithreading question banks
    └── APA-insturction.md    # Instructions/prompt for the Advanced Programming AI agent
```

---

## 📄 Core Components

### 🤖 1. AI Agent Instructions
Each module has its own dedicated system prompt file to guide the AI exam generation agent to analyze inputs, calibrate tone, and structure outputs:
- **Cybersecurity Instructions ([CyberSec/Cyberinstructions.md](CyberSec/Cyberinstructions.md)):** Focuses on cryptographic algorithms, network protocol security, and threat mitigation.
- **Advanced Programming Instructions ([AdvancedPro/APA-insturction.md](AdvancedPro/APA-insturction.md)):** Focuses exclusively on Java backend engineering, Spring Boot architectures, JPA mappings, Thymeleaf, and multithreading concurrency, ensuring "Full Mark" calibration rules are applied.

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
This module is focused on modern Java backend development, Spring Boot, Object-Relational Mapping (ORM), and Multithreading.

* **Lectures ([AdvancedPro/Lect/](AdvancedPro/Lect/)):**
  - [Lect1-JDBC](AdvancedPro/Lect/Lect1-JDBC) – Java Database Connectivity API core steps and statements.
  - [Lec3-HTTPServlet](AdvancedPro/Lect/Lec3-HTTPServlet) – HttpServlets, RequestDispatchers, redirects, and stateful Cookies.
  - [Lec5-MVC-Thymleaf](AdvancedPro/Lect/Lec5-MVC-Thymleaf) – Model-View-Controller pattern basics and Thymeleaf templates.
  - [Lect6-Spring_Boot_Architecture.md](AdvancedPro/Lect/Lect6-Spring_Boot_Architecture.md) – Spring Boot layered architecture and application flow.
  - [Lect7-IOC_DI_SpringBoot2.md](AdvancedPro/Lect/Lect7-IOC_DI_SpringBoot2.md) – Inversion of Control (IoC), Dependency Injection (DI), and bean definitions.
  - [Lect9-Session_Req_Singleton_Proxy_Vs_Bean_SpringBoot3.md](AdvancedPro/Lect/Lect9-Session_Req_Singleton_Proxy_Vs_Bean_SpringBoot3.md) – Scopes (Request, Session, Singleton), Proxying, and injection conflicts.
  - [Lect10_Hibernate_ORM_Vs_JPA_Thymleaf_SpringBoot.md](AdvancedPro/Lect/Lect10_Hibernate_ORM_Vs_JPA_Thymleaf_SpringBoot.md) – JPA entities, relationship mappings (`@ManyToOne`, `@ManyToMany`), `JpaRepository`, and Thymeleaf form binding.
  - [Lect11_Scheduler_sleep_yield_join_Priority_MultiThreading1.md](AdvancedPro/Lect/Lect11_Scheduler_sleep_yield_join_Priority_MultiThreading1.md) – Thread creation, runnable execution, priority scheduling, and basic thread control (`sleep`, `yield`, `join`).
  - [Lect12 ThreadPool(Exuotor ,RaceCondition, Sync)-MultiThreading part 2](AdvancedPro/Lect/Lect12%20ThreadPool(Exuotor%20,RaceCondition,%20Sync)-MultiThreading%20part%202) – Concurrency thread pools (`ExecutorService`), race conditions, critical regions, and synchronized methods/blocks.

* **Previous Exams ([AdvancedPro/PrevExams/](AdvancedPro/PrevExams/)):**
  - [25.md](AdvancedPro/PrevExams/25.md) & [25-26.md](AdvancedPro/PrevExams/25-26.md) – Reverted historical exam scripts completely rewritten to feature Spring Boot, JPA, and Thymeleaf technologies instead of raw Servlets, JSP, and traditional JDBC.

* **AI Generated Question Banks ([AdvancedPro/AI-QestionBank/](AdvancedPro/AI-QestionBank/)):**
  - [Lect9_Scopes_questions.md](AdvancedPro/AI-QestionBank/Lect9_Scopes_questions.md) – Question bank for Spring Bean scopes, Sessions, and Dynamic Proxies.
  - [Lect10_JPA_questions.md](AdvancedPro/AI-QestionBank/Lect10_JPA_questions.md) – Question bank for ORM, entity mappings, relationships, and Thymeleaf.
  - [Lect11_Multithreading1_questions.md](AdvancedPro/AI-QestionBank/Lect11_Multithreading1_questions.md) – Question bank for Process vs Thread memory, execution states, priority hints, and thread coordination.
  - [Lect12_ThreadPool_Synchronization_questions.md](AdvancedPro/AI-QestionBank/Lect12_ThreadPool_Synchronization_questions.md) – Question bank for fixed thread pools, critical regions, race conditions (read-modify-write cycle), and object-level/class-level locking.

---

## 🛠️ How to Generate Exam Question Banks

If you are using an LLM / AI agent to generate new question banks or solve exams in this workspace, follow these steps:

1. **Provide Context:** Feed the lecture contents (from `CyberSec/Lec/` or `AdvancedPro/Lect/`) and target past exams (from the corresponding `PrevExam/` or `PrevExams/` folder).
2. **Inject the Instructions:** Feed the contents of either [CyberSec/Cyberinstructions.md](CyberSec/Cyberinstructions.md) or [AdvancedPro/APA-insturction.md](AdvancedPro/APA-insturction.md) as the system prompt or primary prompt instructions.
3. **Execute and Save:** Save generated questions, guide answers, and coverage gap analysis to the appropriate directory (e.g. `CyberSec/GuideAnswer/` or `AdvancedPro/AI-QestionBank/`).
