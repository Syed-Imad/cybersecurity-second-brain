# Asymmetric Cryptography

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/asymmetric #status/reviewed

---

## What is it?
Encryption using a mathematically linked key pair — a public key anyone can have, and a private key only you hold.

## The Analogy
A letterbox with a slot. Anyone in the world can post a letter through the slot (public key = the slot). But only you have the key to open the box and read the letters (private key = the box key).

## The Two Uses

| Goal | Who encrypts | Who decrypts | What it proves |
|------|-------------|-------------|----------------|
| **Confidentiality** | Sender uses recipient's **public key** | Recipient uses their **private key** | Only the recipient can read it |
| **Authentication** | Sender uses their own **private key** | Anyone uses sender's **public key** | Only the sender could have sent it |

## Asymmetric vs Symmetric
| | Symmetric | Asymmetric |
|--|-----------|-----------|
| Keys | 1 shared key | Public + private pair |
| Speed | Fast | Slow (100–1000× slower) |
| Key exchange | Problem | Solved |
| Use for | Bulk data | Key exchange, signatures |

## In Practice: Hybrid Encryption
Almost all real systems (TLS, PGP) use **both**:
1. Asymmetric to securely exchange a symmetric key
2. Symmetric to encrypt the actual data

## Connected concepts
- [[RSA]]
- [[Diffie-Hellman Key Exchange]]
- [[Elliptic Curve Cryptography ECC]]
- [[Digital Signatures]]
- [[TLS Transport Layer Security]] — uses hybrid encryption

---
*Source: WM242 Week 4 | Last reviewed: June 2026*
