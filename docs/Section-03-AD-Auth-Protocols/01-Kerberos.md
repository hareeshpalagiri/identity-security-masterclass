Chapter 01 — Kerberos (Medium Depth)

🔰 1) What is Kerberos?
Kerberos is the default authentication protocol in Active Directory. It uses tickets and shared secrets to authenticate securely without sending passwords over the network.
Why it matters

Faster and more secure than NTLM
Enables Single Sign‑On (SSO) to domain resources
Forms the basis for many enterprise auth flows and delegation models


🧠 2) Core Concepts

Key Distribution Center (KDC): Runs on every Domain Controller; issues all Kerberos tickets.
TGT (Ticket Granting Ticket): Proof that a user has been authenticated.
TGS (Service Ticket): Grants access to a specific service (file server, SQL, web app).
SPN (Service Principal Name): Unique identifier that maps a service instance to an account (often a service account).
Pre‑authentication: Client proves knowledge of the secret before KDC issues a TGT.


🏗️ 3) How Kerberos Works (High‑Level Flow)
(1) User → DC (AS-REQ): “I am Alice” + pre-auth proof
(2) DC → User (AS-REP): TGT (encrypted with KDC key)

(3) User → DC (TGS-REQ): “I need CIFS ticket for \\filesrv01”
(4) DC → User (TGS-REP): Service Ticket for CIFS/filesrv01

(5) User → File Server: Presents Service Ticket
(6) File Server → Grants access (if ACLs permit)

Where:

AS‑REQ / AS‑REP = Authentication Service exchange (getting TGT)
TGS‑REQ / TGS‑REP = Ticket Granting Service exchange (getting service ticket)


🔑 4) Tickets & Encryption

TGT: Encrypted with the krbtgt account’s secret; only the KDC can read it.
Service Ticket: Encrypted with the service account’s secret (based on the SPN).
Session keys: Shared keys inside tickets used to protect messages between client and service.

Common encryption types (etypes): AES256, AES128, (legacy) RC4.

Best practice: Prefer AES; eliminate RC4 where possible.


🧾 5) Kerberos & Active Directory Objects

User accounts authenticate to get a TGT.
Computer accounts use Kerberos for machine authentication.
Service accounts (standard or gMSA) hold SPNs for services (CIFS/HTTP/MSSQL).
SPN hygiene is critical: duplicate or missing SPNs break auth and can create security risk.


🧩 6) Delegation Models (Overview)

Unconstrained Delegation: Service can reuse user tickets to access any service. Avoid unless absolutely necessary.
Constrained Delegation (KCD): Service can act on behalf of users only to specific back‑end services (safer).
Resource‑Based Constrained Delegation (RBCD): Back‑end resource controls who can delegate to it (more flexible, recommended).


🔍 7) Event IDs & Troubleshooting (Quick Reference)





























ScenarioKey EventsSuccessful logon4624 (Logon success)Failed logon (Kerberos pre‑auth failed)4771TGT issued4768TGS (service ticket) issued4769Service ticket failure4770 / 4771 (context‑dependent)
Tips

For access failures, check if the SPN exists and points to the correct account.
Confirm supported encryption types match between client, service account, and DC.
Time sync (NTP) must be within ±5 minutes.


🛡️ 8) Common Attack Techniques (Awareness)

This section is for defensive awareness—you’ll cover details in your AD Attacks section.



Kerberoasting: Requesting TGS for SPN accounts, then attempting to crack the service account hash offline.

Signals: Spike in 4769 for specific SPNs; RC4 tickets; non‑admin users requesting many service tickets.
Mitigations: Use gMSA, rotate secrets, enforce AES, monitor 4769 patterns, least privilege on SPN accounts.



AS‑REP Roasting: If “Do not require Kerberos pre‑auth” is set, attacker can request AS‑REP and crack offline.

Signals: Unusual 4768 without pre‑auth; flagged user settings.
Mitigations: Ensure pre‑auth is required for all user accounts.



Golden Ticket: Forged TGT using krbtgt hash → full domain access.

Mitigations: Protect DCs, rotate krbtgt twice during incident response, harden Tier‑0.



Delegation Abuse (Unconstrained/KCD/RBCD): Misconfigured delegation can enable lateral movement.

Mitigations: Avoid unconstrained, use KCD/RBCD carefully, audit delegation settings regularly.




🛠️ 9) Hardening & Best Practices
Identity & Policy

Enforce Kerberos pre‑authentication on all user accounts.
Block NTLM where feasible; prefer Kerberos (with AES).
Use gMSA for services; rotate credentials automatically.
Implement tiered administration; protect DCs as Tier‑0.

SPN & Service Hygiene

Avoid SPNs on highly privileged accounts.
Periodically scan for duplicate/missing SPNs.
Prefer AES ciphers; disable RC4 for service accounts where supported.

Monitoring

Forward 4768/4769/4771 to SIEM.
Baseline normal TGS volume per service; alert on spikes.
Watch for user accounts requesting TGS for many distinct SPNs.

Operational

Keep time synchronized (Kerberos is time‑sensitive).
Patch DCs and key services promptly.
Document delegation paths; review KCD/RBCD configurations quarterly.


🧪 10) Quick Troubleshooting Playbook

User can’t access a service


Check SPN exists (setspn -L <account>) and is correct.
Review Event 4769/4771 on DCs & service host.
Verify encryption types (account flags) and time sync.


Kerberoasting suspicion


Query SIEM for unusual 4769 spikes per SPN and per user.
Confirm service accounts use AES and long, random secrets (or gMSA).
Rotate affected service account credentials if needed.


Delegation issue


Map the path (front‑end → back‑end).
For KCD, verify msDS-AllowedToDelegateTo on the front‑end account.
For RBCD, verify msDS-AllowedToActOnBehalfOfOtherIdentity on the resource.


🧾 11) Summary
Kerberos is the primary AD authentication protocol.
With correct SPN hygiene, strong encryption (AES), enforced pre‑auth, and targeted monitoring (4768/4769/4771), you gain secure, performant SSO and reduce exposure to roasting and delegation‑abuse attacks.
