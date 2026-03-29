📘 Section 06 — Entra ID (Azure AD) Cloud Identity Fundamentals


Welcome to Section 06, the beginning of your journey into the cloud identity world with Microsoft Entra ID — the successor to Azure AD.
While earlier sections focused on:

IAM Core
Active Directory
Authentication Protocols
AD Security Hardening
AD Attack Techniques

This section represents the shift from on‑prem identity → to cloud identity.
Microsoft Learn describes Entra ID as Microsoft’s cloud-based directory & identity management service, providing authentication, SSO, Conditional Access, device identity, and identity governance. [learn.microsoft.com]
This section covers everything from the fundamentals of Entra ID to hybrid identity, application identity, external collaboration, and cloud identity security.

🎯 Learning Outcomes
By the end of Section‑06, you will understand:
✔ How Entra ID is architected (tenants, directories, users, groups, devices)
✔ Modern authentication (OAuth2, OIDC, SAML)
✔ Device identity & join types (Azure AD Join, Hybrid Join, Cloud Kerberos Trust)
✔ Hybrid Identity using Azure AD Connect & Cloud Sync
✔ Entra ID Security hardening & Zero Trust controls
✔ External collaboration (B2B) & customer identity (B2C)
✔ Monitoring, auditing & incident response in Entra
✔ App registrations, enterprise apps, permissions & consent
✔ Identity Protection (risk-based detection)
These topics align directly with Microsoft’s Entra platform capabilities. [us.informa...eb-pro.net]

🗂 Chapters in Section‑06
Below is the complete list of files included in this section:

01 — What is Entra ID?
01-What-is-Entra-ID.md
Introduction to Entra ID, tenants, directories, objects, cloud identity, and Zero Trust principles.

02 — Entra ID Architecture & Topology
02-Entra-ID-Architecture-Topology.md
Tenant-level architecture, directory structure, identity objects, domain services, and role topology.

03 — Entra ID Authentication Protocols (OAuth2, OIDC, SAML)
03-Entra-ID-Authentication-Protocols.md
Modern authentication protocols, token flows, OAuth roles, OIDC claims, and SAML federations.
Supported by Microsoft’s identity platform protocol documentation. [windows-ac...ectory.com]

04 — Entra ID Security Hardening
04-Entra-ID-Security-Hardening.md
MFA, Passwordless, Conditional Access, Identity Protection, device compliance, app governance.
Built on Microsoft’s security & access control guidance. [learn.microsoft.com]

05 — Users, Groups & Devices
05-Users-Groups-Devices.md
User lifecycles, group types (M365/Dynamic/Security), device join models, and identity relationships.

06 — App Registration & Enterprise Applications
06-App-Registration-Enterprise-Applications.md (to be generated)
App identities, service principals, API permissions, consent, SSO methods.

07 — Azure AD Connect (Hybrid Identity)
07-Azure-AD-Connect.md
PHS, PTA, federation, Seamless SSO, Cloud Sync, Hybrid Join, Cloud Kerberos Trust.
Based on Microsoft’s authentication & synchronization architecture. [github.com]

08 — Entra External Identities (B2B/B2C)
09-B2B-B2C.md
Partner collaboration (B2B), customer identity (B2C), federation, social logins, External ID.

09 — Identity Protection (Risk-Based Security)
06-Entra-ID-Protection.md
User risk, sign-in risk, leaked credentials, risk detections, automated remediation.
Based on Microsoft’s Identity Protection engine. [community....eworks.com]

10 — Monitoring, Auditing & Incident Response
10-Monitoring-Auditing-Incident-Response.md
Sign-in logs, audit logs, risk logs, Sentinel integration, SOC workflows, incident response playbooks.
Aligned with Entra’s monitoring and health documentation. [learn.microsoft.com]

🧵 Mind Map of Section‑06
Entra ID Cloud Identity
 ├─ Fundamentals
 │   ├─ What is Entra ID?
 │   ├─ Architecture/Topology
 │   └─ Auth Protocols
 ├─ Security
 │   ├─ MFA/Passwordless
 │   ├─ Conditional Access
 │   ├─ Identity Protection
 ├─ Identity Objects
 │   ├─ Users
 │   ├─ Groups
 │   └─ Devices
 ├─ Hybrid Identity
 │   ├─ PHS
 │   ├─ PTA
 │   ├─ Cloud Sync
 │   ├─ Hybrid Join
 │   └─ Cloud Kerberos Trust
 ├─ App Identity
 │   ├─ App Registrations
 │   ├─ Enterprise Apps
 │   └─ Permissions & Consent
 ├─ External Identity
 │   ├─ B2B
 │   └─ B2C
 └─ Operations & IR
     ├─ Auditing
     ├─ Monitoring
     └─ Threat Response


🎯 Summary
Section‑06 is the complete, modern foundation for understanding Microsoft Entra ID:

How it works
How identity flows in the cloud
How devices and apps join the identity fabric
How to secure it with Zero Trust
How to integrate on-prem AD
How to monitor, audit, and respond
