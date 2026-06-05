# Exam 25 - Detailed Guide Answers
## CCY2001: Introduction to Cybersecurity

---

## Question One (8 Points) - Feistel Cipher & DES Operations
> **📺 YouTube Search Keyword:** *"Feistel Cipher and DES algorithm explained"*

### Part a) Feistel Cipher Structure - Encryption & Decryption (4 Points)

**Overview:**
The Feistel cipher is a symmetric structure that divides plaintext into two halves and processes them through multiple rounds with identical operations for both encryption and decryption.

**Feistel Cipher Structure:**

```
ENCRYPTION PROCESS:
┌─────────────────────────────────────────┐
│ 64-bit Plaintext (or any block)        │
└─────────────────────────────────────────┘
           ↓
┌─────────────────────────────────────────┐
│ Initial Permutation (IP)                │
└─────────────────────────────────────────┘
           ↓
    Split into two halves:
    L₀ (left) | R₀ (right)
           ↓
    ┌─────────────────────────────────────┐
    │ Round 1 to Round N:                 │
    │ L₁ = R₀                             │
    │ R₁ = L₀ ⊕ F(R₀, K₁)                │
    │                                     │
    │ L₂ = R₁                             │
    │ R₂ = L₁ ⊕ F(R₁, K₂)                │
    │ ... (repeat for each round)        │
    └─────────────────────────────────────┘
           ↓
    Combine: R_n | L_n
           ↓
┌─────────────────────────────────────────┐
│ Final Permutation (FP)                  │
└─────────────────────────────────────────┘
           ↓
    64-bit Ciphertext
```

**DECRYPTION PROCESS:**
```
The Feistel structure allows identical decryption operations!

64-bit Ciphertext
           ↓
┌─────────────────────────────────────────┐
│ Initial Permutation (IP)                │
└─────────────────────────────────────────┘
           ↓
    Split into two halves:
    L₀ | R₀ (from ciphertext)
           ↓
    ┌─────────────────────────────────────┐
    │ Apply rounds in REVERSE order:      │
    │ Use K_n, K_{n-1}, ..., K_1         │
    │                                     │
    │ L₁ = R₀                             │
    │ R₁ = L₀ ⊕ F(R₀, K_n)               │
    │ ... (apply same formula)           │
    └─────────────────────────────────────┘
           ↓
    Combine: R_n | L_n
           ↓
┌─────────────────────────────────────────┐
│ Final Permutation (FP)                  │
└─────────────────────────────────────────┘
           ↓
    64-bit Plaintext (recovered)
```

**Key Feature:** Both encryption and decryption use the SAME round function F, just with keys in reverse order!

**Formulas:**
- **Encryption Round i:** $L_i = R_{i-1}$ and $R_i = L_{i-1} \oplus F(R_{i-1}, K_i)$
- **Decryption Round i:** Same formula, but using subkeys in reverse order

---

### Confusion and Diffusion

**Confusion:**
- **Definition:** Makes the relationship between ciphertext and key as complex as possible
- **How Achieved:** Through the round function F, which performs complex substitution operations on the right half
- **Purpose:** Make it difficult to deduce the key from ciphertext analysis
- **Example in DES:** The S-Boxes (Substitution Boxes) provide confusion

**Diffusion:**
- **Definition:** The statistical structure of plaintext is dissipated into long-range statistics of ciphertext
- **How Achieved:** Each plaintext bit affects the value of many ciphertext bits
- **Purpose:** Hide patterns in the plaintext
- **Example in DES:** 
  - Permutation operations spread bits across the block
  - The Feistel structure means each round mixes left and right halves
  - After enough rounds, each plaintext bit influences every ciphertext bit

**Shannon's Principles:**
Claude Shannon identified that effective block ciphers combine both properties:
- **Confusion:** Hides relationship between plaintext, key, and ciphertext (substitution)
- **Diffusion:** Spreads plaintext information over entire ciphertext (permutation)

**Diagram (Optional):**
```
Plaintext Block
    ↓
┌───────────────────────────┐
│ Confusion Layer           │
│ (Substitution - S-Boxes)  │
└───────────────────────────┘
    ↓
┌───────────────────────────┐
│ Diffusion Layer           │
│ (Permutation - P-Box)     │
└───────────────────────────┘
    ↓
Ciphertext Block
(Each plaintext bit affects multiple ciphertext bits)
```

---

### Part b) DES S-Box Operations with All-Ones Input (4 Points)

**Given:** All 48-bits input to S-Boxes are 1 (binary: 111111...111111)

**Step i: S-Box Substitution Operation**

**Understanding S-Boxes:**
- DES has 8 S-Boxes (S1 through S8)
- Each S-Box maps 6 input bits to 4 output bits
- 48 input bits = 8 S-Boxes × 6 bits each
- Output = 8 S-Boxes × 4 bits = 32 bits

**S-Box Structure:**
- Row selection: Using bits 1 and 6 (outer bits): `111111` → row = `11` (binary) = 3 (decimal)
- Column selection: Using bits 2, 3, 4, 5 (inner bits): `1111` (binary) = 15 (decimal)

**Input Processing:**
```
All-Ones 48-bit input:
111111 | 111111 | 111111 | 111111 | 111111 | 111111 | 111111 | 111111
  S1   |  S2   |  S3   |  S4   |  S5   |  S6   |  S7   |  S8
```

**S-Box Lookup:**
For each S-Box with input `111111`:
- Outer bits (bits 1,6): `1...1` = `11` (binary) = 3 (decimal) → Row 3
- Inner bits (bits 2,3,4,5): `1111` (binary) = 15 (decimal) → Column 15

**Example S-Box Output:**
Looking at standard DES S-Box tables:
- S1[3][15] = (some value from S1 table at row 3, column 15)
- S2[3][15] = (some value from S2 table)
- ... (same for S3 through S8)

**Typical Result Example:**
If we use the standard DES S-Boxes, all-ones input produces:
```
S1 output: 4-bits
S2 output: 4-bits  
S3 output: 4-bits
S4 output: 4-bits
S5 output: 4-bits
S6 output: 4-bits
S7 output: 4-bits
S8 output: 4-bits
─────────────────────
Total: 32-bit output
```

**General Answer (without specific S-Box tables):**
The 48-bit all-ones input will produce a 32-bit output by looking up each 6-bit group in its corresponding S-Box.

---

### Step ii: Permutation (P) Operation

**What is P Operation:**
- Applies to the 32-bit output from S-Boxes
- Permutation table (P) specifies which input bit goes to which output position
- Provides diffusion by spreading S-Box output bits across the 32-bit result

**Permutation Table (Conceptual):**
The P permutation rearranges the 32 bits according to a fixed permutation table:
```
Output Bit 1 ← comes from Input Bit 16
Output Bit 2 ← comes from Input Bit 7
Output Bit 3 ← comes from Input Bit 20
... (and so on for all 32 bits)
```

**Process:**
1. Take the 32-bit output from S-Boxes
2. Reorder the bits according to the P permutation table
3. Generate 32-bit output to XOR with left half

**Example Calculation:**
```
S-Box Output: b₁b₂b₃...b₃₂
      ↓
[Apply P Permutation]
      ↓
P Output: (arrangement of above bits according to P table)
```

**Final Result:**
The permuted output is then XORed with the left half in the Feistel formula:
$$R_i = L_{i-1} \oplus P(\text{S-Box Output})$$

**Detailed Steps Summary:**
1. **Input:** 48-bit all-ones
2. **S-Box Substitution:** 48 bits → 32 bits (each 6-bit group substituted via its S-Box)
3. **P Permutation:** Rearrange 32 bits according to P table
4. **Output:** 32-bit result ready for XOR operation

---

## Question Two (12 Points) - RSA Key Exchange & Digital Signatures
> **📺 YouTube Search Keyword:** *"RSA Encryption and Digital Signatures examples"*

### Part A: Symmetric Key Exchange with RSA (6 Points)

**Question:** Encrypt a symmetric key (derived from first 4 letters of last name) for secure exchange with authentication and secrecy.

**Step i: Convert ASCII and Form Symmetric Key**

**Process:**
1. Take first 4 letters of your last name
2. Convert each to ASCII decimal value

**Example:** Last name "SMITH"
```
S → ASCII 83
M → ASCII 77
I → ASCII 73
T → ASCII 84

Symmetric Key (as single number): 83778384
Or as individual bytes: [83, 77, 73, 84]
```

**Standard ASCII Decimal Values:**
```
A-Z: 65-90
a-z: 97-122
```

---

### Step ii: RSA Encryption Using Friend's Public Key (Secrecy)

**Requirement:** Confidentiality (secrecy) — only your friend can read the key

**Your Setup:**
- Your Public Key (PUA): e_A = 29, n_A = 133
- Your Private Key (PRA): d_A = 41, n_A = 133
- Friend's Public Key (PUB): e_B = 7, n_B = 187  
- Friend's Private Key (PRB): d_B = 23, n_B = 187

**Algorithm for SECRECY:** Encrypt each key byte with the recipient's public key
$$C = M^{e_B} \mod n_B$$

**Step-by-Step Detailed Example:**

Let's say last name = "SMITH" → first 4 letters: S, M, I, T  
Key bytes: M₁=83, M₂=77, M₃=73, M₄=84

Since n_B = 187, each ASCII value (65–90) is less than 187, so we can encrypt each byte individually.

**Encrypt each byte with friend's public key PUB = {7, 187}:**
```
C₁ = 83^7 mod 187
C₂ = 77^7 mod 187
C₃ = 73^7 mod 187
C₄ = 84^7 mod 187
```

**Example detailed calculation for C₁ = 83^7 mod 187:**
```
83^1 = 83
83^2 = 6889 mod 187 = 6889 - 36×187 = 6889 - 6732 = 157
83^4 = 157^2 mod 187 = 24649 mod 187 = 24649 - 131×187 = 24649 - 24497 = 152
83^7 = 83^4 × 83^2 × 83^1 mod 187
     = 152 × 157 × 83 mod 187
     = 152 × 157 mod 187 = 23864 mod 187 = 23864 - 127×187 = 23864 - 23749 = 115
     = 115 × 83 mod 187 = 9545 mod 187 = 9545 - 51×187 = 9545 - 9537 = 8

C₁ = 8
```

**Send to friend:** The encrypted values C₁, C₂, C₃, C₄

---

### Friend Decrypts Using Private Key

**Friend receives ciphertexts and performs:**
$$M = C^{d_B} \mod n_B = C^{23} \mod 187$$

**Example: Decrypt C₁ = 8:**
```
M₁ = 8^23 mod 187 = 83 ✓ (recovers original ASCII value for 'S')
```

---

### If Authentication Is Required (Brief Explanation)

If authentication is also needed, Alice could use a **digital signature**:
1. **Sign first:** Compute signature S = M^{d_A} mod n_A using her private key
2. **Then encrypt:** Compute C = S^{e_B} mod n_B using friend's public key

This provides **both secrecy and authentication**:
- **Secrecy:** Only the friend (with PRB) can decrypt
- **Authentication:** Only Alice (with PRA) could have signed the message
- **Non-repudiation:** Alice cannot deny sending the key, because only she has PRA

The friend would reverse the process: first decrypt with PRB, then verify with PUA.

---

### Security Properties

| Property | How Achieved |
|----------|-------------|
| **Secrecy** | Encrypt with friend's public key (PUB) |
| **Authentication** (if required) | Sign with your private key (PRA) before encrypting |
| **Non-repudiation** (if required) | Only you have your private key |

---

### Part B: Digital Signature - Calculation & Verification (6 Points)

**Given:**
- Alice's Public Key: (e=5, n=35)
- Alice's Private Key: (d=5, n=35)
- Hash Function: $H(m) = (\sum \text{ASCII values}) \mod 100$
- Message: "Hello"

---

### Part i: Calculate Digital Signature

**Step 1: Compute hash of the message**
```
H → 72
e → 101
l → 108
l → 108
o → 111

Sum = 72 + 101 + 108 + 108 + 111 = 500
```

**Step 2: Apply hash function**
$$H = 500 \mod 100 = 0$$

**Step 3: Sign the hash with Alice's private key**
$$\text{Signature} = H^d \mod n = 0^5 \mod 35$$

**Calculation:**
```
0^5 = 0
0 mod 35 = 0

Signature = 0
```

**Answer:** Digital Signature = **0**

> **Note:** The hash value of "Hello" is 0 (as given in the exam example). Any number raised to any power is still 0, so the signature is 0. This is a simplified demonstration.

---

### Part ii: Verify Digital Signature

**How Bob Verifies:**

**Step 1: Recover hash from signature using Alice's public key**
$$H_{\text{recovered}} = \text{Signature}^e \mod n = 0^5 \mod 35$$

**Calculation:**
```
0^5 = 0
0 mod 35 = 0
H_recovered = 0
```

**Step 2: Compute hash of received message**
```
Message: "Hello"
H=72, e=101, l=108, l=108, o=111
Sum = 500
H_computed = 500 mod 100 = 0
```

**Step 3: Compare hashes**
```
H_recovered = 0
H_computed  = 0

0 = 0  ← HASHES MATCH ✓
```

**Verification Result:** **SIGNATURE IS VALID** ✓

**Explanation:** 
- Bob recovers the hash value from the signature using Alice's public key
- Bob independently computes the hash of the received message
- Since both values match (0 = 0), the signature is verified
- This confirms: (1) the message has not been tampered with (integrity), and (2) it was indeed signed by Alice (authentication)

---

### Part iii: Modified Message Attack - "Help"

**If attacker changes message to "Help":**

**Step 1: Compute hash of modified message (given in exam)**
```
H → 72
e → 101
l → 108
p → 112

Sum = 72 + 101 + 108 + 112 = 393
H_modified = 393 mod 100 = 93

Wait — the exam states: "l=108, l=108, p=112, sum=501"
Let's use the exam's given values:
H=72, e=101, l=108, l=108, p=112
Sum = 72 + 101 + 108 + 108 + 112 = 501
H_modified = 501 mod 100 = 1
```

> **Note:** The exam gives "Help" with ASCII values H=72, e=101, l=108, **l=108**, p=112 (5 characters including two 'l's). Using their given sum of 501: hash = 1.

**Step 2: Verification process (Bob's side)**
- Bob receives: Message "Help", Signature = 0 (unchanged from original)
- Bob recovers hash from signature: H_recovered = 0^5 mod 35 = **0**
- Bob computes hash of "Help": H_computed = 501 mod 100 = **1**

**Step 3: Compare**
```
H_recovered = 0
H_computed  = 1

0 ≠ 1  ← HASHES DO NOT MATCH ✗
```

**Result:** **VERIFICATION FAILS** ✗

**Conclusion:** 
Bob will detect that the message was tampered with because:
- The hash of "Help" (1) does NOT match the recovered hash from signature (0)
- This proves the message was modified after Alice signed it
- The attacker cannot forge a valid signature without Alice's private key
- **Security Property:** The digital signature ensures that ANY modification to the message will be detected during verification

---

## Question Two (Part 2) - Terminology (2 Points)
> **📺 YouTube Search Keyword:** *"Cryptography terminology: Confusion Diffusion MAC PKI IPSec"*

### Write Scientific Terms:

**i) A property in the encryption algorithm that makes each plaintext digit affect the value of many ciphertext digits**

**Answer: DIFFUSION**

**Explanation:**
- Spreads plaintext information across the ciphertext
- Each plaintext bit influences multiple ciphertext bits
- Hides patterns from the plaintext
- Achieved through permutation operations
- Definition: "The statistical structure of the plaintext is dissipated into long-range statistics of the ciphertext"

---

**ii) The most secure way to distribute the public key is**

**Answer: PUBLIC KEY INFRASTRUCTURE (PKI) or DIGITAL CERTIFICATE**

**More specific answer: CERTIFICATE AUTHORITY (CA) signed DIGITAL CERTIFICATE**

**Explanation:**
- Distributes public keys with authentication guarantees
- Binds identity to public key
- Third-party verification prevents impersonation
- Uses digital certificates signed by trusted CA
- Prevents man-in-the-middle attacks

---

**iii) Protocol that encapsulates the whole datagram into another datagram to hide the original parameters and provide secure communication over an insecure network**

**Answer: IPSec (IP Security) or VPN (Virtual Private Network)**

**More specific: IPSec - Tunneling Mode**

**Explanation:**
- IPSec encapsulates entire IP datagrams
- Hides original source/destination addresses
- Creates secure tunnel over insecure networks (Internet)
- Used in VPNs
- Operates at network layer (Layer 3)
- Provides confidentiality and authentication

---

**iv) A security mechanism that uses a secret code concatenated with the message and inputted to a hash algorithm to obtain a secure hash code**

**Answer: HMAC (Hash-based Message Authentication Code) or MAC (Message Authentication Code)**

**More specific: HMAC**

**Explanation:**
- HMAC = Hash(Key + Message + Key)
- Key is secret (known only to sender and receiver)
- Provides message authentication and integrity
- Different from digital signature (doesn't prove non-repudiation)
- Uses symmetric key (unlike signatures which use private key)
- Output is called Message Authentication Code or Tag

---

## Question Three - Multiple Choice (4 Points)
> **📺 YouTube Search Keyword:** *"Network Security Firewalls IDS and Cryptography basics"*

### i) One of the following is NOT true about DES
**Answer: (b) Use a key of 56-bit length in each round**

**Explanation:**
- **(a) Based on Feistel Structure** - TRUE ✓
  - DES explicitly uses Feistel cipher structure
  - Reference: "Data are encrypted in 64-bit blocks using a 56-bit key based on Feistel Cipher Concept"

- **(b) Use a key of 56-bit length in each round** - FALSE ✗
  - This is the INCORRECT statement
  - DES uses 56-bit OVERALL key
  - Each round uses a 48-bit SUBKEY (derived from the 56-bit key)
  - Key Schedule generates different 48-bit subkeys for each of the 16 rounds
  - Reference: "Selecting 24-bits from each half" = 48 bits total per round

- **(c) Has initial symmetric key of 64-bits** - TRUE ✓
  - Input key is 64-bit (64-bit with parity bits)
  - After parity check removal: 56-bit usable key

- **(d) Has a good Avalanche effect** - TRUE ✓
  - Small change in plaintext or key produces large change in ciphertext
  - Property of secure encryption algorithms

---

### ii) One of the following is TRUE about AES
**Answer: (d) Use different algorithms for decryption**

- **(a) Its encryption algorithm needs more time than DES** - FALSE ✗
  - AES is generally FASTER than DES despite better security
  - Modern hardware optimizations make AES very efficient

- **(b) The plaintext block size is varied...** - FALSE ✗
  - AES ALWAYS uses 128-bit block size (fixed)
  - Only KEY SIZE varies (128/192/256-bit)
  - The terminology AES-128/192/256 refers to KEY size, not block size

- **(c) Use fixed number of rounds...** - FALSE ✗
  - Number of rounds DEPENDS on key size:
    - AES-128: 10 rounds
    - AES-192: 12 rounds
    - AES-256: 14 rounds
  - NOT independent of key size

- **(d) Use different algorithms for decryption** - TRUE ✓
  - Unlike Feistel-based ciphers, AES has different encryption and decryption
  - Encryption: SubBytes → ShiftRows → MixColumns → AddRoundKey
  - Decryption: InvSubBytes → InvShiftRows → InvMixColumns → AddRoundKey
  - This is a fundamental design difference from DES

---

### iii) Message Authentication Code is a security mechanism to achieve
**Answer: (b) Data Origin Authentication AND (c) Data Integrity** (likely multiple answers)

- **(a) Peer-entity Authentication** - PARTIALLY (but not primary)
  - Authenticates message origin (weak form of entity authentication)
  - Not strong entity authentication like mutual authentication

- **(b) Data Origin Authentication** - TRUE ✓
  - Verifies message came from claimed sender
  - Only authorized parties have the MAC key
  - Proves origin of data

- **(c) Data Integrity** - TRUE ✓
  - Detects if message was modified
  - Any bit change produces different MAC
  - Receiver verifies MAC hasn't changed

- **(d) Digital Signature** - FALSE ✗
  - MAC does NOT provide non-repudiation
  - Digital signature uses asymmetric keys (provides non-repudiation)
  - MAC uses symmetric keys (only sender and receiver have it)

---

### iv) Applies rules to incoming/outgoing IP packets, forwarding or discarding them based on source/destination IP addresses, port numbers, and protocols
**Answer: (b) Packet Filtering Firewall**

- **(a) Application-Level Firewall** - FALSE
  - Operates at Layer 7 (Application)
  - Examines application data content

- **(b) Packet Filtering Firewall** - TRUE ✓
  - Operates at Layer 3-4 (Network/Transport)
  - Examines IP addresses, ports, protocols
  - Forwards or discards based on rules
  - Fast but less sophisticated

- **(c) Internal Firewall** - FALSE
  - Not a standard firewall type classification

- **(d) Circuit-Level Firewall** - FALSE
  - Operates at Transport layer
  - Monitors TCP/UDP connections
  - Doesn't filter packets based on addresses/ports directly

---

### v) The Network-based Intrusion Detection System (NIDS)
**Answer: (c) Monitors traffic at selected points on a network**

- **(a) Takes action to block or mitigate attacks** - FALSE
  - IDS is PASSIVE (detects and alerts)
  - IPS (Intrusion Prevention System) TAKES ACTION (blocks)

- **(b) Examines user and software activity on each host** - FALSE
  - This describes Host-based IDS (HIDS)
  - NIDS is network-based (not host-based)

- **(c) Monitors traffic at selected points on a network** - TRUE ✓
  - NIDS sits at strategic network points
  - Monitors all traffic passing through
  - Detects suspicious patterns
  - Sends alerts to administrators

- **(d) Provides secure communication over an insecure network** - FALSE
  - This describes VPN or IPSec

---

### vi) A security mechanism created by generating a hash value for a message and encrypting it with the sender's private key
**Answer: (c) Digital Signature**

- **(a) Data Origin Authentication** - PARTIAL (but not complete)
  - Digital signature provides this, but more than just origin auth

- **(b) Peer-Entity Authentication** - FALSE
  - Doesn't authenticate identity of entities
  - Only authenticates message origin

- **(c) Digital Signature** - TRUE ✓
  - Hash of message created
  - Hash encrypted with sender's private key (signing)
  - Receiver verifies with sender's public key
  - Provides: Authentication, Non-repudiation, Integrity

- **(d) Message Authentication Code** - FALSE
  - MAC uses symmetric key and hash directly
  - Doesn't use public-private key pair

---

### vii) A system for managing digital certificates and public-key encryption
**Answer: (a) Public-Key Infrastructure (PKI)**

- **(a) Public-Key Infrastructure** - TRUE ✓
  - Complete system for managing public keys
  - Includes: Certificate Authorities, Registration Authorities, Repositories
  - Issues, distributes, and revokes digital certificates
  - Binds identities to public keys
  - Provides trust infrastructure

- **(b) Public-Key Cryptography** - FALSE
  - This is the cryptographic method/algorithms
  - Not a system for managing certificates

- **(c) Public-Key Certificate** - FALSE
  - This is a single component of PKI
  - Not the entire infrastructure/system

- **(d) RSA** - FALSE
  - This is a specific algorithm
  - Not a management system

---

### viii) Certificate of public key (e.g. X.509) is digitally signed by:
**Answer: (c) Certificate Authority Private Key**

**Explanation:**
- A public-key certificate binds an identity to a public key.
- To prevent tampering and forgery, the Certificate Authority (CA) signs the certificate using its own **Private Key**.
- Anyone can then verify the authenticity of the certificate using the CA's well-known **Public Key**.

---

### c) Identify True or False and then correct the false: (2 Points)

**i. Although DES has been considered an insecure algorithm and possibly broken, a modified version called Triple-DES is used till now and considered secure.**
- **Answer:** **True**
- **Justification:** Triple-DES (3DES) applies the DES cipher three times with different keys (112-bit or 168-bit effective key sizes), which successfully defeats the brute-force vulnerabilities of single DES. Although it is slower than AES and is being phased out, it is still considered cryptographically secure.

**ii. Hash functions are used for message authentication and the creation of digital signatures. They take a fixed-size input (message) and produce a variable output.**
- **Answer:** **False**
- **Correction:** Hash functions take a **variable-size** input and produce a **fixed-size** output (referred to as a message digest or hash value).

**iii. The preimage resistance property of a hash algorithm is to be infeasible to find two different messages that produce the same hash value.**
- **Answer:** **False**
- **Correction:** Finding two different messages that produce the same hash value is the **collision resistance** property. Preimage resistance (one-way property) means that given a hash value $h$, it is computationally infeasible to find any message $x$ such that $H(x) = h$.

**iv. The Intrusion Detection System acts as a barrier between a network and the outside world, controlling traffic based on security policies.**
- **Answer:** **False**
- **Correction:** A **Firewall** acts as a barrier between a network and the outside world, controlling traffic based on security policies. An **Intrusion Detection System (IDS)** is a passive monitoring system that detects and alerts on suspicious activity but does not block traffic by default.

---

## Question Four (Incident Response) (12 Points)
> **📺 YouTube Search Keyword:** *"IDS vs IPS vs Firewall, Incident Response lifecycle NIST, SIEM in forensics"*

### a) IDS, IPS, and Firewall Comparison (4 Points)

| Security Device | Primary Function | Operational Mode | Typical Network Deployment |
|:---|:---|:---|:---|
| **Firewall** | Filters traffic (forwards/discards packets) based on security rules. | Inline | Perimeters of the network (external) or between zones (internal/DMZ) to restrict access. |
| **IDS (Intrusion Detection)** | Monitors traffic, detects policy violations, logs events, and alerts admins. | Passive / Out-of-band | Strategic monitor points (e.g., inside DMZ, behind firewalls, or on sensitive hosts). |
| **IPS (Intrusion Prevention)** | Detects threats in real-time and actively blocks or mitigates malicious traffic. | Inline | In the direct path of traffic at critical network boundaries where blocking is required. |

---

### b) Incident Response (IR) Plan & Process (4 Points)

- **Incident Response (IR) Plan:** A structured, documented set of procedures that guides an organization in detecting, responding to, and recovering from security incidents/breaches.
- **Incident Response Process:** Typically consists of: **Preparation** $\rightarrow$ **Detection & Analysis** $\rightarrow$ **Containment, Eradication & Recovery** $\rightarrow$ **Post-Incident Activity (Lessons Learned)**.

#### Actions to Address the Scenario (Brute-Force Logins & Unauthorized Data Transfers):
1. **Detection & Analysis:**
   - Review log data and SIEM reports to isolate target systems and trace the source IP addresses executing the failed login attempts.
   - Monitor netflow/outbound logs to identify the source of the unauthorized data transfers, what data is being exfiltrated, and the destination external servers.
2. **Containment:**
   - Configure the firewall to immediately block the malicious external IP addresses.
   - Temporarily lock the user accounts targeted by the brute-force attacks.
   - Isolate the internal server performing unauthorized transfers from the local network to halt data exfiltration.
3. **Eradication:**
   - Scan the isolated server for malware, Trojans, or unauthorized access backdoors and remove them.
   - Force password resets and mandate Multi-Factor Authentication (MFA) across the organization.
   - Locate and patch the underlying application or OS vulnerabilities that allowed the compromise.
4. **Recovery:**
   - Restore database files and application components from verified, clean backups.
   - Put systems back online and establish strict real-time logging and monitoring on the affected entities.
5. **Post-Incident Activity:**
   - Conduct a "lessons learned" review to document what happened, response efficiency, and update firewall/endpoint policies to prevent recurrence.

---

### c) Role of SIEM in Digital Forensics (4 Points)

A **SIEM (Security Information and Event Management)** system supports forensics during investigations by:
- **Centralized Log Aggregation:** Pulls and standardizes log files from host operating systems, databases, firewalls, and IDSs into a central repository.
- **Event Correlation:** Connects separate activities (e.g., correlating a series of failed logins with subsequent outbound data flows on the firewall) to map out the attack path.
- **Data Integrity & Compliance:** Stores log entries in a tamper-resistant format, preserving evidence for investigation and maintaining a secure chain of custody.
- **Timeline Construction:** Allows forensics teams to query logs and build an exact chronology of the attack to determine the timeline of events.

---

## Question Five (Network and End-Points Security) (12 Points)
> **📺 YouTube Search Keyword:** *"IPSec transport vs tunnel mode, TLS architecture and record protocol, Key Distribution Center vs Key Translation Center"*

### a) IPsec Transport Mode vs Tunnel Mode (4 Points)

- **Datagram Structure:**
  - **Transport Mode:** Encrypts and optionally authenticates only the IP payload. The original IP header remains intact and readable.
  - **Tunnel Mode:** Encrypts the entire original IP packet (original IP header + IP payload) and encapsulates it inside a new IP packet with a new outer IP header.
- **Devices Performing Security Services:**
  - **Transport Mode:** Performed directly by the end systems (Host-to-Host).
  - **Tunnel Mode:** Typically performed by security gateways (firewalls, routers, or VPN concentrators) on behalf of host computers (Gateway-to-Gateway).
- **Typical Applications:**
  - **Transport Mode:** Secure host-to-host network services (e.g., remote desktop connections between two servers).
  - **Tunnel Mode:** Creating Virtual Private Networks (VPNs) over public networks to connect branch offices.

#### Structure Sketches:

```
TRANSPORT MODE (ESP):
┌────────────────────┬──────────────┬────────────────────────────┐
│ Original IP Header │  ESP Header  │ TCP/UDP Payload (Encrypted)│
└────────────────────┴──────────────┴────────────────────────────┘
                     |<───────────────── Encrypted ─────────────>|

TUNNEL MODE (ESP):
┌────────────────┬──────────────┬────────────────────┬────────────────────────────┐
│ New IP Header  │  ESP Header  │ Original IP Header │ TCP/UDP Payload (Encrypted)│
└────────────────┴──────────────┴────────────────────┴────────────────────────────┘
                 |<──────────────────────── Encrypted ───────────────────────────>|
```

---

### b) TLS/SSL Security Architecture & Services (4 Points)

#### i. TLS Protocol Suite Components:
1. **Record Protocol:** The core protocol that handles the encapsulation, fragmentation, compression (optional), MAC addition, and encryption of application data.
2. **Handshake Protocol:** Allows the server and client to authenticate each other, negotiate encryption algorithms, and establish the session keys.
3. **Change Cipher Spec Protocol:** A single-byte signal indicating that subsequent data packets will be encrypted using the newly negotiated keys.
4. **Alert Protocol:** Transmits alerts (warnings or fatal errors, such as handshake failures) to the peer.
5. **Heartbeat Protocol:** An extension that monitors connection status without renegotiating parameters.

#### ii. Security Services & Operation:
- **Confidentiality:** Handled by the **Record Protocol** by encrypting payload data with the negotiated symmetric key.
- **Message Integrity:** Handled by the **Record Protocol** by appending a Message Authentication Code (MAC) to the message.
- **Authentication:** Handled by the **Handshake Protocol** during the initial negotiation through public-key certificates (e.g., X.509).

#### Operation Sketch (Record Protocol Processing):
```
      APPLICATION DATA
             │
             ▼
      [ Fragmentation ]      (Divide data into blocks ≤ 2^14 bytes)
             │
             ▼
       [ Compression ]       (Optional layer)
             │
             ▼
         [ Add MAC ]         (Calculate integrity code using HMAC)
             │
             ▼
        [ Encrypt ]          (Encrypt data + MAC using symmetric key)
             │
             ▼
     [ Add Record Header ]   (Prepend Content-Type, TLS version, length)
             │
             ▼
     TCP transport layer
```

---

### c) Key Distribution: KTC vs KDC (4 Points)

- **Key Distribution Center (KDC):** The trusted third party **generates** the session key. A requests communication with B, and the KDC returns the generated key encrypted under A's master key and B's master key.
- **Key Translation Center (KTC):** One of the communicating entities (A) **generates** the session key itself, encrypts it under its own master key, and sends it to the KTC. The KTC decrypts it and **translates** (re-encrypts) it using B's master key, then sends it back to A to forward to B.

#### Step-by-Step Sketches:

#### 1. Key Distribution Center (KDC) Protocol:
```
      A                         KDC                         B
      │                          │                          │
      │ 1. Request session key   │                          │
      ├─────────────────────────>│                          │
      │                          │                          │
      │ 2. E(Ka, Ks) + E(Kb, Ks) │                          │
      │<─────────────────────────┤                          │
      │                          │                          │
      │ 3. Forward E(Kb, Ks)     │                          │
      ├────────────────────────────────────────────────────>│
      │                          │                          │
      │◄───────────────── 4. Secure Session ───────────────>│
```
- **Step 1:** Host A requests a session key from KDC to connect securely with B.
- **Step 2:** KDC generates session key $Ks$, encrypts it under A's master key ($Ka$), and encrypts it under B's master key ($Kb$). It sends both to A.
- **Step 3:** A decrypts $E(Ka, Ks)$ to obtain $Ks$, and forwards $E(Kb, Ks)$ directly to B.
- **Step 4:** B decrypts using $Kb$ to obtain $Ks$. Both parties now share $Ks$ for secure communication.

#### 2. Key Translation Center (KTC) Protocol:
```
      A                         KTC                         B
      │                          │                          │
      │ 1. A generates Ks.       │                          │
      │    Send E(Ka, Ks)        │                          │
      ├─────────────────────────>│                          │
      │                          │                          │
      │ 2. Translate to E(Kb,Ks) │                          │
      │<─────────────────────────┤                          │
      │                          │                          │
      │ 3. Forward E(Kb, Ks)     │                          │
      ├────────────────────────────────────────────────────>│
      │                          │                          │
      │◄───────────────── 4. Secure Session ───────────────>│
```
- **Step 1:** Host A generates the session key $Ks$ on its own, encrypts it using $Ka$, and requests translation from KTC.
- **Step 2:** KTC decrypts the packet using $Ka$ to recover $Ks$. It then encrypts $Ks$ using B's master key $Kb$ (translating the key) and sends it back to A.
- **Step 3:** A forwards the translated key packet $E(Kb, Ks)$ to B.
- **Step 4:** B decrypts using $Kb$ to retrieve $Ks$. Both parties now share $Ks$ for secure communication.

---

## Summary Table of Key Concepts

| Concept | Definition | Key Property |
|---------|-----------|--------------|
| **Feistel Cipher** | Divides plaintext into two halves, processes through rounds | Same structure for encryption/decryption |
| **DES** | 64-bit block, 56-bit key, 16 rounds | Based on Feistel structure |
| **AES** | 128-bit block, 128/192/256-bit key, 10/12/14 rounds | Different encryption/decryption algorithms |
| **Confusion** | Complex relationship between key and ciphertext | Substitution (S-Boxes) |
| **Diffusion** | Plaintext affects many ciphertext bits | Permutation operations |
| **RSA** | Public-key encryption | Based on factoring difficulty |
| **Digital Signature** | Hash + encryption with private key | Provides non-repudiation |
| **MAC** | Hash with shared secret key | No non-repudiation |
| **PKI** | System for managing public keys | Distributes certificates |
| **NIDS** | Network-based intrusion detection | Monitors network traffic |

---
