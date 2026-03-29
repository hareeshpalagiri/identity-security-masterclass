📘 Section 07 — Entra ID Security
Chapter 01 — Entra ID Security Fundamentals
Medium Depth — One Sub‑Chapter Only

🔰 1) Introduction
Microsoft Entra ID Security provides a cloud‑native identity protection framework that defends against modern credential theft, token replay, risky sign‑ins, privilege escalation, and misconfigured applications.
It acts as the security control plane for Microsoft 365, Azure, SaaS apps, and hybrid identity.
This chapter provides a single, consolidated Entra ID Security overview, aligned with Zero Trust identity principles.

🧠 2) Why Entra ID Security Matters
Identity is the new attack surface. Modern attackers rarely start by breaking firewalls — they target:

Passwords (spray, guess, replay)
Token theft
OAuth app misuse
MFA fatigue
Old/basic authentication APIs
Over‑permissioned service principals
Admin accounts with no governance

Entra ID is the central broker for all authentication, so securing it directly protects every connected app and service.

🧩 3) Core Components of Entra ID Security
1. Strong Authentication Stack

Multifactor Authentication (MFA)
Passwordless (FIDO2, Hello for Business, Authenticator)
Number matching for MFA
Modern authentication enforcement

2. Conditional Access Enforcement
Policies evaluate sign‑in context in real-time:

User risk
Sign‑in risk
Device compliance
Managed vs unmanaged device
App type
Network/location

CA ensures Zero Trust enforcement with block, require MFA, require compliant device, or session controls.

3. Privileged Identity and Access Governance

Just‑In‑Time access (PIM)
Remove standing admin assignments
Time‑bound elevation
Access Reviews for privileged roles
Admin segregation (Global Admin vs Workload Admin roles)


4. Identity Protection (Risk-Based Policies)
Entra ID Protection uses cloud intelligence to detect:

Leaked credentials
Impossible travel
TOR/proxy sign-ins
Malware‑linked IPs
Token replay anomalies

It then enforces:

Require MFA
Block access
Force password reset
Notify SOC teams


5. Application & Service Principal Security

Admin consent workflow
Restrict user consent
Require verified publishers
Review app API permissions
Replace secrets with certificates
Disable unused enterprise apps

Service principals are now a primary lateral movement target → keep them tightly governed.

🏗️ 4) How Entra ID Security Protects the Identity Lifecycle
[User Attempts Sign-in]
       │
       ▼
[Strong Auth → MFA/Passwordless]
       │
       ▼
[Conditional Access → Evaluate Risk/Device/App]
       │
       ▼
[Token Issued + Continuous Access Evaluation (CAE)]
       │
       ▼
[Identity Protection → Risk-Based Decisions]
       │
       ▼
[PIM → Privilege Elevation Control]
       │
       ▼
[Auditing / Monitoring / Alerting]

Entra ID ensures every authentication and privileged action is continuously evaluated and enforced.

🔐 5) Common Entra ID Attack Paths
A) Consent Phishing
Malicious app requests excessive permissions → attacker gains mailbox/file access.
B) Token Replay
Stolen refresh tokens used from unmanaged endpoints.
C) MFA Fatigue Attacks
Repeated push notifications → accidental approval.
D) Password Spray
Low‑and‑slow broad credential guessing.
E) Abuse of Over‑Permissioned Service Principals
A compromised app identity = persistent domain-wide access.
F) Legacy Authentication Bypass
SMTP/POP/IMAP/basic auth endpoints still accepting passwords.

🛡️ 6) Hardening & Best Practices (Operational)
✔ Strong Authentication

Enforce MFA for all users
Move admins to passwordless
Prefer FIDO2 or Windows Hello for Business

✔ Conditional Access Essentials

Require MFA
Block legacy authentication
Require compliant or hybrid‑joined devices
Block high‑risk sign-ins
Restrict admin access to trusted networks

✔ Privileged Access Governance

Enable PIM for all admin roles
Eliminate standing Global Admin
Use privileged access workstations (PAWs)

✔ App Security

Disable user consent
Enforce admin consent workflow
Rotate secrets; move to certificates
Audit enterprise apps monthly

✔ Logging & Monitoring
Enable Entra → Diagnostic Settings → send to:

Log Analytics / Sentinel
SIEM
Monitoring platform

Monitor:

Sign‑ins
Audit logs
App activity
Privilege elevations
Risk detections


🛠️ 7) Troubleshooting & Incident Handling
Scenario A — “Unexpected block” from CA
Check:

CA evaluation details
Device compliance
Sign‑in risk reason

Scenario B — Frequent MFA prompts

Session duration policy
Multiple overlapping CA policies
Non-modern clients

Scenario C — Suspicious sign-ins

Investigate via Identity Protection
Map IP patterns
Reset sessions/tokens
Revoke refresh tokens

Scenario D — Unauthorized app created

Remove enterprise app
Block user consent
Review audit logs
Check service principal permissions


🧾 8) Summary
Entra ID Security enforces Zero Trust by combining:

Strong authentication
Conditional Access
Privileged identity governance (PIM)
Identity Protection risk engine
App governance
Comprehensive logging and auditing

A hardened Entra ID tenant significantly reduces the likelihood of credential compromise, token abuse, or privileged escalation — making it one of the most important layers of modern enterprise security.
