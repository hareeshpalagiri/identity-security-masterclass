📘 Section 06 — Zero Trust

Chapter 05 — Conditional Access (Zero Trust Enforcement)


🔰 1) Introduction
Conditional Access (CA) is Microsoft Entra ID’s real‑time access decision engine. It forms the enforcement layer of Zero Trust, evaluating every sign‑in and applying policies based on identity, device, location, app, risk, and session context.
Instead of trusting a login just because the password is correct, CA enforces:

Strong authentication
Device compliance
Location/network rules
Session controls
Risk‑based access


In Zero Trust architecture, Conditional Access = "policy brain" that verifies every access request.


🧠 2) Why Conditional Access Matters
✔ Identity is the new security boundary
Passwords alone are insufficient. CA ensures authentication is context‑aware.
✔ Modern attacks target tokens and sessions
Attackers steal:

Tokens
Cookies
Refresh tokens
Credentials from unmanaged devices

CA detects & stops risky behavior.
✔ Hybrid environments need unified enforcement
CA enforces consistent policy across:

Cloud apps
On-prem apps via Entra Application Proxy
SaaS integrations

✔ Compliance and governance
CA enforces regulatory requirements for:

MFA
Device controls
Session restrictions
Geo/IP filtering


🧩 3) Core Concepts
Conditional Access Policy
A rule evaluated at sign‑in containing:

Conditions (If…)
Controls (Then…)

Signals/Conditions

User / group
Device platform & compliance
App type (Web, O365, legacy)
Sign‑in risk level (Entra ID Protection)
Location / network
Client app type (web, mobile, legacy)

Controls

Require MFA
Require device compliance
Require Hybrid Join
Require Passwordless
Block access
Enforce session restrictions via Defender for Cloud Apps

Grant vs Session Controls

Grant: Allow if MFA is passed
Session: Limit download, enforce conditional session, restrict access


🏗️ 4) How Conditional Access Works (Flow)
[User Sign-in] 
      │
      ▼
[Entra ID collects signals]
   • Identity
   • Device
   • Location
   • Risk
   • App
   • Session context
      │
      ▼
[Evaluate Conditional Access Policies]
      │
      ├── Block? → Access Denied
      ├── Require MFA? → Challenge
      ├── Require Compliant Device? → Intune Check
      ├── Apply Session Controls? → MCAS
      ▼
[Access Granted with Token]


Important: Conditional Access is evaluated on token issuance, not after access begins.
Continuous Access Evaluation (CAE) monitors risky events in real-time.


🔐 5) Security Risks & Threats Addressed
1. Compromised Credentials

MFA requirement
Passwordless (FIDO2 / Authenticator)

2. Token Replay / Refresh Token Theft

CAE revokes tokens in real time
Session restrictions reduce exposure window

3. Impossible Travel & Atypical Behavior

Risk-based policies block suspicious sign-ins

4. Unmanaged Device Access

Block non-compliant, non-hybrid joined devices

5. Legacy Authentication

Block Basic Auth
Block non-modern protocols

6. Malicious App Consent

App Enforcement
Publisher verification enforcement


🛡️ 6) Hardening & Best Practices
✔ 1. Enforce MFA for Everyone
Base policy:

Require MFA for interactive sign-ins
Exempt break-glass accounts only (with strict monitoring)

✔ 2. Block Legacy Authentication
Legacy endpoints bypass CA.
✔ 3. Require Compliant or Hybrid-Joined Devices
Laptop/desktop must be:

Intune compliant
Or Hybrid/Azure AD joined

✔ 4. Protect Admin Roles with Stronger Policies
For privileged roles:

Require MFA
Require compliant device
Disallow risky sign-ins
Restrict to trusted IP ranges

✔ 5. Use Named Locations & IP Policies
Mark:

Corporate offices
Known secure VPN ranges
Countries to block

✔ 6. Browser + App Session Controls
via Microsoft Defender for Cloud Apps:

Block download of sensitive data
Monitor copy/paste or printing from browser
Enforce conditional session with watermarking

✔ 7. Break-Glass Accounts

At least two
Strong unique passwords
Excluded from CA
Alerting on every sign-in


🛠️ 7) Operations — Logs, Events & Troubleshooting
📌 Logs in Entra ID

Sign-in Logs → CA evaluation details
Audit Logs → CA policy changes
Risky Sign-ins → Triggered by risky attempts

📌 Troubleshooting Tools

“What If” tool in CA portal
Sign-in logs → CA policy evaluation
“Report-Only Mode” for testing policies
Sentinel Workbooks for CA

📌 Common Troubleshooting Scenarios
Scenario A — MFA Prompt Loop
Cause:
Multiple CA policies requiring MFA → Conditional chain
Fix:
Consolidate requirements.
Scenario B — Device marked as non-compliant
Cause:
Intune non-compliance or outdated policy
Fix:
Re-evaluate compliance / sync device.
Scenario C — Blocked access unexpectedly
Cause:
Risk level set to “Block High Risk”
Fix:
Validate risky sign-in cause in Entra ID Protection.

🧭 8) Policy Framework: The “Baseline Five” Recommended Set
1. Require MFA for All Users
Strong auth enforcement.
2. Block Legacy Authentication
Prevents password spray and brute-force bypass.
3. Require Compliant Devices for Admins
Admin workstations must be:

Intune managed
Compliant
Encrypted, patched

4. Require MFA for Admin Roles
Critical control.
5. Require Passwordless for High-Risk Scenarios
Use FIDO2/Hello for Business.

🔁 9) Advanced Controls — CA + Zero Trust
Continuous Access Evaluation (CAE)
Revokes tokens when:

Location changes
Password reset
Risk increases
Device compliance changes

Identity Protection Risk-Based Policies
Risk levels:

Low
Medium
High

Enforce:

Block high-risk
Require MFA on medium-risk
Reset password on high-risk user risk

App Enforced Restrictions
Protect data in SaaS apps like:

SharePoint
OneDrive
Teams


🧾 10) Summary
Conditional Access is the core enforcement layer of Zero Trust — ensuring that each access request is validated against real-time signals.
By combining MFA, device compliance, risk analysis, and session controls, CA prevents:

Credential theft
Token replay
Lateral movement
Unmanaged device access
Legacy protocol abuse

A strong CA strategy = A strong Zero Trust posture.
