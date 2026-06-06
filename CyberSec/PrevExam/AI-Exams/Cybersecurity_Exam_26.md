# Exam 26
## CCY2001: Introduction to Cybersecurity

**Total Points: 40**
**Total Estimated Time: 60 minutes**

---

## Question One (10 Points) - Symmetric Ciphers & Block Operations 
*(Estimated Time: 15 mins)*

**a) Vigenere Cipher Operations (4 Points)**
Encrypt the plaintext "SECURE SYSTEM" using the Vigenere cipher with the keyword "CYBER". Show your work and the calculation for each letter. 
*(Hint: A=0, B=1, ... Z=25)*

**b) Principles of Confusion and Diffusion (6 Points)**
Claude Shannon introduced the concepts of Confusion and Diffusion to prevent statistical analysis of ciphertexts. 
1. Define **Confusion** and **Diffusion**. 
2. Briefly explain how AES (Advanced Encryption Standard) achieves both concepts compared to DES (Data Encryption Standard). Mention specific operations/layers in your explanation.

---

## Question Two (10 Points) - Asymmetric Encryption & Digital Signatures 
*(Estimated Time: 15 mins)*

**a) RSA Key Exchange and Encryption (5 Points)**
Assume you are setting up an RSA encryption system. You select two prime numbers: **p = 5** and **q = 11**, and choose a public exponent **e = 3**.
1. Calculate the modulus **n** and the Euler’s totient **Φ(n)**.
2. Calculate the private exponent **d**.
3. Using the public key, encrypt the message **M = 8**. Show your mathematical steps.

**b) Secure Communications Architecture (5 Points)**
Alice wants to send a sensitive and authenticated document to Bob over an insecure channel. She decides to use a combination of Symmetric Encryption, Hashing, and Asymmetric Encryption to achieve both **Confidentiality** and **Non-repudiation**. 
Draw a block diagram OR write out the exact step-by-step cryptographic sequence Alice performs to secure the message, and the sequence Bob performs to verify and read it upon receiving.

---

## Question Three (10 Points) - Network Security Protocols & Architecture
*(Estimated Time: 15 mins)*

**a) IPSec Architecture: Transport vs Tunnel Mode (5 Points)**
IPSec provides security at the network layer. 
Explain the structural difference between **Transport Mode** and **Tunnel Mode**. Support your answer by sketching the packet structure for both modes when using ESP (Encapsulating Security Payload).

**b) Network Defense Systems: Firewall vs IDS vs IPS (5 Points)**
In incident response and network architecture, Firewalls, Intrusion Detection Systems (IDS), and Intrusion Prevention Systems (IPS) play different roles.
1. Compare their primary operational functions (Inline vs Passive).
2. State the primary action each system takes when malicious traffic is detected on a network.

---

## Question Four (10 Points) - Terminology & Concepts
*(Estimated Time: 15 mins)*

**a) Terminology Fill-in-the-Blanks (5 Points)**
Provide the proper scientific term for the following definitions:
1. An algorithm that takes a variable-length message and produces a fixed-length output (digest).
2. The trusted entity responsible for issuing, verifying, and signing X.509 digital certificates.
3. A property of modern hash functions where changing just a single bit of the input produces a drastically different hash output.
4. A trusted third-party server that both generates and distributes symmetric session keys to communicating entities.
5. The specific TLS/SSL sub-protocol responsible for encrypting, MAC-tagging, and compressing application data.

**b) True or False (5 Points)**
Identify whether the following statements are True or False. **If False, correct the statement**:
1. AES uses a Feistel network structure for its encryption and decryption rounds, which allows the decryption algorithm to be identical to the encryption algorithm.
2. In public-key cryptography, a digital signature is verified using the sender's public key.
3. Message Authentication Codes (MAC) provide non-repudiation because they use a shared secret key.
4. The SSL/TLS Handshake protocol handles the initial authentication, cipher suite negotiation, and establishment of a shared symmetric key.
5. DES uses a block size of 128 bits and an effective key length of 56 bits.
