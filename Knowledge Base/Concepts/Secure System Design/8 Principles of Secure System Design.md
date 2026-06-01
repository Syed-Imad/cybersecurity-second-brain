# 8 Principles of Secure System Design

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/system-design #status/reviewed

---

## What are they?
Eight foundational rules for designing systems that are secure by default, not bolted on afterwards.

## The Analogy
Building a house. You don't add locks as an afterthought — you design the doors, windows, and layout with security in mind from the blueprint stage.

## The 8 Principles

| Principle | One-line meaning | Example |
|-----------|-----------------|---------|
| **Least Privilege** | Give users only what they absolutely need | A marketing intern can't access payroll |
| **Defence in Depth** | Multiple layers of security — attacker must break all of them | Firewall + login + encryption + monitoring |
| **Separation of Duties** | Split critical tasks — no one person can do everything alone | Two signatures needed to authorise a payment |
| **Fail-Safe Defaults** | When in doubt, deny. Default state is locked, not open | New user account starts with no permissions |
| **Economy of Mechanism** | Keep it simple — complexity hides vulnerabilities | Fewer components = fewer things to break |
| **Complete Mediation** | Check every single access, every single time — no caching of "yes" | Re-authenticate for sensitive operations |
| **Open Design** | Security shouldn't rely on the design being secret | AES is public — its strength comes from the maths, not secrecy |
| **Psychological Acceptability** | If security is too annoying, users will bypass it | Single sign-on instead of 10 separate passwords |

## Exam Scenario Tips
When you see a scenario, map the flaw to its violated principle:
- "Users share admin accounts" → violates **Least Privilege** and **Separation of Duties**
- "The system uses a homemade encryption algorithm" → violates **Open Design**
- "Tokens are cached and never re-checked" → violates **Complete Mediation**
- "The security system is so complex nobody uses it" → violates **Psychological Acceptability**

## Connected concepts
- [[STRIDE Threat Model]]
- [[Secure SDLC]]
- [[Access Control Types]]

---
*Source: WM242 Week 8 | Last reviewed: June 2026*
