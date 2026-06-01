# Salting

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/hashing #status/reviewed

---

## What is it?
Adding a random value (the salt) to a password before hashing it, so that identical passwords produce different hashes.

## The Analogy
Two people both use the password "password123". Without salt, they get the same hash — one lookup table cracks both. With salt, you add a unique random string to each before hashing. Now they produce completely different outputs and pre-computed attack tables are useless.

## How It Works
1. Generate a random salt (e.g. `x7fK9p`) per user
2. Combine: `hash("password123" + "x7fK9p")`
3. Store the hash AND the salt in the database
4. On login: retrieve salt, hash the input with it, compare

## What It Defeats
| Attack | Without salt | With salt |
|--------|-------------|-----------|
| **Rainbow tables** | ✅ Works — precomputed hashes match | ❌ Fails — salt makes every hash unique |
| **Dictionary attack** | ✅ Fast — one hash per word | ❌ Slower — must hash with every user's salt |
| **Two users, same password** | Both have identical hashes — one crack, two accounts | Different hashes — must crack separately |

## Connected concepts
- [[Hash Functions]]
- [[Preimage Resistance]]
- [[Collision Resistance]]
- [[Key Derivation Functions KDF]] — KDFs like Argon2 and bcrypt have salting built in

---
*Source: WM242 Week 3 | Last reviewed: June 2026*
