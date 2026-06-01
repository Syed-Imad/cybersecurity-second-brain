# HMAC — Hash-based Message Authentication Code

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/hashing #status/reviewed

---

## What is it?
A hash computed using both the message and a secret key. Provides integrity AND authentication — not just integrity like a plain hash.

## The Analogy
A plain hash is like a wax seal on a letter — anyone can see if it's been broken. HMAC is like a wax seal where only you and the recipient have the unique stamp. If the seal matches, you know it came from someone with the key.

## Plain Hash vs HMAC
| | Plain Hash | HMAC |
|--|-----------|------|
| Input | Message only | Message + secret key |
| Proves | Data unchanged | Data unchanged AND came from key holder |
| Attack | Anyone can recompute hash after tampering | Can't fake without the key |

## How HMAC Is Computed
Two-step hashing process:
1. **Inner hash:** `H(inner_key_pad + message)`
2. **Outer hash:** `H(outer_key_pad + inner_hash_result)`

Formula: `HMAC = H(outer_key_pad, H(inner_key_pad, message))`

Two passes prevent length extension attacks.

## Where It's Used
- SSL/TLS
- IPsec
- SSH
- API authentication tokens

## Connected concepts
- [[Hash Functions]]
- [[MAC Message Authentication Code]]
- [[TLS Transport Layer Security]]
- [[SSH]]

---
*Source: WM242 Week 3 | Last reviewed: June 2026*
