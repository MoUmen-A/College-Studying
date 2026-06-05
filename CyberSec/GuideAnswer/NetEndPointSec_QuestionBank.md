# Cybersecurity Fundamentals — Question Bank
**Course:** CCY2001: Introduction to Cybersecurity  
**Topic Covered:** Network Endpoint Security (Topic 7)  
**Total Questions:** 30  
**Difficulty Distribution:** ~30% Easy · ~40% Medium · ~30% Hard

---

## Section 1 — Topic Summary

- **Network Security Components** include Device Security (protecting routers, switches, and end systems), Firewalls, Intrusion Detection Systems (IDS), and Intrusion Prevention Systems (IPS).
- **Firewalls** act as a security choke point implementing "defense in depth," with four control techniques: Service control, Direction control, User control, and Behavior control. Types include Packet Filtering, Stateful Inspection, Application-Level Proxy, and Circuit-Level Proxy firewalls.
- **DMZ (Demilitarized Zone)** networks sit between external and internal firewalls, hosting externally accessible services (Web, Email, DNS servers) while protecting the internal enterprise network through layered firewall defenses.
- **Intrusion Detection Systems (IDS)** consist of three components — Sensors, Analyzers, and User Interface — and use two detection approaches: Misuse Detection (signature-based, accurate but cannot detect novel attacks) and Anomaly Detection (behavior-based, detects unknown attacks but trades off between false positives and false negatives).
- **IDS classification** includes Host-based IDS (HIDS) — monitoring a single host using threshold and profile-based strategies — and Network-based IDS (NIDS) — monitoring network traffic using string, port, and header condition signatures, deployed at four strategic sensor locations.

---

## Section 2 — Tone Analysis

The past exams use a **formal academic tone** with precise technical vocabulary. Questions favour directive verbs such as *"describe,"* *"explain,"* *"choose,"* *"write the scientific term,"* and *"sketch the block diagram."* MCQ items follow a consistent pattern: a stem with four choices (a–d or i–iv), one correct answer, and distractors that reference real but incorrect concepts. Multi-part questions escalate from recall to application. Mark allocations range from 2 pts (scientific term / MCQ) to 12–14 pts (complex application problems). The 2025 exam already includes questions on Packet Filtering Firewall and NIDS, confirming this topic is actively tested.

---

## Section 3 — Question Bank

---

### Multiple Choice (MCQ)

---

### Q1 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**  
A firewall provides an additional layer of defense following the military doctrine known as:  
a. Perimeter Security  
b. Defense in Depth  
c. Zero Trust Architecture  
d. Least Privilege

**Guide answer:**  
**b. Defense in Depth**

**Key points to include:**
- The lecture explicitly states that firewalls follow the "defense in depth" military doctrine
- This involves multiple layers of defense to insulate internal systems from external threats

**Common mistakes to avoid:**  
Students sometimes select "Perimeter Security" because firewalls sit at the network perimeter. However, the lecture specifically references the "defense in depth" doctrine, which emphasises multiple overlapping layers — not just perimeter-based protection.

---

### Q2 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**  
Which firewall technique controls how particular services are used, for example filtering email to eliminate spam?  
a. Service control  
b. Direction control  
c. User control  
d. Behavior control

**Guide answer:**  
**d. Behavior control**

**Key points to include:**
- Behavior control governs *how* services are used (e.g., filtering spam, limiting access to portions of a web server)
- Service control determines *which* services are accessible
- Direction control determines the *direction* of allowed traffic
- User control governs access based on *who* is requesting it

**Common mistakes to avoid:**  
Students often confuse Service control with Behavior control. Service control decides *what* services are allowed; Behavior control decides *how* an allowed service is used. The spam filtering example is the key distinguisher.

---

### Q3 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**  
One of the following is a weakness of Packet Filtering Firewalls:  
a. They are complex and slow to process  
b. They cannot prevent attacks that employ application-specific vulnerabilities  
c. They require advanced user authentication  
d. They examine upper-layer data thoroughly

**Guide answer:**  
**b. They cannot prevent attacks that employ application-specific vulnerabilities**

**Key points to include:**
- Packet filters do not examine upper-layer (application) data
- They are actually simple and fast (opposite of option a)
- They do NOT support advanced user authentication (option c describes something they lack, not a weakness they have)
- They are also vulnerable to TCP/IP specification exploits like IP address spoofing

**Common mistakes to avoid:**  
Students may select option (c) because packet filters lack advanced authentication — but the question asks for a weakness (vulnerability), not a missing feature. The inability to inspect application-layer data is the critical weakness that allows application-specific attacks to pass through.

---

### Q4 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**  
An Intrusion Detection System (IDS) comprises three logical components. Which of the following is NOT one of them?  
a. Sensors  
b. Analyzers  
c. Encryptors  
d. User Interface

**Guide answer:**  
**c. Encryptors**

**Key points to include:**
- The three IDS components are: Sensors (collect data), Analyzers (determine if intrusion occurred), and User Interface (view output/control system)
- Encryptors are not part of an IDS

**Common mistakes to avoid:**  
Students who do not study the IDS architecture may confuse encryption components with IDS components. The IDS is a detection and monitoring system — it does not encrypt data.

---

### Q5 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**  
The Network-based Intrusion Detection System (NIDS):  
a. Takes action to block or mitigate attacks  
b. Examines user and software activity on each host on a network  
c. Monitors traffic at selected points on a network  
d. Provides secure communication over an insecure network

**Guide answer:**  
**c. Monitors traffic at selected points on a network**

**Key points to include:**
- NIDS monitors network traffic for particular network segments or devices
- Option (a) describes an IPS, not an IDS
- Option (b) describes a Host-based IDS
- Option (d) describes a VPN or IPsec

**Common mistakes to avoid:**  
Students frequently confuse IDS with IPS. An IDS **detects** and **alerts**; it does not take action to block attacks — that is the role of an Intrusion Prevention System (IPS). Also, NIDS monitors *network traffic*, not individual host activity (which is HIDS).

---

### Q6 — MCQ | Bloom's: Understand | Difficulty: Hard | Marks: 2

**Question:**  
In a Packet Filtering Firewall, the default policy "Default = discard" means:  
a. That which is not expressly prohibited is permitted  
b. All packets are discarded regardless of rules  
c. That which is not expressly permitted is prohibited  
d. Only encrypted packets are forwarded

**Guide answer:**  
**c. That which is not expressly permitted is prohibited**

**Key points to include:**
- "Default = discard" is the more restrictive policy — blocks everything not explicitly allowed
- "Default = forward" (option a) is the opposite — allows everything not explicitly blocked
- These are the two default policies available in packet filtering firewalls

**Common mistakes to avoid:**  
Students may confuse the two default policies. The secure approach is "Default = discard" (whitelist model), while "Default = forward" (blacklist model) is more permissive and therefore less secure.

---

### Fill-in-the-Blank

---

### Q7 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**  
A __________ is a hardware and/or software capability that limits access between a network and devices attached to the network, in accordance with a specific security policy.

**Guide answer:**  
Firewall

**Key points to include:**
- Exact definition from the lecture material
- Firewalls can be hardware, software, or both

**Common mistakes to avoid:**  
Students sometimes write "router" or "IDS." A router forwards traffic based on routing tables, and an IDS detects intrusions — neither limits access according to a security policy the way a firewall does.

---

### Q8 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**  
The process of collecting information about events occurring in a computer system or network and analyzing them for signs of intrusions is called __________.

**Guide answer:**  
Intrusion Detection

**Key points to include:**
- This is the exact definition from the lecture
- Distinct from "Intrusion Prevention" which also takes action to stop attacks

**Common mistakes to avoid:**  
Writing "Intrusion Prevention" instead of "Intrusion Detection." Detection involves collecting and analyzing information; prevention involves additionally taking action to block the intrusion.

---

### Q9 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**  
A __________ firewall tightens up the rules for TCP traffic by creating a directory of outbound TCP connections, allowing incoming traffic to high-numbered ports only for packets that fit the profile of an existing connection entry.

**Guide answer:**  
Stateful Inspection

**Key points to include:**
- Stateful Inspection maintains a connection state table (directory of outbound TCP connections)
- It only allows inbound packets that correspond to an established outbound connection

**Common mistakes to avoid:**  
Writing "Packet Filtering" — while both filter packets, a standard packet filter applies static rules without tracking connection state. Stateful Inspection specifically tracks the state of active connections.

---

### Q10 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Medium | Marks: 2

**Question:**  
The region between an external firewall and one or more internal firewalls, where externally accessible systems such as Web servers, email servers, and DNS servers are typically located, is called a __________ network.

**Guide answer:**  
DMZ (Demilitarized Zone)

**Key points to include:**
- DMZ sits between external and internal firewalls
- Houses servers that need external connectivity
- Provides a buffer zone protecting the internal enterprise network

**Common mistakes to avoid:**  
Students may write "perimeter network" or "subnet" — while these terms are related, the specific term from the lecture is DMZ (Demilitarized Zone).

---

### Short Answer

---

### Q11 — Short Answer | Bloom's: Remember | Difficulty: Easy | Marks: 4

**Question:**  
List the four techniques of operation (control types) that a firewall uses and briefly describe each one.

**Guide answer:**  
The four firewall techniques of operation are:
1. **Service control** — determines the types of Internet services that can be accessed, inbound or outbound, filtering traffic based on IP address, protocol, or port number.
2. **Direction control** — determines the direction in which particular service requests may be initiated and allowed to flow through the firewall.
3. **User control** — controls access to a service according to which user is attempting to access it, typically applied to local users and may apply to external users using secure authentication such as IPsec.
4. **Behavior control** — controls how particular services are used, for example filtering email to eliminate spam or limiting external access to portions of a local Web server.

**Key points to include:**
- All four types named and described
- Specific examples for each control type as provided in the lecture

**Common mistakes to avoid:**  
Students often confuse Service control with Behavior control. Service control determines *which* services are available; Behavior control determines *how* allowed services are used.

---

### Q12 — Short Answer | Bloom's: Understand | Difficulty: Medium | Marks: 5

**Question:**  
Describe the three logical components of an Intrusion Detection System (IDS) and explain the role of each.

**Guide answer:**  
An IDS comprises three logical components:
1. **Sensors** — responsible for collecting data from various parts of the system. Input types include network packets, log files, and system call traces. Sensors forward collected information to the analyzer.
2. **Analyzers** — receive input from one or more sensors or other analyzers. The analyzer determines if an intrusion has occurred and provides output indicating the intrusion, including supporting evidence and guidance about what actions to take.
3. **User Interface** — enables a user to view output from the system or control the behavior of the system. In some systems, it may report to a manager, director, or console component.

**Key points to include:**
- All three components named with their specific roles
- Types of input for sensors (network packets, log files, system call traces)
- Analyzer determines intrusion occurrence and provides guidance
- User interface allows viewing output and controlling system behavior

**Common mistakes to avoid:**  
Students sometimes confuse the Analyzer with the Sensor. The Sensor *collects* data; the Analyzer *evaluates* it to determine if an intrusion has occurred. The Analyzer also provides guidance on corrective actions.

---

### True / False + Justify

---

### Q13 — True/False + Justify | Bloom's: Understand | Difficulty: Easy | Marks: 3

**Question:**  
"Packet Filtering Firewalls examine upper-layer application data to prevent application-specific attacks."

**Guide answer:**  
**False.** Packet Filtering Firewalls do **not** examine upper-layer data. They filter packets based only on information in the IP packet header — including source/destination IP addresses, source/destination port numbers, the IP protocol field, and the interface. Because they lack the ability to inspect application-layer content, they **cannot** prevent attacks that exploit application-specific vulnerabilities or functions.

**Key points to include:**
- Packet filters operate on network/transport layer headers only
- They cannot see or analyse application-layer data
- This is explicitly listed as a weakness of packet filtering firewalls

**Common mistakes to avoid:**  
Simply stating "False" without explaining what packet filters actually examine and why this limitation matters. Full marks require explaining both what they do and what they cannot do.

---

### Q14 — True/False + Justify | Bloom's: Analyse | Difficulty: Medium | Marks: 3

**Question:**  
"Misuse detection (signature-based IDS) is superior to anomaly detection because it can detect both known and unknown attacks."

**Guide answer:**  
**False.** Misuse detection uses pattern-matching algorithms operating on large databases of known attack signatures. While it is **accurate and generates few false alarms**, its significant disadvantage is that it **cannot detect novel or unknown attacks** — only attacks matching known signatures. It is **anomaly detection** that can detect previously unknown attacks, because it looks for deviations from normal behavior rather than matching specific patterns. However, anomaly detection has its own drawback: a significant trade-off between false positives and false negatives.

**Key points to include:**
- Misuse detection: accurate, few false alarms, but cannot detect unknown attacks
- Anomaly detection: detects unknown attacks, but trades off between false positives and false negatives
- Neither approach is absolutely superior — each has distinct strengths and weaknesses

**Common mistakes to avoid:**  
Accepting the statement because misuse detection is "accurate." Accuracy for known attacks does not extend to unknown attacks. Students must distinguish between detecting known patterns (misuse) and detecting deviations from normal behavior (anomaly).

---

### Q15 — True/False + Justify | Bloom's: Understand | Difficulty: Easy | Marks: 3

**Question:**  
"A Host-based IDS can detect both external intrusions (from outside the network) and internal intrusions (from authorized users), which is something that neither network-based IDS nor firewalls can achieve."

**Guide answer:**  
**True.** The primary benefit of a Host-based IDS is that it can detect **both external and internal intrusions**. Since it monitors activity directly on the host system — including user accounts, processes, and data files — it can identify when authorized users exceed their legitimate access levels or conduct unauthorized activity. Network-based IDS and firewalls focus on network traffic and cannot observe what happens at the host level after traffic has been permitted through.

**Key points to include:**
- HIDS monitors the host directly (processes, user accounts, data files)
- Can detect internal misuse by authorized users
- NIDS and firewalls only monitor network traffic, not host-level activity

**Common mistakes to avoid:**  
Stating "False" because firewalls can block external attacks. The question specifically asks about *detecting* both external and internal intrusions — firewalls block but do not detect internal misuse, and NIDS cannot observe host-level activity from authorized users.

---

### Q16 — True/False + Justify | Bloom's: Understand | Difficulty: Medium | Marks: 3

**Question:**  
"An Application-Level Proxy Firewall allows end-to-end TCP connections between internal and external hosts."

**Guide answer:**  
**False.** An Application-Level Proxy Firewall (also called an Application Level Gateway) does **not** allow end-to-end TCP connections. Instead, it acts as a **relay** of application-level traffic. The user contacts the gateway, provides authentication credentials, and the gateway then contacts the remote host on behalf of the user, relaying TCP segments between the two endpoints. If the gateway does not implement the proxy code for a specific application, that service cannot be forwarded across the firewall.

**Key points to include:**
- No direct end-to-end TCP connection between user and remote host
- Gateway acts as an intermediary relay
- Requires proxy code for each supported application
- Unsupported services are completely blocked

**Common mistakes to avoid:**  
Confusing Application-Level Proxy with Circuit-Level Proxy. Both prevent end-to-end TCP connections, but Application-Level Proxy examines and controls application-specific content, while Circuit-Level Proxy relays TCP segments without examining contents after connection setup.

---

### Application (Scenario-Based)

---

### Q17 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 8

**Question:**  
A university's IT department wants to deploy a firewall to protect its internal network while still allowing external users to access the university's website, email server, and DNS server.

**(a)** Describe the network architecture the IT department should deploy, including the role of external and internal firewalls. (Marks: 4)

**(b)** Explain how the internal firewall provides two-way protection with respect to the publicly accessible servers. (Marks: 4)

**Guide answer:**  
**(a)** The IT department should deploy a **DMZ (Demilitarized Zone) network architecture**:
- An **external firewall** is placed at the edge of the university network, just inside the boundary router connecting to the Internet. It provides a measure of access control and protection for the DMZ systems consistent with their need for external connectivity, and also provides a basic level of protection for the rest of the network.
- The Web server, email server, and DNS server are placed in the **DMZ** — the region between the external and internal firewalls — because they require external connectivity.
- An **internal firewall** protects the bulk of the enterprise network (administrative systems, student databases, workstations) from both external attacks and attacks originating from compromised DMZ systems.

**(b)** The internal firewall provides **two-way protection**:
1. **Protects the internal network from DMZ attacks** — if a DMZ system (e.g., the web server) is compromised by malware such as worms, rootkits, or bots, the internal firewall prevents these threats from reaching internal servers and workstations.
2. **Protects DMZ systems from internal attacks** — the internal firewall also guards the DMZ systems from attacks launched from within the internal protected network, ensuring that an insider threat cannot compromise public-facing services.

Additionally, internal firewalls can protect portions of the internal network from each other (e.g., protecting internal servers from internal workstations and vice versa).

**Key points to include:**
- DMZ architecture with external and internal firewalls
- Publicly accessible servers placed in DMZ
- External firewall provides first layer of defense
- Internal firewall provides two-way protection (inward and outward)
- Malware types mentioned: worms, rootkits, bots

**Common mistakes to avoid:**  
Placing the web, email, and DNS servers behind the internal firewall — this would block legitimate external access. These servers must be in the DMZ to balance accessibility with protection. Also, forgetting the two-way nature of internal firewall protection.

---

### Q18 — Application | Bloom's: Analyse | Difficulty: Hard | Marks: 10

**Question:**  
A financial institution's security team is evaluating two IDS approaches — misuse detection and anomaly detection — for deployment on their banking network.

**(a)** Explain the operating principle of each approach. (Marks: 4)

**(b)** Describe the key advantage and disadvantage of each approach. (Marks: 4)

**(c)** Which approach (or combination) would you recommend for a financial institution and why? (Marks: 2)

**Guide answer:**  
**(a)**
- **Misuse Detection** is based on rules that specify system events, sequences of events, or observable properties that indicate security incidents. It uses **pattern-matching algorithms** operating on large databases of known attack patterns (signatures). When network activity matches a known signature, an alert is generated.
- **Anomaly Detection** searches for activity that is **different from the normal behavior** of system entities and system resources. It first establishes a baseline of normal behavior, then flags deviations from that baseline as potential intrusions.

**(b)**
- **Misuse Detection:**
  - *Advantage:* Accurate and generates **few false alarms** because it matches against known, verified attack patterns.
  - *Disadvantage:* **Cannot detect novel or unknown attacks** — only attacks whose signatures exist in the database can be identified.
- **Anomaly Detection:**
  - *Advantage:* Able to detect **previously unknown attacks** based on deviation from normal behavior, without requiring a pre-existing signature.
  - *Disadvantage:* Significant **trade-off between false positives and false negatives**. A loose interpretation catches more intruders but also more legitimate users (false positives); a tight interpretation misses more intruders (false negatives).

**(c)** For a financial institution, a **combination of both approaches** is recommended. Misuse detection provides reliable, accurate alerts for known attacks (critical for compliance and reducing alert fatigue). Anomaly detection provides coverage against novel zero-day attacks that may target financial systems — which is essential given the high-value nature of banking data. The lecture notes that there is an overlap between intruder and authorized user behavior, and the practice of anomaly detection is described as both "a compromise and art" — making AI-based approaches increasingly valuable. In a high-risk environment, the cost of a missed novel attack (false negative) far outweighs the cost of investigating false positives.

**Key points to include:**
- Misuse detection = signature/pattern matching; Anomaly detection = deviation from normal behavior
- Trade-off between false positives and false negatives in anomaly detection
- Overlap between intruder and authorized user behavior profiles
- Combined approach provides comprehensive coverage

**Common mistakes to avoid:**  
Recommending only one approach without justifying why the other's strengths are not needed. In a high-security environment like banking, relying solely on misuse detection leaves the institution vulnerable to zero-day attacks, while relying solely on anomaly detection creates too many false alarms.

---

### Q19 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 6

**Question:**  
A network administrator needs to configure a Packet Filtering Firewall to allow inbound email (SMTP, port 25) to the company's mail gateway (IP: 192.168.1.10), but block all inbound email from a known spam source (IP: 10.0.0.5). All other inbound traffic should be denied by default.

**(a)** State which default policy should be applied and explain why. (Marks: 2)

**(b)** Write the firewall rules in order of priority to implement this configuration. (Marks: 4)

**Guide answer:**  
**(a)** The **"Default = discard"** policy should be applied: *"That which is not expressly permitted is prohibited."* This is the more secure approach because it blocks all traffic that is not explicitly allowed, ensuring that only intended services are accessible. For a corporate network, this prevents unexpected traffic from reaching internal systems.

**(b)** Rules (processed in order):

| Rule | Source IP | Dest IP | Protocol | Dest Port | Action |
|------|-----------|---------|----------|-----------|--------|
| A | 10.0.0.5 | * | * | * | **Discard** |
| B | * | 192.168.1.10 | TCP | 25 | **Allow** |
| C (Default) | * | * | * | * | **Discard** |

- **Rule A** blocks all traffic from the known spam source (10.0.0.5) — placed first so it takes priority over Rule B.
- **Rule B** allows inbound SMTP (TCP port 25) to the mail gateway.
- **Rule C** is the default discard rule — blocks everything else.

**Key points to include:**
- Default = discard is the secure choice
- Rule ordering matters: specific block rule before the general allow rule
- Fields match the packet filtering criteria from the lecture (source IP, dest IP, protocol, port)

**Common mistakes to avoid:**  
Placing Rule B before Rule A — this would allow SMTP from the spam source before it could be blocked. Firewall rules are processed in order; the block rule for 10.0.0.5 must come first. This mirrors the lecture example where SPIGOT is blocked before the general SMTP allow rule.

---

### Q20 — Application | Bloom's: Apply | Difficulty: Hard | Marks: 8

**Question:**  
A company's security operations center (SOC) needs to deploy Network-based Intrusion Detection System (NIDS) sensors across the enterprise network, which includes an external firewall, a DMZ with web and email servers, an internal firewall, internal servers (database, file server), and user workstations on internal LANs.

**(a)** Identify the four types of locations where NIDS sensors can be placed. (Marks: 4)

**(b)** Explain which sensor locations would be most useful for detecting attacks from inside the organization. (Marks: 4)

**Guide answer:**  
**(a)** The four types of NIDS sensor locations are:
1. **Outside the main enterprise firewall** — useful for establishing the overall level of threat directed at the enterprise network from the Internet.
2. **In the network DMZ** (inside the main firewall but outside internal firewalls) — monitors for penetration attempts targeting Web and other externally accessible services.
3. **Behind internal firewalls, on major backbone networks** — monitors traffic to/from internal servers and database resources, detecting attacks that have bypassed the external firewall and DMZ.
4. **Behind internal firewalls, on LANs supporting user workstations** — monitors traffic on internal user networks.

**(b)** **Locations 3 and 4** (behind internal firewalls) are most useful for detecting attacks from inside the organization. These sensors monitor internal network segments and can detect:
- Unauthorized access attempts by employees targeting internal servers or databases (Location 3)
- Malicious activity on user workstation LANs such as lateral movement, unauthorized data access, or malware propagation (Location 4)
- More specific attacks at network segments that would not be visible at the perimeter

Since internal attackers are already past the external firewall and DMZ, sensors at Locations 1 and 2 would not detect their activity. Only sensors monitoring internal traffic can identify insider threats.

**Key points to include:**
- All four locations named with their specific monitoring purposes
- Locations 3 and 4 for insider threat detection (explicitly stated in the lecture)
- NIDS sensors can only see packets on the network segment they are attached to
- Multiple sensors feed information to a central NIDS manager

**Common mistakes to avoid:**  
Assuming Location 1 (outside the external firewall) can detect internal attacks — sensors outside the firewall only see Internet-facing traffic. Also, forgetting that NIDS sensors can only monitor the specific network segment they are attached to.

---

### Compare & Contrast

---

### Q21 — Compare & Contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 6

**Question:**  
Compare and contrast **Misuse Detection** and **Anomaly Detection** as approaches to intrusion detection, in terms of operating principle, accuracy, and ability to detect unknown threats.

**Guide answer:**  

| Aspect | Misuse Detection | Anomaly Detection |
|--------|-----------------|-------------------|
| **Operating principle** | Based on rules specifying system events or properties indicating security incidents; uses pattern-matching on databases of known attack **signatures** | Searches for activity that **deviates from normal behavior** of system entities and resources |
| **Accuracy** | **High accuracy** — generates few false alarms because it matches verified, known patterns | Lower accuracy — significant **trade-off between false positives and false negatives** |
| **Unknown threat detection** | **Cannot detect** novel or unknown attacks; limited to attacks whose signatures exist in the database | **Can detect** previously unknown attacks by identifying abnormal behavior |
| **False positives** | Few false positives | More false positives (loose interpretation catches intruders but also flags legitimate users) |
| **False negatives** | More false negatives for unknown attacks (they simply go undetected) | Depends on interpretation strictness — tight interpretation increases false negatives |
| **Maintenance** | Requires frequent signature database updates | Requires establishing and maintaining accurate behavioral baselines |

Both approaches aim to detect intrusions, and the lecture notes that in practice, the typical behavior of an intruder overlaps with that of an authorized user — making perfect detection impossible with either approach alone.

**Key points to include:**
- Misuse = signature matching; Anomaly = deviation from baseline
- Trade-off between false positives and false negatives in anomaly detection
- Behavioral overlap between intruders and authorized users
- AI plays a growing role in anomaly detection

**Common mistakes to avoid:**  
Declaring one approach universally better than the other. Each has clear advantages and disadvantages, and the lecture emphasises that anomaly detection involves "compromise and art."

---

### Q22 — Compare & Contrast | Bloom's: Analyse | Difficulty: Hard | Marks: 8

**Question:**  
Compare and contrast **Host-based IDS (HIDS)** and **Network-based IDS (NIDS)** in terms of monitoring scope, detection capabilities, deployment strategy, and ability to detect internal threats.

**Guide answer:**  

| Aspect | Host-based IDS (HIDS) | Network-based IDS (NIDS) |
|--------|----------------------|-------------------------|
| **Monitoring scope** | Monitors characteristics and events on a **single host** (one system at a time) | Monitors **network traffic** for particular network segments or devices |
| **What it examines** | User accounts, processes, data files, system call traces, log files on the host | Network packets as they pass by a sensor point |
| **Detection strategies** | Uses anomaly and misuse protection; anomaly detection uses **threshold detection** (frequency thresholds for events) and **profile-based** detection (activity profiles per user) | Uses three signature types: **string signatures** (text strings indicating attacks), **port signatures** (connection attempts to known vulnerable ports), and **header condition signatures** (dangerous header combinations) |
| **Internal threat detection** | Can detect **both external and internal intrusions** — its primary benefit | Primarily detects external threats; limited visibility into host-level internal misuse |
| **Deployment** | Installed on individual vulnerable or sensitive systems (e.g., database servers, administrative systems) | Sensors distributed at key network points feeding information to a **central NIDS manager** |
| **Visibility** | Can see the **intended outcome** of an attack by directly monitoring targeted data files and processes | Can only see packets on the network segment to which the sensor is attached |

Both HIDS and NIDS are complementary — HIDS provides deep visibility into individual hosts and can detect insider threats, while NIDS provides broad network-level visibility across multiple segments.

**Key points to include:**
- HIDS monitors a single host; NIDS monitors network segments
- HIDS detects internal and external intrusions; NIDS primarily external
- HIDS strategies: threshold + profile-based; NIDS signatures: string, port, header condition
- HIDS sees attack outcomes; NIDS sees only passing packets

**Common mistakes to avoid:**  
Stating that NIDS is always better because it monitors the whole network. NIDS can only see packets on its segment and cannot detect host-level internal misuse — this is the primary advantage of HIDS.

---

### Q23 — Compare & Contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 6

**Question:**  
Compare and contrast **Packet Filtering Firewall** and **Application-Level Proxy Firewall** in terms of how they process traffic, the layer at which they operate, transparency to users, and their respective strengths and weaknesses.

**Guide answer:**  

| Aspect | Packet Filtering Firewall | Application-Level Proxy Firewall |
|--------|--------------------------|----------------------------------|
| **Operating layer** | Network/Transport layer (IP and TCP/UDP headers) | Application layer |
| **Traffic processing** | Applies rules to each IP packet based on header fields (source/dest IP, port, protocol, interface); forwards or discards | Acts as a relay — user connects to the gateway, gateway authenticates, then connects to remote host on user's behalf |
| **Connection type** | Allows direct end-to-end connections between source and destination | **No end-to-end connection** — gateway relays traffic between two separate connections |
| **Transparency** | Transparent to users and very fast | Not transparent — user must interact with the gateway (authentication, remote host name) |
| **Content inspection** | Does NOT examine upper-layer (application) data | **Examines** application-level data; can support only specific application features |
| **Strengths** | Simple, fast, transparent | Deep application-level control; can restrict specific application features; stronger security per application |
| **Weaknesses** | Cannot prevent application-specific attacks; vulnerable to IP spoofing; susceptible to misconfiguration | Slower due to application-level processing; requires proxy code for each application; unsupported services are completely blocked |

**Key points to include:**
- Packet filter = network layer, transparent, fast but shallow inspection
- Application proxy = application layer, deep inspection but slower
- Application proxy requires proxy code per application
- Packet filter is vulnerable to spoofing and misconfiguration

**Common mistakes to avoid:**  
Claiming that Packet Filtering Firewalls provide no security because they don't inspect application data. They do provide effective network-layer filtering — they simply cannot protect against application-layer attacks. The two types complement each other in a defense-in-depth strategy.

---

### Essay / Long Answer

---

### Q24 — Essay | Bloom's: Evaluate | Difficulty: Hard | Marks: 15

**Question:**  
Discuss the different types of firewalls covered in the lecture — Packet Filtering, Stateful Inspection, Application-Level Proxy, and Circuit-Level Proxy. For each type, explain its operating principle, describe its strengths and weaknesses, and evaluate which combination of firewall types would provide the most comprehensive security for an enterprise network. Support your answer with the concept of DMZ network architecture.

**Guide answer:**  

**Introduction:**  
Firewalls are a fundamental security mechanism providing "defense in depth" for enterprise networks. Four major types of firewalls operate at different layers and offer distinct trade-offs between performance, security depth, and ease of configuration.

**1. Packet Filtering Firewall:**  
A Packet Filtering Firewall applies rules to each incoming and outgoing IP packet, forwarding or discarding based on header fields: source/destination IP address, source/destination port number, IP protocol field, and interface. Rules are processed in order, with two possible default policies: "Default = discard" (whitelist — more secure) and "Default = forward" (blacklist — less secure).

*Strengths:* Simple, transparent to users, and very fast. *Weaknesses:* Cannot examine upper-layer data (vulnerable to application-specific attacks), does not support advanced user authentication, vulnerable to TCP/IP exploitation such as IP address spoofing, and susceptible to misconfiguration.

**2. Stateful Inspection Firewall:**  
A Stateful Inspection Firewall tightens rules for TCP traffic by maintaining a **directory of outbound TCP connections**. It allows incoming traffic to high-numbered ports only for packets matching the profile of an existing established connection. This provides context-aware filtering that standard packet filters lack.

*Strengths:* Better security than basic packet filtering by tracking connection state. *Weaknesses:* Still does not inspect application-layer content.

**3. Application-Level Proxy Firewall:**  
Also called an Application Level Gateway, this firewall acts as a relay of application-level traffic. Users connect to the gateway, provide authentication, and the gateway contacts the remote host on their behalf. It does not permit end-to-end TCP connections. Only applications for which proxy code is implemented are supported; all others are blocked. The gateway can be configured to support only specific features of an application.

*Strengths:* Deep application-level inspection and control; can enforce fine-grained policies (e.g., allowing specific application features). *Weaknesses:* Not transparent; slower processing; requires proxy implementation per application; unsupported services are completely blocked.

**4. Circuit-Level Proxy Firewall:**  
A Circuit-Level Gateway sets up two TCP connections — one between itself and an inner host, and one between itself and an outer host. Once established, it relays TCP segments **without examining contents**. Security is determined by which connections are allowed.

*Strengths:* More flexible than application proxy (doesn't need per-application proxy code after connection setup); provides connection-level control. *Weaknesses:* Does not inspect data content after connection establishment; limited security compared to application-level inspection.

**Enterprise DMZ Architecture:**  
The most comprehensive enterprise security deploys multiple firewall types in a DMZ architecture:
- An **external firewall** (packet filtering or stateful inspection for performance) at the network edge provides fast, high-throughput first-line defense
- **DMZ network** hosts externally accessible servers (Web, email, DNS)
- An **internal firewall** (application-level proxy for critical segments) provides stringent filtering to protect enterprise servers and workstations
- Internal firewalls provide **two-way protection** — protecting the internal network from compromised DMZ systems (worms, rootkits, bots) and protecting DMZ systems from internal attacks
- Additional internal firewalls can protect portions of the internal network from each other

**Conclusion:**  
No single firewall type provides complete protection. A defense-in-depth strategy combining fast packet filtering at the perimeter with deeper application-level inspection internally, organized around a DMZ architecture, provides the most comprehensive security posture. This layered approach ensures that if one defense is bypassed, additional layers still protect critical assets.

**Key points to include:**
- All four firewall types with operating principles
- Strengths and weaknesses of each
- DMZ architecture with external and internal firewalls
- Two-way protection of internal firewall
- Defense in depth as the recommended strategy
- Specific threats in DMZ context (worms, rootkits, bots)

**Common mistakes to avoid:**  
- Declaring one firewall type as universally best without acknowledging trade-offs
- Forgetting Circuit-Level Proxy (students often only remember three types)
- Not explaining how DMZ architecture implements defense in depth
- Confusing Application-Level and Circuit-Level proxies — the key difference is that Application-Level examines content while Circuit-Level does not

---

### Q25 — Essay | Bloom's: Evaluate | Difficulty: Hard | Marks: 15

**Question:**  
Discuss the concept of Intrusion Detection Systems (IDS) in network endpoint security. In your answer, explain the definition of intrusion and intrusion detection, describe the two main approaches to intrusion detection (with their advantages and disadvantages), differentiate between Host-based and Network-based IDS, and evaluate the role of AI in improving intrusion detection.

**Guide answer:**  

**Introduction:**  
Intrusion Detection Systems are a critical component of network endpoint security. As firewalls alone cannot prevent all attacks — particularly those from authorized insiders or novel threats — IDS provides an essential layer of monitoring and alerting.

**Definitions:**
- **Intrusion:** Violations of security policy, characterized as attempts to affect the confidentiality, integrity, or availability of a computer or network. Violations can come from external attackers accessing systems from the Internet or from authorized users who overstep their authorization levels or conduct unauthorized activity.
- **Intrusion Detection:** The process of collecting information about events occurring in a computer system or network and analyzing them for signs of intrusions.
- **Intrusion Detection System:** Hardware or software products that gather and analyze information from various areas within a computer or network for the purpose of finding and providing real-time or near-real-time warning of unauthorized access attempts.

**Two Approaches to Intrusion Detection:**

1. **Misuse Detection (Signature-based):** Based on rules specifying system events, event sequences, or observable properties believed to indicate security incidents. Uses pattern-matching algorithms operating on large databases of known attack signatures.
   - *Advantage:* Accurate and generates few false alarms
   - *Disadvantage:* Cannot detect novel or unknown attacks

2. **Anomaly Detection (Behavior-based):** Searches for activity that differs from normal behavior of system entities and resources.
   - *Advantage:* Can detect previously unknown attacks based on behavioral deviation
   - *Disadvantage:* Significant trade-off between false positives and false negatives. A loose interpretation catches more intruders but also more legitimate users (false positives); a tight interpretation misses more intruders (false negatives)

**Behavioral Overlap:**
The typical behavior of an intruder differs from that of an authorized user, but there is an **overlap** between these behaviors. This overlap is the fundamental challenge in anomaly detection — it is impossible to draw a perfect boundary between legitimate and malicious behavior.

**Host-based IDS (HIDS):**
HIDS monitors the characteristics of a single host for suspicious activity. It adds specialized security software to vulnerable systems (database servers, administrative systems). HIDS uses both anomaly and misuse protection. For anomaly detection, two strategies are used:
- **Threshold detection:** Defines thresholds for the frequency of occurrence of various events, independent of user
- **Profile-based:** Develops a profile of each user's activity to detect behavioral changes

HIDS's primary benefit is detecting **both external and internal intrusions** — something NIDS and firewalls cannot achieve. It can determine exactly which processes and user accounts are involved in an attack and can see the intended outcome of attacks by directly monitoring targeted data files and processes.

**Network-based IDS (NIDS):**
NIDS monitors network traffic by examining packets as they pass sensor points. It uses three signature types:
- **String signatures:** Text strings indicating possible attacks
- **Port signatures:** Connection attempts to well-known, frequently attacked ports
- **Header condition signatures:** Dangerous or illogical combinations in packet headers

NIDS sensors are limited to seeing packets on their attached network segment. Deployment typically involves multiple sensors at strategic locations feeding a central NIDS manager. The four sensor locations are: outside the external firewall, in the DMZ, behind internal firewalls on backbone networks, and behind internal firewalls on user LANs.

**The Role of AI:**
The lecture explicitly states "Here is the role of AI" in the context of anomaly detection's false positive/false negative trade-off. AI and machine learning can significantly improve anomaly detection by:
- Learning more accurate behavioral baselines from large datasets
- Reducing false positive rates through intelligent pattern recognition
- Adapting to evolving normal behavior over time
- Making the "compromise and art" of anomaly detection more systematic and data-driven
- Better distinguishing the overlapping behavioral profiles of intruders and authorized users

**Conclusion:**  
IDS is essential for comprehensive network security, complementing firewalls with active monitoring and detection. The combination of misuse and anomaly detection, deployed across both hosts and network segments, provides the broadest coverage. AI represents the next frontier in making anomaly detection practical and accurate at scale.

**Key points to include:**
- Definitions of intrusion, intrusion detection, and IDS
- Both detection approaches with advantages and disadvantages
- Behavioral overlap between intruders and authorized users
- HIDS vs NIDS differences with specific strategies and signature types
- Four NIDS sensor locations
- AI's role in improving anomaly detection

**Common mistakes to avoid:**
- Confusing IDS with IPS — IDS detects and alerts; IPS additionally takes preventive action
- Ignoring the behavioral overlap concept, which is central to understanding anomaly detection limitations
- Not mentioning the four NIDS sensor locations
- Forgetting HIDS's unique advantage of detecting internal intrusions

---

### Q26 — Short Answer | Bloom's: Remember | Difficulty: Medium | Marks: 5

**Question:**  
Write the scientific term for each of the following:

**(a)** Applies rules to incoming/outgoing IP packets, forwarding or discarding them based on source/destination IP addresses, port numbers, and protocols.

**(b)** A type of firewall that acts as a relay of application-level traffic and does not permit end-to-end TCP connections.

**(c)** An IDS detection approach that uses pattern-matching algorithms operating on large databases of attack signatures.

**(d)** The IDS detection strategy that defines thresholds for the frequency of occurrence of various events, independent of user.

**(e)** A firewall that sets up two TCP connections and relays segments without examining the contents.

**Guide answer:**  
**(a)** Packet Filtering Firewall  
**(b)** Application-Level Proxy Firewall (Application Level Gateway)  
**(c)** Misuse Detection (Signature-based detection)  
**(d)** Threshold Detection  
**(e)** Circuit-Level Proxy Firewall (Circuit-Level Gateway)

**Key points to include:**
- Exact terms as used in the lecture material
- Alternative names are acceptable (e.g., "Gateway" and "Firewall")

**Common mistakes to avoid:**  
- Confusing Application-Level Proxy with Circuit-Level Proxy (key difference: application proxy inspects content; circuit-level does not)
- Writing "anomaly detection" for (c) — anomaly detection looks for deviations from normal behavior, while misuse detection matches known signatures
- Confusing threshold detection with profile-based detection — threshold is user-independent, profile-based tracks individual user behavior

---

### Q27 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 6

**Question:**  
An organization notices that its Host-based IDS is generating an unusually high number of false positives, flagging legitimate administrator activities as potential intrusions.

**(a)** Explain which detection approach (misuse or anomaly) is most likely causing this issue and why. (Marks: 3)

**(b)** Suggest how the IDS configuration could be adjusted to reduce false positives without significantly increasing false negatives. (Marks: 3)

**Guide answer:**  
**(a)** The issue is most likely caused by **anomaly detection** with a **loose interpretation** of intruder behavior. Anomaly detection works by comparing current activity against established baselines of normal behavior. If the anomaly detection thresholds are too sensitive (loose interpretation), legitimate but unusual administrator activities (such as bulk file operations, system configuration changes, or after-hours access) will be flagged as deviations from normal behavior, generating false positives.

Misuse detection is unlikely to cause this issue because it matches against specific known attack signatures — legitimate administrator activities would not match attack patterns.

**(b)** Two configuration adjustments can help:
1. **Switch from threshold detection to profile-based detection** for administrator accounts. Profile-based detection builds individual activity profiles per user. Since administrator accounts have legitimately different usage patterns (more system access, configuration changes), a profile tailored to each administrator would better distinguish their normal activities from genuine intrusions.
2. **Tighten the interpretation of intruder behavior** — but with caution. The lecture warns that tightening the interpretation reduces false positives but increases false negatives (intruders not identified). The optimal approach is to find a balance — the lecture describes this as "a compromise and art in the practice of anomaly detection."

**Key points to include:**
- Anomaly detection with loose interpretation causes false positives
- Profile-based detection can reduce false positives by learning individual user patterns
- Trade-off between false positives and false negatives
- The "compromise and art" nature of anomaly detection

**Common mistakes to avoid:**  
Suggesting to simply disable anomaly detection — this would eliminate false positives but also remove the ability to detect novel attacks. The goal is to tune the system, not disable it.

---

### Q28 — Compare & Contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 6

**Question:**  
Compare and contrast the roles of the **external firewall** and **internal firewall** in a DMZ network architecture, in terms of placement, filtering stringency, and what each protects.

**Guide answer:**  

| Aspect | External Firewall | Internal Firewall |
|--------|------------------|-------------------|
| **Placement** | At the edge of the enterprise network, just inside the boundary router connecting to the Internet/WAN | Between the DMZ and the bulk of the enterprise network |
| **Filtering stringency** | Provides a measure of access control and **basic level** of protection | Adds **more stringent filtering** compared to the external firewall |
| **What it protects** | DMZ systems (consistent with their need for external connectivity) and provides basic protection for the rest of the network | Enterprise servers, workstations, and the internal network from external attacks that penetrate the DMZ |
| **Direction of protection** | Primarily protects inward (from Internet to DMZ/internal network) | Provides **two-way protection** — protects internal network from compromised DMZ systems AND protects DMZ from internal attacks |
| **Additional capability** | First line of defense against Internet-based threats | Can protect portions of the internal network from each other (e.g., servers from workstations) |

Both firewalls work together in a defense-in-depth strategy. The external firewall handles the initial filtering for the publicly accessible DMZ, while the internal firewall provides the critical, more stringent defense for the enterprise's most sensitive assets.

**Key points to include:**
- External = edge placement, basic filtering; Internal = deeper placement, stringent filtering
- Internal firewall provides two-way protection
- Internal firewall can segment internal network portions
- Both work together in defense-in-depth

**Common mistakes to avoid:**  
Stating that the external firewall provides stronger filtering than the internal firewall. The opposite is true — the internal firewall has more stringent filtering because it protects the most sensitive assets. The external firewall is less restrictive because DMZ systems need external connectivity.

---

### Q29 — True/False + Justify | Bloom's: Analyse | Difficulty: Hard | Marks: 3

**Question:**  
"An NIDS sensor deployed at a single location can monitor all traffic across the entire enterprise network."

**Guide answer:**  
**False.** An NIDS sensor can **only see the packets that happen to be carried on the network segment to which it is attached**. It cannot see traffic on other segments. This is why NIDS deployment typically involves **multiple sensors distributed at key network points** to gather traffic data, with all sensors feeding information on potential threats to a **central NIDS manager**. The lecture identifies four strategic sensor locations (outside the external firewall, in the DMZ, behind internal firewalls on backbone networks, and behind internal firewalls on user LANs) precisely because no single sensor can provide full coverage.

**Key points to include:**
- NIDS sensors are limited to their attached network segment
- Multiple sensors at key locations are required for comprehensive coverage
- Sensors feed into a central NIDS manager
- Four specific sensor locations exist for a reason

**Common mistakes to avoid:**  
Assuming that NIDS monitors the entire network from one point. This fundamental limitation is why strategic placement of multiple sensors is critical. Students should reference the four location types to demonstrate understanding.

---

### Q30 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**  
The three types of signatures used by Network-based IDS to identify suspicious packets are __________ signatures, __________ signatures, and __________ signatures.

**Guide answer:**  
String signatures, Port signatures, and Header condition signatures

**Key points to include:**
- String signatures look for text strings indicating possible attacks
- Port signatures watch for connection attempts to well-known, frequently attacked ports
- Header signatures watch for dangerous or illogical combinations in packet headers

**Common mistakes to avoid:**  
Confusing NIDS signature types with HIDS detection strategies (threshold and profile-based). These are different detection mechanisms used by different types of IDS.

---

## Section 4 — Study Tips

1. **Firewall types and their operating layers:** Understand the four firewall types (Packet Filtering, Stateful Inspection, Application-Level Proxy, Circuit-Level Proxy) and what distinguishes each — especially the difference between Application-Level and Circuit-Level Proxies, as this is a common confusion point. The 2025 exam already tested Packet Filtering Firewall knowledge (Q iv on page 2), confirming this is an exam-priority topic.

2. **IDS detection approaches — the false positive/false negative trade-off:** The overlap between intruder and authorized user behavior profiles is a critical conceptual point. Be able to explain why tightening anomaly detection reduces false positives but increases false negatives, and vice versa. The lecture explicitly mentions AI as relevant here — understand why.

3. **DMZ architecture and two-way firewall protection:** This is a common scenario-based question target. Know the placement of external and internal firewalls, what goes in the DMZ, and the two-way protection role of the internal firewall (protecting internal network from compromised DMZ systems, and protecting DMZ from internal attacks). The specific threats mentioned — worms, rootkits, bots — should be memorized.

---

## Section 5 — Coverage Gap Analysis

| Concept | Why It May Be Worth Testing | Suggested Question Type |
|---------|---------------------------|------------------------|
| **IPS vs IDS distinction** | The lecture mentions IPS alongside IDS but does not detail it. Past exams tested the difference (option a in Q v, 2025 exam: "Takes action to block or mitigate attacks"). | True/False + Justify or MCQ |
| **Device Security (routers, switches, end systems)** | Mentioned at the start of the lecture as a Network Security Component but not elaborated. May appear as a "write the scientific term" question. | Fill-in-the-blank |
| **Packet Filtering rule processing order** | The lecture describes how rules are processed (match → invoke rule; no match → default action) but this procedural detail is easily overlooked. | Application (write firewall rules) |
| **NIDS central manager architecture** | Sensors feeding data to a central manager is mentioned but not deeply explored. Could be tested as part of a diagram question. | Short Answer or Application |

*Note: All major concepts from the lecture have been covered by the question bank above. The gaps listed are minor details that could appear in more targeted questions.*
