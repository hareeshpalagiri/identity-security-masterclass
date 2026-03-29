 05 — Incident Response (IR) Playbooks
A clean, professional, SOC‑aligned guide to identity-focused incident response & SOAR automation in Microsoft Sentinel.

🎯 Purpose of This Chapter
This section gives you:

Practical incident response workflows
Real-world attack scenarios
Standard operating procedures (SOPs)
Sentinel automation playbooks (SOAR)
Analyst checklists

These playbooks are adapted from real SOC environments and are designed to reduce:

Response time
Escalation complexity
Analyst fatigue
Human error


🏹 **Mahabharata Analogy —
“Battlefield counter‑moves against enemy strategies.”**
Just as the Pandavas planned responses to each Kaurava tactic
(Ghatotkacha for Karna, Bhima for Duryodhana, Arjuna for Jayadratha),
modern SOC teams must prepare tactical playbooks for every identity attack.

🧠 1. IR Playbook Philosophy
Every IR playbook consists of:

Detect
Validate
Contain
Eradicate
Recover
Review & Improve

Sentinel SOAR lets you automate 60–90% of these steps.

⚔️ 2. Real‑World IR Scenario Playbooks (Identity-Focused)
🔥 Scenario 1 — Compromised User Account / Suspicious Sign-In
Detection Indicators:

Impossible travel
Multiple failed logons
Sign-ins from unusual IPs
Entra ID risky user alert
MFA fatigue attack
OAuth token misuse


Playbook (Manual / SOC Workflow)
1. Validate

Review Entra sign‑in logs
Confirm MFA success/failure patterns
Check device info (OS, browser, location)
Validate user’s activity with manager

2. Contain

Force password reset
Revoke refresh tokens
Block the user temporarily
Disable the account if needed

3. Eradicate

Remove suspicious OAuth consents
Clear unknown devices from user profile
Reset MFA methods (require re-registration)

4. Recover

Re-enable account
Apply stronger CA policy (e.g., require compliant device)

5. Lessons Learned

Identify root cause (phishing, reused password)
Update CA policies


✔ Sentinel Automation Suggestions (SOAR)
Use a Logic App to automatically:

Suspend the user (Disable-AzureADUser)
Revoke sessions (/invalidate-all-refresh-tokens)
Notify SOC & user’s manager in Teams
Create a ServiceNow ticket
Require MFA re-registration

Trigger:
“UserRiskLevel == High OR SignInRisk == High”


🔥 Scenario 2 — Pass-the-Hash (PtH) or Lateral Movement
Detection Indicators:

Entra sign-in anomalies
Defender for Identity alert: “Suspected Pass-the-Hash”
Unusual NTLM authentication from workstation
Logon type 3 (network logons) from unexpected hosts
Multiple admin logons in short window


Playbook
1. Validate

Confirm unusual 4624/4625 events
Review DFI alert details
Map lateral movement path

2. Contain

Isolate affected hosts through Defender EDR
Disable compromised accounts
Trigger password reset for privileged users

3. Eradicate

Remove malware from compromised endpoints
Rotate local admin passwords (LAPS)
Reset KRBTGT (if domain compromise suspected) — with caution

4. Recover

Reconnect systems
Patch vulnerabilities
Apply PAW usage for admins


✔ Sentinel Automation Suggestions
SOAR workflow:

Auto-isolate endpoint in Defender
Disable suspicious accounts
Rotate LAPS passwords
Alert Tier‑1 & Tier‑2 teams
Send incident card in Teams



🔥 Scenario 3 — Kerberoasting Attempt
Detection Indicators:

High volume of Event ID 4769
Requests for service accounts with weak passwords
DFI alert: “Suspected Kerberoasting”


Playbook
1. Validate

Verify spike in TGS requests
Check which SPNs were targeted
Identify source device

2. Contain

Isolate the initiating machine
Temporarily disable targeted service accounts

3. Eradicate

Reset service account credentials
Move accounts to gMSA where possible
Enforce AES encryption

4. Recover

Audit all SPN service accounts
Document changes


✔ Sentinel Automation Ideas
SOAR Playbook:

Disable service accounts targeted in roasting attempt
Force rotation through automation script
Notify application owners
Update SIEM watchlists for attacker IP



🔥 Scenario 4 — DCSync Attack
Detection Indicators:

Defender for Identity: “Suspected DCSync”
Event ID 4662 with replication privileges
Unexpected usage of DS-Replication-Get-Changes


Playbook
1. Validate

Verify account used for DCSync
Check recent ACL changes
Confirm if the account was supposed to have replication rights

2. Contain

Disable the account immediately
Reset passwords for all privileged accounts
Rotate KRBTGT (twice, safely)

3. Eradicate

Fix ACL misconfigs
Remove unintended replication permissions
Cleanup shadow admins

4. Recover

Validate identity infrastructure
Tighten tiering model


✔ Sentinel Automation
Trigger playbook on DCSync alert:

Disable account
Revoke token
Escalate incident to Tier‑3 automatically
Launch forensic script collection
Notify identity engineering



🔥 Scenario 5 — Golden Ticket Attack (Domain Compromise)
Detection Indicators:

DFI alert
Unusual 4768/4769 patterns
Persistence across resets
Logons with high privileges without corresponding Kerberos requests


Playbook
1. Validate

Confirm DFI Golden Ticket alert
Examine unusual TGT lifetimes

2. Contain

Isolate all affected systems
Disable all privileged accounts
Emergency KRBTGT rotation plan

3. Eradicate

Rebuild compromised DCs
Remove unauthorized accounts
Reset all service account passwords

4. Recover

Re-enable trusted accounts
Rebuild DC trust relationships


✔ Sentinel Automation
Due to severity, automation should be limited:

Auto-open P1 incident
Notify CISO + Identity leads immediately
Pull forensic data automatically (EDR pack)
Provide step-by-step instruction in Teams



🛠 3. Sentinel SOAR Playbook Examples (Automation Blueprints)
Below are automation blueprints in plain English (implementation via Logic Apps):

✔ Automated User Suspension Playbook
Trigger:
High-risk user (from Entra ID or DFI)
Actions:

Disable account
Invalidate all refresh tokens
Require password reset
Require MFA re-registration
Notify SOC + Manager
Open a ticket in ITSM
Add user to "Under Investigation" watchlist


✔ Automated Endpoint Isolation Playbook
Trigger:
Defender for Identity or Defender for Endpoint “Lateral Movement” alert
Actions:

Isolate machine in Defender
Collect forensic artifacts
Dump running processes
Notify SOC Teams channel
Auto-tag machine in Sentinel workbook


✔ Automated Service Account Hardening Playbook
Trigger:
Kerberoasting alert
Actions:

Disable service account
Reset password to random strong value
Email application owner
Check if account can be converted to gMSA
Auto-create change request


✔ Automated DCSync Response Playbook
Trigger:
DCSync detection
Actions:

Disable offending account
Rotate KRBTGT (with human approval gate)
Alert Tier 3
Extract forensic DC logs
Update incident timeline automatically


🧵 4. Mind Map
IR Playbooks
 ├─ Compromised Account
 │   ├─ Validate
 │   ├─ Block
 │   ├─ Reset
 │   └─ Automate
 ├─ Lateral Movement / PtH
 │   ├─ Isolate host
 │   ├─ Disable user
 │   └─ Automate EDR actions
 ├─ Kerberoasting
 │   ├─ Detect SPN targeting
 │   ├─ Reset service accounts
 ├─ DCSync
 │   ├─ Disable account
 │   ├─ KRBTGT rotation
 ├─ Golden Ticket
 │   ├─ Rebuild DCs
 │   ├─ Emergency IR mode
 ├─ SOAR Playbooks
 │   ├─ Auto-disable users
 │   ├─ Auto-isolate machines
 │   ├─ Auto-reset credentials
 │   └─ Auto-notify SOC


🎯 Summary
This IR Playbook chapter provides:

Real-world identity attack response
Standardized SOC procedures
Rapid containment strategies
Automated Sentinel SOAR workflows
Enterprise-class playbooks for AD, Entra, and hybrid identity

With these playbooks, your SOC can respond to:

Compromised accounts
Kerberoasting
PtH / lateral movement
DCSync
Golden Ticket
Hybrid identity breaches

Quickly, consistently, and with automation.
