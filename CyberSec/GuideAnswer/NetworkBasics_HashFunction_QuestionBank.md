# Cybersecurity Fundamentals — Question Bank
**Course:** CCY2001: Introduction to Cybersecurity  
**Topics Covered:** Network Security Basics (Topic 6) · Cryptographic Hash Functions (Topic 4 – Part 4)  
**Total Questions:** 30  
**Difficulty Distribution:** ~30% Easy · ~40% Medium · ~30% Hard

---

## Section 1 — Topic Summary

- **Network security operates at multiple TCP/IP layers:** IPsec secures the network layer, TLS/SSL secures the transport layer, and application-specific protocols (S/MIME, Kerberos) secure individual applications.
- **TLS architecture** consists of the Record Protocol (providing confidentiality and message integrity) and four upper-layer protocols: Handshake, Change Cipher Spec, Alert, and Heartbeat.
- **HTTPS** provides encryption, data integrity, and authentication for web communications using TLS over HTTP.
- **Wireless networks** face unique threats including accidental/malicious association, MAC spoofing, man-in-the-middle attacks, DoS, and network injection — addressed by IEEE 802.11i security.
- **IPsec** provides access control, connectionless integrity, data origin authentication, replay rejection, and confidentiality via two protocols (AH and ESP) operating in Transport or Tunnel mode.
- **Cryptographic hash functions** accept variable-length input and produce fixed-size output with one-way and collision-free properties, forming the basis for message authentication, MAC, and digital signatures.
- **SHA evolution** progressed from SHA-1 (160-bit, now considered insecure) to SHA-2 (256/384/512-bit) and SHA-3 (competition winner in 2012, intended to complement SHA-2).

---

## Section 2 — Tone Analysis

The past exams use a **formal academic tone** with precise technical vocabulary. Questions favour directive verbs such as *"describe,"* *"explain,"* *"choose,"* *"write the scientific term,"* and *"sketch the block diagram."* MCQ items follow a consistent pattern: a stem with four choices (i–iv or a–d), one correct answer, and distractors that reference real but incorrect concepts. Multi-part questions escalate from recall to application (e.g., Q1 2023: encrypt → apply substitution → show steps). Mark allocations range from 2 pts (scientific term / MCQ sets) to 12–14 pts (complex application problems).

---

## Section 3 — Question Bank

---

### Multiple Choice (MCQ)

---

### Q1 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**  
One of the following protocols operates at the network layer to provide security services:  
a. TLS  
b. S/MIME  
c. IPsec  
d. Kerberos

**Guide answer:**  
**c. IPsec**

**Key points to include:**
- IPsec provides security at the IP (network) layer
- TLS operates above TCP (transport layer)
- S/MIME and Kerberos are application-layer security mechanisms

**Common mistakes to avoid:**  
Students often confuse TLS with IPsec because both provide encryption. The distinction is the layer at which they operate — TLS sits above TCP while IPsec sits at the IP layer.

---

### Q2 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**  
The TLS Record Protocol provides two services for TLS connections. These services are:  
a. Authentication and Non-repudiation  
b. Confidentiality and Message Integrity  
c. Access Control and Data Origin Authentication  
d. Key Exchange and Digital Signature

**Guide answer:**  
**b. Confidentiality and Message Integrity**

**Key points to include:**
- Confidentiality is achieved through a shared secret key defined by the Handshake Protocol for symmetric encryption
- Message Integrity is achieved through a MAC using a shared secret key also defined by the Handshake Protocol

**Common mistakes to avoid:**  
Students sometimes select "Authentication" because TLS does involve authentication — but it is the Handshake Protocol (not the Record Protocol) that handles authentication.

---

### Q3 — MCQ | Bloom's: Understand | Difficulty: Easy | Marks: 2

**Question:**  
HTTPS provides three important areas of protection. Which of the following is NOT one of them?  
a. Encryption  
b. Data integrity  
c. Non-repudiation  
d. Authentication

**Guide answer:**  
**c. Non-repudiation**

**Key points to include:**
- HTTPS provides encryption, data integrity, and authentication
- Non-repudiation is a separate security service typically associated with digital signatures, not HTTPS

**Common mistakes to avoid:**  
Confusing authentication with non-repudiation. HTTPS authenticates that you are communicating with the intended website, but it does not provide proof that a specific party sent a message (non-repudiation).

---

### Q4 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**  
Which wireless network threat occurs when a wireless device is configured to appear as a legitimate access point to steal passwords from legitimate users?  
a. Accidental association  
b. Malicious association  
c. Ad hoc networks  
d. Network injection

**Guide answer:**  
**b. Malicious association**

**Key points to include:**
- Malicious association involves a rogue device impersonating a legitimate access point
- Accidental association is unintentional connection to a neighbouring network
- Network injection targets exposed routing/management protocols

**Common mistakes to avoid:**  
Confusing malicious association with man-in-the-middle. While malicious association can lead to MITM attacks, the specific term for a fake access point designed to steal credentials is malicious association.

---

### Q5 — MCQ | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**  
The Secure Hash Algorithm (SHA) depends on the concept of:  
a. Cipher Block Chain  
b. Symmetric Block Cipher  
c. Asymmetric Encryption  
d. Message Authentication Code

**Guide answer:**  
**a. Cipher Block Chain**

**Key points to include:**
- SHA uses a structure similar to CBC — it processes message blocks sequentially using an initial value CV₀
- Each iteration computes CVᵢ = E(Yᵢ₋₁, CVᵢ₋₁), resembling CBC but without a key
- The final block CVL is used as the hash value

**Common mistakes to avoid:**  
Students may select MAC because hash functions are used in MACs, but the question asks about the internal structure concept of SHA, which is based on a cipher block chaining approach.

---

### Q6 — MCQ | Bloom's: Understand | Difficulty: Hard | Marks: 2

**Question:**  
In IPsec, which mode encrypts the entire IP packet and adds a new header for the next hop, making it suitable for VPN gateway-to-gateway security?  
a. Transport Mode with AH  
b. Transport Mode with ESP  
c. Tunnel Mode  
d. Handshake Mode

**Guide answer:**  
**c. Tunnel Mode**

**Key points to include:**
- Tunnel Mode encrypts the entire original IP packet and wraps it in a new IP header
- Routers along the path cannot examine the inner IP header
- Transport Mode only encrypts the IP payload (data), not the header
- Tunnel Mode is preferred for VPN and gateway-to-gateway communication

**Common mistakes to avoid:**  
Students confuse Transport Mode and Tunnel Mode. The key distinction: Transport Mode encrypts data only (host-to-host), Tunnel Mode encrypts the entire packet (gateway-to-gateway / VPN).

---

### Fill-in-the-Blank

---

### Q7 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**  
A hash function H accepts a variable-length block of data M as input and produces a fixed-size hash value h, expressed as h = __________.

**Guide answer:**  
H(M)

**Key points to include:**
- The notation h = H(M) is the standard representation of a hash function operation

**Common mistakes to avoid:**  
Writing E(M) or D(M), which represent encryption and decryption functions respectively, not hash functions.

---

### Q8 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**  
When a hash function is used to provide message authentication, the hash function value is often referred to as a __________.

**Guide answer:**  
Message Digest

**Key points to include:**
- The term "Message Digest" specifically refers to the hash value when used in the context of message authentication

**Common mistakes to avoid:**  
Students often write "MAC" (Message Authentication Code), but MAC is a specific mechanism involving a secret key. The generic term for a hash value used for message authentication is Message Digest.

---

### Q9 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Easy | Marks: 2

**Question:**  
__________ is a protocol for secure network communications designed to be relatively simple and inexpensive to implement, originally focused on providing a secure remote logon facility to replace TELNET.

**Guide answer:**  
Secure Shell (SSH)

**Key points to include:**
- SSH replaced TELNET and other insecure remote logon schemes
- SSH has become the method of choice for remote login and X tunneling

**Common mistakes to avoid:**  
Writing "SSL" or "TLS" instead of SSH. SSL/TLS secure web communications, while SSH specifically targets remote logon and command-line access.

---

### Q10 — Fill-in-the-blank | Bloom's: Remember | Difficulty: Medium | Marks: 2

**Question:**  
A cryptographic hash function has two essential properties: the __________ property (computationally infeasible to find data that maps to a pre-specified hash result) and the __________ property (computationally infeasible to find two data objects that map to the same hash result).

**Guide answer:**  
one-way ; collision-free (collision resistance)

**Key points to include:**
- One-way property = pre-image resistance
- Collision-free property = collision resistance
- Both properties are essential for a cryptographic hash function

**Common mistakes to avoid:**  
Students may reverse the two properties or use vague terms like "irreversible" instead of the precise term "one-way."

---

### Short Answer

---

### Q11 — Short Answer | Bloom's: Understand | Difficulty: Easy | Marks: 4

**Question:**  
Describe the four higher-layer protocols defined as part of the TLS architecture and state the main purpose of the TLS Record Protocol.

**Guide answer:**  
The four higher-layer protocols in TLS are: (1) the **Handshake Protocol**, which negotiates security parameters and establishes the shared secret keys; (2) the **Change Cipher Spec Protocol**, which signals transitions in ciphering strategies; (3) the **Alert Protocol**, which conveys TLS-related alerts such as errors or warnings; and (4) the **Heartbeat Protocol**, which keeps the connection alive. The **TLS Record Protocol** provides two core services — **confidentiality** (via symmetric encryption using keys established by the Handshake Protocol) and **message integrity** (via a MAC using a shared secret key).

**Key points to include:**
- All four protocols named correctly: Handshake, Change Cipher Spec, Alert, Heartbeat
- Record Protocol provides confidentiality and message integrity
- Handshake Protocol defines the shared secret keys used by the Record Protocol

**Common mistakes to avoid:**  
Omitting the Heartbeat Protocol (students often only recall three of the four). Also, confusing the Record Protocol with the Handshake Protocol — the Record Protocol handles data protection, while the Handshake Protocol handles key negotiation.

---

### Q12 — Short Answer | Bloom's: Remember | Difficulty: Easy | Marks: 4

**Question:**  
List the security services provided by IPsec.

**Guide answer:**  
IPsec provides the following security services: (1) **Access control** — restricting who can access network resources; (2) **Connectionless integrity** — ensuring data has not been altered in transit; (3) **Data origin authentication** — verifying the source of the data; (4) **Rejection of replayed packets** — preventing replay attacks by detecting duplicate packets; and (5) **Confidentiality (encryption)** — protecting data content from eavesdropping.

**Key points to include:**
- All five services: access control, connectionless integrity, data origin authentication, rejection of replayed packets, confidentiality
- These services are provided through two protocols: AH and ESP

**Common mistakes to avoid:**  
Listing "non-repudiation" as an IPsec service — IPsec does not provide non-repudiation. Also, forgetting "rejection of replayed packets," which is a distinct service from integrity.

---

### True / False + Justify

---

### Q13 — True/False + Justify | Bloom's: Understand | Difficulty: Easy | Marks: 3

**Question:**  
"IPsec Transport Mode encrypts the entire IP packet including the IP header, making it suitable for VPN gateway-to-gateway security."

**Guide answer:**  
**False.** Transport Mode encrypts only the IP payload (data) and optionally authenticates it, but does **not** encrypt the IP header. It is suitable for host-to-host traffic (e.g., ESP between two endpoints). The description given — encrypting the entire IP packet and adding a new header for next-hop routing — applies to **Tunnel Mode**, which is the mode suitable for VPN gateway-to-gateway security.

**Key points to include:**
- Transport Mode encrypts data only, not the IP header
- Tunnel Mode encrypts the entire original IP packet
- Tunnel Mode is used for VPNs and gateway-to-gateway communication

**Common mistakes to avoid:**  
Simply stating "False" without explaining which mode actually encrypts the full packet. Full marks require naming Tunnel Mode as the correct alternative and explaining the difference.

---

### Q14 — True/False + Justify | Bloom's: Analyse | Difficulty: Medium | Marks: 3

**Question:**  
"SHA-1 has been broken in practice, which is why NIST developed SHA-2 and began the process to complement it with SHA-3 for certain applications."

**Guide answer:**  
**False (partially).** SHA-1 has **not** been fully "broken" in the traditional sense — no one has demonstrated a practical technique for producing arbitrary collisions in a practical amount of time at the time of the lecture. However, SHA-1 is **considered insecure** and has been phased out in favour of SHA-2. NIST announced SHA-3 in 2007 not because SHA-2 was broken, but because SHA-2 shares the same mathematical structure as its predecessors, and NIST wanted a fundamentally different backup standard in case SHA-2 becomes vulnerable in the future.

**Key points to include:**
- SHA-1 is considered insecure but was not "broken" in a fully practical sense
- SHA-2 is the current standard
- SHA-3 was designed as a complement (not replacement) for SHA-2, using a different internal structure

**Common mistakes to avoid:**  
Students often accept the statement as fully true. The nuance is that SHA-1 was phased out proactively, and SHA-3 complements (not replaces) SHA-2. The motivation for SHA-3 was structural diversity, not a direct vulnerability in SHA-2.

---

### Q15 — True/False + Justify | Bloom's: Understand | Difficulty: Medium | Marks: 3

**Question:**  
"A Message Authentication Code (MAC) and a Digital Signature both use a hash function, so they are fundamentally the same mechanism."

**Guide answer:**  
**False.** While both MAC and digital signatures use hash functions, they differ fundamentally. A **MAC** uses a **secret key** shared between two parties — the hash is computed over the message concatenated with the secret key, providing data origin authentication and integrity. A **Digital Signature** uses **asymmetric cryptography** — the hash of the message is encrypted with the sender's **private key**, and anyone with the sender's **public key** can verify it. Digital signatures additionally provide **non-repudiation**, which MAC cannot provide since both parties share the same key.

**Key points to include:**
- MAC uses a shared secret key (symmetric)
- Digital signature uses private key for signing and public key for verification (asymmetric)
- Digital signatures provide non-repudiation; MAC does not

**Common mistakes to avoid:**  
Stating they are the same because both involve hashing. The key difference lies in symmetric vs asymmetric key usage and the property of non-repudiation.

---

### Q16 — True/False + Justify | Bloom's: Understand | Difficulty: Easy | Marks: 3

**Question:**  
"SSH was originally developed to provide secure web browsing as a replacement for HTTP."

**Guide answer:**  
**False.** SSH (Secure Shell) was developed to provide a **secure remote logon facility** to replace **TELNET** and other insecure remote logon schemes — not web browsing. Secure web browsing is provided by **HTTPS** (HTTP over TLS/SSL). SSH is primarily used for remote command-line access, file transfers, and tunnelling.

**Key points to include:**
- SSH replaces TELNET for secure remote login
- HTTPS (not SSH) secures web browsing
- SSH is used for remote login, X tunnelling, and encrypted command-line sessions

**Common mistakes to avoid:**  
Confusing SSH with HTTPS/SSL. Both provide encryption, but for entirely different use cases.

---

### Application (Scenario-Based)

---

### Q17 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 6

**Question:**  
A company's internal web application currently uses plain HTTP for communication between employees' browsers and the internal server. The IT security team reports that sensitive employee data (login credentials, personal information) is being transmitted in plaintext.

**(a)** Explain what security risks this creates. (Marks: 2)

**(b)** Recommend a protocol-level solution and describe the three areas of protection it provides. (Marks: 4)

**Guide answer:**  
**(a)** Using plain HTTP means all data between the browser and server is transmitted in cleartext. This exposes the company to **eavesdropping** (attackers on the network can read credentials and personal data), **data tampering** (attackers can modify data in transit without detection), and **man-in-the-middle attacks** (attackers can impersonate the server).

**(b)** The company should implement **HTTPS** (HTTP over TLS). HTTPS provides three areas of protection:
1. **Encryption** — encrypts all exchanged data (URLs, document contents, form data, cookies, HTTP headers) to prevent eavesdropping
2. **Data integrity** — ensures data cannot be modified or corrupted during transfer without being detected
3. **Authentication** — proves that users are communicating with the intended server, protecting against man-in-the-middle attacks

**Key points to include:**
- Identification of plaintext risks: eavesdropping, tampering, impersonation
- HTTPS as the solution (not just "SSL" or "encryption")
- All three protection areas named and briefly explained

**Common mistakes to avoid:**  
Suggesting "use a VPN" or "use IPsec" without addressing the application-layer requirement. The question specifically targets browser-to-server communication, which is best solved by HTTPS at the transport layer.

---

### Q18 — Application | Bloom's: Apply | Difficulty: Hard | Marks: 8

**Question:**  
An organisation wants to connect two branch offices securely over the public Internet. All traffic between the two offices must be fully encrypted, and intermediate routers should not be able to inspect the content or the original IP headers of the packets.

**(a)** Identify the appropriate IPsec mode for this requirement and explain why it is suitable. (Marks: 3)

**(b)** Name the two protocols used by IPsec and explain which one would best fulfil the confidentiality requirement. (Marks: 3)

**(c)** Explain why Transport Mode would NOT be appropriate for this scenario. (Marks: 2)

**Guide answer:**  
**(a)** **Tunnel Mode** is the appropriate IPsec mode. In Tunnel Mode, the **entire original IP packet** (including the IP header) is encrypted and encapsulated within a new IP packet with a new header for the next hop. This means intermediate routers can only see the outer header and cannot inspect the original source/destination addresses or the payload. This makes it ideal for **VPN gateway-to-gateway security** between two branch offices.

**(b)** The two IPsec protocols are:
1. **Authentication Header (AH)** — provides connectionless integrity, data origin authentication, and replay protection, but does **not** provide encryption
2. **Encapsulating Security Payload (ESP)** — provides all services of AH **plus confidentiality (encryption)**

ESP is the protocol that fulfils the confidentiality requirement since AH does not encrypt data.

**(c)** Transport Mode would NOT be appropriate because it only encrypts the **IP payload** (data portion) while leaving the original IP header exposed. Intermediate routers could still see the original source and destination IP addresses. Additionally, Transport Mode is designed for **host-to-host** communication (e.g., between two endpoints), not for **gateway-to-gateway** scenarios where all traffic between two entire networks must be secured.

**Key points to include:**
- Tunnel Mode encrypts the entire packet; Transport Mode encrypts only the payload
- ESP provides confidentiality; AH does not
- Tunnel Mode is for gateway-to-gateway / VPN; Transport Mode is for host-to-host

**Common mistakes to avoid:**  
Saying AH can provide confidentiality (it cannot). Also, not explaining *why* Transport Mode fails — simply saying "it's not suitable" without explaining that the IP header remains visible is insufficient for full marks.

---

### Q19 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 6

**Question:**  
Alice wants to send a message to Bob and ensure that Bob can verify the message has not been tampered with and that it genuinely originated from Alice. They share a secret value S. Alice does not require confidentiality — the message can be readable by anyone.

**(a)** Describe the message authentication method Alice should use, including the steps performed by both Alice and Bob. (Marks: 4)

**(b)** Explain why an attacker who intercepts the message cannot forge a valid replacement. (Marks: 2)

**Guide answer:**  
**(a)** Alice should use a hash-based message authentication approach with a shared secret:
1. Alice computes a hash value over the **concatenation of the message M and the secret value S**: h = H(M || S)
2. Alice sends both the message M and the hash value h to Bob
3. Bob, who also possesses S, recomputes the hash: h' = H(M || S)
4. Bob compares h' with the received h — if they match, the message is authentic and unaltered

**(b)** An attacker who intercepts the message **does not know the secret value S**. Without S, the attacker cannot compute a valid hash for a modified message. Even if the attacker changes the message, they cannot generate the correct hash value that Bob will compute using S, so any tampering will be detected.

**Key points to include:**
- Hash computed over M concatenated with S
- Both sender and receiver must possess S
- Comparison of computed hash with received hash
- Attacker cannot forge because S is unknown to them

**Common mistakes to avoid:**  
Confusing this method with digital signatures. This is a symmetric (shared-secret) approach — it does not involve public/private keys. Also, students sometimes describe encrypting the entire message, but the question explicitly states confidentiality is not required.

---

### Q20 — Application | Bloom's: Analyse | Difficulty: Hard | Marks: 8

**Question:**  
A university campus has a large wireless network with multiple access points across different buildings. The IT department has received reports of the following incidents:
- Students in Building A are unknowingly connecting to a nearby office's Wi-Fi network
- A rogue device in the library is advertising itself as "CampusWiFi" and capturing login credentials
- The campus WLAN has been experiencing severe performance degradation due to floods of protocol messages targeting the access points

**(a)** Identify the specific wireless network threat for each of the three incidents. (Marks: 3)

**(b)** For the rogue device threat, explain the attack mechanism and suggest one countermeasure. (Marks: 3)

**(c)** Name the IEEE standard that addresses WLAN security and briefly describe its purpose. (Marks: 2)

**Guide answer:**  
**(a)**
1. Building A incident → **Accidental association** — overlapping transmission ranges cause students to unintentionally connect to a neighbouring network
2. Library rogue device → **Malicious association** — a wireless device is configured to appear as a legitimate access point to steal passwords
3. Performance degradation → **Denial of Service (DoS)** — an attacker bombards wireless access points with protocol messages designed to consume system resources

**(b)** In a malicious association attack, the attacker sets up a wireless device configured to broadcast the same SSID as the legitimate campus network (e.g., "CampusWiFi"). When users connect, all their traffic — including login credentials — passes through the attacker's device. **Countermeasure:** Implement **IEEE 802.11i security** with mutual authentication (e.g., WPA2-Enterprise with 802.1X), which requires the access point to authenticate itself to the client as well, preventing connections to rogue APs. Additionally, deploying **Wireless Intrusion Detection Systems (WIDS)** can detect and alert on rogue access points.

**(c)** **IEEE 802.11i** is the standard that addresses WLAN security. It defines security enhancements for IEEE 802.11 wireless networks, including robust authentication mechanisms, key management, and encryption protocols to protect wireless communications from eavesdropping, unauthorised access, and data tampering.

**Key points to include:**
- Correct identification of all three threats
- Mechanism of malicious association clearly explained
- A concrete, specific countermeasure (not just "improve security")
- IEEE 802.11i named as the WLAN security standard

**Common mistakes to avoid:**  
Labelling the rogue device as a "man-in-the-middle attack" — while MITM may result from it, the specific threat category is malicious association. Also, suggesting "change the Wi-Fi password" as a countermeasure, which does not address rogue AP detection.

---

### Compare & Contrast

---

### Q21 — Compare & Contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 6

**Question:**  
Compare and contrast **IPsec Transport Mode** and **IPsec Tunnel Mode** in terms of what is encrypted, use cases, and suitability for different network architectures.

**Guide answer:**  

| Aspect | Transport Mode | Tunnel Mode |
|---|---|---|
| **What is encrypted** | Only the IP payload (data) is encrypted; the original IP header remains visible | The entire original IP packet (header + data) is encrypted and encapsulated in a new IP packet |
| **Header visibility** | Intermediate routers can see source and destination IP addresses | Intermediate routers can only see the outer header; original IP addresses are hidden |
| **Traffic analysis** | Susceptible to traffic analysis (endpoints are visible) | Resistant to traffic analysis (original endpoints are hidden) |
| **Primary use case** | Host-to-host communication (e.g., ESP between two endpoints) | Gateway-to-gateway security (e.g., VPN between two networks) |
| **Overhead** | Lower overhead (no additional IP header) | Higher overhead (adds a new IP header) |

Both modes can use either AH or ESP as the security protocol, and both provide authentication and integrity services. The fundamental distinction is the scope of protection: Transport Mode protects only the data payload, while Tunnel Mode protects the entire original packet.

**Key points to include:**
- Transport Mode: data only, host-to-host, allows traffic analysis
- Tunnel Mode: entire packet, gateway-to-gateway, hides original headers
- Both use AH or ESP

**Common mistakes to avoid:**  
Stating that Transport Mode provides no security — it does provide encryption of the payload and optional authentication, just not full packet encryption. Also, forgetting to mention the traffic analysis vulnerability of Transport Mode.

---

### Q22 — Compare & Contrast | Bloom's: Analyse | Difficulty: Hard | Marks: 6

**Question:**  
Compare and contrast **Message Authentication Code (MAC)** and **Digital Signature** as message authentication mechanisms, in terms of key usage, security services provided, and verification process.

**Guide answer:**  

| Aspect | Message Authentication Code (MAC) | Digital Signature |
|---|---|---|
| **Key type** | Uses a **shared secret key** (symmetric) between sender and receiver | Uses the sender's **private key** for signing and the sender's **public key** for verification (asymmetric) |
| **How it works** | Takes a secret key and data block as input, produces a hash value (MAC) associated with the message | The hash value of the message is encrypted with the sender's private key |
| **Who can verify** | Only parties who possess the shared secret key | **Anyone** who knows the sender's public key |
| **Non-repudiation** | **Not provided** — since both parties share the same key, either party could have generated the MAC | **Provided** — only the sender possesses the private key, so only they could have produced the signature |
| **Security services** | Data origin authentication + integrity | Data origin authentication + integrity + **non-repudiation** |
| **Performance** | Generally faster (symmetric operations) | Generally slower (asymmetric operations) |

Both mechanisms use hash functions and aim to verify that a message has not been altered and that it originates from the expected source. The key difference is that digital signatures provide non-repudiation through asymmetric cryptography, while MAC relies on a shared secret.

**Key points to include:**
- MAC = symmetric (shared key), Digital Signature = asymmetric (private/public key)
- Digital Signature provides non-repudiation; MAC does not
- Both provide integrity and authentication

**Common mistakes to avoid:**  
Claiming that MAC provides non-repudiation. Since both parties share the key, either could have produced the MAC, so the sender can deny having sent the message.

---

### Q23 — Compare & Contrast | Bloom's: Analyse | Difficulty: Medium | Marks: 6

**Question:**  
Compare and contrast **TLS (Transport Layer Security)** and **IPsec** in terms of the protocol layer at which they operate, transparency to applications, and typical use cases.

**Guide answer:**  

| Aspect | TLS | IPsec |
|---|---|---|
| **Protocol layer** | Operates just above TCP (between transport and application layers) | Operates at the IP layer (network layer) |
| **Transparency** | Can be transparent to applications (as part of the protocol suite) or embedded in specific applications (e.g., browsers with HTTPS) | Transparent to end users and applications — security is applied at the network level without application modification |
| **Scope** | Secures individual application connections (e.g., HTTPS for web, each application must implement or invoke TLS) | Secures all IP traffic between endpoints — provides a general-purpose solution for all applications |
| **Filtering** | Does not include packet-level filtering | Includes a filtering capability so that only selected traffic incurs IPsec processing overhead |
| **Typical use cases** | HTTPS web browsing, secure email, application-level secure channels | VPNs, gateway-to-gateway security, network-wide encryption |

Both TLS and IPsec provide confidentiality, integrity, and authentication. The primary difference is the level at which they operate: TLS secures specific connections at the transport/application boundary, while IPsec secures all traffic at the network layer.

**Key points to include:**
- TLS = above TCP, IPsec = at IP layer
- IPsec is transparent to applications; TLS may require application-level integration
- IPsec has filtering capability; TLS does not

**Common mistakes to avoid:**  
Stating that only one of them provides encryption — both do. The distinction is about the layer, scope, and transparency, not about the security services themselves.

---

### Essay / Long Answer

---

### Q24 — Essay | Bloom's: Evaluate | Difficulty: Hard | Marks: 12

**Question:**  
Discuss the evolution of the Secure Hash Algorithm (SHA) from SHA-1 through SHA-2 to SHA-3. In your answer, explain the security concerns that motivated each transition, describe how the internal structure of SHA relates to cipher block chaining, and evaluate NIST's decision to develop SHA-3 as a complement to (rather than a replacement for) SHA-2.

**Guide answer:**  

**Introduction:**  
The Secure Hash Algorithm family represents a critical component of modern cryptographic security. Its evolution reflects the ongoing challenge of maintaining cryptographic resilience against advancing computational capabilities and analytical techniques.

**SHA-1:**  
SHA was originally designed by NIST and published as a federal information processing standard in 1993, with a revised version (SHA-1) published in 1995. SHA-1 produces a 160-bit hash value. While SHA-1 has not been fully "broken" — no one has demonstrated a technique for producing arbitrary collisions in a fully practical timeframe — it has been **considered insecure** and has been phased out in favour of SHA-2. Theoretical weaknesses were identified that reduced the collision resistance below the expected 2⁸⁰ level.

**Internal structure and CBC relationship:**  
The general structure of secure hash code can use block ciphers as hash functions. Using an initial value CV₀, the computation proceeds as CVᵢ = E(Yᵢ₋₁, CVᵢ₋₁), with the final block CVL serving as the hash value. This structure is **similar to Cipher Block Chaining (CBC) but without a key**. In SHA-512, this manifests as processing 1024-bit message blocks through 80 rounds, where every bit of the hash code is a function of every bit of the input — ensuring that even a single-bit change in the input propagates to affect the entire hash output.

**SHA-2:**  
In 2002, NIST produced a revised standard defining three new versions: SHA-256, SHA-384, and SHA-512, collectively known as SHA-2. These versions offer significantly longer hash values (256, 384, and 512 bits), dramatically increasing collision resistance. However, SHA-2 shares the **same mathematical structure and operations** as its predecessors (SHA-1), which raised concerns about potential systemic vulnerabilities.

**SHA-3 and NIST's decision:**  
Recognising that it would take years to develop and deploy a replacement should SHA-2 become vulnerable, NIST proactively announced a public competition in 2007 for SHA-3. The winning design (Keccak) was announced in October 2012. Crucially, SHA-3 was designed to **complement** SHA-2, not replace it. This decision is sound because:
1. SHA-2 remains secure with no practical attacks demonstrated
2. SHA-3 uses a fundamentally **different internal structure**, providing algorithmic diversity
3. If a structural weakness is found in SHA-2's CBC-like architecture, SHA-3 offers an immediate fallback that would not share the same vulnerability

**Conclusion:**  
The SHA evolution demonstrates proactive cryptographic governance — addressing potential future threats before they materialise. NIST's complementary approach ensures that the cryptographic community has a diverse set of tools available, reducing the systemic risk of relying on a single algorithmic family.

**Key points to include:**
- SHA-1: 160-bit, phased out (not fully "broken" but considered insecure)
- SHA-2: 256/384/512-bit, same mathematical structure as SHA-1
- SHA-3: competition-based, different internal structure, complements SHA-2
- CBC-like structure of hash functions (CVᵢ = E(Yᵢ₋₁, CVᵢ₋₁))
- Rationale for complement vs replacement approach
- SHA-512: every bit of hash is function of every bit of input

**Common mistakes to avoid:**  
- Stating SHA-1 was "broken" without nuance — it was phased out proactively
- Claiming SHA-3 replaces SHA-2 — it complements it
- Not explaining the structural concern (SHA-2 shares SHA-1's structure)
- Ignoring the CBC connection in hash function design

---

### Q25 — Essay | Bloom's: Evaluate | Difficulty: Hard | Marks: 12

**Question:**  
Discuss the security facilities available at different layers of the TCP/IP protocol stack. In your answer, explain the advantages and limitations of implementing security at the network layer (IPsec), transport layer (TLS), and application layer (S/MIME, Kerberos). Evaluate which approach provides the best balance of security coverage and flexibility, and justify your answer.

**Guide answer:**  

**Introduction:**  
Security in the TCP/IP model can be implemented at multiple layers, each with distinct advantages and trade-offs. Understanding where to place security mechanisms is critical for designing robust network architectures.

**Network Layer — IPsec:**  
IPsec provides security at the IP layer. Its primary advantage is **transparency** — it is invisible to end users and applications, requiring no application-level modifications. It offers a **general-purpose solution** that protects all IP traffic. IPsec also includes a **filtering capability**, allowing only selected traffic to incur processing overhead. It provides access control, connectionless integrity, data origin authentication, rejection of replayed packets, and confidentiality through two protocols (AH and ESP) operating in Transport or Tunnel mode.

*Limitations:* IPsec requires complex configuration (Security Associations, key management via IKE), and Tunnel Mode adds overhead by encapsulating entire packets. It also cannot provide application-specific security granularity — it treats all traffic between two endpoints equally.

**Transport Layer — TLS:**  
TLS operates just above TCP, providing a **reliable end-to-end secure service**. It is not a single protocol but two layers: the Record Protocol (confidentiality + message integrity) and upper-layer management protocols (Handshake, Change Cipher Spec, Alert, Heartbeat). TLS can be implemented transparently as part of the protocol suite or embedded in specific applications (e.g., all browsers implement HTTPS).

*Limitations:* TLS secures individual connections, not all network traffic. Each application must explicitly use TLS, which means security gaps can exist if an application does not implement it. TLS also depends on TCP and therefore does not work with UDP-based protocols (until DTLS).

**Application Layer — S/MIME, Kerberos:**  
Application-specific security services can be **tailored to the specific needs** of a given application. S/MIME secures email (SMTP), while Kerberos provides strong authentication for client/server applications using secret-key cryptography, allowing nodes on a non-secure network to prove their identity securely.

*Limitations:* Each application must implement its own security mechanism independently, leading to duplication of effort. Security is only as good as each individual implementation, and new applications must be developed with security in mind from the start.

**Evaluation:**  
No single approach provides the "best" solution in all cases — the optimal strategy depends on the security requirements:
- **IPsec** is ideal for network-wide protection (e.g., VPNs between offices) where all traffic must be secured transparently
- **TLS** offers the best balance of **flexibility and coverage** for client-server applications, particularly web-based systems, because it can be applied per-connection with relatively low complexity
- **Application-layer** solutions are necessary when security requirements are unique to a specific protocol

In practice, a **defence-in-depth** approach combining all three layers provides the most robust security posture.

**Key points to include:**
- IPsec: transparent, general-purpose, filtering capability, AH/ESP
- TLS: above TCP, Record Protocol + 4 upper protocols, per-connection
- Application layer: tailored but requires per-application implementation
- Comparison of advantages and limitations for each layer
- Defence-in-depth as the recommended approach

**Common mistakes to avoid:**  
- Declaring one layer absolutely "best" without acknowledging trade-offs
- Forgetting to mention IPsec's filtering capability
- Not distinguishing between TLS as transparent protocol suite vs embedded in applications
- Omitting Kerberos or S/MIME when discussing application-layer security

---

### Q26 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 6

**Question:**  
Sketch (in text form) the block diagram that fulfils the following security requirement:

Alice needs to send a message to Bob with message authentication (no confidentiality required). Alice will use a cryptographic hash function and a shared secret value S to ensure Bob can verify the message has not been altered and that it originated from Alice.

**Guide answer:**  
```
Alice side:
   Message (M) + Secret (S) → Concatenate → [M || S] → Hash Function H → Hash value h
   Send: M + h → ─────────────────────────→ (over network)

Bob side:
   Receive: M + h
   M + Secret (S) → Concatenate → [M || S] → Hash Function H → Hash value h'
   Compare: h' == h ?
   → Match: Message is authentic and unaltered
   → Mismatch: Message has been tampered with
```

This corresponds to **Message Authentication Example (c)** from the lecture: both parties share a common secret value S. Alice computes H(M || S) and appends the hash to M. Bob recomputes H(M || S) using his copy of S and compares. Since S is never transmitted, an attacker cannot forge a valid hash for a modified message.

**Key points to include:**
- Concatenation of M and S before hashing
- Hash value transmitted alongside the message
- S is NOT transmitted over the network
- Receiver recomputes and compares

**Common mistakes to avoid:**  
- Encrypting the entire message (question states no confidentiality required)
- Forgetting to show that S is concatenated with M before hashing
- Sending S alongside the message (which would defeat the purpose)

---

### Q27 — Application | Bloom's: Apply | Difficulty: Hard | Marks: 8

**Question:**  
Alice needs to send a confidential and digitally signed message to Bob. The confidentiality must be fulfilled using a symmetric key algorithm. Assume they have each other's public key certificates and the digital signature must be achieved using a cryptographic hash algorithm.

**(a)** Sketch (in text form) the block diagram showing how Alice prepares and sends the message. (Marks: 5)

**(b)** Explain the role of the hash function in this process. (Marks: 3)

**Guide answer:**  
**(a)**
```
Alice side:
   Step 1 — Digital Signature:
   Message (M) → Hash Function H → Hash value h
   h → Encrypt with Alice's Private Key (PRA) → Digital Signature (DS)

   Step 2 — Confidentiality:
   [M + DS] → Encrypt with Symmetric Key (K) → Ciphertext (C)

   Step 3 — Key Exchange:
   Symmetric Key (K) → Encrypt with Bob's Public Key (PUB) → Encrypted Key (EK)

   Send to Bob: C + EK

Bob side:
   EK → Decrypt with Bob's Private Key (PRB) → Symmetric Key (K)
   C → Decrypt with K → [M + DS]
   DS → Decrypt with Alice's Public Key (PUA) → h
   M → Hash Function H → h'
   Compare: h == h' → Signature verified
```

**(b)** The hash function serves two critical roles:
1. **Efficiency** — instead of encrypting the entire message with Alice's private key (which is computationally expensive for asymmetric encryption), only the fixed-size hash value is encrypted to create the digital signature. This is significantly faster.
2. **Integrity verification** — the hash value acts as a unique fingerprint of the message. If even a single bit of the message is altered in transit, the recomputed hash will not match the decrypted signature hash, immediately detecting tampering.

**Key points to include:**
- Hash of message encrypted with sender's private key = digital signature
- Message + signature encrypted with symmetric key for confidentiality
- Symmetric key encrypted with receiver's public key for key exchange
- Hash provides efficiency (only hash is signed, not entire message) and integrity

**Common mistakes to avoid:**  
- Encrypting the entire message with the private key instead of just the hash
- Forgetting the key exchange step (symmetric key must be shared securely)
- Not distinguishing between confidentiality (symmetric encryption) and authentication (digital signature)

---

### Q28 — Short Answer | Bloom's: Remember | Difficulty: Medium | Marks: 4

**Question:**  
Write the scientific term for each of the following:

**(a)** A protocol that encapsulates the whole datagram into another datagram to hide the original datagram parameters.

**(b)** A security mechanism that uses a secret code concatenated with the message and inputted to a hash algorithm to obtain a secure hash code.

**(c)** A property in the hash algorithm that makes it computationally infeasible to find any pair of data inputs that gives the same hash code.

**(d)** A computer-network authentication protocol that allows nodes communicating over a non-secure network to prove their identity to one another in a secure manner using secret-key cryptography.

**Guide answer:**  
**(a)** IPsec Tunnel Mode (or Tunnelling Protocol)  
**(b)** Message Authentication Code (MAC)  
**(c)** Collision-free property (Collision resistance)  
**(d)** Kerberos

**Key points to include:**
- Exact terms as used in the lecture material
- Tunnel Mode specifically involves encapsulating the entire datagram
- Collision-free = no two inputs produce the same hash

**Common mistakes to avoid:**  
- For (a): writing "VPN" — VPN is a use case, not the specific mechanism
- For (b): writing "Digital Signature" — digital signatures use private keys, not shared secrets
- For (c): writing "one-way property" — one-way refers to pre-image resistance, not collision resistance
- For (d): writing "SSH" — SSH is for secure remote login, not network authentication protocol

---

### Q29 — MCQ | Bloom's: Understand | Difficulty: Medium | Marks: 2

**Question:**  
In the SHA-512 algorithm, every bit of the hash code is a function of every bit of the input. This property ensures that:  
a. The hash code is always unique for any input  
b. Changing one bit of the input will not change the hash code  
c. The complex repetition of the basic function produces results that are well mixed, making it unlikely for two similar messages to have the same hash  
d. The hash code can be reversed to obtain the original message

**Guide answer:**  
**c.** The complex repetition of the basic function F produces results that are well mixed; it is unlikely that two messages chosen at random, even if they exhibit similar regularities, will have the same hash code.

**Key points to include:**
- SHA-512 uses 80 rounds of processing on 1024-bit message blocks
- The "well mixed" property means even similar inputs produce vastly different outputs
- This is directly quoted from the lecture material

**Common mistakes to avoid:**  
Selecting (a) — uniqueness is not guaranteed (collisions theoretically exist), but they are computationally infeasible to find. Selecting (d) — hash functions are one-way and cannot be reversed.

---

### Q30 — Application | Bloom's: Apply | Difficulty: Medium | Marks: 5

**Question:**  
A small business currently uses TELNET for remote administration of their servers. Their network security consultant advises them to switch to a different protocol.

**(a)** Identify the protocol the consultant would recommend and explain why. (Marks: 3)

**(b)** List two additional uses of this protocol beyond remote login. (Marks: 2)

**Guide answer:**  
**(a)** The consultant would recommend **SSH (Secure Shell)**. TELNET transmits all data — including passwords and commands — in plaintext, making it vulnerable to eavesdropping and credential theft. SSH provides **encrypted communication** for remote login, ensuring that all data exchanged between the administrator and the server is protected from interception. SSH was specifically designed as a secure replacement for TELNET.

**(b)** Beyond remote login, SSH is used for:
1. **X tunnelling** — securely forwarding graphical application displays over the network
2. **Secure file transfer** — SSH-based protocols (SCP, SFTP) enable encrypted file transfers between systems

**Key points to include:**
- SSH replaces TELNET specifically
- TELNET's vulnerability is plaintext transmission
- SSH provides encryption for remote sessions
- X tunnelling and file transfer as additional uses

**Common mistakes to avoid:**  
Recommending TLS or HTTPS — these secure web communications, not remote terminal access. The question specifically targets remote server administration, which is SSH's domain.

---

## Section 4 — Study Tips

1. **IPsec Transport vs Tunnel Mode:** This distinction is a recurring exam favourite (appeared in both 2023 and 2025 exams). Make sure you can clearly articulate what each mode encrypts, the use case for each, and why Tunnel Mode is preferred for VPNs. Draw the packet diagrams to visualise the difference.

2. **MAC vs Digital Signature distinction:** Questions on this topic require you to know the key type (symmetric vs asymmetric), which security services each provides, and crucially that only digital signatures provide non-repudiation. Past exams have tested this through both MCQ and "write the scientific term" formats.

3. **SHA evolution timeline and rationale:** Understand the progression SHA-1 → SHA-2 → SHA-3, the structural concern (shared mathematical operations), and that SHA-3 complements rather than replaces SHA-2. Also know the CBC-like internal structure of hash functions (CVᵢ = E(Yᵢ₋₁, CVᵢ₋₁)).

---

## Section 5 — Coverage Gap Analysis

| Concept | Why It May Be Worth Testing | Suggested Question Type |
|---|---|---|
| **IEEE 802.11i phases of operation** (Discovery, Authentication, Association) | The lecture mentions specific operational phases but no question directly tests the sequence or purpose of each phase | Short Answer or Application |
| **TLS Handshake Protocol detailed action** | The lecture references the Handshake Protocol action flow but questions focus on Record Protocol services | Application or Essay |
| **Mobile Device Security Elements** | Mentioned in the lecture but not elaborated — if exam material includes this, a short answer question would be appropriate | Short Answer |
| **S/MIME specific functionality** | Mentioned as application-layer security for SMTP but not deeply tested | Fill-in-the-blank or MCQ |
| **SHA-512 specific constants and round structure** (Ki, Wi, 80 rounds, 1024-bit blocks) | Detailed processing parameters are in the lecture but not tested beyond the conceptual level | MCQ or Short Answer |

---

*Generated following the exam question generator instructions. Questions are calibrated against 3 past exam samples (2023, 2025, and AI-generated) for tone, difficulty, and mark allocation.*
