Chapter 02 — Entra Connect (Azure AD Connect / Cloud Sync)
Medium Depth · Masterclass Style

🔰 1) Introduction
Entra Connect (formerly Azure AD Connect) is the synchronization and identity bridge between on‑prem Active Directory and Microsoft Entra ID (Azure AD).
It ensures that:

Users
Groups
Passwords
Devices
Key identity attributes

…remain consistent across both identity systems.
Entra Connect is the heart of Hybrid Identity, enabling unified login, cloud authentication, Conditional Access, and seamless SSO.
Microsoft now supports two synchronization technologies:

Entra Connect Sync (Azure AD Connect Classic)
Entra Cloud Sync (Modern, Lightweight, Cloud‑Managed)

This chapter provides a complete overview of both.

🧠 2) Why Entra Connect Matters
A Hybrid Identity environment fails without a reliable sync engine.
Entra Connect enables:
✔ Unified user identity
Same username/password across on‑prem & cloud.
✔ Cloud authentication & MFA
Cloud-first features rely on synced objects.
✔ Device identity
Hybrid join requires device writeback and registration.
✔ Zero Trust access
Conditional Access uses Entra ID identity signals.
✔ Operational consistency
Admins maintain users in AD; changes flow to the cloud.
Without Entra Connect, organizations face fragmented identity, inconsistent access, and security gaps.

🧩 3) Entra Connect Architecture (Classic Sync)
Key Components:
🔹 1. Sync Engine

Handles imports, synchronizations, and exports.
Uses “Connector Space” and “Metaverse”.

🔹 2. Connector Account

AD DS Connector
Entra ID Connector
Requires Tier‑0 protection (extremely sensitive).

🔹 3. Password Hash Sync (PHS)

Password hashes from AD → re‑hashed and synced to Entra ID.

🔹 4. Pass‑Through Authentication (PTA)

Optional agents validate passwords on-prem.

🔹 5. Writeback Features

Password writeback (SSPR)
Device writeback
Group writeback
Hybrid join registration

These help bridge on-prem AD with cloud identity features.

🏗️ 4) Entra Cloud Sync (Modern Sync)
A cloud-native alternative to Azure AD Connect Classic.
Cloud Sync Characteristics

Lightweight agent on-prem
Sync logic runs in the cloud (not locally)
Scales across multiple forests
Built-in high availability
No SQL Express, no metaverse management
Lower administrative burden

Ideal For:

Multi-forest, multi-domain environments
Cloud-first organizations
Lightweight synchronization needs
Eliminating complex AD Connect infrastructure


🔐 5) Authentication Models Supported
Entra Connect supports:

A) Password Hash Sync (PHS)
Recommended for most organizations

Syncs password hash → securely rehashed → Entra ID.
Authentication happens in the cloud.
Enables:

Conditional Access
Identity Protection
Passwordless
CAE (Continuous Access Evaluation)




B) Pass‑Through Authentication (PTA)
Used when password validation must stay on-prem.

Cloud sends authentication request → PTA agent → DC.
Works with Seamless SSO.
Redundancy: Deploy multiple agents.


C) Federation (ADFS)
Legacy & discouraged.

Used only for old SAML apps or regulatory restrictions.
Complex, costly, and not Zero Trust–friendly.


🧩 6) Sync Cycle & Identity Flow
[Active Directory] 
     │  (Import)
     ▼
[Connector Space] 
     │  (Sync Rules)
     ▼
[Metaverse]
     │  (Export)
     ▼
[Microsoft Entra ID]

Cycle frequency:

30 min default sync
Manual delta sync for urgent changes
Event-based provisioning for Cloud Sync


🔐 7) Security Considerations
1. Treat Entra Connect Server as Tier‑0
Because it:

Holds connector credentials
Syncs privileged accounts
Can modify cloud identities

This server must be protected like a domain controller.

2. Protect PTA Agents
PTA is highly sensitive — compromise = password interception opportunity.

Install on secure servers
Use multiple agents for HA
Monitor PTA logs


3. Monitor for Sync Tampering
An attacker may:

Modify synchronization rules
Insert malicious attributes
Add accounts to privileged groups

Monitor:

Entra Audit Logs
Entra Connect Health
Event logs on sync servers


4. Disable Unused Writeback Options
Only enable:

Password writeback
Group writeback
Device writeback
If your organization requires them.

Unused writeback = unnecessary attack surface.

🛠️ 8) Troubleshooting & Operational Tips
Common Issues & Fixes

A) Password not updating in Entra

Check PHS status in Entra Connect Health
Check if password writeback is enabled
Validate sync rules


B) Users not appearing in cloud

Check OU filtering
Check scoping filters
Ensure userPrincipalName format is valid
Validate domain is verified in Entra ID


C) Hybrid Join not working

Check SCP configuration
Check device writeback
Validate GPOs
Review AD Connect Device Registration logs


D) PTA failures

Ensure at least 2 PTA agents
Check connection to DCs
Inspect PTA Agent logs
Check service account permissions


🧭 9) Best Practices (Admin Checklist)
✔ Use PHS + Seamless SSO (recommended baseline)
✔ Deploy multiple PTA agents if using PTA
✔ Keep Entra Connect patched & updated
✔ Enable password writeback for SSPR
✔ Protect Entra Connect as Tier‑0
✔ Migrate to Cloud Sync for multi-forest estates
✔ Enforce naming consistency for UPNs

🧾 10) Summary
Entra Connect is the backbone of Hybrid Identity. It synchronizes identity data between on-prem AD and Microsoft Entra ID to deliver unified access, modern authentication, and Zero Trust capabilities.
There are two sync engines:

Classic Sync (Azure AD Connect) — full control, legacy-heavy
Cloud Sync — modern, lightweight, scalable

Strong identity protection requires:

PHS as the primary authentication method
PTA only when necessary
ADFS only when unavoidable
Hardening of sync servers & PTA agents
Continuous monitoring & health checks

When done right, Entra Connect enables a smooth and secure identity transformation.
