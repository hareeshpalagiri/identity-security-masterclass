📘 Section 07 — Audit & Logging
Comprehensive Monitoring for Active Directory, Entra ID & Hybrid Identity

🔰 1. Introduction
Audit & Logging is one of the most critical disciplines in identity security.
Modern identity attacks (Kerberoasting, Token theft, MFA fatigue, Password Spray, DCSync) succeed not because controls fail, but because organizations lack:

Proper logging
Centralized visibility
Alerting on the right signals
Retention and investigation capability

This chapter provides a complete reference for what to log, how to log, and how to detect attacks across:

Active Directory (AD)
Microsoft Entra ID (Azure AD)
Hybrid Identity (AD Connect / Cloud Sync)


🧠 2. Why Identity Logging Matters
Identity is the new security perimeter.
Without logging, you cannot detect:

Lateral movement
Credential harvesting
Password spray attempts
MFA abuse
Suspicious token usage
OAuth consent grants
Privileged role changes

Logging enables:

Detection — catch attacks early
Forensics — reconstruct events
Compliance — meet audit requirements
Investigation — understand root cause


🏛️ 3. Logging Categories (Overview)



































CategoryPurposeExamplesAuthentication LogsTrack sign‑insEvent 4624, Entra Sign‑in LogsAuthorization LogsTrack privilege changesPIM logs, AD group changesDirectory Services LogsTrack AD changesEvent 4662Threat Detection LogsSecurity alertsEntra ID Protection, MDI alertsApplication LogsApp access & token usageOAuth token events

🖥️ 4. Active Directory On‑Prem Audit Logging
🔹 4.1 Must-Enable Windows Audit Policies
Enable under Advanced Audit Policy:
Account Logon

Audit Kerberos Authentication Service
Audit Kerberos Ticket Events

Logon/Logoff

Audit Logon
Audit Logoff

Account Management

Audit User Account Management
Audit Group Management
Audit Computer Account Management

Directory Services Access

Audit Directory Service Access
Audit Directory Service Changes


🔹 4.2 Critical AD Event IDs
Authentication





























Event IDDescription4624Successful login4625Failed login (password spray indicator)4768Kerberos TGT request4769Kerberos TGS request (Kerberoasting begins)4776NTLM authentication
Privilege & Group Changes

























Event IDDescription4728User added to Global group4732User added to Local group4720New user account created4722Account enabled
Directory Operations





















Event IDDescription4662Directory object modified5136AD object changes5137New object created
Attack-Specific

























AttackEvent IDsDCSync4662 (replication rights)Golden Ticket4769 with anomaliesKerberoastingHigh volume 4769 requestsPass-the-Hash4624 Type 3 anomalies

☁️ 5. Entra ID (Azure AD) Logging
🔹 5.1 Core Logs
1. Sign‑in Logs
Shows:

Successful sign‑ins
Failed sign‑ins
Conditional Access results
MFA status
Token details

2. Audit Logs
Tracks:

Role assignments
User creation
Group changes
Application consent events
Policy changes

3. Entra ID Protection Logs
Risk detections:

Atypical travel
Impossible travel
Anonymous IP logins
Leaked credentials
Malware-linked sign-ins
Token replay

4. Provisioning Logs
If using SCIM / HR provisioning:

Account created
Updated
Deactivated


🔐 6. Hybrid Identity Logging (AD Connect / Cloud Sync)

























ComponentWhat to LogAzure AD ConnectSync cycles, failures, export errorsCloud SyncObject sync failures, connector errorsPass-through Authentication (PTA)Authentication agent failuresSeamless SSOKerberos tickets issued for cloud
Monitor AD Connect server logs:

Application logs
SyncEngine logs
PTA Agent Operational logs


🧩 7. Detection Use Cases (What to Detect)
🚨 7.1 Password Spray Detection
Indicators:

Many 4625 failures with same source IP
Entra “Password Spray Detected” risk
High volume of sign-in errors 50126 / 50140

🚨 7.2 Kerberoasting
Indicators:

Spike in Event 4769
Service accounts with RC4 tickets
Non-admin users requesting TGS tickets

🚨 7.3 DCSync Attempt
Indicators:

Event 4662 with replication rights
MDI alert: “DCSync attack detected”

🚨 7.4 Suspicious OAuth App Consent
Indicators:

Admin consent granted
Rare permissions (Mailbox.ReadWrite, Directory.ReadWrite.All)

🚨 7.5 Impossible Travel
Indicators:

User signs in from India → 2 mins later from US
Entra ID Protection “Atypical Travel”


📡 8. Centralizing Logs
Options:

Microsoft Sentinel (recommended)
Splunk
Elastic
QRadar
Chronicle

Pipe logs from:

Event Forwarder → Sentinel
Entra → Diagnostic Settings → Log Analytics
Azure AD Connect Server → Agent


📊 9. Sample Architecture Diagram
           [ Active Directory ]
         Events: 4624, 4625, 4768, 4769
                     |
                     v
   [ Windows Event Forwarding / Agent ]
                     |
                     v
                [ Sentinel ]
                   /   \
        [Entra ID Logs] [MDI Alerts]
                   \   /
                [SOC / SIEM]


🛠️ 10. Audit & Logging Best Practices
✔ Identity & Sign-in

Enable MFA logging
Enable Conditional Access logging
Block legacy authentication

✔ Active Directory

Enable Advanced Audit Policy
Forward logs to SIEM
Monitor 4768/4769/4625 consistently

✔ Entra ID

Enable Diagnostic Settings → Send to Log Analytics
Monitor risky sign‑ins
Monitor app consents

✔ Hybrid

Monitor AD Connect Sync cycle failures
Audit PTA agent health
Watch SSO Kerberos ticket anomalies


🧾 11. Summary
Audit & Logging is essential to:

Detect threats early
Investigate incidents
Understand attack paths
Build Zero Trust visibility

Proper logging across AD + Entra ID + Hybrid identity gives you complete control over identity security.
