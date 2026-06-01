# WM242 Implementing Secure Systems — Study Guide

**Module:** WM242 | **Year:** 2 | **Generated:** June 2026
**Atomic notes:** [[MOC WM242 Implementing Secure Systems]]
**Status:** Phase 1 complete

> This is the readable version. Read this to learn. Use the Concepts notes to query and link.
> Everything here is explained with analogies and examples — no walls of jargon.

---

## Part 1 — What Cryptography Is and Why It Exists

Cryptography is the science of securing communication. The word comes from the Greek *kryptos* (hidden) and *graphi* (information). At its core, it's about transforming information so that only the intended recipient can understand it.

Before we get into the mechanics, it helps to understand what we're protecting against. There are four core threats in any communication:

**Eavesdropping** — someone intercepts your message and reads it. Alice sends a love letter to Bob; Eve reads it in transit. Cryptography's answer: encrypt the message so Eve reads gibberish.

**Tampering** — someone intercepts your message and changes it. Alice sends a bank transfer for £100; Eve changes it to £10,000. Cryptography's answer: hashing and message authentication codes prove whether a message was altered.

**Impersonation** — someone pretends to be you. Eve sends Bob a message claiming to be Alice. Cryptography's answer: digital signatures prove the identity of the sender.

**Replay attacks** — someone captures a legitimate message and sends it again later. Cryptography's answer: timestamps and nonces (one-time values) make replays detectable.

The three pillars everything maps back to are the **CIA Triad**:
- **Confidentiality** — only authorised parties can read the data
- **Integrity** — data hasn't been altered
- **Availability** — the system works when you need it

Claude Shannon — the father of information theory — identified two principles that underpin every modern cipher. **Confusion** means making the relationship between the key and the ciphertext as complex as possible, so knowing the ciphertext tells you nothing about the key. **Diffusion** means spreading the influence of each plaintext character across the whole ciphertext, so patterns in the original message are hidden. Every strong cipher uses both. AES, which you'll meet shortly, is a masterclass in applying them.

---

## Part 2 — The First Ciphers (and Why They Failed)

The earliest ciphers were **substitution** ciphers — replace each letter with another. The most famous is the **Caesar cipher**, used by Julius Caesar, where every letter is shifted by a fixed number. Shift by 3 and A becomes D, B becomes E, and so on. Encryption is just `(x + n) mod 26`. Simple, elegant, and completely broken by modern standards — there are only 25 possible keys, so a computer breaks it instantly.

The **Vigenère cipher** improved on this by using a keyword. Each letter of the message is shifted by the corresponding letter of the keyword, so the same letter in the message gets encrypted differently each time the keyword cycles. Harder to break but still vulnerable to frequency analysis.

The **One-Time Pad** is theoretically unbreakable — XOR each character of the message with a truly random key of the same length, never reuse the key. The catch: the key must be genuinely random, as long as the message, and shared securely in advance. At scale, this is impractical.

**Transposition ciphers** work differently — the letters stay the same but their positions change. The **Rail Fence cipher** writes the message in a zigzag across N rows and reads off row by row. "SECRET MESSAGE" across 3 rails becomes "SESEERTESGCMA".

**Frequency analysis** is how you break substitution ciphers. In English, E appears roughly 13% of the time, T about 9%, A about 8%. Find the most frequent symbol in a ciphertext and it's likely E. Work outward from there. Al-Kindi, a 9th-century Arab scholar, invented this technique — it remained the primary cryptanalysis tool for centuries.

---

## Part 3 — Symmetric Cryptography (One Key for Both)

Symmetric cryptography uses a single secret key shared between sender and receiver. Think of a padlock where the same key locks and unlocks it. Fast, efficient, great for encrypting large amounts of data. The problem: how do you securely share that key in the first place?

### DES — The First Standard

**DES (Data Encryption Standard)** was developed by IBM in the early 1970s and became the US federal standard. It uses a **56-bit key** and a **64-bit block size**, structured as a **Feistel network** — a clever design where the same algorithm works for both encryption and decryption just by reversing the key schedule. Each of its 16 rounds splits the data in half, applies a function to the right half using a subkey, XORs the result with the left half, then swaps them.

The problem: 56 bits is too short. By the late 1990s, hardware had advanced to the point where all 2⁵⁶ possible keys could be searched in a matter of hours. DES is now considered obsolete.

### AES — The Current Standard

**AES (Advanced Encryption Standard)** was designed by Belgian cryptographers Vincent Rijmen and Joan Daemen, adopted by NIST in 2000, and is now used everywhere — HTTPS, VPNs, Wi-Fi, file encryption, messaging apps. Unlike DES it is not a Feistel network; it's a **substitution-permutation network** operating on a 4×4 matrix of bytes.

Key sizes are 128, 192, or 256 bits. The 128-bit version has 10 rounds, 192 has 12, 256 has 14. Each main round applies four operations:

1. **SubBytes** — every byte is replaced using a fixed lookup table (the S-box). This is confusion — the relationship between input and output is non-linear and complex.
2. **ShiftRows** — the rows of the 4×4 matrix are shifted left by 0, 1, 2, and 3 positions respectively. This moves bytes into different columns, spreading their influence.
3. **MixColumns** — each column is multiplied by a fixed matrix over a finite field. This is the heaviest diffusion step — one byte affects all four bytes in its column.
4. **AddRoundKey** — the state is XORed with the round subkey derived from the original key.

The **final round** skips MixColumns. The **initial round** only does AddRoundKey. This is a common exam question — know which operation is omitted in the final round.

### Modes of Operation

Block ciphers like AES encrypt exactly one fixed-size block at a time. Real messages are longer. Modes of operation define how you chain multiple block encryptions together:

**ECB (Electronic Code Book)** encrypts each block independently. The fatal flaw: identical plaintext blocks produce identical ciphertext blocks. Encrypt a bitmap image with ECB and the shapes are still visible in the ciphertext. Never use ECB for real data.

**CBC (Cipher Block Chaining)** XORs each plaintext block with the previous ciphertext block before encrypting. The first block uses a random Initialisation Vector (IV). Identical plaintexts now produce different ciphertexts. This is the most common mode for general use.

**CTR (Counter Mode)** encrypts a counter value and XORs it with the plaintext. Parallelizable — blocks can be encrypted simultaneously. Fast and flexible.

CFB and OFB use feedback mechanisms and are error-resilient — a corrupted bit in transmission doesn't cascade into corruption of later blocks.

When a message doesn't fill a complete final block, **padding** fills the gap. PKCS7 pads with N bytes each having the value N — if 3 bytes are needed, the padding is `03 03 03`.

---

## Part 4 — Hash Functions (One-Way Fingerprints)

A hash function takes any input and produces a fixed-length output — a fingerprint of the data. The best analogy is a meat grinder: put any amount of raw meat in, always get the same type of minced output. Put the same steak in twice, get identical mince. Put a slightly different steak in, get completely different mince. You can never reconstruct the original steak from the mince.

Three properties matter:

**One-way (Preimage Resistance):** Given a hash output h, it should be computationally infeasible to find any input that produces h. This is why passwords are stored as hashes rather than plaintext — even if the database is stolen, the attacker can't reverse the hashes to get the passwords.

**Collision Resistance:** It should be infeasible to find two different inputs that produce the same hash. If I can find a collision, I can substitute one document for another without the hash changing — devastating for digital signatures.

**Avalanche Effect:** A single bit change in the input produces a completely different output. SHA-256 of "hello" and SHA-256 of "hellp" look nothing alike. This ensures patterns in the input don't leak into the output.

The algorithms: **MD5** (128-bit) and **SHA-1** (160-bit) are broken — collisions have been found. Use **SHA-256** or higher for anything security-relevant. For passwords specifically, use **Argon2** — it's intentionally slow and memory-hard, which means brute-forcing a database full of Argon2 hashes is orders of magnitude harder than SHA-256.

**Salting** solves the rainbow table problem. A rainbow table is a precomputed lookup of `hash → input` for millions of common passwords. If you salt — add a random unique value to each password before hashing — the precomputed table becomes useless because every password now has a unique input even if two users share the same password.

**HMAC (Hash-based Message Authentication Code)** adds a secret key into the hash computation. A plain hash proves integrity — the data hasn't changed. An HMAC proves integrity *and* authentication — the data hasn't changed *and* it came from someone who knows the shared secret key. HMAC does two nested hash operations to prevent length extension attacks. It's used in TLS, IPsec, and SSH.

---

## Part 5 — Asymmetric Cryptography (Two Keys)

Symmetric crypto has one unsolved problem: how do you securely share the key in the first place? If you could share it securely, you wouldn't need encryption. Asymmetric cryptography solves this.

The analogy: a letterbox with a slot. Anyone can post a letter through the slot (public key). Only you have the key to open the box (private key). Crucially, you can hand out a thousand copies of the slot design — it doesn't help anyone open the box.

Every user has two mathematically linked keys. Anything encrypted with the public key can only be decrypted with the private key. Anything signed with the private key can be verified with the public key. The asymmetry enables two separate use cases:

- **Confidentiality:** Encrypt with recipient's public key → only they can decrypt with their private key
- **Authentication:** Encrypt/sign with your own private key → anyone can verify with your public key, proving it came from you

### Diffie-Hellman Key Exchange

Before RSA encryption, there is Diffie-Hellman — a method for two strangers to agree on a shared secret over a public channel without ever transmitting the secret. The paint mixing analogy explains it perfectly: both parties start with the same public colour (yellow). Each adds their own private colour. They exchange the mixed colours publicly. Each then adds the other's mix to their own private colour — and both arrive at the same final colour. An observer sees yellow and two mixed colours but never the private colours or the final result.

Mathematically: both agree on public numbers P (a large prime) and G (a generator). Alice picks private key a, computes G^a mod P and sends it. Bob picks private key b, computes G^b mod P and sends it. Alice raises Bob's value to the power a mod P. Bob raises Alice's value to the power b mod P. Both arrive at G^ab mod P — the shared secret. Security relies on the discrete logarithm problem: knowing G^a mod P, finding a is computationally infeasible for large enough numbers.

### RSA

RSA is based on a simple observation: multiplying two large primes is easy, but factoring the result back into those primes is extremely hard. Given a 2048-bit number that's the product of two primes, finding those primes would take longer than the age of the universe with current computers.

Key generation: choose primes p and q, compute n = p×q (the modulus), compute φ(n) = (p−1)(q−1), choose public exponent e, find private exponent d such that d×e ≡ 1 mod φ(n). Public key is (e, n). Private key is (d, n). Encrypt with C = M^e mod n. Decrypt with M = C^d mod n.

RSA is slow — roughly 1000× slower than AES. In practice, RSA is used to exchange an AES key, and AES encrypts the actual data. This hybrid approach combines the key exchange advantage of asymmetric crypto with the speed advantage of symmetric crypto.

---

## Part 6 — Key Management

A cryptographic system is only as secure as its key management. The strongest algorithm in the world means nothing if the key is stored in plaintext in a text file.

NIST SP 800-57 defines the key lifecycle in four phases: **pre-operational** (generation, certification, distribution), **operational** (activation, use, backup, rotation), **post-operational** (archival, recovery), and **deletion** (destruction, zeroization).

Key generation must be truly random — using a weak random number generator is a critical vulnerability. Keys must be stored securely — ideally in **Hardware Security Modules (HSMs)**, tamper-resistant physical devices that keep keys inside and expose only an API for cryptographic operations. Keys must be rotated regularly. When compromised, they must be revoked immediately.

**Key Derivation Functions (KDFs)** solve a different problem: deriving strong cryptographic keys from weak human-memorable passwords. The formula is `KDF(password, salt, difficulty, key size)`. The salt prevents rainbow tables. The difficulty factor — number of iterations — makes brute force slow. Argon2, bcrypt, scrypt, and PBKDF2 are all KDFs. Argon2 is the current gold standard.

---

## Part 7 — Digital Signatures and PKI

Digital signatures provide three things simultaneously: **authenticity** (this came from who it claims), **integrity** (it hasn't been altered), and **non-repudiation** (the sender can't deny it). They use asymmetric cryptography in a specific way.

To sign: hash the document, then encrypt that hash with your private key. The encrypted hash is the signature. To verify: decrypt the signature with the sender's public key to get the claimed hash, then hash the received document yourself. If the hashes match, the document is authentic and unchanged. The signature is tied to the private key — only the true owner could have produced it.

Three common signature algorithms: **RSA** (based on prime factorisation, large keys, used in SSL/TLS and email), **DSA** (discrete logarithm, moderate keys), and **ECDSA** (elliptic curve discrete logarithm, small keys — 256-bit ECDSA is equivalent to 3072-bit RSA). ECDSA is used in Bitcoin and most modern mobile applications.

The **PKI (Public Key Infrastructure)** is the system that makes public keys trustworthy at scale. The problem: anyone can generate a key pair and claim to be anyone. PKI solves this by having **Certificate Authorities (CAs)** — trusted third parties that digitally sign certificates binding a public key to a verified identity.

An **X.509 certificate** contains: the subject's public key, the subject's identity, the issuer (CA) name, validity dates, serial number, and the CA's digital signature over all of this. When your browser connects to a website, it verifies the site's certificate was signed by a CA your OS trusts. The chain of trust goes: root CA → intermediate CA → website certificate.

When a certificate needs to be invalidated before expiry (key compromise, organisation change), two mechanisms exist: **CRL (Certificate Revocation List)** — a periodically published list of revoked certificates, but potentially stale — and **OCSP (Online Certificate Status Protocol)** — a real-time query to the CA returning "good", "revoked", or "unknown" for a specific certificate.

---

## Part 8 — Security Protocols

**TLS (Transport Layer Security)** is what HTTPS runs on. It provides confidentiality (symmetric encryption), integrity (HMAC), and authentication (PKI/certificates) in a single protocol. The TLS handshake negotiates cipher suites, authenticates the server via certificate, and establishes a session key — all before a single byte of application data is sent. TLS 1.3 is the current version; TLS 1.0 and 1.1 are deprecated.

**PGP (Pretty Good Privacy)** is a hybrid cryptosystem for email and files. Message encrypted with a randomly generated symmetric key. That symmetric key encrypted with the recipient's public key. Both sent together. Recipient uses their private key to get the symmetric key, then decrypts the message. Also uses digital signatures for authentication.

**SSH (Secure Shell)** secures remote access to servers. Uses public key cryptography for authentication — you generate a key pair, put the public key on the server, and authenticate using your private key without ever transmitting a password.

**IPSec** secures IP-layer communications. Used in VPNs. Has two components: **AH (Authentication Header)** for integrity and **ESP (Encapsulating Security Payload)** for confidentiality and authentication.

---

## Part 9 — SSO and Authentication

**SSO (Single Sign-On)** lets you log in once and access multiple services. The analogy: a festival wristband. Show your ID once at the gate, get a wristband, and that wristband gets you into every stage and bar without showing ID again.

Technically: you log in to an Identity Provider (Google, Microsoft), which issues a token stored in your browser. Every other service checks that token with the Identity Provider rather than asking for your password.

Protocols: **SAML** uses XML, designed for enterprise web SSO. **OAuth 2.0** is authorisation (what can this app access?) not authentication (who are you?). **OIDC** (OpenID Connect) adds authentication on top of OAuth 2.0 — the most modern approach, uses JWT tokens. **Kerberos** uses tickets and mutual authentication in corporate networks. **LDAP** is a directory protocol for looking up user information.

**MFA (Multi-Factor Authentication)** requires at least two of: something you know (password), something you have (phone, hardware token), something you are (biometrics). The principle: compromising one factor isn't enough.

---

## Part 10 — Cryptanalysis

Cryptanalysis is the science of breaking cryptographic systems without the key. Understanding attacks is essential for understanding why good cryptography is designed the way it is.

Attack types by what the attacker has access to: **ciphertext-only** (only encrypted data), **known-plaintext** (some plaintext and its ciphertext), **chosen-plaintext** (attacker can choose what gets encrypted), **chosen-ciphertext** (attacker can choose what gets decrypted).

**Differential cryptanalysis** studies how differences in input pairs propagate through a cipher to the output. By choosing plaintext pairs with a specific XOR difference, certain output differences occur with higher probability than random — this leaks information about the key. It targets the last round of a block cipher specifically, because the attacker can partially decrypt the ciphertext using guessed key bits and check whether expected differences appear.

**Linear cryptanalysis** finds linear approximations — equations involving XORs of specific plaintext, ciphertext, and key bits that hold with probability slightly above or below 0.5. Enough chosen plaintext samples and you can extract key bits.

**Side-channel attacks** don't attack the algorithm at all — they exploit physical information leaking from the implementation: timing differences, power consumption, electromagnetic emissions. A device taking longer to process a 1 vs a 0 leaks key bits through timing alone.

---

## Part 11 — Advanced Topics

### Quantum Cryptography
Shor's algorithm, running on a sufficiently powerful quantum computer, can factor large integers efficiently — which breaks RSA, DH, and ECC. Grover's algorithm halves the effective security of symmetric ciphers (AES-256 becomes roughly AES-128 strength against quantum). These aren't hypothetical: NIST has already begun standardising post-quantum algorithms.

**QKD (Quantum Key Distribution)** uses individual photons to distribute cryptographic keys. Security comes from physics: measuring a quantum state disturbs it (the uncertainty principle), and quantum states cannot be copied (the no-cloning theorem). Any eavesdropper necessarily introduces detectable errors.

**BB84** (Bennett & Brassard, 1984): Alice sends photons polarised in one of four states (H, V, +45°, −45°). Bob measures each with a randomly chosen basis. They compare which bases they used — not the results — over a public channel. Bits where they used the same basis form the key. A sample is disclosed to test for errors; high error rate means Eve was present.

### Post-Quantum Cryptography
PQC is classical cryptography redesigned to resist quantum attacks. It runs on normal hardware — no quantum tech required. Four main families: **lattice-based** (Learning With Errors problem — leading candidate, supports both encryption and signatures), **code-based** (McEliece, based on error-correcting codes, very large keys, long history of security), **hash-based** (SPHINCS+, XMSS — signatures only, security depends only on hash function security), **multivariate** (solving systems of nonlinear equations — signatures only). NIST has selected algorithms from lattice-based and hash-based families for standardisation.

### Homomorphic Encryption
Homomorphic encryption lets you perform computations on encrypted data without decrypting it. The result, when decrypted, matches what you'd get computing on the plaintext. The glove box analogy: scientists can manipulate samples inside a sealed box without touching them directly. Only the key holder can open the box and retrieve results.

**PHE (Partial)** supports one operation type (addition or multiplication) unlimited times. **FHE (Full)** supports both, but is currently around one million times slower than plaintext computation due to the need to manage "noise" — a small random term added to ciphertext for security that grows with each operation and must be periodically reduced via bootstrapping.

### Elliptic Curve Cryptography
ECC provides equivalent security to RSA with much smaller keys — a 256-bit ECC key matches a 3072-bit RSA key. Based on the algebraic structure of elliptic curves over finite fields. The equation y² = x³ + ax + b defines a curve; operations on points on that curve (point addition, scalar multiplication) provide the hard mathematical problem. Given a public key Q = dP (where P is a known base point and d is the private key), finding d from Q is the Elliptic Curve Discrete Logarithm Problem — computationally infeasible. ECDSA for signatures, ECDH for key exchange. Used in Bitcoin, TLS 1.3, and most modern mobile security.

---

## Part 12 — Secure System Design

### The 8 Principles

Good security is designed in from the start, not bolted on afterwards. Eight principles guide this:

**Least Privilege** — give users and processes only the access they need, nothing more. A marketing employee doesn't need access to payroll databases.

**Defence in Depth** — multiple independent layers of security. An attacker who breaks through the firewall still faces application-level controls, encryption, and monitoring.

**Separation of Duties** — split critical actions so no single person can complete them alone. Financial transactions requiring two authorisations. Developers who can't deploy directly to production.

**Fail-Safe Defaults** — the default state is secure. New accounts have no permissions. Closed ports until explicitly opened. Automatic session expiry.

**Economy of Mechanism** — keep it simple. Every additional component is a potential vulnerability. Simple systems are easier to reason about, audit, and secure.

**Complete Mediation** — check every access, every time. Never cache an authorisation decision. If a user's permissions changed, the next request should reflect that.

**Open Design** — security shouldn't depend on the design being secret. AES is public; its strength comes from mathematics, not obscurity. Secret algorithms can't be audited.

**Psychological Acceptability** — if security is too inconvenient, users bypass it. SSO is more secure than 10 separate passwords because users actually use it properly.

### STRIDE Threat Model

STRIDE is a structured approach to thinking about threats during design. Each letter is a threat category: **Spoofing** (pretending to be someone else), **Tampering** (modifying data), **Repudiation** (denying you did something), **Information Disclosure** (data leaks), **Denial of Service** (making the system unavailable), **Elevation of Privilege** (gaining more access than authorised).

For every system component, run through STRIDE: could an attacker do this? If yes, design a mitigation.

### Legal and Ethical Aspects

Cryptography is governed by law. The FCA regulates financial institutions' use of encryption. PCI-DSS mandates encryption of cardholder data in storage and transit. GDPR requires protection of personal data. Payment Services Regulations 2017 protect electronic payment data. Export controls in some countries restrict exporting strong cryptographic technology.

Ethically: backdoors — deliberate weaknesses inserted for government access — are considered unethical because they weaken security for everyone. Transparency is preferred: open, peer-reviewed algorithms like AES are stronger than proprietary "security through obscurity" approaches.

---

*Generated from WM242 lecture materials by Claude | June 2026*
*For atomic notes and links: see [[MOC WM242 Implementing Secure Systems]]*
