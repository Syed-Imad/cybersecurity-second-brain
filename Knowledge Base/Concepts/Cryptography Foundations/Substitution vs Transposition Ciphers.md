# Substitution vs Transposition Ciphers

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/foundations #topic/classical-crypto #status/reviewed

---

## What is it?
The two fundamental ways to disguise a message — either replace the letters or rearrange them.

## The Analogy
- **Substitution** — swap every word in a sentence for a code word. "Dog" becomes "Alpha". The sentence structure stays the same.
- **Transposition** — scramble the word order in a sentence. The words are unchanged but the order is shuffled.

## Side by Side

| | Substitution | Transposition |
|--|-------------|--------------|
| **What changes** | The letters themselves | The position of the letters |
| **What stays same** | The positions | The actual letters |
| **Example** | Caesar Cipher, Vigenère | Rail Fence Cipher |

## Classic Examples

### Caesar Cipher
- Shift every letter by a fixed number (key)
- E(x) = (x + n) mod 26
- D(x) = (x − n) mod 26
- Example: n=3, "HELLO" → "KHOOR"
- **Weakness:** Only 25 possible keys — brute force in seconds

### Vigenère Cipher
- Keyword-based shifting — each letter shifted by its corresponding keyword letter
- Harder than Caesar but still broken by frequency analysis

### One-Time Pad (Vernam Cipher)
- XOR each character with a truly random key as long as the message
- **Theoretically unbreakable** — but key must be truly random, never reused, and as long as the message
- Impractical at scale

### Rail Fence Cipher
- Write message in a zigzag across N rails, read row by row
- Example: "SECRET MESSAGE" on 3 rails → "SESEERTESGCMA"

## How to Crack Them
- [[Frequency Analysis]] — E is the most common letter in English. Find the most common letter in ciphertext → likely E.
- Look for common pairs: th, he, in, er
- Look for single-letter words: a, I
- Common 3-letter words: the, and

## Connected concepts
- [[Frequency Analysis]]
- [[Cryptanalysis Types]]
- [[AES Advanced Encryption Standard]] — modern ciphers combine both techniques

---
*Source: WM242 Week 1 | Last reviewed: June 2026*
