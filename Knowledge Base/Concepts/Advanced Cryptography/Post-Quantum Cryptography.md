# Post-Quantum Cryptography (PQC)

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/quantum #status/reviewed

---

## What is it?
Classical cryptographic algorithms redesigned to resist attacks from quantum computers. Runs on normal hardware — no quantum tech required.

## The Threat
- **Shor's algorithm** — breaks RSA, ECC, Diffie-Hellman (all public-key crypto)
- **Grover's algorithm** — halves the effective key length of symmetric ciphers (AES-256 becomes AES-128 strength)

## PQC vs QKD
| | PQC | QKD |
|--|-----|-----|
| How secure | Mathematical hardness | Laws of physics |
| Hardware needed | Normal computers | Quantum hardware + specialist fibre |
| Scalable | ✅ Yes | ❌ Limited by distance and cost |
| Ready now | ✅ Nearly | ❌ Very niche |

## The 4 Families

| Family | Hard problem | Use |
|--------|-------------|-----|
| **Lattice-based** | Learning With Errors (LWE) | Encryption + signatures — leading candidate |
| **Code-based** | Decoding random error-correcting codes | Encryption (McEliece) — huge keys |
| **Hash-based** | Security of hash functions | Signatures only (XMSS, SPHINCS+) |
| **Multivariate** | Solving nonlinear polynomial systems | Signatures only |

## Standardisation
NIST is leading a global process to standardise PQC algorithms. Selected algorithms published 2024.

## Connected concepts
- [[Quantum Key Distribution QKD]]
- [[RSA]] — broken by Shor's
- [[Elliptic Curve Cryptography ECC]] — broken by Shor's
- [[Lattice-Based Cryptography]]

---
*Source: WM242 Week 13 | Last reviewed: June 2026*
