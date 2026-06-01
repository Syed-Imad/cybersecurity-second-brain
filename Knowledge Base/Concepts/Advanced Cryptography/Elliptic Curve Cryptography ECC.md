# Elliptic Curve Cryptography (ECC)

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/asymmetric #topic/advanced-crypto #status/reviewed

---

## What is it?
A form of asymmetric cryptography based on the algebraic structure of elliptic curves. Achieves equivalent security to RSA with much smaller keys.

## The Analogy
RSA is like a combination lock with 4,096 digits. ECC is a different, cleverer lock that's just as hard to crack but only needs 256 digits. Smaller, faster, and just as secure.

## The Maths (simplified)
- Curve equation: **y² = x³ + ax + b**
- Operations on points on the curve:
  - **Point addition:** P + Q = R (draw a line through P and Q, find where it intersects the curve)
  - **Scalar multiplication:** nP = adding P to itself n times
- **Hard problem:** Given P and Q = nP, finding n is computationally infeasible (ECDLP)

## Key Generation
- Private key: random number **d**
- Public key: **Q = dP** (where P is the publicly known base point)
- Security: knowing Q and P, you cannot find d

## ECC vs RSA

| | ECC | RSA |
|--|-----|-----|
| 256-bit ECC ≈ | — | 3072-bit RSA |
| Speed | Faster | Slower |
| Power consumption | Lower | Higher |
| Ideal for | Mobile, IoT, smartcards | Servers |

## Applications
- **ECDSA** — digital signatures (used in Bitcoin, TLS)
- **ECDH** — key exchange (replaces DH)
- SSL/TLS, SSH, cryptocurrency

## Popular Curves
- **NIST P-256** — widely used in TLS
- **Curve25519** — modern, considered very secure
- **secp256k1** — Bitcoin's curve

## Connected concepts
- [[Asymmetric Cryptography]]
- [[Diffie-Hellman Key Exchange]] — ECDH is the ECC version
- [[Digital Signatures]] — ECDSA
- [[Post-Quantum Cryptography]] — ECC is broken by Shor's algorithm

---
*Source: WM242 Week 15 | Last reviewed: June 2026*
