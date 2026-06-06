# Exam 23 - Detailed Guide Answers
## CCY2001: Introduction to Cybersecurity

---

## Question One (12 Points) - Symmetric Encryption & Block Ciphers
> **📺 YouTube Search Keyword:** *"Vigenere Autokey cipher and AES ShiftRows explained"*

### Part a) Vigenere Autokey Encryption (4 Points)
**Question:** Encrypt "attack will occur tomorrow" using your last name as a keyword.

**Answer Approach:**

The Vigenere Autokey cipher is a variation of the Vigenere cipher where the plaintext itself becomes part of the key.

**Steps:**
1. **Prepare the plaintext:** Remove spaces: `ATTACKWILLOCCURTOMORROW`
2. **Prepare the key:** 
   - Start with your last name (e.g., if last name is "SMITH"): `SMITH`
   - Then append the plaintext: `SMITH` + `ATTACKWILLOCCURTOMORR` = `SMITHATTACKWILLOCCURTO`
3. **Encryption formula:** 
   - For each plaintext letter position: `C = (P + K) mod 26`
   - Where P = plaintext letter position (A=0, B=1, ... Z=25)
   - K = key letter position
4. **Example calculation:**
   ```
   Plaintext:  A T T A C K W I L L O C C U R T O M O R R O W
   Key:        S M I T H A T T A C K W I L L O C C U R T O M
   Ciphertext: S H B T J K Q B L N Y Y U F C I Q O C I I G I
   ```

**Key Concept:** In Vigenere Autokey, the plaintext becoming part of the key makes it more secure than regular Vigenere cipher because the key pattern is less repetitive.

---

### Part b) AES-128 Substitution & Shift Rows Operations (8 Points)
**Question:** Encrypt the first 16 letters of your full name (in ASCII-hex) using SubBytes and ShiftRows.

**Answer Approach:**

**Step 1: Prepare the plaintext**
- Take first 16 letters of your name (if less than 16, repeat)
- Example: "Ahmed Moumen abdo" → "AHMEDMOUMENABDOA"
- Convert each character to ASCII then to hexadecimal

**Example ASCII-Hex Conversion:**
```
A = 65 (decimal) = 41 (hex)
H = 72 (decimal) = 48 (hex)
M = 77 (decimal) = 4D (hex)
E = 69 (decimal) = 45 (hex)
D = 68 (decimal) = 44 (hex)
M = 77 (decimal) = 4D (hex)
O = 79 (decimal) = 4F (hex)
U = 85 (decimal) = 55 (hex)
M = 77 (decimal) = 4D (hex)
E = 69 (decimal) = 45 (hex)
N = 78 (decimal) = 4E (hex)
A = 65 (decimal) = 41 (hex)
B = 66 (decimal) = 42 (hex)
D = 68 (decimal) = 44 (hex)
O = 79 (decimal) = 4F (hex)
A = 65 (decimal) = 41 (hex)
```

**Step 2: Create State Array (4×4)**
```
Initial State Array:
| 41 | 48 | 4D | 45 |
| 44 | 4D | 4F | 55 |
| 4D | 45 | 4E | 41 |
| 42 | 44 | 4F | 41 |
```

**Step 3: Apply SubBytes Operation**
- Use the AES S-Box substitution table
- Each hexadecimal value is replaced according to the S-Box
- The first hex digit indicates row, second indicates column
- Example: `41` → Row 4, Column 1 → (Look up in S-Box) → Result value

**Simplified S-Box Example (showing concept):**
For each byte, look up the substitution:
```
Example: 41 → S[4][1] (from standard S-Box)
```

**Step 4: After SubBytes (Substituted State Array)**
```
| Sub[41] | Sub[48] | Sub[4D] | Sub[45] |
| Sub[44] | Sub[4D] | Sub[4F] | Sub[55] |
| Sub[4D] | Sub[45] | Sub[4E] | Sub[41] |
| Sub[42] | Sub[44] | Sub[4F] | Sub[41] |
```

**Step 5: Apply ShiftRows Operation**
The ShiftRows operation shifts each row:
- Row 0: No shift
- Row 1: Shift left by 1 byte
- Row 2: Shift left by 2 bytes
- Row 3: Shift left by 3 bytes

**Result after ShiftRows:**
```
| Sub[41] | Sub[48] | Sub[4D] | Sub[45] |  (Row 0 - no shift)
| Sub[4D] | Sub[4F] | Sub[55] | Sub[44] |  (Row 1 - shift left by 1)
| Sub[4E] | Sub[41] | Sub[4D] | Sub[45] |  (Row 2 - shift left by 2)
| Sub[41] | Sub[42] | Sub[44] | Sub[4F] |  (Row 3 - shift left by 3)
```

**Key Concepts:**
- **SubBytes:** Provides confusion (makes relationship between ciphertext and key complex)
- **ShiftRows:** Provides diffusion (spreads each plaintext bit over multiple ciphertext bits)

---

## Question Two (8 Points) - RSA Key Exchange
> **📺 YouTube Search Keyword:** *"RSA Key Exchange Authentication and Secrecy"*

**Question:** Use RSA to securely exchange a DES key with authentication and secrecy.

**Given:**
- Your keys: PRA = {41, 133}, PUA = {29, 133}
- Friend's keys: PRB = {23, 187}, PUB = {7, 187}
- DES key: First 8 letters of your name in ASCII

**Answer Approach:**

**Step 1: Prepare the DES Key**
- Convert first 8 letters to ASCII decimal
- Example: "AHMEDMOU" (from Ahmed Moumen) → A(65) H(72) M(77) E(69) D(68) M(77) O(79) U(85)
- Combine into a single number (or encrypt in blocks)

**Step 2: Achieve Both Secrecy and Authentication**

For both secrecy AND authentication using RSA:
1. **First, Sign the message with your private key** (Authentication):
   - `S = M^d_A mod n_A`
   - `S = M^41 mod 133`

2. **Then, Encrypt the signed message with friend's public key** (Secrecy):
   - `C = S^e_B mod n_B`
   - `C = S^7 mod 187`

**Step 3: Detailed Calculation Example**
```
Let's say DES key M = 100 (simplified for example)

Step 1: Sign with your private key (authentication)
S = 100^41 mod 133
  = (100^32 × 100^8 × 100^1) mod 133

  *Detailed Square-and-Multiply Step:*
  - 100^1 mod 133 = 100
  - 100^2 mod 133 = 10000 mod 133 = 25
  - 100^4 mod 133 = 25^2 mod 133 = 625 mod 133 = 93
  - 100^8 mod 133 = 93^2 mod 133 = 8649 mod 133 = 4
  - 100^16 mod 133 = 4^2 mod 133 = 16
  - 100^32 mod 133 = 16^2 mod 133 = 256 mod 133 = 123

  *Final Calculation:*
  S = (123 × 4 × 100) mod 133
  S = 49200 mod 133 = 123
  → Signature S = 123

Step 2: Encrypt with friend's public key (secrecy)
C = 123^7 mod 187
  = (123^4 × 123^2 × 123^1) mod 187
  = (137 × 169 × 123) mod 187
  = 183
  → Final ciphertext C = 183
```

**Step 4: What Your Friend Receives and Does**

Your friend will:
1. Decrypt with their private key: `S = C^23 mod 187`
2. Verify with your public key: `M = S^29 mod 133`

**Key Security Properties:**
- **Secrecy:** Only friend can decrypt (has private key PRB)
- **Authentication:** Only you could have signed it (only you have private key PRA)
- **Non-repudiation:** You cannot deny signing it later

---

## Question Three (6 Points) - Security Block Diagrams
> **📺 YouTube Search Keyword:** *"Cryptography block diagrams: Confidentiality Authentication Digital Signatures TLS"*

### Part a) Confidentiality & Authentication (2 Points)
**Requirement:** Ensure Bob knows the message is from Alice AND nobody else can read it.

**Solution:** Use public-key cryptography with both encryption and digital signature

**Block Diagram:**
```
Alice's Side (Sending):
Plaintext Message
    ↓
[Sign with Alice's Private Key]
    ↓
[Encrypt with Bob's Public Key]
    ↓
Ciphertext sent to Bob

Bob's Side (Receiving):
Ciphertext
    ↓
[Decrypt with Bob's Private Key]
    ↓
[Verify signature with Alice's Public Key]
    ↓
Plaintext Message (VERIFIED from Alice)
```

**Protocol:**
1. Alice signs the message with her private key → provides authentication
2. Alice encrypts the signed message with Bob's public key → provides confidentiality
3. Bob decrypts with his private key
4. Bob verifies signature with Alice's public key

---

### Part b) Symmetric Encryption with Digital Signature (2 Points)
**Requirement:** Confidential + digitally signed message using symmetric encryption + hash

**Block Diagram:**
```
Alice's Side:
Message
    ↓
[Hash Function (SHA/MD5)]
    ↓
Hash Value
    ↓
[Sign Hash with Alice's Private Key] (Digital Signature)
    ↓
Message + Digital Signature
    ↓
[Encrypt with Symmetric Key (AES)]
    ↓
Encrypted Message + Signature

Send Encrypted Message + Signature to Bob
Also: Send Symmetric Key encrypted with Bob's Public Key

Bob's Side:
Encrypted Message
    ↓
[Get Symmetric Key from Alice's encrypted message using Bob's Private Key]
    ↓
[Decrypt Message with Symmetric Key]
    ↓
Message + Digital Signature
    ↓
[Verify Signature using Alice's Public Key]
    ↓
[Compute Hash of Received Message]
    ↓
[Compare computed hash with decrypted hash]
    ↓
Message VERIFIED and Confidential
```

**Key Exchange:**
- Symmetric key is encrypted with Bob's public key
- Only Bob can decrypt it with his private key

---

### Part c) TLS/SSL Connection (Server-Client) (2 Points)
**Requirement:** AES + MAC(SHA512) over connection-oriented protocol, no pre-shared certificates

**Block Diagram:**
```
Client ←→ Server (TCP Connection)

1. Handshake Phase (without pre-shared certs):
   - Client generates random number RC
   - Server generates random number RS
   - Use Diffie-Hellman or similar to establish shared secret

2. Symmetric Key Derivation:
   Random Numbers (RC + RS)
        ↓
   [Key Derivation Function]
        ↓
   Shared Symmetric Key

3. Data Transfer Phase:
   Application Data
        ↓
   [AES Encryption with Symmetric Key]
        ↓
   Encrypted Data
        ↓
   [MAC using SHA512 on (Encrypted Data + Sequence Number)]
        ↓
   Encrypted Data + MAC Tag
        ↓
   Send over TCP

4. Receiving Side:
   Encrypted Data + MAC Tag
        ↓
   [Verify MAC using SHA512]
        ↓
   [Decrypt using AES with Symmetric Key]
        ↓
   Original Application Data
```

**Protocol Details:**
- Uses connection-oriented protocol (TCP)
- AES provides confidentiality
- MAC-SHA512 provides message integrity
- Handshake establishes shared symmetric key without pre-shared certificates

---

## Question Four (14 Points) - Multiple Choice & Concept Questions

### Part a) Feistel Cipher Design Features (2 Points)
**Correct Answers: (i) and (ii)**

**Explanation:**

**(i) Greater complexity of the round function means greater resistance to cryptanalysis** ✓
- **TRUE:** This is a fundamental principle of Feistel cipher design. The round function F is responsible for the security. Greater complexity in F makes cryptanalysis harder.
- **Lecture Reference:** "Greater complexity generally means greater resistance to cryptanalysis"

**(ii) The decryption algorithm is independent of the round function** ✓
- **TRUE:** One of Feistel's key advantages is that the decryption algorithm has exactly the same structure as encryption. Both use the same round function F.
- **Lecture Reference:** "The same steps, with the same key, are used to reverse the encryption"
- **Formula:** 
  - Encryption: $R_i = L_{i-1} \oplus F(R_{i-1}, K_i)$ and $L_i = R_{i-1}$
  - Decryption: Uses the same formula but processes ciphertext

**(iii) Larger key size will increase encryption/decryption speeds** ✗
- **FALSE:** Larger key sizes DECREASE speed (takes more time to process). Greater security comes at the cost of reduced speed.
- **Lecture Reference:** "Larger key size means greater security but may decrease encryption/decryption speeds"

**(iv) Larger block size will increase encryption/decryption speeds** ✗
- **FALSE:** Larger block sizes mean GREATER SECURITY but REDUCED SPEED.
- **Lecture Reference:** "Larger block sizes mean greater security but reduced encryption/decryption speed"

---

### Part b) SHA-512 Hash Function Properties (2 Points)
**Correct Answers: (iii) and (iv)**

**(i) Every bit of the hash code is unique and not a function of the input** ✗
- **FALSE:** Every bit IS a function of the input (see answer iv)

**(ii) Only one bit of the hash code is a function of the input** ✗
- **FALSE:** Every bit is a function of the entire input

**(iii) Changing one bit of the input will change the whole hash code** ✓
- **TRUE:** This is the Avalanche Effect property of cryptographic hash functions
- **Important:** Small change in input produces dramatically different hash output
- This makes hash functions extremely sensitive to input changes

**(iv) Every bit of the hash code is a function of every bit of the input** ✓
- **TRUE:** This is another manifestation of the avalanche effect
- Each output bit depends on all input bits
- This ensures strong diffusion property

**Cryptographic Property:** These properties (avalanche effect and diffusion) make SHA-512 suitable for:
- Digital signatures
- Data integrity verification
- Password hashing

---

### Part c) False Statement About DES (1 Point)
**Correct Answer: (ii)**

**(i) Based on Feistel Structure** ✓
- TRUE: DES is explicitly based on Feistel cipher structure
- Reference: "Data are encrypted in 64-bit blocks using a 56-bit key based on Feistel Cipher Concept"

**(ii) Use a key of 56-bit length in each round** ✗
- **FALSE:** DES uses a 56-bit key, but it generates different 48-bit subkeys for each round (not 56-bit)
- Key Schedule: Initial key (64-bit with parity) → 56-bit after PC1 → 48-bit for each round through PC2
- Reference: "Initial Permutation of the key (PC1) which selects 56-bits in two 28-bit halves"
- Then "Selecting 24-bits from each half" (total 48-bits) for function F

**(iii) Has initial symmetric key of 64-bits** ✓
- TRUE: DES starts with a 64-bit key (includes 8 parity bits, resulting in 56 usable bits)

**(iv) Has a good Avalanche effect** ✓
- TRUE: DES demonstrates strong avalanche effect
- Reference: "A small change in either the plaintext or the key should produce a significant change in the ciphertext"

---

### Part d) True Statement About AES (1 Point)
**Correct Answer: Needs clarification - likely (d) Use different algorithms for decryption**

**(a) Its encryption algorithm needs more time than DES** ✗
- Generally FALSE: AES is typically faster than DES despite being more secure
- AES uses efficient operations (ShiftRows, MixColumns designed to be hardware-efficient)

**(b) The plaintext block size is varied according to AES-128, AES-192, and AES-256** ✗
- FALSE: All AES variants use a FIXED 128-bit block size
- Only the KEY SIZE varies (128, 192, or 256 bits)
- The numbers (128/192/256) refer to key size, not block size

**(c) Use fixed number of rounds independent of the key size** ✗
- FALSE: Number of rounds DEPENDS on key size:
  - AES-128: 10 rounds
  - AES-192: 12 rounds
  - AES-256: 14 rounds

**(d) Use different algorithms for decryption** ✓
- TRUE: Unlike Feistel-based ciphers (like DES), AES uses structurally different encryption and decryption algorithms
- AES uses InvShiftRows, InvSubBytes, InvMixColumns for decryption
- This is a fundamental difference from DES

---

## Summary of Key Concepts

### Confusion and Diffusion
- **Confusion:** Makes relationship between ciphertext and key complex (e.g., SubBytes in AES)
- **Diffusion:** Spreads plaintext information across ciphertext (e.g., ShiftRows, MixColumns in AES)

### DES vs AES
| Aspect | DES | AES |
|--------|-----|-----|
| **Structure** | Feistel-based | Substitution-Permutation Network |
| **Block Size** | 64-bit | 128-bit |
| **Key Size** | 56-bit | 128/192/256-bit |
| **Rounds** | 16 | 10/12/14 |
| **Round Function** | Same for encryption/decryption | Different for encryption/decryption |
| **Security** | Broken (too small key) | Secure (current standard) |

### RSA Security
- Relies on difficulty of factoring large numbers
- Current standard: 2048-bit modulus (617 decimal digits)
- Provides: Confidentiality, Authentication, Non-repudiation

---

### Part e) DES S-Box Question (1 Point)
**Question:** Suppose that the input of the 5th S-box of the DES algorithm is (110110), then the output of this S-box will be:

**Correct Answer: (iv) 1110**

**Explanation:**
The DES algorithm uses 8 substitution boxes (S-boxes 1-8). Each S-box takes a 6-bit input and produces a 4-bit output.

**For S-box 5 with input 110110:**
1. **Extract row and column bits:**
   - Row = First and Last bits = 1 and 0 = binary 10 = decimal 2
   - Column = Middle 4 bits = 1011 = decimal 11

2. **Look up in S-box 5 table:**
   - Row 2, Column 11 of S-box 5
   - The value at this position is 14 in decimal = 1110 in binary

3. **Output:** 1110 (4 bits)

**Key Concept:** Each DES S-box is a fixed lookup table designed to provide non-linear substitution, which is crucial for the security of DES.

**Common mistakes to avoid:**
Students often confuse the row/column extraction method or use the wrong S-box table. Remember: row uses the outer bits (first and last), column uses the inner 4 bits.

---

### Part f) Message Authentication Code Purpose (1 Point)
**Question:** Message Authentication Code is a security mechanism to achieve:

**Correct Answer: (i) Peer-entity Authentication and (iii) Data Integrity**

**(i) Peer-entity Authentication** ✓
- **TRUE:** MAC proves that a message came from a legitimate peer who possesses the secret key
- This provides authentication (knowing who sent the message)

**(ii) Data Origin Authentication** ✗
- Related but not the primary purpose listed in standards
- Authentication of data origin is achieved through digital signatures, not just MAC

**(iii) Data Integrity** ✓
- **TRUE:** MAC detects any modification to the message during transmission
- If any bit changes, the MAC value will not match
- Formula: MAC = HASH(Key | | Message)
- Even a single bit change in the message produces a completely different MAC (avalanche effect)

**(iv) Digital Signature** ✗
- FALSE: MAC is NOT a digital signature
- **Key difference:**
  - MAC: Uses shared secret key (symmetric)
  - Digital Signature: Uses private/public key pair (asymmetric)
  - MAC does not provide non-repudiation
  - Digital signature provides non-repudiation

**Lecture Reference:** "Message Authentication Code provides both peer-entity authentication and message integrity assurance"

---

### Part g) Public-Key Cryptography Uses (1 Point)
**Question:** Public-Key Cryptography can be used to achieve the following security services / mechanisms except one which is:

**Correct Answer: (iv) Secure chat application**

**(i) Key Exchange** ✓
- **TRUE:** Public-key cryptography is excellent for key exchange
- Example: RSA, Diffie-Hellman
- Used in TLS/SSL handshake to exchange symmetric keys

**(ii) Data Origin Authentication** ✓
- **TRUE:** Digital signatures (using private key) authenticate the source
- Receiver verifies with sender's public key

**(iii) Data Integrity** ✓
- **TRUE:** Digital signatures guarantee integrity
- Any modification is detected when verification fails

**(iv) Secure chat application** ✗
- **FALSE:** This is NOT a typical use of public-key cryptography alone
- **Why?** Public-key cryptography is too slow for real-time bulk message encryption
- **Solution in practice:** Use public-key for authentication and key exchange, then use symmetric encryption for actual message content
- Secure chat apps use: RSA/ECDH (key exchange) + AES (message encryption)

**Lecture Reference:** "Public-key cryptography is computationally expensive and is primarily used for key exchange and digital signatures, not for bulk data encryption in real-time applications"

---

### Part h) SHA Algorithm Concept (1 Point)
**Question:** The Secure Hash Algorithm (SHA) depends on the concept of:

**Correct Answer: (ii) Symmetric Block Cipher** (or potentially (iv) depending on curriculum emphasis)

**(i) Cipher Block Chain** ✗
- FALSE: CBC is a mode of operation for block ciphers, not the underlying concept of SHA

**(ii) Symmetric Block Cipher** ✓
- **TRUE:** SHA internally uses block cipher concepts
- SHA uses iterative compression function similar to block cipher chaining
- Process: Divide input into blocks → Process each block iteratively → Produce hash output
- Reference: "SHA uses a Merkle-Damgård construction with iterative block processing"

**(iii) Asymmetric Encryption** ✗
- FALSE: SHA is symmetric (not dependent on public/private key pairs)
- SHA produces a fixed-size hash regardless of input

**(iv) Message Authentication Code** ✗
- FALSE: This is reversed — MAC depends on hash functions, not the other way around
- MAC = HASH(Key | | Message)

**Key Concept:** SHA (along with MD5) are cryptographic hash functions that use symmetric block cipher principles for their construction, particularly the concept of iterative chaining and substitution-permutation networks.

---

### Part i) X.509 Certificate Signing (1 Point)
**Question:** X.509 Certificate of public key is digitally signed by:

**Correct Answer: (iii) Certificate Authority Private Key**

**(i) User Private Key** ✗
- FALSE: The user's private key is NEVER included or used to sign the certificate
- Private keys must remain secret

**(ii) User Public Key** ✗
- FALSE: Signing with a public key is not cryptographically sound
- Public keys cannot be used for signing (they're for verification only)

**(iii) Certificate Authority Private Key** ✓
- **TRUE:** The CA uses its own private key to digitally sign the X.509 certificate
- This creates the signature chain of trust:
  1. CA takes the certificate data (including user's public key)
  2. CA hashes it: HASH(Certificate_Data)
  3. CA signs the hash with its private key: Signature = HASH^CA_Private_Key
  4. This signature is attached to the certificate

**(iv) Certificate Authority Public Key** ✗
- FALSE: Public key cannot be used for signing

**Trust Model:**
```
User wants to verify a certificate:
1. Get CA's public key (from browser/OS trust store)
2. Use CA's public key to verify the signature
3. If verification succeeds → Certificate is authentic
4. User can now trust the user's public key in the certificate
```

**Lecture Reference:** "X.509 certificates form a chain of trust where a higher-level CA digitally signs the certificate of a lower-level entity"

---

### Part j) X.509 Certificate Content (1 Point)
**Question:** X.509 Certificate of public key does not contain one of the following:

**Correct Answer: (i) User Private Key**

**(i) User Private Key** ✓
- **DOES NOT CONTAIN:** User private key is NEVER included in any certificate
- Violates fundamental security principle: private keys must remain secret
- Even the CA does not know or store the user's private key

**(ii) User Public Key** ✗
- **CONTAINS:** This is the primary content of the certificate
- The public key is explicitly included so others can use it for encryption/verification

**(iii) User Name and ID** ✗
- **CONTAINS:** Certificate includes Distinguished Name (DN) with:
  - Common Name (CN)
  - Organization (O)
  - Country (C)
  - Other identifying information

**(iv) Certificate Serial Number** ✗
- **CONTAINS:** Every X.509 certificate has a unique serial number assigned by the CA
- Used for certificate revocation (CRL), expiration tracking, etc.

**Typical X.509 Certificate Contents:**
```
- Version
- Serial Number
- Signature Algorithm
- Issuer (CA information)
- Validity (NotBefore, NotAfter dates)
- Subject (User information)
- Subject Public Key Info (THE PUBLIC KEY)
- Extensions (key usage, extended key usage, etc.)
- Signature (CA's digital signature)
```

---

### Part k) Fill-in-the-Blank Terminology (10 Points)
**Question:** Write the scientific term according to each of the following:

**Answers:**

**(i) A property in the encryption algorithm that makes each plaintext digit affect the value of many ciphertext digits:**
- **Answer:** Diffusion (or Diffusion property)
- **Explanation:** Diffusion spreads the influence of each input bit across many output bits, making patterns difficult to detect. Example: AES ShiftRows and MixColumns operations provide diffusion.

**(ii) A technique in the encryption algorithms in which each plaintext element is replaced by a new corresponding ciphertext element:**
- **Answer:** Substitution (or Substitution technique / Substitution-Permutation)
- **Explanation:** Each plaintext letter/byte is replaced with a different ciphertext letter/byte. Examples: S-boxes in DES and AES, Vigenère cipher.

**(iii) Generate the message hash code and encrypt it with user private key is a security mechanism that is called:**
- **Answer:** Digital Signature (or Digital Signature Scheme)
- **Explanation:** 
  - Process: Message → Hash → Encrypt with Private Key → Signature
  - Provides: Authentication, Non-repudiation, Integrity
  - Verification: Decrypt with Public Key → Compare with newly computed hash

**(iv) The most secure way to distribute the public key is:**
- **Answer:** Public-Key Certificate (or X.509 Certificate / PKI / Certificate Authority)
- **Explanation:** Certificates are digitally signed by trusted Certificate Authorities, preventing forgery or impersonation. More secure than sending plain public keys.

**(v) Protocol for secure network communications designed to be relatively simple:**
- **Answer:** SSL/TLS (or Transport Layer Security / Secure Sockets Layer)
- **Explanation:** TLS is the standard protocol for secure internet communication, running at layer 4-5. Simpler design compared to more complex security protocols.

**(vi) Protocol that encapsulate the whole datagram into another datagram to hide the original datagram parameters:**
- **Answer:** IPSec (or IP Security / IPSec Protocol)
- **Explanation:** IPSec encrypts and encapsulates IP datagrams, providing end-to-end security at the network layer. Hides original source/destination IPs and payload.

**(vii) A trusted third party that generate session keys and distribute them to different entities so they can communicate securely:**
- **Answer:** KDC (Key Distribution Center) or Key Server
- **Explanation:** KDC generates and distributes symmetric session keys. Used in Kerberos authentication protocol and corporate security systems.
- **Related term:** KTC (Key Translation Center) — similar but may also translate/convert keys.

**(viii) A function that seems to be irreversible without knowing a certain value:**
- **Answer:** One-way function (or Trapdoor function / One-way hash function)
- **Explanation:** Without the secret key (trapdoor), the function cannot be reversed. Examples: Hash functions (SHA, MD5), modular exponentiation in RSA.

**(ix) A security mechanism that use a secret code concatenated with the message and inputted to a hash algorithm to obtain a secure hash code:**
- **Answer:** HMAC (Hash-based Message Authentication Code) or Message Authentication Code (MAC)
- **Explanation:** Formula: HMAC = HASH(Key | | Message). Provides both authentication and integrity.

**(x) A property in the hash algorithm that makes it computationally infeasible to find any pair of data inputs that gives the same hash code:**
- **Answer:** Collision Resistance (or Second Preimage Resistance)
- **Explanation:** It should be computationally infeasible to find two different inputs that produce the same hash output. This ensures unique identification and prevents forgery.
- **Related:** Preimage Resistance (hard to find input given hash), Avalanche Effect (small change in input → big change in output)

---

### Part l) True/False Statements with Correction (5 Points)
**Question:** Which ones of the following sentences are right and which are wrong? If it's wrong, correct the sentence:

**Answers:**

**(i) Although DES has been considered unsecure algorithm and possibly broken, a modified version called Triple-DES are used till now and considered as secure.**

**Status:** ✓ **TRUE** (with minor correction)

**Explanation:**
- This statement is essentially correct
- **Minor detail:** Triple-DES (3DES or TDEA) uses three DES encryptions with two or three different keys
- **Correction (if needed):** "Although DES has been considered an insecure algorithm and possibly broken, a modified version called Triple-DES is still used in some legacy systems and was considered secure (though now being phased out by AES)"
- **Current status:** 3DES is being deprecated — NIST discontinued support as of December 31, 2023
- **Lecture reference:** "Triple-DES applies DES encryption three times with two or three different keys"

---

**(ii) The difference between the Key Translation Center (KTC) and the Key Distribution Center (KDC) is that the KTC can translate the session key while the KDC can distribute the session key. But no one of them can generate that key.**

**Status:** ✗ **FALSE**

**Correction:**
"The difference between the Key Translation Center (KTC) and the Key Distribution Center (KDC) is that the KTC can translate/convert session keys from one format to another, while the KDC both generates AND distributes session keys to different entities for secure communication."

**Explanation:**
- **KDC (Key Distribution Center):**
  - Generates session keys
  - Distributes session keys to authenticated entities
  - Example: Kerberos KDC
  - Actively creates and manages keys

- **KTC (Key Translation Center):**
  - Translates/converts existing keys
  - May convert between different encryption formats
  - Does NOT generate new keys (as stated)
  - More passive role

- **Error in original statement:** Claims neither can generate keys — this is FALSE for KDC
- **Correct statement:** KDC generates and distributes; KTC translates existing keys

---

**(iii) The life time of the symmetric key is related to how often you use that key. The more you use it the more you can keep it.**

**Status:** ✗ **FALSE**

**Correction:**
"The lifetime of the symmetric key is inversely related to how often you use it. The more frequently you use a key, the shorter its cryptographic lifetime should be and the sooner it should be replaced. This is because increased usage increases the risk of compromise through cryptanalysis."

**Explanation:**
- **Correct principle:** Key lifetime is inversely proportional to usage frequency
- **Reasoning:**
  - Frequent use increases ciphertext available for cryptanalysis
  - More encrypted messages = more data for attackers to analyze
  - Increases probability of key compromise
  - Higher usage = shorter key lifetime recommended

- **Best practice:** 
  - Heavy-use keys: Replace daily or weekly
  - Light-use keys: May be kept for months or years
  - Session keys: Typically last minutes to hours

- **Original error:** Statement reversed the relationship

---

**(iv) Public-key certificate is the most trusted way to distribute public-keys because no one can forge this certificate. So you can send it to any one over unsecure network.**

**Status:** ✓ **MOSTLY TRUE** (with important clarification)

**Explanation:**
- **Correct part:** Certificates are digitally signed by trusted Certificate Authorities, making them extremely difficult to forge
- **Important clarification:** "Public-key certificates can be securely distributed over unsecure networks ONLY because they are digitally signed by trusted Certificate Authorities. The signature itself prevents forgery. However, it is important that the CA's public key (used to verify the certificate) is obtained from a trusted source."

**More complete answer:**
"Yes, certificates can be sent over insecure networks because:
1. The certificate contains a digital signature from the CA
2. Forging a signature requires the CA's private key (which is secret)
3. The recipient can verify authenticity using the CA's public key
4. The CA's public key is distributed through a trust chain (browser/OS trust stores)
5. Even if intercepted, the certificate cannot be altered without detection"

**Important caveat:**
- Trust ultimately relies on secure distribution of the CA's root public key
- Browsers and operating systems maintain trusted root CA certificates
- If the CA's key is compromised, the entire chain of trust fails

---

**(v) The Secure Hash Algorithm (SHA-1) has been considered "broken algorithm", so NIST developed (SHA-2) and began the process to complement it with (SHA-3) for certain applications.**

**Status:** ✓ **TRUE**

**Explanation:**
- **SHA-1 status:** Cryptographically broken and unsuitable for further use as of 2020
  - Hash collision attacks demonstrated
  - NIST officially deprecated SHA-1 as of January 1, 2011
  - Major browsers stopped accepting SHA-1 certificates after 2017

- **SHA-2 development:** NIST developed SHA-2 family in 2001
  - Includes: SHA-224, SHA-256, SHA-384, SHA-512
  - Much stronger than SHA-1
  - Currently secure and recommended (as of 2024)

- **SHA-3 development:** NIST held a competition and selected SHA-3 in 2012
  - Provides additional security margin
  - Different construction (Sponge construction vs Merkle-Damgård)
  - Used for specific applications requiring higher security levels
  - Optional for general purposes (SHA-2 still recommended for most uses)

- **Timeline:**
  ```
  2005: SHA-1 vulnerabilities published
  2011: SHA-1 deprecated by NIST
  2015: Major browsers stop supporting SHA-1
  2017: Practical collision attacks demonstrated
  2020: SHA-1 officially broken for all uses
  ```

**Lecture reference:** "NIST has recommended the use of SHA-2 and is developing SHA-3 for future applications requiring enhanced security"

---
