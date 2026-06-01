# Modes of Operation

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/symmetric #status/reviewed

---

## What is it?
Block ciphers encrypt fixed-size blocks. Modes of operation define how to apply a block cipher to messages of any length.

## The Analogy
A stamp that can only stamp one square at a time. Modes are the rules for how you stamp across an entire page — do each square independently? Or use each stamp to influence the next one?

## The 5 Main Modes

### ECB — Electronic Code Book
- Each block encrypted **independently**
- **Problem:** identical plaintext blocks → identical ciphertext blocks. Patterns visible.
- ❌ Never use for real data

### CBC — Cipher Block Chaining
- Each plaintext block is **XORed with the previous ciphertext block** before encrypting
- Needs an **Initialisation Vector (IV)** for the first block
- ✅ Most common for general use
- Error in one block corrupts the next block too

### CFB — Cipher Feedback
- Uses a feedback mechanism — previous ciphertext is encrypted then XORed with plaintext
- Needs IV
- ✅ Error resilient

### OFB — Output Feedback
- Like CFB but feeds back the **output of the cipher**, not the ciphertext
- Needs IV
- ✅ Error resilient — errors don't propagate

### CTR — Counter
- A counter value is encrypted then XORed with plaintext
- ✅ **Parallelizable** — blocks can be encrypted simultaneously
- ✅ Fast

## Padding
Block ciphers need the message to be an exact multiple of the block size. When it isn't, padding is added:
- **PKCS7** — pad with N bytes, each byte has the value N (e.g. 3 missing bytes → `03 03 03`)
- **ISO 10126** — random padding bytes, last byte = number of padding bytes
- **TBC** — if last bit is 0, pad with 1s; if 1, pad with 0s

## Connected concepts
- [[AES Advanced Encryption Standard]]
- [[Symmetric Cryptography]]

---
*Source: WM242 Week 2 | Last reviewed: June 2026*
