# PKI — Public Key Infrastructure

**Module:** [[WM242 Implementing Secure Systems]]
**Tags:** #module/WM242 #year/2 #topic/pki #status/reviewed

---

## What is it?
The complete system — hardware, software, people, policies — for managing digital certificates and public keys at scale.

## The Analogy
A passport system. The government (CA) issues passports (certificates) that bind your photo (public key) to your identity. Border control (relying parties) trust passports because they trust the issuing government. You don't need to personally know every border guard — trust flows through the system.

## Key Components
| Component | Role |
|-----------|------|
| **CA (Certificate Authority)** | Issues and signs digital certificates |
| **RA (Registration Authority)** | Subordinate CA — handles enrolment on CA's behalf |
| **Certificate** | Digitally signed document binding a public key to an identity |
| **CRL** | List of revoked certificates |
| **OCSP** | Real-time certificate status checking |

## PKI Topologies
| Type | Description |
|------|-------------|
| **Single-root** | One root CA issues all certificates — simple, single org |
| **Hierarchical** | Root CA → intermediate CAs → end users — scalable |
| **Cross-certified** | Peer-to-peer — CAs mutually trust each other |

## X.509 Certificate Contents
- Version, Serial number
- Algorithm used to sign it
- Issuer (CA) name
- Validity period (start/end)
- Subject name (who it's issued to)
- Subject's public key

## Certificate Revocation
| Method | How it works | Trade-off |
|--------|-------------|-----------|
| **CRL** | Download a list of revoked certs periodically | Can be stale |
| **OCSP** | Real-time query to CA for single cert status | Requires internet, faster |

## Connected concepts
- [[Digital Signatures]]
- [[X.509 Certificates]]
- [[TLS Transport Layer Security]] — uses PKI for authentication
- [[Certificate Authority CA]]

---
*Source: WM242 Week 7 | Last reviewed: June 2026*
