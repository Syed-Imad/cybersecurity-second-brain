# Cryptanalysis Types

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/cryptanalysis #status/reviewed

---

## What is it?
The science of breaking cryptographic systems — finding weaknesses without knowing the key.

## The Analogy
A lockpicker's toolkit. Different tools for different locks. The lockpicker doesn't have the key but uses knowledge of how locks work to open them anyway.

## Attack Types (by what the attacker has)

| Attack | What attacker has | Strength |
|--------|------------------|---------|
| **Ciphertext-only** | Only encrypted data | Weakest — uses frequency analysis |
| **Known-plaintext** | Some plaintext + its ciphertext | Medium |
| **Chosen-plaintext** | Can choose plaintexts to encrypt | Strong |
| **Chosen-ciphertext** | Can choose ciphertexts to decrypt | Very strong |
| **Related-key** | Ciphertexts from related keys | Very specific |

## Classical Methods
- **Frequency analysis** — most common ciphertext letter = most common plaintext letter (E in English)
- **Kasiski examination** — finds repeating patterns in polyalphabetic ciphers
- **Index of coincidence** — measures how closely letter frequencies match a language

## Modern Attack Techniques
| Attack | Target | How |
|--------|--------|-----|
| **Brute force** | Any cipher | Try every possible key |
| **Differential cryptanalysis** | Block ciphers (DES) | Study how input differences affect output |
| **Linear cryptanalysis** | Block ciphers | Find linear approximations of cipher operations |
| **Meet-in-the-middle** | Multi-layer encryption | Attack from both ends simultaneously |
| **Side-channel** | Implementation | Timing, power consumption, electromagnetic emissions |

## Differential Cryptanalysis
- Choose pairs of plaintexts with a fixed difference
- Encrypt both, observe output differences
- Certain output differences occur with higher probability — reveals key bits
- Targets the last round first (final round's subkey can be tested against ciphertext)

## Historical Note
- **Al-Kindi** (9th century) — invented frequency analysis
- **Alan Turing** — broke Enigma in WWII using computational cryptanalysis

## Connected concepts
- [[Frequency Analysis]]
- [[AES Advanced Encryption Standard]] — designed to resist differential and linear cryptanalysis
- [[DES Data Encryption Standard]] — vulnerable to differential cryptanalysis

---
*Source: WM242 Week 11 | Last reviewed: June 2026*
