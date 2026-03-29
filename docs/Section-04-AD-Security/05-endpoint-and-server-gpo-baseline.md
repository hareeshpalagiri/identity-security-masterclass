🏹 **Mahabharata Strategy Analogy —
“Each warrior enters only the tent meant for them.”**
During the war:

Common soldiers stayed in outer tents
Archers had separate zones
Commanders had restricted sanctum tents
Entry rules were strict:
A foot soldier cannot enter a commander’s tent.
If anyone crossed into the wrong zone →
risk of information leak, ambush, or moral collapse

This separation — tents, weapon areas, strategic halls —
mirrors Tier‑0, Tier‑1, Tier‑2 isolation in Active Directory.

“Trust is defined by where you’re allowed to enter.”
That is exactly what “Endpoint & Server GPO Baseline” enforces.

It ensures that no high‑privilege credential ever lands in a low‑trust endpoint,
just like a Senapati never steps into a commoner’s camp.

🔐 1. What Is a Tier‑Aware GPO Baseline? (Simple Definition)
It is a set of Group Policy Object controls applied at the OU level to enforce:

Who can log on to which machines
Who cannot log on anywhere else
Which tier each machine belongs to
Credential hygiene controls (LAPS, restrictions, protections)
Workstation/server hardening baselines

Purpose:
Stop privileged credentials from being exposed to unsafe devices.
This is a critical component of Microsoft’s Privileged Access Strategy and the Enterprise Access Model.
 [github.com], [github.com]

🧭 2. Why This Baseline Exists — Hastinapura Example

























Without Tiered GPOWith Tiered GPODomain Admin logs into a helpdesk PC → malware steals tokenTier‑0 credentials are blocked from Tier‑2 devicesServer admin logs into user laptop → credential theft → lateral movementTier‑1 admin cannot log into Tier‑2 endpointsHelpdesk credentials spread across serversTier‑2 accounts blocked from all serversOne breach → full forest compromiseBreach is contained to its tier
This implements the clean source principle:
High-trust credentials must NEVER touch low-trust systems.
 [github.com]

🎬 3. Animation Placeholder
[GIF Placeholder: "Tier‑0 admin tries to RDP into Tier‑2 → blocked"]
Scene 1: Tier‑2 laptop infected  
Scene 2: Malware tries to steal DA creds → blocked by GPO  
Scene 3: T0 Admin logs in from PAW → allowed  
Scene 4: GPO policy trees for Tier 0/1/2  


🧠 4. Core Concepts (Simple + Deep)

⭐ 4.1 “Allow Logon” vs “Deny Logon”
The most powerful GPO controls for tier isolation are:

Allow log on locally
Deny log on locally
Allow log on through Remote Desktop Services
Deny log on through RDS

Correct configuration = No wrong-tier logons ever occur.

⭐ 4.2 The Most Important Rule

Tier‑0 accounts must never log on to Tier‑1 or Tier‑2 machines.
Tier‑1 accounts must never log on to Tier‑2 machines.

If violated, the entire security model collapses.

⭐ 4.3 GPO Must Be Linked to Tier OUs
Never link these to the root of the domain.
Always enforce at:
OU=Tier0
OU=Tier1
OU=Tier2

This mirrors how war tents were physically separated.

⭐ 4.4 LAPS (Local Admin Password Solution) Required
Prevents password reuse across systems and stops lateral pivot via local admin accounts.
 [github.com]

⭐ 4.5 Combine With PAWs
Tier‑0 admins must sign in ONLY from PAWs, never normal workstations.

🕸 5. Tiered GPO Architecture (Mermaid Diagram)
PowerShellflowchart TD  subgraph T0[ Tier 0 – Identity & Control ]    T0GPO[GPO: Allow Tier0 Admins<br/>Deny Tier1/Tier2<br/>PAW Only]  end  subgraph T1[ Tier 1 – Servers & Apps ]    T1GPO[GPO: Allow Tier1 Admins<br/>Deny Tier0/Tier2]  end  subgraph T2[ Tier 2 – Workstations ]    T2GPO[GPO: Allow Tier2 Admins / Helpdesk<br/>Deny Tier0/Tier1]  end  T0GPO --> T1GPO --> T2GPOShow more lines
This visually represents downward trust flow only, never upward.

🔧 6. Practical GPO Settings (Copy‑Ready)

✔ 6.1 Tier‑0 GPO (Domain Controllers, PKI, AADC)
Allow Logons:
SG_Tier0_Admins

Deny Logons:
Domain Users
SG_Tier1_Admins
SG_Tier2_Admins
All Non‑PAW Machines

Additional Tier‑0 settings:

Disable PowerShell v2
Enable Credential Guard
Enforce LDAP Signing & Channel Binding
Disable SMBv1
Disable RDP for non‑T0 accounts
Enable Protected Users for Tier‑0 accounts


✔ 6.2 Tier‑1 GPO (Servers)
Allow:
SG_Tier1_Admins

Deny:
SG_Tier0_Admins
SG_Tier2_Admins

Additional:

LAPS enforced
SMB signing required
Restrict interactive logon for service accounts
Harden WinRM & PowerShell Remoting


✔ 6.3 Tier‑2 GPO (Workstations)
Allow:
SG_Tier2_Admins
Helpdesk Groups

Deny:
SG_Tier0_Admins
SG_Tier1_Admins

Additional:

Disable local admin accounts
Enforce LAPS
Block RDP inbound
Harden browser / disable legacy auth
Enable ASR rules (reduce phishing/ransomware)


📂 7. Actual GPO Path (Group Policy Editor)
Computer Configuration
 └─ Windows Settings
    └─ Security Settings
       └─ Local Policies
          └─ User Rights Assignment

Modify these:

Allow log on locally
Deny log on locally
Allow log on through Remote Desktop Services
Deny log on through Remote Desktop Services


⚔️ 8. Attacks This Baseline Stops
🛑 Pass‑the‑Hash from Workstations
Tier‑0 creds never appear on Tier‑2 devices → no hash to steal.
🛑 Lateral Movement (Workstation → Server → DC)
Deny rules block upward logon.
🛑 Credential Residue on wrong tier
No accidental admin logins.
🛑 Golden Ticket expansion
Attackers cannot pivot upward if tier boundaries are respected.
 [github.com]

🛡 9. Defense Strategy — “Right Warrior in Right Tent”
Mandatory

Tier OU structure
Allow/Deny logon GPOs
LAPS everywhere
PAWs for Tier‑0
SMB Signing (especially for T1)
LDAP Signing + Channel Binding on DCs

Recommended

JEA for admin operations
Conditional Access for admin identities
Continuous audit of logon patterns


🔧 10. Quick Commands (Copy‑Paste)
Check effective logon rights:
PowerShellsecedit /export /cfg C:\temp\secpol.infSelect-String C:\temp\secpol.inf -Pattern "SeInteractiveLogonRight|SeRemoteInteractiveLogonRight"Show more lines
Check current tier group membership:
PowerShellwhoami /groups``Show more lines
Check applied GPO:
PowerShellgpresult /rShow more lines
Check LAPS password:
PowerShellGet-LapsADPassword -Identity "PC01" -AsPlainTextShow more lines

🧵 11. Mind Map (Placeholder)
Tiered GPO Baseline
 ├─ Tier 0 (Identity)
 │   ├─ Allow T0 only
 │   ├─ Deny T1/T2
 │   ├─ PAWs only
 ├─ Tier 1 (Servers)
 │   ├─ Allow T1 only
 │   ├─ Deny T0/T2
 ├─ Tier 2 (Workstations)
 │   ├─ Allow T2/helpdesk
 │   ├─ Deny T0/T1
 ├─ LAPS everywhere
 ├─ Credential protection
 ├─ Endpoint hardening
 └─ Monitoring & audit


📚 References


Microsoft Enterprise Access Model (privileged access strategy)
 [github.com]


Tiered Model & Clean Source Principle (Quest Blog)
 [github.com]


Logon restriction enforcement (Ravenswood AD Attack Mitigation)
