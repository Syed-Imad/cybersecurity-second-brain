# Quantum Key Distribution (QKD)

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/quantum #status/reviewed

---

## What is it?
A method of distributing cryptographic keys using quantum physics, where any eavesdropping attempt is physically detectable.

## The Analogy
Sending a message written on soap bubbles. If anyone tries to read it in transit, the bubbles pop — and both sender and receiver immediately know someone was listening.

## Why It's Needed
Shor's algorithm (1994) can break RSA and ECC on a quantum computer. QKD provides a key exchange method whose security comes from physics, not maths — so quantum computers can't break it.

## How It Works
- Uses individual photons (single particles of light) to transmit key bits
- Each photon's polarisation encodes a 0 or 1
- **Uncertainty principle:** measuring a quantum state disturbs it
- **No-cloning theorem:** you cannot copy an unknown quantum state
- Therefore: if Eve intercepts and re-transmits photons, she inevitably introduces detectable errors

## BB84 Protocol (Bennett & Brassard, 1984)
The first and most important QKD protocol:
1. Alice sends photons in one of 4 polarisation states: H, V, +45°, −45°
2. Bob measures each using a randomly chosen basis (H/V or diagonal)
3. After transmission, Alice and Bob compare **which basis they used** (not the results) over a public channel
4. Bits where they used the **same basis** form the key
5. They sacrifice a sample to check for errors — if error rate is too high, Eve was present

## Limitations
- Requires dedicated fibre optic cables — can't share with regular internet traffic
- Distance limited — quantum states degrade over distance (can't use traditional repeaters)
- Much slower than classical key exchange
- Commercial systems exist but expensive and niche

## Connected concepts
- [[Post-Quantum Cryptography]] — mathematical alternative to QKD
- [[RSA]] — what Shor's algorithm breaks
- [[Diffie-Hellman Key Exchange]] — what QKD replaces for key exchange

---
*Source: WM242 Week 12 | Last reviewed: June 2026*
