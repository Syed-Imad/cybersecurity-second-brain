# Preimage and Collision Resistance

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/hashing #status/reviewed

---

## What are they?
Two core security properties that every cryptographic hash function must have.

## Preimage Resistance
**Definition:** Given a hash h, it should be computationally infeasible to find any input m such that H(m) = h.

**The Analogy:** You see the mince coming out of the grinder. You cannot reconstruct what steak went in.

**Why it matters:** If preimage resistance broke, an attacker who stole a password hash database could reverse every hash to get the original passwords.

## Collision Resistance
**Definition:** It should be computationally infeasible to find two different inputs m1 and m2 such that H(m1) = H(m2).

**The Analogy:** Two completely different steaks should never produce identical mince. If they could, an attacker could substitute one document for another without the hash changing.

**Birthday Attack:** Exploits the fact that collisions become probable far sooner than expected. For a 128-bit hash (MD5), collisions become likely after just ~2⁶⁴ attempts — not 2¹²⁸. This is why MD5 is broken.

## Number of Possible Hashes
`2^(bit length)` — e.g. SHA-256 has 2²⁵⁶ possible outputs.

## Connected concepts
- [[Hash Functions]]
- [[Salting]]
- [[Cryptanalysis Types]] — birthday attacks

---
*Source: WM242 Week 3 | Last reviewed: June 2026*
