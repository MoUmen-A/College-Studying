# Cybersecurity Fundamentals - Comprehensive Exam
**Course:** CCY2001: Introduction to Cybersecurity  
**Topics Covered:** Computer Malwares & Cyberattacks  
**Total Questions:** 15  
**Difficulty:** Mixed (Easy, Medium, Hard)

---

## Section 1: Multiple Choice Questions

**1. (Easy) Which of the following is a primary characteristic of a computer virus?**
A. It replicates across networks without any user action.
B. It locks out the screen and asks for a financial payment.
C. It requires an executable file to be run by the user to become active.
D. It intercepts network traffic through a man-in-the-middle attack.

**2. (Easy) Which type of malware primarily opens a backdoor on a victim's computer, masquerading as legitimate software, so hackers can establish control?**
A. Trojan Horse
B. Spyware
C. Adware
D. Browser Hijacker

**3. (Medium) A company reports that its servers are experiencing an overwhelming amount of traffic originating from thousands of compromised machines distributed globally. This is best described as:**
A. SQL Injection
B. Denial of Service (DoS)
C. Distributed Denial of Service (DDoS)
D. Path Traversal

**4. (Hard) The "Ping of Death" (PoD) is a type of DoS attack. It specifically exploits which of the following vulnerabilities?**
A. Utilizing cross-site scripting (XSS) to flood the server.
B. Sending an ICMP request that exceeds the 65,535-byte maximum size limitation, causing memory overflow.
C. Hijacking the SSL certificate to drop packets.
D. Submitting a single quote character `(')` to bypass database authentication.

**5. (Medium) Which of the following attacks relies heavily on psychological manipulation, creating a sense of urgency, and impersonating trusted entities (like banks)?**
A. Cryptojacking
B. Phishing
C. Rootkit injection
D. Zero-Day Exploitation

**6. (Hard) A malware infection has completely taken over a system's application programming interfaces (APIs) at the administrator level. When the user requests the OS to start the antivirus, this malware interrupts the request and sends a fake response. What type of malware is this?**
A. Botnet
B. Rootkit
C. Scareware
D. Adware

**7. (Medium) If a cybercriminal uses a technique encoding special characters like `%2e%2e/%2f` in a web request to access restricted sensitive files such as `/etc/passwd`, they are performing:**
A. Path Traversal (Directory Traversal)
B. DNS Spoofing
C. HTTP Spoofing
D. A Shrew Attack

**8. (Medium) Your computer's fans are unusually loud, it is overheating, and CPU usage has unexpectedly spiked to 100% despite only having a web browser open. Which attack is most likely taking place?**
A. Spamming
B. Ransomware (Screen-Locking type)
C. Cryptojacking
D. XSS (Cross-Site Scripting)

**9. (Hard) In which attack does a hacker exploit the TCP retransmission timeout (RTO) mechanism by sending short synchronized bursts of traffic to disrupt connections on the same link?**
A. SYN Flood
B. ICMP Flooding
C. Shrew Attack
D. Backscatter

**10. (Medium) An attacker inputs `admin' OR 1=1 --` into a website's login form, which successfully logs them into the dashboard. What attack vector was utilized?**
A. Zero-Day Exploit
B. Man-in-the-Middle (MITM)
C. Command & Control Hijacking
D. SQL Injection

**11. (Medium) What is the primary difference between a Worm and a Virus?**
A. Worms encrypt files, Viruses only steal data.
B. Worms can replicate and spread across a network without any user interaction, whereas Viruses need a host executable to be run.
C. Worms are types of Trojans, while Viruses are types of Spyware.
D. Worms use social engineering, Viruses use zero-day exploits.

**12. (Easy) An employee gets a phone call from someone claiming to be from the IT department, urgently asking for their login credentials. This specific form of attack is referred to as:**
A. Smishing
B. Vishing (Voice Phishing)
C. General Phishing
D. Spamming

---

## Section 2: Diagram & Scenario Analysis

**13. (Medium) Analyze the network architecture depicted below:**

```text
          [Attacker / Bot-Herder]
                    | (Commands)
          +---------+---------+
          V         V         V
      [Zombie]  [Zombie]  [Zombie] 
          |         |         | (Malicious Traffic)
          +-----> [Victim Server] <-----+
```
**Based on the diagram and your knowledge of computer malware, what type of attack is being orchestrated?**
A. A centralized Spyware data exfiltration.
B. A traditional Denial of Service (DoS) attack from a single node.
C. A Distributed Denial of Service (DDoS) using a Botnet.
D. A Scareware distribution campaign.

**14. (Hard) Examine the two attack scenarios represented below:**

```text
SCENARIO 1:
[Client] <=======================> [Server]
                  |
                  V (Secretly Monitoring)
              [Attacker]

SCENARIO 2:
[Client]                           [Server]
                                     ^ 
                                     | (Forged Identity)
              [Attacker] ------------+
```
**Which pair of attack terms best describes Scenario 1 and Scenario 2 respectively?**
A. Scenario 1: Man-In-The-Middle (Active interception); Scenario 2: DDoS
B. Scenario 1: Passive Attack (Eavesdropping); Scenario 2: Masquerade (Impersonation)
C. Scenario 1: Botnet Attack; Scenario 2: Path Traversal
D. Scenario 1: Replay Attack; Scenario 2: Cryptojacking

**15. (Medium) You receive a pop-up window loudly alarming you that "15 VIRUSES HAVE BEEN DETECTED" and urging you to urgently download a "Free Antivirus Scanner" to fix your system. However, your computer is functioning normally otherwise. What is the most likely categorization of this popup?**
A. Scareware designed to exploit fear and spread actual malware.
B. A genuine browser-hijacked alert from the OS kernel.
C. Encrypting Ransomware initiating its locking sequence.
D. A Zero-Day vulnerability warning.

---

## Answer Key

1. **C** (A virus requires execution to activate and replicate.)
2. **A** (Trojan horses masquerade as legitimate software and open backdoors.)
3. **C** (DDoS uses multiple, distributed infected machines to overwhelm a target.)
4. **B** (Ping of Death exploits ICMP limitations exceeding 65,535 bytes.)
5. **B** (Phishing relies on impersonation, fear, and urgency.)
6. **B** (Rootkits gain deep, invisible administrator/kernel level control over OS APIs.)
7. **A** (Path / Directory Traversal aims to escape the web-root to read local system files.)
8. **C** (Cryptojacking silently exploits hardware resources to mine cryptocurrency.)
9. **C** (A Shrew attack targets TCP RTO mechanisms with short bursts.)
10. **D** (SQL Injection uses SQL query manipulation like boolean logic to bypass auth.)
11. **B** (Worms are self-propagating over networks; viruses need user execution.)
12. **B** (Vishing is the telephone/voice equivalent of phishing.)
13. **C** (The architecture clearly shows zombies being commanded to attack a singular target.)
14. **B** (Scenario 1 shows listening without altering traffic = Passive. Scenario 2 shows the attacker pretending to be the client = Masquerade.)
15. **A** (Scareware uses fake, frightening alerts to trick users into downloading payloads.)