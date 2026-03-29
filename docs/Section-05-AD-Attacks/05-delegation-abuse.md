Chapter 05 — Delegation Abuse (Unconstrained / Constrained / RBCD)
(Medium Depth, aligned with earlier AD chapters)

🔰 1) Introduction
Kerberos Delegation allows a service to act on behalf of a user when accessing another service.
It was designed to support multi‑tier applications (e.g., Web → App → SQL).
However, misconfigured delegation becomes one of the most dangerous privilege‑escalation paths in Active Directory.
Delegation abuse allows attackers to:

Impersonate domain users
Impersonate privileged users (Domain Admins, Service Accounts)
Access downstream services without needing passwords
Escalate privileges or move laterally

This chapter explains each delegation model, how attackers abuse them, and how to harden your environment.

🧠 2) Why It Matters
Delegation is often enabled incorrectly because:

Admins don’t fully understand the implications
Legacy apps require outdated models
Services run under privileged accounts
No one audits SPNs or delegation flags

Because delegation re‑uses user tickets automatically, a compromised delegated system becomes a privilege-escalation gateway.

Bottom line: If you compromise a server with delegation → you can often impersonate ANY user allowed for delegation.


🧩 3) Core Concepts

Delegation — A service authenticates to another service “on behalf of” a user.
SPN (Service Principal Name) — Used to identify a service account in Kerberos.
TGT / TGS — Tickets used by Kerberos for user authentication and service access.
Forwardable Tickets — Delegation relies on the ability to forward Kerberos tickets.
S4U (Service for User) — API used to request tickets for users without knowing their passwords.


🏗️ 4) Delegation Types in Active Directory
A) Unconstrained Delegation (MOST DANGEROUS)
Definition:
A service configured with unconstrained delegation can request Kerberos tickets to any service on behalf of any user who authenticates to it.
Security Impact:
If an attacker compromises that server or service account, they can:

Steal TGTs from memory
Impersonate privileged users
Access any service in the domain
Perform Golden‑ticket‑like operations without krbtgt hash

Abuse Example:
If Domain Admin logs into a server with unconstrained delegation enabled → attacker dumps memory → extracts DA’s TGT → full compromise.
How to identify:
The account has this flag enabled:
“Trusted for delegation”

B) Constrained Delegation (KCD)
(Still risky but safer than unconstrained)
Definition:
A service can only delegate to specific, explicitly allowed services.
Example:
WebApp → SQL DB
WebApp can impersonate user only to MSSQL/SQL01, not anything else.
Abuse Impact:
If attacker compromises the WebApp:

They impersonate any user to the allowed back‑end services
They bypass MFA for that back‑end service
They can request service tickets via S4U2Proxy and S4U2Self

Still dangerous if misconfigured:

If WebApp runs as a privileged account
If back‑end service is sensitive (file server, LDAP, SQL)


C) Resource-Based Constrained Delegation (RBCD)
(The most modern and flexible model)
Definition:
Instead of the front‑end service deciding whether it can delegate, the back‑end resource decides “who is allowed to impersonate users”.
Represented by attribute:
msDS‑AllowedToActOnBehalfOfOtherIdentity
Why attackers love RBCD:
If attacker can modify ACLs on a target computer account, they can:

Add their own compromised machine/service
Allow it to impersonate ANY user (including Domain Admin)
Request TGS tickets for privileged accounts
Achieve DA‑level compromise without krbtgt hash

This is one of the most abused delegation models in modern AD attacks.

🔐 5) Security Risks / Common Attack Patterns
1) Unconstrained Delegation Abuse

Dump LSASS → extract TGTs
Use Rubeus to export & reuse tickets
Privilege escalation → steal Domain Admin tickets
Pass-the-ticket to DCs, SQL servers, etc.

2) Constrained Delegation Abuse

Abuse S4U2Self to impersonate users
Abuse S4U2Proxy to access back‑end services
Impersonate high-priv users to SQL/LDAP services

3) RBCD Attack Path

Modify msDS-AllowedToActOnBehalfOfOtherIdentity
Register a fake machine account (computer account quota allows 10 per user)
Delegate it to the target server
Use Rubeus / Impacket to impersonate ANY user
Gain code execution on high-value systems


🛡️ 6) Hardening & Best Practices
1. Eliminate Unconstrained Delegation

Search for accounts with unconstrained delegation:
PowerShellGet-ADObject -Filter {TrustedForDelegation -eq $true} -Properties *Show more lines

Replace with:

Constrained Delegation (if legacy app uses it)
RBCD (safer and fine-grained)
Kerberos protocol transition where needed




2. Restrict Constrained Delegation

Avoid delegating to sensitive back‑end services (e.g., LDAP on DCs)
Restrict to only required services
Ensure service accounts use AES, not RC4


3. Secure RBCD

Protect the ACL of msDS-AllowedToActOnBehalfOfOtherIdentity
Block unconstrained computer creation (set ms-DS-MachineAccountQuota = 0)
Monitor for unusual computer account creation
Monitor every modification of the RBCD attribute


4. Identify Delegation Misconfigurations
Search for delegation usage:
PowerShellFind-ADDelegationShow more lines
(using community tools like ADRecon, Bloodhound collectors, DSInternals)

5. General Hardening

Use gMSA for service accounts (random, regularly rotated passwords)
Disable RC4 for service accounts
Ensure Kerberos Pre-auth is enabled for all users
Audit all delegation flags quarterly
DCs and critical servers must never have delegation enabled


🛠️ 7) Logs, Events & Detection (SOC View)
Key Events

4769 — Service ticket request (TGS)
4624 Type 3 with abnormal impersonation
4738 — User account modifications
4742 — Computer account changes
5136 — Directory object modification (critical for RBCD)

Indicators of Delegation Abuse

Sudden spike in 4769 for SPNs tied to service accounts
Unexpected S4U2Self/S4U2Proxy ticket patterns
New computer accounts created by end users
Modification of RBCD attribute on servers
Ticket requests for high-privileged users by low-privileged machines


🧾 8) Summary
Delegation is powerful — but dangerous when misconfigured.
Unconstrained delegation is legacy and unsafe, constrained delegation is safer but still risky, and RBCD—while flexible—is highly abusable if ACLs are exposed.
Key defensive priorities:

Remove unconstrained delegation
Harden & limit constrained delegation
Protect RBCD attributes
Monitor ticket patterns and account ACL changes
Use gMSA + AES
Ensure strong SPN hygiene

When done correctly, delegation supports multi‑tier applications safely; when done poorly, it opens the door to complete domain compromise.
