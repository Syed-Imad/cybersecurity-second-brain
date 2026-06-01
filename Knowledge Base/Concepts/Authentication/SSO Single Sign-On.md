# SSO — Single Sign-On

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/authentication #status/reviewed

---

## What is it?
Login once, access everything. One authentication event grants access to multiple independent services via a shared token.

## The Analogy
A wristband at a festival. You show your passport (login) once at the entrance. The wristband (token) gets you into every stage, bar, and area without showing ID again.

## How It Works
1. User logs into a central identity provider (e.g. Google)
2. Identity provider creates a token and stores it in the browser
3. User visits another service (e.g. Spotify)
4. Spotify checks the token with Google — not the user's password
5. Google confirms → Spotify grants access

## SSO Protocols Compared

| Protocol | Type | Format | Best for |
|----------|------|--------|---------|
| **SAML** | Auth + authorisation | XML | Enterprise web SSO |
| **OAuth 2.0** | Authorisation (access delegation) | JSON tokens | "Login with Google" |
| **OIDC** | Authentication layer on OAuth 2.0 | JWT (ID token) | Modern SSO with profile info |
| **Kerberos** | Ticket-based mutual auth | Binary tickets | Corporate networks |
| **LDAP** | Directory access protocol | — | Looking up user info |

> OIDC is OAuth 2.0 + "who are you?" on top

## MFA — Multi-Factor Authentication
Requires 2+ of:
- **Something you know** — password, PIN
- **Something you have** — phone, hardware token
- **Something you are** — fingerprint, face, iris

## SSO Benefits vs Risks
| Benefits | Risks |
|---------|-------|
| One credential to manage | Single point of failure — compromise the IdP, lose everything |
| Easier to audit | Token theft allows session hijacking |
| Smaller attack surface | App compatibility issues |

## Connected concepts
- [[OAuth 2.0]]
- [[SAML]]
- [[Kerberos]]
- [[TLS Transport Layer Security]] — SSO tokens travel over TLS

---
*Source: WM242 Week 10 | Last reviewed: June 2026*
