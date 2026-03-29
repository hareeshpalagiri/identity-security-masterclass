📘 02 — AD Audit Configuration (Active Directory Auditing Essentials)
A medium‑depth, Mahabharata‑aligned guide for configuring proper auditing in Active Directory for monitoring, threat detection, and IR.

🏹 **Mahabharata Analogy —
“Placing watchtowers around the kingdom.”**
In the Mahabharata:

Yudhishthira deployed watchtowers across the borders.
Guards recorded every:

entry,
exit,
suspicious movement,
messenger arrival,
weapon transport.



Without these watchtowers, the Pandavas would never detect
the spies sent by Shakuni or the ambushes from the Kaurava camp.
AD auditing works the same way:

You place ‘watchtowers’ (audit policies & logs) around your directory
to detect suspicious activity long before damage happens.


🔐 1. What Is AD Auditing? (Simple Definition)
Active Directory auditing is the configuration of:

Group Policy audit settings
Advanced audit policies
SACLs on AD objects
Domain Controller security logs

…to capture essential events related to:

logons
changes in accounts
privilege escalation
password resets
replication abuse (DCSync)
group membership changes
GPO changes
object modifications

AD auditing = the visibility layer for threat detection and incident response.

🧭 2. Why AD Audit Configuration Is Critical
✔ Detect breaches early
Logon anomalies, password changes, RDP access, and privilege escalation.
✔ Track lateral movement
Attackers often move silently between machines.
✔ Monitor privileged groups
Admins added to Domain Admins? You must know instantly.
✔ Investigate incidents
Audit logs are the “battle history” you read during IR.
✔ Mandatory for modern security
Defender for Identity, Sentinel, and SIEM solutions depend on audit data.

🧱 3. Core Audit Categories You MUST Enable
AD auditing consists of several categories.
✔ 3.1 Logon / Logoff
Captures authentication attempts.
✔ 3.2 Account Logon
Kerberos ticket events (for DCs).
✔ 3.3 Account Management
Users/groups created, deleted, modified.
✔ 3.4 Directory Service Access
AD object modifications (SACL-based).
✔ 3.5 Policy Change
Audit policy tampering, GPO edits.
✔ 3.6 Privilege Use
Detect misuse of sensitive privileges.
✔ 3.7 Object Access
Folder/file/object access.
✔ 3.8 System Events
System restarts, log clearing, security channel events.

⚙️ 4. How to Enable Advanced Auditing (GPO)
Configure via:
Group Policy → 
 Computer Configuration → 
  Policies → 
   Windows Settings → 
    Security Settings → 
     Advanced Audit Policy Configuration

Enable the following subcategories:

⭐ 4.1 Account Logon
Audit Kerberos Authentication Service
Audit Kerberos Service Ticket Operations


⭐ 4.2 Logon/Logoff
Audit Logon
Audit Logoff
Audit Special Logon
Audit Other Logon/Logoff Events


⭐ 4.3 Account Management
Audit User Account Management
Audit Computer Account Management
Audit Security Group Management
Audit Distribution Group Management
Audit Other Account Management Events


⭐ 4.4 Directory Service Access
Audit Directory Service Changes
Audit Directory Service Access


⭐ 4.5 Policy Change
Audit Authentication Policy Change
Audit Authorization Policy Change
Audit Audit Policy Change


⭐ 4.6 Privilege Use
Audit Sensitive Privilege Use


⭐ 4.7 Object Access
Audit File System
Audit Registry
Audit Removable Storage


🧿 5. Configuring SACLs for AD Object Auditing
Even if Directory Services auditing is enabled,
AD does NOT log object-level changes
unless SACLs (System Access Control Lists) are configured.
You must set SACLs on:

Domain root
AdminSDHolder
Domain Admins
Enterprise Admins
Key OUs
Service accounts
GPO containers
GroupPolicy objects
Sensitive objects (KRBTGT, ADFS, privileged groups)

Example:
Open Active Directory Users & Computers →
View → Advanced Features →
Right-click object → Security → Advanced → Auditing.
Enable:
Everyone → All Properties → Success & Failure

For AdminSDHolder:
Domain Admins / Enterprise Admins → Modify, Write, Full Control


🔥 6. Mandatory Auditing for Defender for Identity (DFI)
To get full visibility in DFI, you must enable:

Audit Kerberos Authentication Service
Audit Kerberos Service Ticket Operations
Audit Directory Service Access
Audit Logon
Audit Account Management

DFI relies on these events to detect:

Pass‑the‑Hash
Golden Ticket
DCSync
Recon
Lateral movement
Privilege escalation


⚠️ 7. Common AD Audit Misconfigurations
❌ Audit policies missing on Domain Controllers
DCs require different audit policies than normal servers.
❌ Not enabling “Audit Directory Service Changes”
This prevents capturing GPO, group membership, and object changes.
❌ No SACLs on sensitive groups
You won’t catch privilege escalation events.
❌ Overlogging
Too many events → storage, SIEM overload.
❌ Underlogging
Gaps in data → incomplete investigations.

🛠 8. Recommended AD Audit Baseline
Here is a clean baseline for production:

Domain Controllers
✔ Logon/Logoff
✔ Account Logon
✔ Directory Service Access
✔ Directory Service Changes
✔ Account Management
✔ Policy Change
✔ System Events

Member Servers
✔ Logon/Logoff
✔ Object Access
✔ Policy Change
✔ System Events
✔ Privilege Use

Workstations
✔ Logon/Logoff
✔ Object Access
✔ Policy Change
✔ Process Creation (4688)

🕸 9. High-Value Events to Monitor













































ActionEvent IDNew user created4720User added to DA group4728 / 4732Password reset attempt4723 / 4724Kerberos TGT request4768TGS ticket request4769DCSync attempt4662Audit logs cleared1102Process created4688Service installed4697 / 7045
These map directly to your IR Playbooks.

🧵 10. Mind Map
AD Audit Configuration
 ├─ Audit Categories
 │   ├─ Logon/Logoff
 │   ├─ Account Logon
 │   ├─ Account Mgmt
 │   ├─ Directory Services
 │   ├─ Policy Change
 │   ├─ Privilege Use
 │   └─ System Events
 ├─ SACLs
 │   ├─ Groups
 │   ├─ OUs
 │   └─ Critical Objects
 ├─ Tools
 │   ├─ Event Viewer
 │   ├─ GPO
 │   └─ SIEM
 ├─ Defender for Identity
 └─ IR Enablement


🎯 Summary
AD Audit Configuration is the foundation of:

forensic investigation
threat hunting
lateral movement detection
privilege escalation monitoring
directory security
Defender for Identity signals
Microsoft Sentinel correlation

Without proper audit configuration:
you are blind in Active Directory.
With it:
you gain full visibility into every important identity action in your domain.
