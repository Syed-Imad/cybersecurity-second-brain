# WM242 — Implementing Secure Systems
### Complete Study Guide

```
╔══════════════════════════════════════════════════════════════╗
║          IMPLEMENTING SECURE SYSTEMS  ·  WM242               ║
║          Year 2  ·  Warwick  ·  Generated June 2026          ║
╚══════════════════════════════════════════════════════════════╝
```

> **How to use this guide**
> Read it top to bottom for a first pass. Then close it and do active recall.
> For quick lookups, use the Concepts notes. For navigation, use the MOC.
> → [[MOC WM242 Implementing Secure Systems]]

---

## Table of Contents

| # | Topic | Key concept |
|---|-------|-------------|
| [1](#1--what-cryptography-is-and-why-it-exists) | What Cryptography Is | CIA Triad, Shannon's principles |
| [2](#2--classical-ciphers) | Classical Ciphers | Caesar, Vigenère, OTP, Rail Fence |
| [3](#3--symmetric-cryptography) | Symmetric Cryptography | AES, DES, modes, padding |
| [4](#4--hash-functions) | Hash Functions | SHA-256, salting, HMAC |
| [5](#5--asymmetric-cryptography) | Asymmetric Cryptography | RSA, Diffie-Hellman |
| [6](#6--key-management) | Key Management | Lifecycle, KDFs, storage |
| [7](#7--digital-signatures--pki) | Digital Signatures & PKI | Signing, CA, X.509, CRL |
| [8](#8--security-protocols) | Security Protocols | TLS, PGP, SSH, IPSec |
| [9](#9--sso--authentication) | SSO & Authentication | OAuth, SAML, OIDC, MFA |
| [10](#10--cryptanalysis) | Cryptanalysis | Attack types, differential, linear |
| [11](#11--quantum--post-quantum) | Quantum & Post-Quantum | QKD, BB84, PQC families |
| [12](#12--homomorphic-encryption) | Homomorphic Encryption | PHE, FHE, noise |
| [13](#13--elliptic-curve-cryptography) | Elliptic Curve Cryptography | ECDSA, ECDH, ECC vs RSA |
| [14](#14--secure-system-design) | Secure System Design | 8 principles, STRIDE |
| [15](#15--legal-ethical--regulatory) | Legal & Ethical | GDPR, PCI-DSS, backdoors |

---

## 1 · What Cryptography Is and Why It Exists

> **The one-liner:** Cryptography is the science of securing communication by transforming information so only intended parties can read it.

### The Problem It Solves

Imagine sending a postcard. Anyone who handles it — the postal worker, a nosy neighbour — can read it. The internet works the same way. Data hops across dozens of servers before reaching its destination. Without cryptography, every hop is a postcard.

```
WITHOUT CRYPTO                    WITH CRYPTO
─────────────                     ───────────
Alice ──[HELLO]──► Router         Alice ──[X9#mK]──► Router
                     │                                  │
                   Eve ← reads it                     Eve ← sees gibberish
                     │                                  │
              ──[HELLO]──► Bob                  ──[X9#mK]──► Bob
                                                            │
                                                        decrypts → HELLO
```

### The Four Threats

| Threat | What happens | Cryptography's answer |
|--------|-------------|----------------------|
| **Eavesdropping** | Eve intercepts and reads the message | Encryption — Eve reads gibberish |
| **Tampering** | Eve changes the message in transit | Hashing / MACs — alteration is detectable |
| **Impersonation** | Eve pretends to be Alice | Digital signatures — only Alice has her private key |
| **Replay attacks** | Eve re-sends a captured message later | Timestamps and nonces — old messages are rejected |

### The CIA Triad

```
              Confidentiality
                    ▲
                   / \
                  /   \
                 /     \
                /       \
               ▼         ▼
          Integrity ── Availability
```

| Pillar | Meaning | Example threat |
|--------|---------|----------------|
| **Confidentiality** | Only authorised parties can read the data | Eavesdropping |
| **Integrity** | Data hasn't been altered | Tampering |
| **Availability** | System works when you need it | DDoS attack |

### Shannon's Two Principles

Claude Shannon — father of information theory — identified the foundations of every strong cipher:

| Principle | Meaning | Example in AES |
|-----------|---------|----------------|
| **Confusion** | Complex relationship between key and ciphertext | SubBytes operation |
| **Diffusion** | Each plaintext bit influences many ciphertext bits | ShiftRows + MixColumns |

> **Why this matters:** A cipher that lacks confusion is vulnerable to key analysis. One that lacks diffusion leaks patterns from the plaintext. AES uses both aggressively — that's why it's unbroken.

---

## 2 · Classical Ciphers

> **The one-liner:** Early ciphers either replaced letters (substitution) or shuffled them (transposition). Both are easily broken today.

### Two Fundamental Approaches

```
SUBSTITUTION — letters change, positions stay
─────────────────────────────────────────────
Plaintext:   H E L L O
             ↓ ↓ ↓ ↓ ↓   (shift by 3)
Ciphertext:  K H O O R

TRANSPOSITION — positions change, letters stay
───────────────────────────────────────────────
Plaintext:   S E C R E T
             (rearranged across rails)
Ciphertext:  S C E E R T
```

### The Four Classic Ciphers

#### Caesar Cipher
```
Alphabet:   A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
Shift n=3:  D E F G H I J K L M N O P Q R S T U V W X Y Z A B C

HELLO  →  KHOOR
```

| Property | Detail |
|----------|--------|
| Type | Substitution |
| Key | Shift value n (0–25) |
| Formula | E(x) = (x + n) mod 26 |
| Weakness | Only 25 possible keys — brute forced in seconds |

#### Vigenère Cipher
Uses a keyword. Each letter of the message is shifted by the corresponding keyword letter, cycling if needed.

```
Message:  H E L L O
Keyword:  D O G D O
          ↓ ↓ ↓ ↓ ↓
Result:   K S R O C
```

Harder than Caesar, but still broken by frequency analysis once you know the keyword length (found via Kasiski examination).

#### One-Time Pad (Vernam Cipher)
```
Message:  01001000  (H)
Key:      11010110  (random)
XOR:      10011110  (ciphertext)
```

| Property | Detail |
|----------|--------|
| Security | **Theoretically unbreakable** |
| Requirement | Key must be: truly random, same length as message, used only once |
| Weakness | Key distribution is impractical at scale |

#### Rail Fence Cipher

Message: `SECRET MESSAGE` across 3 rails:

```
Rail 1:  S . . . R . . . S . . . E
Rail 2:  . E . C . E . M . S . A .
Rail 3:  . . . T . . . E . . G . .

Read rows: SRSE + ECEMSA + TEG  →  SESEERTESGCMA
```

### How to Break Them — Frequency Analysis

```
English letter frequency (approximate):
E ████████████ 13%
T ████████     9%
A ███████      8%
O ███████      8%
I ██████       7%
N ██████       7%
...
```

**Method:** Count the most frequent symbol in ciphertext → likely E. Work outward using common patterns:
- Single-letter words: **A**, **I**
- Common 2-letter words: of, to, in, it, is, be
- Common 3-letter words: **the**, **and**
- Common doubled letters: ss, ee, tt, ll, oo

---

## 3 · Symmetric Cryptography

> **The one-liner:** One shared key encrypts and decrypts. Fast and efficient — but both parties need the same key, which creates a distribution problem.

```
      ┌─────────┐    SECRET KEY    ┌─────────┐
      │  ALICE  │ ←────────────── │   BOB   │
      └────┬────┘                 └────┬────┘
           │                           │
    Encrypt with key             Decrypt with key
           │                           │
           └──────► CIPHERTEXT ────────┘
```

| Property | Detail |
|----------|--------|
| Keys | 1 shared secret key |
| Speed | Fast — good for large data |
| Weakness | Key distribution problem |
| Non-repudiation | ✗ Cannot prove which party sent a message |

### DES — Data Encryption Standard

```
╔════════════════════════════════════╗
║  DES — OBSOLETE. DO NOT USE.       ║
║  Key: 56 bits  Block: 64 bits      ║
║  Structure: Feistel Network        ║
║  Rounds: 16                        ║
╚════════════════════════════════════╝
```

**The Feistel Network — one round:**
```
Input block (64 bits)
         │
    ┌────┴────┐
    L         R
    │         │
    │    ┌────┤ ← subkey Kn
    │    │ f()│
    │    └────┤
    │         │
  XOR ◄───────┘
    │         │
    └────┬────┘
   new R     new L  (swapped)
```

**Why DES is broken:** 56-bit key = 2⁵⁶ possible keys ≈ 72 quadrillion. Sounds large but modern hardware brute-forces it in hours.

---

### AES — Advanced Encryption Standard

```
╔════════════════════════════════════════════════╗
║  AES — THE CURRENT STANDARD                    ║
║  Key sizes:  128 / 192 / 256 bits              ║
║  Block size: 128 bits (4×4 byte matrix)        ║
║  Structure:  Substitution-permutation network  ║
╚════════════════════════════════════════════════╝
```

**AES operates on a 4×4 grid of bytes:**
```
┌──┬──┬──┬──┐
│b0│b4│b8│b12│
├──┼──┼──┼──┤
│b1│b5│b9│b13│
├──┼──┼──┼──┤
│b2│b6│b10│b14│
├──┼──┼──┼──┤
│b3│b7│b11│b15│
└──┴──┴──┴──┘
```

**Round structure:**
```
Plaintext
    │
    ▼
AddRoundKey ◄── Initial round key
    │
    ▼  ┌─────────────────────────────────────────────────┐
    │  │ MAIN ROUNDS (repeat 9×/11×/13× depending on key)│
    │  │                                                  │
    │  │  SubBytes   → replace each byte via S-box        │
    │  │      │         (confusion)                       │
    │  │      ▼                                           │
    │  │  ShiftRows  → shift row i left by i positions    │
    │  │      │         (moves bytes between columns)     │
    │  │      ▼                                           │
    │  │  MixColumns → multiply each column by a matrix   │
    │  │      │         (heavy diffusion)                 │
    │  │      ▼                                           │
    │  │  AddRoundKey → XOR with round subkey             │
    │  └─────────────────────────────────────────────────┘
    │
    ▼  ┌──────────────────────────────────────────────────┐
    │  │ FINAL ROUND                                      │
    │  │  SubBytes → ShiftRows → AddRoundKey              │
    │  │  ⚠️  MixColumns is SKIPPED in the final round    │
    │  └──────────────────────────────────────────────────┘
    │
    ▼
Ciphertext
```

> ⚠️ **Exam trap:** MixColumns is omitted in the final round. This comes up constantly.

**What each operation does:**

| Operation | Purpose | Shannon principle |
|-----------|---------|-------------------|
| SubBytes | Non-linear byte substitution via S-box | Confusion |
| ShiftRows | Rotates rows — mixes bytes across columns | Diffusion |
| MixColumns | Linear transformation of each column | Diffusion |
| AddRoundKey | XOR with subkey derived from master key | Key mixing |

---

### Modes of Operation

Block ciphers encrypt exactly one 128-bit block. Real messages are longer. Modes define how to chain block encryptions together.

#### ECB — Electronic Code Book ❌
```
Block 1  →  [AES]  →  Cipher 1
Block 2  →  [AES]  →  Cipher 2
Block 3  →  [AES]  →  Cipher 3

Problem: same plaintext block = same ciphertext block
```

> **The penguin problem:** Encrypt a bitmap image with ECB and the pixel patterns remain visible in the output. The structure of the data leaks through. Never use ECB for real data.

#### CBC — Cipher Block Chaining ✅ (most common)
```
IV ──┐
     XOR ◄── Plaintext 1  →  [AES]  →  Ciphertext 1 ──┐
                                                         XOR ◄── Plaintext 2  →  [AES]  →  Ciphertext 2
```

Each block's ciphertext feeds into the next block's encryption. Identical plaintexts produce different ciphertexts. Needs a random IV for the first block.

#### CTR — Counter Mode ✅ (fast, parallelizable)
```
Counter 1  →  [AES]  →  Keystream 1  XOR  Plaintext 1  =  Ciphertext 1
Counter 2  →  [AES]  →  Keystream 2  XOR  Plaintext 2  =  Ciphertext 2
Counter 3  →  [AES]  →  Keystream 3  XOR  Plaintext 3  =  Ciphertext 3
```

All blocks can be encrypted simultaneously. Very fast.

#### Modes Summary

| Mode | Parallel? | IV needed? | Error propagation | Use |
|------|:---------:|:----------:|:-----------------:|-----|
| ECB | ✅ | ✗ | None | ❌ Never |
| CBC | ✗ | ✅ | Next block corrupted | General use |
| CFB | ✗ | ✅ | Limited | Streaming |
| OFB | ✗ | ✅ | None | Streaming |
| CTR | ✅ | ✅ | None | High-performance |

### Padding

When a message doesn't fill the final block, padding fills the gap.

| Scheme | Rule | Example (3 bytes short) |
|--------|------|------------------------|
| **PKCS7** | Pad with N bytes each having value N | `03 03 03` |
| **ISO 10126** | Random bytes, last byte = count | `A7 3F 03` |
| **TBC** | If last bit = 0, pad 1s. If 1, pad 0s | `11111111` |

---

## 4 · Hash Functions

> **The one-liner:** A one-way function that converts any input into a fixed-length fingerprint. Cannot be reversed.

```
                    ┌──────────────┐
"hello"  ──────────►│  SHA-256     │──────► 2cf24dba5fb0a30e...
                    └──────────────┘

"hellp"  ──────────►│  SHA-256     │──────► 4a8a08f09d37b73c...
(1 bit different)   └──────────────┘        (completely different)
```

> **The meat grinder analogy:** Put any amount of raw meat in — always get the same type of minced output. Put the same cut in twice — identical mince. Put a slightly different cut in — completely different mince. You can never reconstruct the original from the mince.

### Required Properties

| Property | Definition | If broken... |
|----------|-----------|--------------|
| **One-way** (preimage resistance) | Given hash h, can't find input m where H(m) = h | Attacker reverses password hashes |
| **Collision resistance** | Can't find m1 ≠ m2 where H(m1) = H(m2) | Attacker substitutes documents undetected |
| **Avalanche effect** | 1 bit change in input → completely different output | Patterns in plaintext leak into hash |

### The Algorithms

| Algorithm | Output | Status | Use |
|-----------|--------|--------|-----|
| MD5 | 128-bit | ❌ **Broken** — collisions found | Legacy only |
| SHA-1 | 160-bit | ❌ **Deprecated** | Do not use |
| SHA-256 | 256-bit | ✅ Current standard | General purpose |
| SHA-512 | 512-bit | ✅ Current standard | Higher security |
| SHA-3 | Variable | ✅ Next-gen | Future-proofing |
| **Argon2** | Variable | ✅ **Best for passwords** | Password hashing |

> **Number of possible SHA-256 hashes:** 2²⁵⁶ = more atoms than in the observable universe

### Salting

```
WITHOUT SALT                    WITH SALT
────────────                    ─────────
User A: password123             User A: password123 + x7fK9p
         │                               │
        SHA-256                         SHA-256
         │                               │
    5baa61e4...                     9a8c2f11...

User B: password123             User B: password123 + mR3nP2
         │                               │
        SHA-256                         SHA-256
         │                               │
    5baa61e4...    ← SAME!          7d4b91cc...    ← DIFFERENT ✅
```

**What salting defeats:**

| Attack | Without salt | With salt |
|--------|-------------|-----------|
| Rainbow tables | ✅ Works instantly | ❌ Fails — every hash is unique |
| Two users same password | One crack = two accounts | Must crack each separately |
| Dictionary attack | One pass cracks everyone | Must rehash per user |

### HMAC

```
Plain hash  →  proves integrity only
                (anyone can compute a hash)

HMAC        →  proves integrity + authentication
                (only someone with the secret key can compute it)

Formula:
HMAC = H( outer_key_pad ║ H( inner_key_pad ║ message ) )
           └─────────────────────────────────────────┘
                    two nested hash passes
                    (prevents length extension attacks)
```

Used in: TLS · IPSec · SSH · API tokens

### MAC vs HMAC vs Hash

| | Hash | MAC | HMAC |
|--|------|-----|------|
| Input | Message | Message + key | Message + key |
| Proves | Data unchanged | Integrity + auth | Integrity + auth |
| Algorithm | Any hash fn | Block cipher (CBC-MAC) | Hash function |
| Attack resistance | Vulnerable to length extension | Implementation dependent | Strong |

---

## 5 · Asymmetric Cryptography

> **The one-liner:** Two mathematically linked keys — public and private. Solves the key distribution problem that breaks symmetric crypto.

### The Letterbox Analogy

```
                  ┌─────────────┐
                  │  LETTERBOX  │
                  │             │
Anyone can post   │  ╔═══════╗  │  Only YOU can
a letter through  │  ║ slot  ║  │  open the box
the slot          │  ╚═══════╝  │  with your key
(public key)      │     [key]   │  (private key)
                  └─────────────┘
```

### Two Use Cases

```
CONFIDENTIALITY                          AUTHENTICATION
───────────────                          ──────────────
Encrypt with recipient's PUBLIC key  →   Sign with YOUR PRIVATE key
Decrypt with recipient's PRIVATE key     Verify with YOUR PUBLIC key

Anyone can encrypt to Bob.               Only Alice could have signed this.
Only Bob can decrypt it.                 Anyone can verify it's from Alice.
```

### Asymmetric vs Symmetric

| | Symmetric | Asymmetric |
|--|-----------|-----------|
| Keys | 1 shared | Public + private pair |
| Speed | Fast (bulk data) | Slow (~1000× slower) |
| Key exchange | Problem | Solved |
| Non-repudiation | ✗ | ✅ |
| Best for | Encrypting data | Key exchange, signatures |

> **In practice — hybrid encryption:**
> 1. Asymmetric key exchange to securely share a symmetric key
> 2. Symmetric encryption for all actual data
> TLS, PGP, and Signal all work this way.

---

### Diffie-Hellman Key Exchange

> **The paint mixing analogy:** Mix your private colour into the shared public colour. Exchange mixed colours publicly. Mix the other's colour with your private colour. Both arrive at the same final colour — but nobody saw either private colour or the final result.

```
Alice                              Bob
─────                              ───
                    Agree on:
              P = 23 (prime)
              G = 9  (generator)

a = 4 (private)                   b = 3 (private)
x = G^a mod P                     y = G^b mod P
  = 9^4 mod 23                      = 9^3 mod 23
  = 6561 mod 23                      = 729 mod 23
  = 6                                = 16

           ──── exchange x=6 and y=16 publicly ────

k = y^a mod P                     k = x^b mod P
  = 16^4 mod 23                     = 6^3 mod 23
  = 65536 mod 23                     = 216 mod 23
  = 9  ✅                            = 9  ✅

              Shared secret = 9
```

Security: knowing G, P, and x=6, finding a=4 is the discrete logarithm problem — computationally infeasible for large numbers.

---

### RSA

> **The core idea:** Multiplying two large primes is easy. Factoring the result back into those primes is extremely hard.

#### Key Generation

```
Step 1:  Choose primes p and q
         p = 11,  q = 13

Step 2:  n = p × q  (the modulus — made public)
         n = 143

Step 3:  φ(n) = (p-1)(q-1)
         φ(n) = 10 × 12 = 120

Step 4:  Choose e where gcd(e, φ(n)) = 1
         e = 7

Step 5:  Find d where d × e ≡ 1 mod φ(n)
         d = 103  (because 7 × 103 = 721 = 6×120 + 1)

Public key:  (e=7,   n=143)
Private key: (d=103, n=143)
```

#### Encryption & Decryption

```
Encrypt:   C = M^e mod n    →    M^7 mod 143
Decrypt:   M = C^d mod n    →    C^103 mod 143
```

#### RSA Key Sizes

| Key size | Security | Use |
|----------|---------|-----|
| 512-bit | ❌ Broken | Never |
| 1024-bit | ❌ Weak | Legacy only |
| 2048-bit | ✅ Minimum acceptable | Current standard |
| 4096-bit | ✅ Strong | High security |

> **Quantum threat:** Shor's algorithm can factor large integers efficiently on a quantum computer. RSA is broken in a post-quantum world. → See [[Post-Quantum Cryptography]]

---

## 6 · Key Management

> **The one-liner:** The strongest algorithm means nothing if the keys are managed poorly. Key management is where most real-world cryptographic failures happen.

### Key Lifecycle

```
┌─────────────────────────────────────────────────────────────┐
│                    KEY LIFECYCLE                            │
│                                                             │
│  PRE-OPERATIONAL    OPERATIONAL    POST-OPERATIONAL  DELETE │
│  ┌────────────┐   ┌────────────┐   ┌────────────┐  ┌────┐  │
│  │ Generate   │   │ Activate   │   │ Archive    │  │Zer-│  │
│  │ Register   │──►│ Use        │──►│ Recover    │─►│oize│  │
│  │ Certify    │   │ Backup     │   │ Reactivate │  │    │  │
│  │ Distribute │   │ Rotate     │   └────────────┘  └────┘  │
│  └────────────┘   │ Revoke     │                            │
│                   └────────────┘                            │
└─────────────────────────────────────────────────────────────┘
```

**The 12 steps in full:**

| # | Step | What happens |
|---|------|-------------|
| 1 | User registration | Entity joins the security domain |
| 2 | User initialisation | Cryptographic software/hardware set up |
| 3 | **Key generation** | Must be truly random — weak RNG = critical vulnerability |
| 4 | Key installation | Key loaded into device or application |
| 5 | Key registration | CA binds public key to identity in a certificate |
| 6 | Normal use | Key used until cryptoperiod expires |
| 7 | **Key backup** | Short-term copy in secure storage during active use |
| 8 | Key update | Replace before cryptoperiod expires |
| 9 | Archival | Long-term offline storage after use ends |
| 10 | De-registration + destruction | All copies destroyed, records removed |
| 11 | Key recovery | Restore from backup if lost (not compromised) |
| 12 | **Key revocation** | Emergency removal if key is compromised |

### Key Storage Types

| Type | Examples | Security | Use when |
|------|---------|---------|---------|
| **Hardware (HSM)** | Smart cards, Hardware Security Modules, tokens | Highest — tamper-resistant | High-value keys, CAs, payment systems |
| **Software** | Files, databases, environment variables | Lower — depends on OS security | Development, low-risk applications |
| **Hybrid** | Encrypted files on hardware devices | Medium | Balance of security and convenience |

### Key Derivation Functions (KDF)

```
          Salt
           │
Password ──┤
           │
     Difficulty (iterations)     →  [  KDF  ]  →  Derived Key
           │
      Key size
           │
```

**Why not just hash the password?**
SHA-256 of "password123" takes microseconds to compute. An attacker can try billions of guesses per second. KDFs are designed to be slow — Argon2 can take 100ms per hash. Same attack now takes millions of years.

| KDF | Type | Strength | Notes |
|-----|------|---------|-------|
| **Argon2** | Password-based | ⭐⭐⭐⭐⭐ | Winner of Password Hashing Competition — best choice |
| bcrypt | Password-based | ⭐⭐⭐⭐ | Widely deployed, still solid |
| scrypt | Password-based | ⭐⭐⭐⭐ | Memory-hard |
| PBKDF2 | Password-based | ⭐⭐⭐ | NIST approved, less memory-hard |
| HKDF | Symmetric-key | ⭐⭐⭐⭐ | For deriving session keys |

---

## 7 · Digital Signatures & PKI

> **The one-liner:** Digital signatures prove a message came from a specific sender and hasn't been altered — using asymmetric cryptography in reverse.

### How Signing Works

```
SENDER (Alice)                              RECEIVER (Bob)
──────────────                              ───────────────

Document                                    Document + Signature
     │                                           │
     ▼                                           ▼
  [Hash]  →  hash value                       [Hash]  →  hash value (from doc)
     │                                              │
     │   Encrypt with                               │   Compare ──► MATCH? ✅ Authentic
     │   Alice's PRIVATE key                        │              MISMATCH? ❌ Tampered
     │                                              │
     ▼                                    Decrypt with
  Signature                               Alice's PUBLIC key
     │                                              │
     └──────────── attached to doc ────────────────┘
```

**What a signature proves:**

| Property | Meaning |
|----------|---------|
| ✅ Authenticity | Only Alice's private key could produce this signature |
| ✅ Integrity | Any change to the document would break the hash |
| ✅ Non-repudiation | Alice cannot deny signing — only she has her private key |
| ❌ Confidentiality | Signing doesn't encrypt — document is still readable |

### Signature Algorithms Compared

| | RSA | DSA | ECDSA |
|--|-----|-----|-------|
| Security basis | Prime factorisation | Discrete logarithm | Elliptic curve DLP |
| Key size needed | 2048–4096 bits | 1024–3072 bits | **256–521 bits** |
| Signing speed | Slow | Moderate | Fast |
| Verification | Fast | Slow | Fast |
| Best for | SSL/TLS, email | Government | Blockchain, IoT, mobile |

---

### PKI — Public Key Infrastructure

> **The passport analogy:** The government (CA) issues passports (certificates) binding your photo (public key) to your identity. Border control trusts passports because they trust the government. You don't need to personally vouch for yourself at every border.

```
ROOT CA
(self-signed certificate — the trust anchor)
     │
     ├──► Intermediate CA
     │         │
     │         ├──► Website Certificate (e.g. bank.com)
     │         └──► Website Certificate (e.g. shop.com)
     │
     └──► Intermediate CA
               │
               └──► Website Certificate (e.g. gov.uk)
```

**PKI Components:**

| Component | Role |
|-----------|------|
| **Root CA** | Top of the trust chain. Self-signed. Trusted by operating systems. |
| **Intermediate CA** | Signed by Root CA. Issues end-entity certificates. |
| **Certificate** | Binds a public key to a verified identity. Signed by a CA. |
| **CRL** | List of revoked certificates. Updated periodically — can be stale. |
| **OCSP** | Real-time revocation check. Query CA for single certificate status. |

### X.509 Certificate Contents

```
┌─────────────────────────────────────────┐
│         X.509 CERTIFICATE               │
├─────────────────────────────────────────┤
│ Version:        3                        │
│ Serial number:  unique ID from CA        │
│ Algorithm:      SHA-256 with RSA         │
│ Issuer:         DigiCert Inc             │
│ Valid from:     2026-01-01               │
│ Valid until:    2027-01-01               │
│ Subject:        bank.com                 │
│ Public key:     [2048-bit RSA key]       │
│ Signature:      [CA's digital signature] │
└─────────────────────────────────────────┘
```

### Certificate Revocation — CRL vs OCSP

| | CRL | OCSP |
|--|-----|------|
| How it works | Download list of revoked certs | Query CA for one cert in real time |
| Freshness | Can be hours/days stale | Real-time |
| Size | Large — entire revoked list | Small — one cert response |
| Requires internet | No (cached list) | Yes |
| Speed | Fast (local check) | Network round-trip |

---

## 8 · Security Protocols

> **The one-liner:** Protocols are the rules that govern how cryptographic operations are combined to secure real communication — email, web traffic, remote access, VPNs.

### TLS — Transport Layer Security

```
Client                                        Server
──────                                        ──────
ClientHello (TLS version, cipher suites) ─────────────────►
                             ◄──── ServerHello + Certificate
                                   (server's public key, signed by CA)
Verify certificate against trusted CA
Generate pre-master secret
Encrypt with server's public key ─────────────────────────►
                             ◄──── Derive session keys (both sides)
Finished ─────────────────────────────────────────────────►
                             ◄──── Finished
═══════════════════ Encrypted Application Data ════════════
```

**TLS provides:**

| Goal | Mechanism |
|------|----------|
| Confidentiality | Symmetric encryption (AES) with negotiated session key |
| Integrity | HMAC on every message |
| Authentication | Server's X.509 certificate verified against trusted CA |

| Version | Status |
|---------|--------|
| SSL 3.0 | ❌ Broken |
| TLS 1.0 | ❌ Deprecated |
| TLS 1.1 | ❌ Deprecated |
| TLS 1.2 | ⚠️ Acceptable |
| **TLS 1.3** | ✅ Current — use this |

### PGP — Pretty Good Privacy

```
Alice wants to send an encrypted, authenticated email to Bob:

1. Generate random symmetric key K
2. Encrypt message with K           →  Encrypted message
3. Encrypt K with Bob's public key  →  Encrypted key
4. Sign with Alice's private key    →  Signature
5. Send: [Encrypted message] + [Encrypted key] + [Signature]

Bob receives:
1. Decrypt key: K = decrypt(Encrypted key, Bob's private key)
2. Decrypt message using K
3. Verify signature using Alice's public key
```

**PGP uses hybrid encryption** — symmetric for speed, asymmetric for key exchange.

### Protocol Comparison

| Protocol | Layer | Primary use | Key crypto |
|----------|-------|------------|-----------|
| **TLS** | Transport | HTTPS, secure web traffic | RSA/ECDH + AES + HMAC |
| **SSH** | Application | Remote server access | RSA/ECDSA key auth |
| **IPSec** | Network | VPNs, IP-layer security | AES + HMAC |
| **PGP** | Application | Email, file encryption | Hybrid (RSA + AES) |

**IPSec components:**

| Component | Purpose |
|-----------|---------|
| **AH** (Authentication Header) | Integrity only — no confidentiality |
| **ESP** (Encapsulating Security Payload) | Confidentiality + integrity + auth |

---

## 9 · SSO & Authentication

> **The one-liner:** Log in once, access everything. SSO uses tokens instead of passwords to grant access across multiple services.

### How SSO Works

```
1. User visits app.com
        │
        ▼
2. app.com redirects to Identity Provider (IdP)
   e.g. Google, Microsoft, Okta
        │
        ▼
3. User logs in at IdP
        │
        ▼
4. IdP creates TOKEN and sends back to app.com
        │
        ▼
5. User visits another-app.com
        │
        ▼
6. another-app.com checks token with IdP
        │
        ▼
7. IdP confirms → access granted ✅
   No password entered again
```

### Protocol Comparison

| Protocol | What it does | Format | Best for |
|----------|-------------|--------|---------|
| **SAML** | Auth + authorisation data exchange | XML | Enterprise web SSO |
| **OAuth 2.0** | Access delegation ("what can this app access?") | JSON tokens | Third-party API access |
| **OIDC** | Authentication layer on top of OAuth 2.0 | JWT (ID token) | Modern SSO with profile info |
| **Kerberos** | Ticket-based mutual authentication | Binary tickets | Corporate networks (AD) |
| **LDAP** | Directory service protocol | — | Looking up user/group info |

> **OIDC vs OAuth 2.0:** OAuth 2.0 answers "what can this app access?" OIDC additionally answers "who is this user?" OIDC = OAuth 2.0 + identity layer.

### MFA — Multi-Factor Authentication

```
┌─────────────────────────────────────────┐
│           THREE FACTORS                  │
│                                          │
│  🧠 Something you KNOW                  │
│     Password, PIN, security question     │
│                                          │
│  📱 Something you HAVE                  │
│     Phone (OTP), hardware token, card    │
│                                          │
│  👁 Something you ARE                   │
│     Fingerprint, face, iris scan         │
│                                          │
│  Requires 2+ of the above               │
└─────────────────────────────────────────┘
```

### SSO Benefits vs Risks

| Benefits | Risks |
|---------|-------|
| One credential to manage | Single point of failure — IdP compromised = all apps compromised |
| Easier to audit and monitor | Token theft enables session hijacking |
| Smaller overall attack surface | App compatibility issues |
| Users less likely to reuse passwords | |

---

## 10 · Cryptanalysis

> **The one-liner:** The science of breaking cryptographic systems without the key — by exploiting weaknesses in design, implementation, or usage.

```
Cryptology
    ├── Cryptography  (making secure systems)
    └── Cryptanalysis (breaking secure systems)
```

### Attack Types — By What the Attacker Has

| Attack | What attacker has | Power |
|--------|------------------|-------|
| **Ciphertext-only** | Only encrypted data | Weakest — frequency analysis |
| **Known-plaintext** | Some plaintext + ciphertext pairs | Medium |
| **Chosen-plaintext** | Can choose what gets encrypted | Strong |
| **Chosen-ciphertext** | Can choose what gets decrypted | Very strong |
| **Related-key** | Ciphertexts from related keys | Specific to some ciphers |

### Classical Methods

| Method | How it works | Breaks |
|--------|-------------|--------|
| **Frequency analysis** | Most common ciphertext symbol → likely E | Caesar, simple substitution |
| **Kasiski examination** | Find repeating patterns → reveals keyword length | Vigenère |
| **Index of coincidence** | Measures letter frequency vs expected language distribution | Polyalphabetic ciphers |

### Modern Attack Techniques

#### Differential Cryptanalysis

```
Choose two plaintexts P1, P2 with a fixed XOR difference (ΔP):

P1: 01001000 01100101  ]
                       }── XOR difference ΔP is fixed
P2: 01001000 01100100  ]

Encrypt both → C1, C2
Observe output difference ΔC

Certain ΔC values occur with HIGHER probability than random.
These biases reveal information about the key bits.
Target: the LAST round (can be partially decrypted using guessed key bits)
```

#### Linear Cryptanalysis

Finds linear equations involving XOR combinations of plaintext, ciphertext, and key bits that hold with probability slightly ≠ 0.5. With enough samples, extract key bits statistically.

#### Side-Channel Attacks

```
Don't attack the algorithm — attack the IMPLEMENTATION.

Timing attack:    operation on 1 takes longer than on 0 → leaks key bits
Power analysis:   power consumption varies with data → leaks key bits
EM emissions:     electromagnetic output reveals internal state
Cache timing:     cache hits vs misses reveal memory access patterns
```

### Attack Comparison

| Attack | Target | Requires | Defends against by |
|--------|--------|---------|-------------------|
| Brute force | Key space | Time + compute | Longer keys |
| Differential | S-boxes in block ciphers | Chosen plaintexts | Resistant S-box design |
| Linear | Linear approximations | Known plaintexts | Non-linear operations |
| Side-channel | Physical implementation | Physical access | Constant-time implementations |
| Meet-in-the-middle | Double encryption | Memory + time | Triple encryption |

---

## 11 · Quantum & Post-Quantum

> **The one-liner:** Quantum computers will break RSA, ECC, and DH. Post-Quantum Cryptography (PQC) is the replacement — classical algorithms redesigned to resist quantum attacks.

### The Quantum Threat

```
SHOR'S ALGORITHM (1994)
────────────────────────
Can factor large integers efficiently on a quantum computer.

Breaks: RSA, Diffie-Hellman, ECC, DSA
→ All public-key cryptography based on factoring or discrete log

GROVER'S ALGORITHM
──────────────────
Halves the effective key length of symmetric ciphers.

AES-256 → effectively AES-128 strength against quantum
Fix: double key lengths (AES-256 remains adequate)
```

### Quantum Key Distribution (QKD)

> **The soap bubble analogy:** A message written on soap bubbles. If anyone tries to read it in transit, the bubbles pop — and both parties immediately know someone was listening.

```
Alice                    Photon channel                    Bob
─────                    ──────────────                    ───
Send photon with         ──────────────►    Measure with
random polarisation:                        random basis:
H, V, +45°, -45°
                               Eve?
                         if Eve intercepts:
                         uncertainty principle
                         disturbs the photon ──► error detected

Compare bases over classical channel:
Where bases match → use those bits as key
High error rate → Eve was present → abort and restart
```

#### BB84 Protocol Steps

| Step | Who | Action |
|------|-----|--------|
| 1 | Alice | Sends photons with random polarisation (H/V or diagonal basis) |
| 2 | Bob | Measures each photon with randomly chosen basis |
| 3 | Both | Compare which bases were used (not results) over public channel |
| 4 | Both | Keep bits where bases matched → raw key |
| 5 | Both | Sacrifice sample to check error rate |
| 6 | Decision | Low errors → no Eve → use key. High errors → Eve present → discard |

**QKD Limitations:**

| Limitation | Why |
|-----------|-----|
| Slow | Single photons only — can't use whole photon bundles |
| Distance limited | Quantum states degrade; can't use standard repeaters |
| Dedicated infrastructure | Requires separate fibre — can't share with internet |
| Expensive | Specialised hardware |

---

### Post-Quantum Cryptography (PQC)

```
PQC vs QKD
──────────
PQC:  Classical algorithms. Runs on normal hardware.
      Security = mathematical hardness.
      Scalable. Deploy as software update.

QKD:  Requires quantum hardware + specialist fibre.
      Security = laws of physics.
      Expensive. Distance-limited. Not scalable yet.

→ PQC is the near-term practical solution.
→ QKD is a long-term physical security layer.
```

**The 4 PQC Families:**

| Family | Hard problem | Key/sig size | Use |
|--------|-------------|-------------|-----|
| **Lattice-based** | Learning With Errors (LWE) | Moderate | Encryption + signatures — **leading candidate** |
| **Code-based** | Decoding random error-correcting codes | Very large keys | Encryption (McEliece) |
| **Hash-based** | Security of hash functions | Small keys, large sigs | Signatures only (SPHINCS+, XMSS) |
| **Multivariate** | Solving nonlinear polynomial systems | Small keys | Signatures only |

> NIST has selected algorithms from lattice-based and hash-based families. Standardisation complete 2024.

---

## 12 · Homomorphic Encryption

> **The one-liner:** Perform computations on encrypted data without decrypting it. The result, when decrypted, equals what you'd get computing on the plaintext.

### The Glove Box Analogy

```
┌─────────────────────────────────────────┐
│          🔒 LOCKED GLOVE BOX            │
│                                          │
│   Scientists insert hands through        │
│   built-in gloves and manipulate         │
│   samples inside — mix, measure,         │
│   process — without opening the box      │
│   or touching samples directly.          │
│                                          │
│   Only the key holder can open the box  │
│   and retrieve the finished result.      │
└─────────────────────────────────────────┘
```

**Real-world use case:**
```
You → [encrypt medical data] → Cloud service
Cloud service → [compute on encrypted data] → [return encrypted result]
You → [decrypt result]

Cloud NEVER sees your actual data. ✅
```

### PHE vs FHE

| | Partial (PHE) | Full (FHE) |
|--|--------------|-----------|
| Operations supported | One type only (+ or ×), unlimited times | Both addition AND multiplication, unlimited times |
| Speed | Fast | ~1,000,000× slower than plaintext |
| Practical today | ✅ | ⚠️ Limited use cases only |
| Example schemes | RSA (×), Paillier (+) | BGV, BFV, CKKS |

**RSA is partially homomorphic (multiplicative):**
```
E(m1) × E(m2) = E(m1 × m2)

Proof:
E(m1) = m1^e mod n
E(m2) = m2^e mod n
E(m1) × E(m2) = (m1 × m2)^e mod n = E(m1 × m2)  ✅
```

### FHE Schemes

All lattice-based. All quantum-safe (based on RLWE hardness).

| Scheme | Operates on | Use case |
|--------|------------|---------|
| **BGV** | Integers | Exact arithmetic |
| **BFV** | Integers | Exact arithmetic |
| **CKKS** | Complex/approximate numbers | Machine learning, statistics |

### The Noise Problem

```
Fresh ciphertext:  [data + small noise]
After 1 operation: [result + slightly larger noise]
After 2 ops:       [result + larger noise]
...
After N ops:       [noise overwhelms data → decryption fails ❌]

Solution: Bootstrapping — a special operation that reduces noise,
allowing more operations. Very expensive computationally.
This is why FHE is ~1 million× slower.
```

---

## 13 · Elliptic Curve Cryptography

> **The one-liner:** Asymmetric cryptography using elliptic curves — same security as RSA but with dramatically smaller keys.

### What is an Elliptic Curve?

```
y² = x³ + ax + b

Graph (over real numbers):

      *     *
   *           *
  *             *
   *           *
     *       *
        * *

Properties:
- Smooth (no sharp corners)
- Symmetric about the x-axis
- Defined over a finite field for cryptography
```

### Point Operations

```
POINT ADDITION: P + Q = R
─────────────────────────
Draw a line through P and Q.
Find where it intersects the curve (call it R').
Reflect R' over the x-axis → R

POINT DOUBLING: P + P = 2P
──────────────────────────
Draw the tangent line at P.
Find where it intersects (R').
Reflect → R

SCALAR MULTIPLICATION: nP
─────────────────────────
Add P to itself n times.
This is the one-way function — easy to compute forward, infeasible to reverse.
```

**The hard problem:** Given public point Q = dP, finding d (the private key) is the Elliptic Curve Discrete Logarithm Problem (ECDLP) — computationally infeasible.

### ECC vs RSA

| | ECC | RSA |
|--|-----|-----|
| 256-bit key ≈ | ⭐ | 3072-bit RSA |
| 384-bit key ≈ | ⭐ | 7680-bit RSA |
| Speed | Faster | Slower |
| Power consumption | Lower | Higher |
| Ideal for | Mobile, IoT, smartcards | Servers |

### ECC Applications

| Application | Protocol | Used in |
|-------------|---------|---------|
| Digital signatures | ECDSA | Bitcoin, TLS, SSH |
| Key exchange | ECDH | TLS 1.3, Signal, WhatsApp |
| Certificates | ECDSA | Modern TLS certificates |

### Popular Curves

| Curve | Used in | Notes |
|-------|--------|-------|
| **NIST P-256** | TLS, most web traffic | NIST standard |
| **Curve25519** | Signal, WireGuard, SSH | Considered most secure design |
| **secp256k1** | Bitcoin | Non-NIST curve |
| **Brainpool** | EU standards | German BSI designed |

> **Quantum threat:** ECDLP is broken by Shor's algorithm. ECC is not quantum-safe. → See [[Post-Quantum Cryptography]]

---

## 14 · Secure System Design

> **The one-liner:** Security must be designed in from the start — not added afterwards. These 8 principles are the checklist.

### The 8 Principles

```
┌─────────────────────────────────────────────────────────────┐
│                 8 SECURE DESIGN PRINCIPLES                  │
├─────────────────────────────────────────────────────────────┤
│  1. Least Privilege        Give only what's needed          │
│  2. Defence in Depth       Multiple independent layers      │
│  3. Separation of Duties   No single point of control       │
│  4. Fail-Safe Defaults     Default = deny, not allow        │
│  5. Economy of Mechanism   Keep it simple                   │
│  6. Complete Mediation     Check every access, every time   │
│  7. Open Design            Security ≠ secrecy of design     │
│  8. Psychological Accept.  If it's annoying, users bypass   │
└─────────────────────────────────────────────────────────────┘
```

| Principle | Scenario example | Violated when |
|-----------|-----------------|---------------|
| **Least Privilege** | Marketing intern can't access payroll | "All staff have admin to avoid helpdesk tickets" |
| **Defence in Depth** | Firewall + auth + encryption + monitoring | Single firewall is the only protection |
| **Separation of Duties** | Two approvals needed to transfer funds | One person controls entire payment process |
| **Fail-Safe Defaults** | New accounts have zero permissions | New accounts get default "standard" access |
| **Economy of Mechanism** | Simple auth flow — one library, well-tested | Homegrown 2000-line authentication module |
| **Complete Mediation** | Check permissions on every API request | "We checked permissions at login, no need after" |
| **Open Design** | Using AES (publicly reviewed) | "Our secret algorithm is more secure" |
| **Psychological Acceptability** | SSO — one login for everything | 10 separate password-protected systems |

---

### STRIDE Threat Model

> Use STRIDE during design — before building. For every system component, ask: can each of these 6 things happen here?

```
╔══════╦═══════════════════════╦══════════════════════╗
║ Letter║ Threat                 ║ CIA Pillar violated  ║
╠══════╬═══════════════════════╬══════════════════════╣
║  S   ║ Spoofing               ║ Authentication        ║
║  T   ║ Tampering              ║ Integrity             ║
║  R   ║ Repudiation            ║ Non-repudiation       ║
║  I   ║ Information Disclosure ║ Confidentiality       ║
║  D   ║ Denial of Service      ║ Availability          ║
║  E   ║ Elevation of Privilege ║ Authorisation         ║
╚══════╩═══════════════════════╩══════════════════════╝
```

**Example — applying STRIDE to a login form:**

| Threat | Question | Mitigation |
|--------|---------|-----------|
| Spoofing | Can someone log in as another user? | Strong passwords + MFA |
| Tampering | Can someone modify their session token? | HMAC-signed tokens |
| Repudiation | Can a user deny performing an action? | Audit logs with timestamps |
| Info Disclosure | Do error messages reveal usernames exist? | Generic error messages |
| DoS | Can someone lock everyone out with failed logins? | Rate limiting + lockout |
| Elevation | Can a normal user access admin functions? | Role checks on every endpoint |

### Access Control Types

| Type | Who decides access | Example |
|------|------------------|---------|
| **DAC** (Discretionary) | Resource owner | File permissions on macOS |
| **MAC** (Mandatory) | System policy — labels | Military classified systems |
| **RBAC** (Role-Based) | User's role | Admin vs user vs guest |
| **ABAC** (Attribute-Based) | Policy + attributes | "Finance staff in UK during business hours" |

### Secure Development Lifecycle

```
Plan → Design → Build → Test → Deploy → Maintain
 │        │        │       │       │        │
Define   Threat   Secure  Pentest  Config  Patch
security model   coding   + SAST  harden  updates
reqs
```

---

## 15 · Legal, Ethical & Regulatory

> **The one-liner:** Cryptography is governed by law. Using the wrong algorithm, weak keys, or building backdoors can result in legal liability — not just security failures.

### Key Legal Frameworks (UK)

| Law / Standard | Who it applies to | What it requires |
|---------------|------------------|-----------------|
| **GDPR** | Anyone processing EU personal data | Encryption of personal data; breach notification |
| **PCI-DSS** | Anyone handling card payments | Encrypt cardholder data in transit + at rest; key management |
| **FCA Regulations** | UK financial institutions | Secure handling of financial data; encryption controls |
| **Payment Services Regulations 2017** | Electronic payment processors | Protect transaction data; customer auth credentials |

**PCI-DSS specifically requires:**
- Encryption of cardholder data in storage and transmission
- Strong cryptographic key management practices
- Failure to comply: fines + increased transaction fees + loss of card processing ability

### The Backdoor Debate

```
ARGUMENT FOR BACKDOORS          ARGUMENT AGAINST
────────────────────            ─────────────────
Law enforcement needs           A backdoor for law enforcement
access to encrypted data        is a backdoor for EVERYONE
for criminal investigations.    who finds it.

                                Security is binary — you either
                                have a secure channel or you don't.
                                A "lawful intercept" backdoor
                                weakens encryption for all users.
```

**Professional stance:** The security community strongly opposes backdoors. Creating intentional weaknesses violates the principle of open design and endangers all users.

### Ethics Quick Reference

| Practice | Ethical? | Why |
|----------|:--------:|-----|
| Using publicly reviewed algorithms (AES) | ✅ | Peer review = stronger security |
| Security through obscurity ("our secret algorithm") | ❌ | Unreviewed, false confidence |
| Inserting backdoors | ❌ | Weakens security for everyone |
| Responsible disclosure of vulnerabilities | ✅ | Gives defenders time to patch |
| Exporting strong crypto to sanctioned states | ❌ | Violates export control law |
| Not encrypting personal data | ❌ | Likely GDPR violation |

### Export Controls
Some countries restrict exporting strong cryptographic technology due to national security concerns. The US Wassenaar Arrangement controls exports of dual-use technologies including cryptographic software above certain key lengths.

---

```
╔══════════════════════════════════════════════════════════════╗
║                    END OF STUDY GUIDE                        ║
║                                                              ║
║  Next step: close this and do active recall.                 ║
║  Write everything you remember — then check the gaps.        ║
║                                                              ║
║  Atomic notes: Knowledge Base/Concepts/                      ║
║  Navigation:   MOC/MOC WM242 Implementing Secure Systems     ║
╚══════════════════════════════════════════════════════════════╝
```

---
*Generated from WM242 lecture materials · June 2026*
*[[MOC WM242 Implementing Secure Systems]] · [[CIA Triad]] · [[AES Advanced Encryption Standard]] · [[RSA]] · [[Digital Signatures]] · [[PKI Public Key Infrastructure]]*
