# Learning Log — 2026-06-01

**Module:** WM242 Implementing Secure Systems
**Phase:** Phase 1 — Ingestion
**Topics covered:** Full module — all 16 weeks
**Session length:** Extended (full module ingestion + system setup)
**Next session planned:** Phase 2 — Active Recall (recommended: 24–48 hours after this)

---

## What Was Covered

Full ingestion of WM242 from raw ZIP/PDF materials at:
`/Users/syedimaduddin/Documents/ISS Module Materials (ALL)`

All 16 weeks processed:
- Week 1 — Introduction to Cryptography (CIA triad, Shannon's principles, Caesar/Vigenère/OTP/Rail Fence ciphers, frequency analysis)
- Week 2 — Symmetric Cryptography (DES, AES, block vs stream, ECB/CBC/CFB/OFB/CTR modes, padding)
- Week 3 — Hash Functions (SHA-256, MD5, salting, HMAC, preimage + collision resistance)
- Week 4 — Asymmetric Cryptography (RSA key generation + worked example, Diffie-Hellman with worked example)
- Week 5 — Key Management (lifecycle phases, 12 steps, KDFs, key storage types)
- Week 7 — Digital Signatures (sign/verify process, RSA vs DSA vs ECDSA, PKI, CA, X.509, CRL, OCSP)
- Week 8 — Secure System Design (8 principles, STRIDE, SDLC, access control types)
- Week 9 — Security Protocols (TLS/SSL handshake, PGP hybrid model, SSH, IPSec)
- Week 10 — SSO Authentication (SSO flow, SAML/OAuth/OIDC/Kerberos/LDAP comparison, MFA)
- Week 11 — Cryptanalysis (attack types, differential/linear cryptanalysis, side-channel attacks)
- Week 12 — Quantum Cryptography (QKD, BB84 protocol, no-cloning theorem, limitations)
- Week 13 — Post-Quantum Cryptography (4 families, NIST standardisation, PQC vs QKD)
- Week 14 — Homomorphic Encryption (PHE vs FHE, BGV/BFV/CKKS, noise problem, Paillier)
- Week 15 — Elliptic Curve Cryptography (ECDLP, key generation, ECDSA/ECDH, popular curves)
- Week 17 — Legal, Ethical & Regulatory (PCI-DSS, FCA, GDPR, export controls, backdoors)
- Week 19 — Secure System Design & Implementation (6-step model, input validation, error handling)

**Practice exam also analysed:** SmartCampus scenario — 5 questions with model answers.

**Outputs created:**
- 20 atomic Zettelkasten notes in Knowledge Base/Concepts/
- 1 MOC (Map of Content) for WM242
- 1 readable Study Guide (narrative format)
- Full second brain project structure set up

---

## What Clicked Well

- **The analogy-first approach worked extremely well.** Every concept was given a concrete everyday analogy before the technical detail. Syed responded positively to this format — keep using it.
- **The meat grinder analogy for hash functions** — one-way, deterministic, irreversible. Landed well.
- **The letterbox analogy for asymmetric cryptography** — slot for posting (public key), key to open (private key). Clear and sticky.
- **The paint mixing analogy for Diffie-Hellman** — the best way to explain why you never transmit the secret.
- **The festival wristband analogy for SSO** — login once, access everything.
- **The glove box analogy for homomorphic encryption** — process without touching.
- **Tables for comparison** (RSA vs DSA vs ECDSA, PHE vs FHE, PQC families) — highly effective for this type of material.
- **Scenario-based practice exam** (SmartCampus) — directly mapped concepts to application. Syed found this format useful.

---

## What Didn't Click / Needs More Work

- **RSA key generation steps** — the modular arithmetic (φ(n), finding d such that d×e ≡ 1 mod φ(n)) was explained but not deeply tested. Likely to be weak in recall.
- **Diffie-Hellman worked example** — the maths was shown but not drilled. May be shaky under exam conditions.
- **AES round operations** — SubBytes/ShiftRows/MixColumns/AddRoundKey explained but the *why* behind each (how it achieves confusion vs diffusion) may not be fully absorbed.
- **FHE noise management** — the bootstrapping concept was mentioned but not fully explained.
- **Homomorphic encryption schemes (BGV/BFV/CKKS)** — names given, brief notes, but distinctions between them are thin.

---

## Questions That Came Up

- How does learning/querying work in this system? *(answered — see README)*
- Should there be a separate readable notes folder? *(answered — Study Guides created)*
- Should there be learning session logs? *(answered — this system)*
- How does the system handle multiple modules that share concepts? *(answered — enrichment model, not rebuild)*

---

## Gaps Identified

- Weeks 6, 16, 18 were not in the available materials — check if these exist and ingest if found
- No atomic notes yet for: TLS detailed handshake, IPSec modes, SAML XML format, Kerberos ticket flow, legal/regulatory specifics
- Phase 2 (active recall) has not been done yet — this is the most important next step
- Phase 3 (scenario testing) not yet done

---

## Useful Things From This Session

- **"Read CLAUDE.md first" prompt** — ensures learning style and context are loaded before every session
- **One question at a time in Phase 3** — don't dump all quiz questions at once. "Wait for my answer before the next question" works well
- **The practice exam format** — analyse a broken system, identify flaws, name attacks, recommend fixes. Syed found this engaging and useful
- **Comparison tables** — very effective for this type of content (protocols, algorithms, attack types)

---

## Where to Pick Up Next

**Recommended next session — Phase 2 Active Recall:**

```
Read CLAUDE.md and Learning Logs/2026-06-01 — WM242 — Phase 1 — Full Ingestion.md

I'm doing Phase 2 active recall on WM242.
I'll write everything I remember from scratch — don't help me yet.
After I paste my recall, tell me:
1. What I got wrong
2. What I missed entirely
3. What was vague or incomplete
4. What to focus on before Phase 3

Specifically probe these weak areas identified in the log:
- RSA key generation steps
- Diffie-Hellman worked example
- AES round operations and what each achieves
- PHE vs FHE distinction
```

**After Phase 2:** Run Phase 3 scenario testing on the weakest topics identified.

---

## Notes

- This was the first session using the Cybersecurity Second Brain system
- The system was built during this session — folder structure, Obsidian vault, GitHub repo, CLAUDE.md, study guide, all 20 atomic notes
- Syed's learning style confirmed: analogies first, fundamentals before detail, visual/tabular formatting, scenario-based testing
- Syed has not attended lectures — starting from zero on most topics. All content came from raw slide PDFs.
- ISS exam was the day after this session — content was taught under time pressure

