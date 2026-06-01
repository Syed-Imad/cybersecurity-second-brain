# Key Derivation Functions (KDF)

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/key-management #status/reviewed

---

## What is it?
An algorithm that derives one or more cryptographic keys from a master key, password, or passphrase.

## The Analogy
A master key for a building that generates unique sub-keys for each room. Each sub-key only opens its own door. Compromise one room key and the master and all other rooms are still safe.

## Formula
`Derived key = KDF(input secret, salt, difficulty, key size)`

| Parameter | Purpose |
|-----------|---------|
| **Input secret** | The master key or password |
| **Salt** | Random value — prevents rainbow table attacks |
| **Difficulty** | Number of iterations — makes brute force slower |
| **Key size** | Length of the output key |

## Types of KDFs
| Type | Examples | Use case |
|------|---------|---------|
| **Password-based** | Argon2, bcrypt, scrypt, PBKDF2 | Hashing passwords |
| **Symmetric-key** | HKDF, CMAC | Deriving session keys |
| **Asymmetric-key** | RSA-KEM, ECIES-KEM | Key encapsulation |

> **Argon2** is the winner of the Password Hashing Competition — best choice for passwords today.

## Connected concepts
- [[Key Lifecycle]]
- [[Salting]]
- [[Hash Functions]]

---
*Source: WM242 Week 5 | Last reviewed: June 2026*
