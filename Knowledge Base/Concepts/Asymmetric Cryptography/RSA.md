# RSA — Rivest-Shamir-Adleman

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/asymmetric #status/reviewed

---

## What is it?
The most widely used asymmetric encryption algorithm. Security based on the difficulty of factorising a very large number into its two prime factors.

## The Analogy
I give you the product of two huge prime numbers (e.g. 2,048 digits long). Finding the two original primes is virtually impossible — it would take longer than the age of the universe. That difficulty is your security.

## Key Generation Steps
1. Choose two large primes **p** and **q**
2. Compute **n = p × q** (the modulus — this is public)
3. Compute **φ(n) = (p−1)(q−1)**
4. Choose **e** where gcd(e, φ(n)) = 1 (public exponent)
5. Find **d** where d × e ≡ 1 mod φ(n) (private exponent)
6. **Public key = (e, n)** | **Private key = (d, n)**

## Encryption and Decryption
- Encrypt: **C = Mᵉ mod n**
- Decrypt: **M = Cᵈ mod n**

## Worked Example (from slides)
- p=11, q=13 → n=143, φ(n)=120
- e=7, d=103 (because 7×103 mod 120 = 1)
- Public key: (7, 143) | Private key: (103, 143)

## RSA is Also Partially Homomorphic
E(m1) × E(m2) = E(m1 × m2) — multiplication works on ciphertexts.

## Weakness
- Broken by **Shor's algorithm** on a quantum computer
- Key must be large (2048–4096 bits) to be secure today

## Connected concepts
- [[Asymmetric Cryptography]]
- [[Diffie-Hellman Key Exchange]]
- [[Digital Signatures]] — RSA is one of the signature algorithms
- [[Post-Quantum Cryptography]] — needed when quantum computers arrive
- [[Homomorphic Encryption]] — RSA has partial homomorphic property

---
*Source: WM242 Week 4 | Last reviewed: June 2026*
