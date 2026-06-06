# Exam 26 - Detailed Guide Answers
## CCY2001: Introduction to Cybersecurity

---

## Question One (10 Points) - Symmetric Ciphers & Block Operations
> **📺 YouTube Search Keyword:** *"Vigenere cipher tutorial and AES Confusion Diffusion"*

### Part a) Vigenere Cipher Operations (4 Points)

**Process:**
The Vigenere Cipher uses the formula: `C = (P + K) mod 26`
Where P is the plaintext index and K is the keyword index (A=0, B=1, ... Z=25).

1. **Prepare Plaintext:** `S E C U R E S Y S T E M` (Remove spaces -> 12 characters)
2. **Align Keyword:** `C Y B E R C Y B E R C Y` (Repeat "CYBER" to match length)

**Calculation:**
*   S (18) + C (2) = 20 -> **U**
*   E (4) + Y (24) = 28 mod 26 = 2 -> **C**
*   C (2) + B (1) = 3 -> **D**
*   U (20) + E (4) = 24 -> **Y**
*   R (17) + R (17) = 34 mod 26 = 8 -> **I**
*   E (4) + C (2) = 6 -> **G**
*   S (18) + Y (24) = 42 mod 26 = 16 -> **Q**
*   Y (24) + B (1) = 25 -> **Z**
*   S (18) + E (4) = 22 -> **W**
*   T (19) + R (17) = 36 mod 26 = 10 -> **K**
*   E (4) + C (2) = 6 -> **G**
*   M (12) + Y (24) = 36 mod 26 = 10 -> **K**

**Final Ciphertext:** `UCDYI GQZWK GK`

---

### Part b) Principles of Confusion and Diffusion (6 Points)

**1. Definitions:**
*   **Confusion:** Makes the mathematical relationship between the ciphertext and the encryption key as complex as possible. It ensures that attackers cannot easily deduce the key from ciphertext statistics. (Primarily achieved through **Substitution** operations).
*   **Diffusion:** Dissipates the statistical structure of the plaintext into the long-range statistics of the ciphertext. Changing one bit of plaintext should influence many bits in the ciphertext (Avalanche Effect). (Primarily achieved through **Permutation/Transposition** operations).

**2. AES vs DES:**
*   **DES Application:** Uses the Feistel structure mixing left/right halves for diffusion, and 8 fixed S-Boxes for confusion.
*   **AES Application:** AES is a Substitution-Permutation Network (SPN). 
    *   **Confusion in AES:** Provided by the **SubBytes** layer (using a highly non-linear Galois field S-Box).
    *   **Diffusion in AES:** Provided by the **ShiftRows** (shifting bytes across columns) and **MixColumns** (mathematically mixing bytes within a column) layers.

---

## Question Two (10 Points) - Asymmetric Encryption & Digital Signatures
> **📺 YouTube Search Keyword:** *"RSA Encryption step by step and Digital Signature process"*

### Part a) RSA Key Exchange and Encryption (5 Points)

**1. Calculate Modulus and Totient:**
*   Primes: `p = 5`, `q = 11`
*   Modulus `n = p × q = 5 × 11 = 55`
*   Euler’s Totient `Φ(n) = (p - 1) × (q - 1) = 4 × 10 = 40`

**2. Calculate Private Exponent (d):**
*   Public key `e = 3`
*   Formula: `(e × d) mod Φ(n) = 1` => `(3 × d) mod 40 = 1`
*   Find a multiple of 40 that, when 1 is added, is divisible by 3.
*   Try k=1: 40(1) + 1 = 41 (Not divisible by 3)
*   Try k=2: 40(2) + 1 = 81 (81 / 3 = 27)
*   Therefore, **d = 27**.

**3. Encrypt Message (M = 8):**
*   Formula: `C = M^e mod n`
*   `C = 8^3 mod 55` 
*   `8^3 = 512`
*   `512 / 55 = 9.30909...` (55 × 9 = 495)
*   `512 - 495 = 17`
*   **Ciphertext C = 17**.

---

### Part b) Secure Communications Architecture (5 Points)

To achieve Confidentiality (nobody else can read it) AND Non-repudiation / Authentication (prove it's uniquely from Alice), Alice uses a combination of symmetric crypto and asymmetric digital signatures:

**Alice's Steps (Sending):**
1.  **Hash:** Alice inputs her message into a Hash Function (e.g., SHA-256) to get a Message Digest.
2.  **Sign:** Alice encrypts the Hash with her **Private Key** (This is the Digital Signature).
3.  **Append:** She attaches the Digital Signature to her original message.
4.  **Encrypt Data:** Alice generates a random **Symmetric Session Key** (e.g., AES) and encrypts the [Message + Signature].
5.  **Encrypt Key:** Alice encrypts the Symmetric Session Key using **Bob's Public Key**.
6.  **Send:** She sends the [Encrypted Message package] + [Encrypted Symmetric Key] to Bob.

**Bob's Steps (Receiving):**
1.  **Decrypt Key:** Bob decrypts the Symmetric Key block using his **Private Key**.
2.  **Decrypt Data:** He uses the recovered Symmetric Key to decrypt the [Message + Signature].
3.  **Hash Verification:** Bob runs the decrypted message through the identical Hash Function to calculate his own hash.
4.  **Signature Verification:** Bob decrypts Alice's Signature using **Alice's Public Key** to recover the originally sent hash.
5.  **Compare:** If Bob's computed hash matches the recovered hash, the message's origin and integrity are mathematically proven.

---

## Question Three (10 Points) - Network Security Protocols & Architecture
> **📺 YouTube Search Keyword:** *"IPSec Transport vs Tunnel Mode and Firewall vs IDS vs IPS"*

### Part a) IPSec Architecture: Transport vs Tunnel Mode (5 Points)

*   **Transport Mode:** Secures end-to-end communication from host to host. It encrypts only the **IP Payload** (data/TCP segments). The original IP header is kept intact, allowing intermediate routers to read the true source and destination.
*   **Tunnel Mode:** Generally secures gateway-to-gateway (e.g., VPNs between routers). It encrypts the **entire original IP Packet** (Payload + Original IP Header) and wraps it inside a completely new outer IP header.

**Structure Sketches:**
```text
TRANSPORT MODE:
[ Original IP Header ] | [ ESP Header ] | [ TCP/UDP Payload (Encrypted) ] | [ ESP Auth/Trailer ]

TUNNEL MODE:
[ New IP Header ] | [ ESP Header ] | [ Original IP Header (Encrypted) ] | [ TCP/UDP Payload (Encrypted) ] | [ ESP Auth/Trailer ]
```

---

### Part b) Network Defense Systems: Firewall vs IDS vs IPS (5 Points)

**1. Operational Stance:**
*   **Firewall:** Operates **Inline** (in the path of traffic). Applies strict access control rules (allow/deny) based on IP, ports, or protocols.
*   **IDS (Intrusion Detection System):** Operates **Passive / Out-of-band**. It receives copies of network traffic via a SPAN/Mirror port, analyzes it securely, but cannot stop transit itself.
*   **IPS (Intrusion Prevention System):** Operates **Inline**. Analyzes traffic deeply for malicious signatures/anomalies and stops threats dynamically.

**2. Primary Actions on Threat Detection:**
*   **Firewall:** Discards / drops packets that violate hardcoded policy ACLs (Access Control Lists).
*   **IDS:** Triggers an alert or logs the event to a SIEM system to notify an administrator. (No physical blocking action).
*   **IPS:** Actively blocks, actively mitigates, drops the malicious packets, or resets the TCP connection in real-time.

---

## Question Four (10 Points) - Terminology & Concepts
> **📺 YouTube Search Keyword:** *"Cryptography terminology RSA MAC SPN block ciphers"*

### Part a) Terminology Fill-in-the-Blanks (5 Points)
1. **Answer:** Hash Function (or Cryptographic Hash)
2. **Answer:** Certificate Authority (CA)
3. **Answer:** Avalanche Effect
4. **Answer:** Key Distribution Center (KDC)
5. **Answer:** TLS Record Protocol

### Part b) True or False (5 Points)

1. **FALSE**
   *   **Correction:** AES uses a Substitution-Permutation Network (SPN) structure, which requires *different* algorithms for encryption and decryption (e.g., ShiftRows vs InvShiftRows). DES uses a Feistel structure.
2. **TRUE** 
   *   *(The sender signs with their private key, so anyone can verify it with their public key).*
3. **FALSE**
   *   **Correction:** Message Authentication Codes (MAC) provide integrity and authentication, but **NOT** non-repudiation because the key is symmetrically shared between both parties (either party could have forged it). Digital Signatures provide non-repudiation.
4. **TRUE** 
   *   *(The Handshake protocol does the heavy lifting of key exchange and certificates before handing off to the Record protocol).*
5. **FALSE**
   *   **Correction:** DES uses a block size of **64 bits**, (while AES uses a 128-bit block). DES does indeed have a 64-bit key with 8 parity bits acting as an effective 56-bit key.
