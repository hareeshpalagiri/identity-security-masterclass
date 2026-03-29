📘 04 — DC Sync & DC Shadow Attacks (Replication Abuse Against Domain Controllers)
A simple, deep, Mahabharata‑based explanation — GitBook‑ready.

🏹 **Mahabharata Analogy —
“When spies infiltrate the king’s scribes and rewrite the royal records.”**
In Hastinapura:

Only trusted scribes could access the royal records room
These records contained genealogies, laws, land rights, royal commands
If an enemy infiltrated the scribes, they could:

Copy confidential documents
Change genealogy to elevate imposters
Modify orders without the king’s knowledge
Insert fake commands as if written by the king



If a scribe is compromised → the kingdom itself is compromised.
This is DC Sync / DC Shadow.

They are attacks against the replication mechanism of Active Directory itself.


DC Sync = Copying the kingdom’s secrets
DC Shadow = Rewriting the kingdom’s secrets

These attacks target the heart of Tier‑0 — Domain Controllers — the core trust plane described in Microsoft's privileged access model. [github.com]

🔐 1. What Are DC Sync & DC Shadow? (Simple Definitions)
DC Sync
An attacker impersonates a Domain Controller and requests secrets via the replication API.
They can extract:

ALL NTLM password hashes
ALL Kerberos AES keys
The KRBTGT account key

This enables:

Golden Ticket
Pass‑the‑Hash
Full domain compromise

DC Shadow
An attacker registers a fake malicious Domain Controller and performs unauthorized replication to push changes into AD.
They can:

Insert SIDHistory
Add themselves to Domain Admins
Modify privileged attributes covertly
Create persistence accounts
Poison directory data

This is stealthy and extremely hard to detect.

🧭 2. Why These Attacks Work — Hastinapura Parallel





























Mahabharata AnalogyAD Attack InterpretationTrusted scribes replicated royal records across provincesDomain Controllers replicate directory dataIf enemy masquerades as a scribe → they can read everythingDC Sync → attacker reads password hashesIf enemy injects fake scrolls into archivesDC Shadow → attacker writes hidden AD changesRoyal system assumes all scribes are honestAD assumes replication partners are trustedNo citizen can detect forged ordersDomain users cannot detect forged directory objects
The kingdom falls if the scribes fall.
AD falls if DC replication falls.

🎬 3. Animation Placeholder
[GIF Placeholder: “Attacker impersonates DC → pulls password hashes → registers rogue DC → pushes malicious changes”]

Scene 1: Attacker steals replication permissions  
Scene 2: Runs DC Sync and fetches KRBTGT hash  
Scene 3: Creates Golden Ticket  
Scene 4: Registers rogue DC via DC Shadow  
Scene 5: Pushes admin rights secretly  
Scene 6: Blue team confused — directory ‘looks normal’  


🧠 4. Core Concepts (Simple + Deep)

⭐ 4.1 AD Replication = Ultimate Trust Path
Active Directory replication allows controllers to exchange:

Password hashes
Kerberos keys
Security descriptors
Group memberships
Privileged attributes

This replication trust path is part of Tier‑0 privileged access pathways described by Microsoft’s EAM model. [github.com]

⭐ 4.2 Who Can Perform Replication?
Accounts with domain replication rights:

Domain Admins
Enterprise Admins
Built‑in Administrators
Domain Controllers (machine accounts)
Accounts with DS-Replication-Get-Changes* rights

If ANY of these accounts are compromised → DC Sync becomes possible.

⭐ 4.3 DC Sync = “Read Everything”
Attacker replicates:

unicodePwd
objectSid
sAMAccountName
ntPwdHistory
msDS-KeyCredentialLink
msDS-SupportedEncryptionTypes

This includes KRBTGT keys → Golden Ticket automatically possible.

⭐ 4.4 DC Shadow = “Write Anything”
Attacker:

Registers new DC metadata
Injects changes via replication
Changes persist even after they leave
Hard to detect because logs appear “legitimate”


🕸 5. DC Sync / DC Shadow Attack Flow (Mermaid Diagram)
Mermaidflowchart TDA[Compromised Admin or Server] --> B[Steal Replication Rights]B --> C{DC Sync?}C -->|Yes| D[Pull Password Hashes<br>KRBTGT Hash<br>User Secrets]D --> E[Golden Ticket / PtH / Full Domain Compromise]C -->|No, DC Shadow| F[Register Rogue DC<br>Modify AD Objects]F --> G[Inject Persistence<br>Add DA Rights<br>SIDHistory Abuse]G --> H[Stealthy Long-Term Control]Show more lines

🔧 6. Hands‑On Attack Examples (Lab‑Only)
⚠ Only perform in an isolated lab.

✔ 6.1 DC Sync Using Mimikatz
PowerShellmimikatz.exelsadump::dcsync /user:contoso\krbtgtShow more lines

✔ 6.2 DC Shadow Using Mimikatz (Typical)
PowerShellmimikatz.exelsadump::dcshadow /object:User1 /attribute:memberOf /value:"CN=Domain Admins,CN=Users,DC=contoso,DC=local"Show more lines
This pushes unauthorized admin membership via replication.

✔ 6.3 Detect “Hidden” Permissions
PowerShellGet-ADObject -LDAPFilter "(adminCount=1)" -Properties *Show more lines

⚔️ 7. Real‑World Attack Scenarios

🛑 7.1 APT Stealth Persistence
APT groups compromise DC → use DC Sync → steal KRBTGT → build Golden Tickets → long-term persistence.

🛑 7.2 Insider Admin Escalation
Malicious admin grants themselves replication rights → DC Sync → escalate privileges → hide tracks.

🛑 7.3 Supply‑Chain Attack
A compromised server with delegated replication rights can perform DC Sync invisibly.

🛑 7.4 Rogue DC via DC Shadow
Attacker registers rogue DC metadata → pushes persistence objects (SIDHistory, admin membership, credential material).

🛡 **8. Defense Strategy —
“Guard the royal records room above all else.”**
Drawn from Microsoft’s privileged access strategy and EAM guidance.
 [github.com]

⭐ 8.1 Protect Tier‑0 Systems (DCs) Absolutely

No admin logons from unsafe endpoints
Use PAWs for Domain Admins
Disable internet on DCs
Patch aggressively
Run LSASS as a protected process


⭐ 8.2 Limit Accounts with Replication Rights
PowerShellGet-ADPermission -Identity "DC=contoso,DC=local" |   Where-Object {$_.ExtendedRights -match "Ds-Replication"}Show more lines
Remove any non‑essential accounts.

⭐ 8.3 Enable Protected Users for Sensitive Accounts
Prevents NTLM usage → reduces credential theft.

⭐ 8.4 Monitor Replication Events

Event ID 4662 with replication rights
Monitoring unusual DRS requests
SIEM alerts for DS-Replication-Get-Changes assignments


⭐ 8.5 Deploy Microsoft Defender for Identity
Detects:

DCSync behavior
Suspicious replication
Unusual DC metadata changes


⭐ 8.6 KRBTGT Rotation (If KRBTGT May Be Compromised)
Reset twice:
Reset-KrbtgtKeys twice, 12–24 hours apart


⭐ 8.7 Block Lateral Movement Paths

Tier isolation
Firewall segmentation
No Domain Admin on Tier‑1 or Tier‑2 systems
Enforce RDP restrictions


🔧 9. Blue Team Quick Commands (Copy‑Ready)
Find accounts with replication rights:
PowerShellGet-ADObject -SearchBase "DC=contoso,DC=local" -LDAPFilter "(objectClass=*)" -Properties * |  Where-Object {$_.nTSecurityDescriptor -match "Replication"}Show more lines
Detect potential DC Shadow metadata:
PowerShellrepadmin /showobjmeta dc01 "CN=Configuration,DC=contoso,DC=local"Show more lines
Compare DC attribute versions:
PowerShellrepadmin /showattr dc01 "CN=User1,CN=Users,DC=contoso,DC=local"Show more lines

🧵 10. Mind Map (Placeholder)
DC Sync / DC Shadow
 ├─ Requirements
 │   ├─ Replication Rights
 │   ├─ DC Compromise
 ├─ DC Sync
 │   ├─ Pull Hashes
 │   ├─ KRBTGT Theft
 ├─ DC Shadow
 │   ├─ Rogue DC Registration
 │   ├─ Unauthorized Attribute Injection
 ├─ Effects
 │   ├─ Golden Ticket
 │   ├─ Persistent Priv Esc
 │   ├─ Hidden Backdoors
 ├─ Defenses
 │   ├─ Protect Tier0
 │   ├─ Limit Replication Rights
 │   ├─ MDI Monitoring
 │   ├─ KRBTGT Rotation
 │   ├─ JEA/JIT/PIM


📚 References


Microsoft Enterprise Access Model — safeguarding control and data planes
 [github.com]


Tiered Administration & Credential Protections (Quest Blog)
 [github.com]
