# Digital Signatures

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/pki #status/reviewed

---

## What is it?
A mathematical mechanism that proves a message came from a specific sender and hasn't been altered. Provides authenticity, integrity, and non-repudiation.

## The Analogy
A wax seal on a letter, but one that's impossible to forge. Only you have the unique stamp (private key). Anyone can verify it's genuine using the public design of your stamp (public key). If anyone tampers with the letter, the seal breaks.

## How It Works
### Signing (sender)
1. Hash the document → get a fixed-length digest
2. Encrypt the hash with your **private key** → this is the signature
3. Attach signature to document and send

### Verifying (receiver)
1. Decrypt the signature using sender's **public key** → get the original hash
2. Hash the received document independently
3. If both hashes match → authentic, unaltered, genuinely from the sender

## Three Signature Algorithms
| | RSA | DSA | ECDSA |
|--|-----|-----|-------|
| Security basis | Prime factorisation | Discrete logarithm | Elliptic curve DLP |
| Key size | 2048–4096 bits | 1024–3072 bits | 256–521 bits |
| Best for | SSL/TLS, email | Government | Blockchain, IoT, mobile |

## What Digital Signatures Prove
- ✅ **Authenticity** — came from the private key holder
- ✅ **Integrity** — document unchanged since signing
- ✅ **Non-repudiation** — signer cannot deny signing

## What They Do NOT Prove
- ❌ Confidentiality — signatures don't encrypt the message
- ❌ That the private key hasn't been stolen

## Connected concepts
- [[PKI Public Key Infrastructure]]
- [[Hash Functions]] — signature is an encrypted hash
- [[X.509 Certificates]] — binds a public key to an identity
- [[RSA]] — one signature algorithm
- [[Elliptic Curve Cryptography ECC]] — ECDSA

---
*Source: WM242 Week 7 | Last reviewed: June 2026*
