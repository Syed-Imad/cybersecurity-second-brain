# Frequency Analysis

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/foundations #topic/cryptanalysis #status/reviewed

---

## What is it?
A technique for breaking substitution ciphers by counting how often each letter appears and matching it to known letter frequencies in a language.

## The Analogy
Imagine every person in a city wears a coloured hat based on their name. You don't know the code, but you notice the red hat appears far more than any other. In English, the most common name is "Emma" — so red probably means E.

## How it Works
1. Count the frequency of every symbol in the ciphertext
2. In English, letters appear with known probabilities:
   - E (13%), T (9%), A (8%), O (8%), I (7%), N (7%)...
3. The most frequent ciphertext letter → likely E
4. Work outward from there using pattern matching

## Key English Patterns to Know
- **Most common letter:** E
- **Most common bigrams:** TH, HE, IN, ER, AN
- **Most common trigrams:** THE, AND, ING
- **Only 1-letter words:** A, I
- **Most common 2-letter words:** OF, TO, IN, IT, IS, BE
- **Most common repeated pairs:** SS, EE, TT, FF, LL, OO

## Limitations
- Doesn't work on polyalphabetic ciphers (e.g. Vigenère) without modification
- Doesn't work on modern ciphers (AES) — they're designed to defeat this completely

## Connected concepts
- [[Substitution vs Transposition Ciphers]]
- [[Cryptanalysis Types]]
- [[Kasiski Examination]] — extends frequency analysis to polyalphabetic ciphers

---
*Source: WM242 Week 1 | Last reviewed: June 2026*
