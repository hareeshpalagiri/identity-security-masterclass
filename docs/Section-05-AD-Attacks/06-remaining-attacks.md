📘 Section 05 — Remaining AD Attack Techniques (Simplified Master Chapter)
A compact, story‑driven summary of all remaining AD attack vectors.

🏹 Mahabharata Analogy —
“Not every battlefield trick needs a full chapter — but the army must know every trick.”
In the war:

Some attacks were large and devastating (like Brahmastra)
Others were small but dangerous (like poisoned arrows, illusions, decoys)
The commanders still trained the army to recognize every single threat,
even if those threats did not deserve a full scroll of training.

This chapter covers all remaining AD attack techniques in one place — simplified, but complete.

⚔️ 1. AS‑REP Roasting
Attack:
If a user account has "Do not require Kerberos pre-authentication" enabled, AD will send an AS‑REP encrypted with the user’s password hash.
Attackers can request this encrypted blob and crack it offline.
Impact:

Recover weak passwords
Immediate lateral movement

Fix:
✔ Ensure no user has pre-auth disabled
✔ Use strong passwords
✔ Enforce MFA where possible

⚔️ 2. Silver Ticket Attacks
Attack:
Silver Tickets are forged Service Tickets (TGS) created using the service account password.
Unlike Golden Tickets (based on KRBTGT), Silver Tickets work only for specific services like:

CIFS (file servers)
HTTP (web apps)
HOST (remote access)

Impact:

Bypass Domain Controller
Persist on specific services
Silent access to servers

Fix:
✔ Strong service account passwords
✔ Use gMSA
✔ Enforce AES-only Kerberos
✔ Monitor unusual TGS activity

⚔️ 3. Enumeration & Reconnaissance
Before any attack, adversaries conduct recon:

LDAP queries (users, groups, SPNs, privileges)
SMB shares enumeration
RPC calls (sessions, services, policies)
DNS zone transfers
Net commands (net user, net group)

Impact:
Recon fuels all later attacks.
Fix:
✔ Limit who can query directory data
✔ Tiered access
✔ Harden LDAP
✔ Monitor enumeration patterns

⚔️ 4. ACL / ACE Abuse (Permission Abuse)
Attackers abuse misconfigured AD permissions like:

GenericAll – full control
GenericWrite – can modify user attributes
WriteOwner – take ownership
WriteDACL – change permissions
Extended Rights – replication rights (DCSync)

Impact:

Escalate privileges without touching passwords
Create hidden persistence
Grant backdoor access to groups or users

Fix:
✔ Regular ACL audits
✔ Remove excessive rights
✔ Monitor changes to admin groups
✔ Use tools (BloodHound / Purple Knight)

⚔️ 5. BloodHound Attack Path Analysis
BloodHound is used by attackers to:

Map entire AD permissions graph
Identify shortest path to Domain Admin
Visualize shadow admin access
Identify misconfigurations at scale

Impact:
Attackers find privilege escalations YOU don’t even know exist.
Fix:
✔ Use BloodHound internally before attackers do
✔ Remove unnecessary edges in the AD graph
✔ Tier your admin accounts
✔ Remove shadow admins

⚔️ 6. GPO Abuse (Privilege Escalation via Group Policy)
Attackers target GPOs because:

GPOs can deploy local administrators
GPOs can run startup scripts
GPOs can install software
GPOs affect thousands of machines

Common abuses:

Modify SYSVOL scripts
Add themselves to local Administrators group
Push malicious scheduled tasks
Replace Registry keys

Fix:
✔ Secure GPO ownership
✔ Monitor SYSVOL integrity
✔ Limit who can modify GPOs
✔ Use “GPO Allow List” approach for Tier‑0/1

⚔️ 7. Skeleton Key Attack
Attack:
Malware injects a “universal password” into LSASS on Domain Controllers.
Effectively:

Any account can authenticate using a master password
while keeping original passwords unchanged.

Impact:

Backdoor to entire domain
Invisible to users
Persist until DCs are rebooted

Fix:
✔ LSASS protection
✔ Credential Guard (where possible)
✔ DC monitoring (Defender for Identity)
✔ Reboot DCs + restore clean state
✔ Patch LSASS vulnerabilities

⚔️ 8. Certificate Services Abuse (AD CS Attacks)
Simplified summary:

ESC1 → Request certificate as any user
ESC2 → Misconfigured template allows privilege escalation
ESC3 → Abuse of enrollment agents
ESC4/5 → Key reuse or template misconfigurations
ESC13 → NTLM relay to certificate services

Impact:

Persistent domain compromise
Full impersonation (via client auth certificates)

Fix:
✔ Harden AD CS
✔ Disable vulnerable templates
✔ Enforce Extended Protection
✔ Restrict enrollment rights

⚔️ 9. Shadow Credentials Abuse
Attackers write malicious values into:
msDS-KeyCredentialLink

This registers FIDO / Passport / Device keys on the victim account.
Effect:
Attacker authenticates as the user without knowing the password.
Fix:
✔ Monitor changes to the attribute
✔ Restrict write permissions
✔ Use Defender for Identity

⚔️ 10. PrinterBug / PetitPotam (NTLM Coercion)
These attacks force a machine to authenticate to attacker-controlled server over NTLM.
Used to trigger:

DCSync
NTLM relay
Hash capture

Fix:
✔ Disable MS-RPRN or restrict access
✔ Enable LDAP signing
✔ Disable NTLM where possible
✔ Patch PetitPotam (modern DCs are protected)

⚔️ 11. RBCD Abuse (Resource-Based Constrained Delegation)
Attackers register themselves as principals allowed to impersonate users to services.
Impact:

Full machine impersonation
Lateral movement
Privilege escalation

Fix:
✔ Validate msDS-AllowedToActOnBehalfOfOtherIdentity
✔ Don’t allow service accounts unnecessary delegation
✔ Monitor attribute changes

⚔️ 12. AdminSDHolder / SDProp Abuse
AdminSDHolder protects privileged groups.
Attackers abuse:

WriteDACL on AdminSDHolder
Modify protected groups
Gain permanent membership

Fix:
✔ Audit AdminSDHolder ACL
✔ Confirm SDProp runs correctly
✔ Restrict who can modify privileged groups

🧵 Mind Map (Simplified)
Remaining AD Attacks
 ├─ AS-REP Roasting
 ├─ Silver Tickets
 ├─ Enumeration / Recon
 ├─ ACL / ACE Abuse
 ├─ BloodHound
 ├─ GPO Abuse
 ├─ Skeleton Key
 ├─ AD CS Abuse
 ├─ Shadow Credentials
 ├─ NTLM Coercion (PrinterBug / PetitPotam)
 ├─ RBCD Abuse
 └─ AdminSDHolder Abuse
