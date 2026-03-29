📘 Section 06 — Zero Trust
Chapter 06 — App Registration & Enterprise Applications (Identity Layer for Zero Trust)
Medium Depth — Same Template Format as Earlier Chapters

🔰 1) Introduction
Modern identity security depends heavily on how applications authenticate and authorize users. In Microsoft Entra ID, this is controlled through:

App Registrations → define the identity of applications
Enterprise Applications → define service principals that live inside your tenant

These two components form the basis of authentication flows like OAuth2, OIDC, SAML, API permissions, single sign‑on, and conditional access.
Because poorly configured applications can become shadow admin backdoors, Zero Trust requires strict governance around them.

🧠 2) Why It Matters
✔ Apps today authenticate using identity tokens
OAuth/OIDC tokens, refresh tokens, and SAML assertions are frequently targeted by attackers.
✔ Applications have permissions equal to (or higher than) users

API permissions
App roles
Admin consent
Misconfigured permissions can lead to full tenant compromise.

✔ Lateral movement now often occurs “through apps”
Attackers use:

Consent phishing
Token replay
Malicious service principals
Over‑permissioned API apps

✔ Zero Trust enforcement requires controlling:

Who the app is
What it can request
Which APIs/data it accesses
How users sign in
Conditional Access enforcement


🧩 3) Core Concepts — App Registrations vs Enterprise Applications
A) App Registration (Developer Object)
Represents the “blueprint” of the application.
It defines:

Redirect URIs
Authentication method (OAuth2/OIDC/SAML)
API permissions
Supported account types
Certificates & secrets

You can think of it as:

“The application’s identity template.”


B) Enterprise Application (Service Principal Object)
Represents the instance of the app inside your tenant.
It defines:

Who can sign in
Which groups/users can access
Assigned roles
Conditional Access policies applied
SSO configuration
User provisioning (SCIM)


“Service principal = the application’s identity in your tenant.”


C) Relationship
One App Registration → can have multiple Enterprise Application instances (across tenants).
Example:
App Registration = definition
Service Principal = deployed copy


🏗️ 4) How Application Authentication Works (High-Level Flow)
[User]  
   │
   ▼
[App Requests Authentication]  
   │
   ▼
[Entra ID Authorization Endpoint]  
   │
   ▼
[User signs in + CA policies enforced]  
   │
   ▼
[App receives token → access permitted]

Token types include:

ID Token (authenticates the user)
Access Token (accesses APIs)
Refresh Token (keeps session alive)


🔐 5) Security Risks / Common Attack Patterns
⭐ 1. Consent Phishing
Users grant permissions to malicious apps.
Attackers gain:

Mail.Read
Files.ReadWrite
Directory.ReadWrite.All (dangerous)

⭐ 2. Over‑Permissioned Apps
Applications granted:

“Read/Write all users”
“Read all mailboxes”
“Modify directory settings”

This becomes unnoticed privilege escalation.
⭐ 3. Stolen Client Secret or Certificate
A leaked secret becomes a backdoor login.
⭐ 4. Abused Service Principals
Compromised SPN acts as:

A persistent access token
A privileged automation identity
A stealth privilege escalation vector

⭐ 5. Legacy Auth Apps
Apps using basic auth or legacy APIs bypass Conditional Access.

🛡️ 6) Hardening & Best Practices (Zero Trust Enforcement)
✔ 1. Enforce Admin Consent Workflow
Block users from consenting to third‑party apps.
Enable:
Azure Portal → Entra ID → Enterprise Applications → User Settings → 
User consent for apps: Do not allow user consent

✔ 2. Use Least-Privilege API Permissions
Prefer:

Delegated minimal scopes
App‑only permissions only when required
Custom roles over built‑ins

✔ 3. Replace Client Secrets with Certificates
Lifecycle:

Use certificate‑based credentials
Store in Key Vault
Rotate automatically

✔ 4. Enforce Conditional Access on Apps
Policies like:

Require MFA
Require compliant device
Block high‑risk sign-ins
Require trusted locations

✔ 5. Block Legacy Auth for Apps
Ensure:

SAML is not misconfigured
Basic auth is fully disabled
No fallback to NTLM/Basic

✔ 6. Review Enterprise Apps Monthly
Check:

Who can sign in
Token lifetimes
App roles
API permissions
CA enforcement
Last sign‑in information

✔ 7. Remove Stale Apps
Inactive service principals = potential backdoors.

🛠️ 7) Operations — Logs, Events & Troubleshooting
A) Logs to Collect

Entra ID Sign‑in Logs → App details
Audit Logs → App registration changes
Risky Sign-ins → App anomalies
MCAS App Governance (optional)

B) Troubleshooting Scenarios
Scenario 1 — App fails CA/MFA requirement
Check:

Sign-in logs → CA evaluation
“Sign‑in Frequency” policy
Whether the app supports modern auth

Scenario 2 — Access Token rejected
Check:

Scopes
Audience (“aud” claim mismatch)
Token signing certificate rotation

Scenario 3 — Certificate expired
Fix:

Update app registration → upload new certificate
Re‑deploy to workload services


🧭 8) Governance Lifecycle (Recommended Process)
🟩 Phase 1 – Request
Submit app request with:

Purpose
Required API permissions
Authentication model
Risk classification

🟦 Phase 2 – Review
Security team validates:

Least‑privilege scopes
Data access
Consent model
Conditional Access requirements

🟧 Phase 3 – Deploy

Create App Registration
Configure Enterprise Application
Apply CA policies
Issue certificate credentials

🟥 Phase 4 – Monitor

Audit logs weekly
API permissions monthly
Remove stale apps every quarter


🧾 9) Summary
App Registrations and Enterprise Applications are critical identity components of Zero Trust.
Poorly configured apps can introduce high‑impact security risks such as unauthorized access, token theft, over‑permissioned API access, and consent phishing.
Zero Trust enforcement requires:

Strong admin-consent restrictions
Least-privilege permissions
Certificate‑based credentials
Conditional Access enforcement
Regular app governance

Well-governed applications → hardened identity perimeter → secure access layer.
