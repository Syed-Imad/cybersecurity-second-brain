# Diffie-Hellman Key Exchange

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/asymmetric #status/reviewed

---

## What is it?
A method for two parties to establish a shared secret over a public channel — without ever transmitting the secret itself.

## The Analogy
Mixing paint colours. You and a friend both start with the same public colour (yellow). You each add your own secret colour privately. You exchange your mixed colours publicly. You each then add the other's mixed colour to your own secret — and both arrive at the same final colour. Anyone watching only ever sees yellow and the two mixed colours — never your secret colours, and never the final result.

## The Steps
1. Alice and Bob agree on public numbers **P** (large prime) and **G** (generator)
2. Alice picks private key **a**, computes **x = Gᵃ mod P**, sends x to Bob
3. Bob picks private key **b**, computes **y = Gᵇ mod P**, sends y to Alice
4. Alice computes shared key: **k = yᵃ mod P**
5. Bob computes shared key: **k = xᵇ mod P**
6. Both arrive at the same k — this is the shared secret

## Worked Example (from slides)
- P=23, G=9
- Alice: a=4 → x = 9⁴ mod 23 = 6
- Bob: b=3 → y = 9³ mod 23 = 16
- Alice: k = 16⁴ mod 23 = **9**
- Bob: k = 6³ mod 23 = **9** ✅ Same secret

## Security
Based on the **discrete logarithm problem** — knowing G, P, and x, finding a is computationally infeasible for large numbers.

## Connected concepts
- [[Asymmetric Cryptography]]
- [[RSA]]
- [[TLS Transport Layer Security]] — DH used in TLS handshake for key exchange
- [[Post-Quantum Cryptography]] — DH is broken by quantum computers

---
*Source: WM242 Week 4 | Last reviewed: June 2026*
