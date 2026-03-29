📄 05-ADFS-Federation.md
Section 08 → Chapter 05 — ADFS / Federation in Hybrid Identity
This is drop‑in ready for your repo:
docs/Section-08-Hybrid-Identity/05-ADFS-Federation.md

Formatted exactly like your previous chapters (Section 01 → 03 style).

📘 Section 08 — Hybrid Identity
Chapter 05 — ADFS & Federation (Legacy Hybrid Authentication Model)
Medium Depth · Zero‑Trust Aligned · One Full Chapter

🔰 1) Introduction
Active Directory Federation Services (ADFS) is an on‑premises identity federation platform used to authenticate users for cloud or third‑party applications using industry protocols like:

SAML 2.0
WS-Federation
OAuth / OIDC

Before Microsoft Entra ID became the dominant cloud identity provider, ADFS was the primary method to enable:

Single Sign-On (SSO)
Multi-factor authentication
Claims-based authorization
Access to SaaS applications

Today, ADFS is considered legacy, but many enterprises still rely on it because of:

Legacy SAML applications
Strict regulatory requirements
Existing investments in ADFS
Complex authentication dependencies

This chapter explains how ADFS works, why it is still used, its security risks, and how to transition out of it.

🧠 2) Why ADFS Still Matters (in 2026)
Even though Microsoft recommends cloud authentication (PHS/PTA), ADFS still appears in environments due to:
✔ Legacy business apps
Older SAML‑based apps require on-prem federation.
✔ Complex authentication logic
Custom claims rules for:

Employee attributes
Smartcard auth
Certificate-based auth
Issuance transforms

✔ Compliance reasons
Some industries require:

Password validation on-prem
On-prem identity provider control

✔ Enterprise mergers & manual MFA integrations
ADFS is sometimes used as a “bridge” during transitions.
✔ Custom integrations
Some apps hard-coded against:

WS-Fed metadata
SAML metadata
ADFS endpoints


🧩 3) ADFS Architecture Overview
A secure ADFS setup typically includes:
1. ADFS Server (STS – Security Token Service)
Issues authentication tokens after validating user credentials.
2. Web Application Proxy (WAP)

Exposed to the internet
Handles pre-auth
Publishes ADFS externally (HTTPS)

3. Active Directory
Used for user authentication.
4. Relying Party Trusts (RPTs)
Each app integrated with ADFS becomes a Relying Party.
5. Claims Rules
Custom rules that shape user identity information:

UPN
Email
Group memberships
Department attributes


🏗️ 4) How ADFS Authentication Works (High-Level)
1. User accesses application (Relying Party)
2. App redirects user to ADFS (HTTP 302 redirect)
3. User authenticates against AD (Kerberos/NTLM)
4. ADFS generates a SAML token with claims
5. Token returned to application
6. Application validates signature → grants access

When external:

User connects to WAP → ADFS
Same flow, except WAP enforces pre-auth


🔐 5) Federation Protocols Supported
1. SAML 2.0
Most common for enterprise apps.
2. WS-Federation
Legacy Microsoft implementation.
3. OAuth2 / OpenID Connect
Supported but less commonly used; most organizations moved OAuth apps to Entra ID.

⚠️ 6) Security Risks & Common Attack Scenarios
1. Token Signing Key Compromise (Golden SAML)
If an attacker obtains the ADFS token-signing certificate:

They can mint valid SAML tokens
Full tenant compromise
Same impact as Golden Ticket in AD

2. WAP Compromise

WAP is internet-facing
If breached → entry point to ADFS

3. ADFS Server Compromise

Attacker gets AD access via delegated access
Steals token-decrypting keys
Modifies claims rules

4. Credential Attacks

Password spray
Brute force
MFA bypass (for poorly configured ADFS MFA integrations)

5. Weak Claim Rules
Applications may trust:

Weak attributes
Group-based authorization not synced with cloud

6. Lack of Logging
ADFS logs are notoriously complex to read, leading to “blind spots”.

🛡️ 7) Hardening ADFS in Hybrid Identity
✔ 1. Protect Token Signing Certificates

Store certificates securely
Rotate signing certificates regularly
Monitor certificate access

✔ 2. Harden the ADFS Server

Tier‑0 asset — protect like a Domain Controller
No web browsing
No SMB, RDP restrictions enforced
Patching regularly

✔ 3. Harden Web Application Proxy

Place behind reverse proxy / WAF
Enforce TLS 1.2+
Reject weak cipher suites
Lock down local admin access

✔ 4. Monitor ADFS Events
Critical event logs:





















Event SourceImportanceAD FS/AdminToken Issuance, FailuresSecurity LogsAuth failures, Kerberos/NTLM issuesWAP logsExternal phishing/brute-force
✔ 5. Use Modern MFA
Avoid:

RSA hard-coded integrations
SMS-based MFA directly through ADFS

Prefer:

Entra MFA as primary
Phone/Authenticator App
FIDO2 (via cloud integration)


🧭 8) Migrating Away from ADFS (Modern Recommendation)
Microsoft recommends moving to PHS or PTA unless federation is absolutely required.
Migration Steps (High Level)
Step 1 — Inventory All Relying Party Trusts
Classify:

Can app support Entra ID?
SAML vs WS-Fed vs OAuth

Step 2 — Migrate Apps to Entra ID
Use:

Enterprise Applications
App Registrations
SAML/XML metadata import

Step 3 — Redirect Federation Services
Switch domain authentication from ADFS → Entra ID.
Step 4 — Retire ADFS
After monitoring traffic for weeks:

Remove RPTs
Remove WAP
Remove ADFS server safely


Goal: Full consolidation of identity in Entra ID → essential for Zero Trust.


🧪 9) Troubleshooting Scenarios
A) ADFS Loop on Login

Wrong RPT identifier
Wrong SAML endpoints
Missing claim rules

B) ADFS Not Issuing Tokens

Certificates expired
ADFS service account password expired
Wrong relying party settings

C) MFA Challenge Not Triggering

Claims rules misconfigured
ADFS MFA adapter error

D) External Login Fails

WAP connectivity
TLS mismatch
Firewall rule misconfiguration


🧾 10) Summary
ADFS is a powerful but legacy federation platform.
It provides SSO and claims-based authentication for older applications, but carries significant complexity and security risk.
A secure approach requires:

Strong protection of token signing certs
Hardened WAP & ADFS
Proper logging & monitoring
Tight claim rules
Migration to Entra ID wherever possible

The long-term Zero Trust goal is clear:

Reduce ADFS footprint → migrate to cloud authentication → modernize access control.
