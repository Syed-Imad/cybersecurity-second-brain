# Key Lifecycle

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/key-management #status/reviewed

---

## What is it?
The complete managed journey of a cryptographic key from creation to destruction.

## The Analogy
Like a staff ID card at a company. It gets created (issued), activated (first day), used daily (operational), eventually expires or gets revoked (someone leaves), and is physically destroyed (shredded).

## 4 Phases (NIST SP 800-57)
| Phase | What happens |
|-------|-------------|
| **Pre-operational** | Generation, registration, certification, distribution |
| **Operational** | Activation, usage, backup, rotation, revocation |
| **Post-operational** | Archival, recovery, reactivation |
| **Deletion** | Destruction / zeroization |

## 12 Lifecycle Steps
1. User registration
2. User initialisation
3. **Key generation** — must be truly random
4. Key installation
5. **Key registration** — CA assigns certificate to public key
6. Normal use
7. **Key backup** — short-term, during operational phase
8. **Key update** — replace before cryptoperiod expires
9. **Archival** — long-term offline storage post-use
10. Key de-registration and destruction
11. **Key recovery** — restore from backup if lost (not compromised)
12. **Key revocation** — emergency removal if compromised

## Key Storage Types
| Type | Examples |
|------|---------|
| **Hardware** | Smart cards, HSMs (Hardware Security Modules), tokens — most secure |
| **Software** | Files, databases on computers — convenient but less secure |
| **Hybrid** | Encrypted files on hardware devices |

## Connected concepts
- [[Key Derivation Functions KDF]]
- [[Certificate Authority CA]]
- [[CRL Certificate Revocation List]] — key revocation mechanism for public keys

---
*Source: WM242 Week 5 | Last reviewed: June 2026*
