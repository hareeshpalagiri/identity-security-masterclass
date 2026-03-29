📘 03 — Golden Ticket Attacks (Forging Unlimited Kerberos Privilege)
A deep, story‑driven Mahabharata-style chapter — GitBook Ready.

🏹 **Mahabharata Analogy —
“When someone forges the king’s divine seal.”**
In ancient kingdoms — including Hastinapura — the royal seal was sacred.

Anyone holding the true seal could issue commands
These commands were trusted automatically by all
A forged seal meant absolute disaster
Entire armies could be misled
Siege orders could be falsified
Forts could be opened from the inside

A Golden Ticket attack is the digital equivalent:

The attacker forges a Kerberos Ticket Granting Ticket (TGT) by stealing the KRBTGT key —
and then issues unlimited, unrestricted authentication across the entire domain.

This is the most devastating form of AD compromise.

🔐 1. What Is a Golden Ticket? (Simple Definition)
A Golden Ticket is a forged Kerberos TGT created by an attacker after acquiring the KRBTGT account’s NTLM hash or AES key from a Domain Controller.
Once the KRBTGT key is stolen:

The attacker can forge TGTs for ANY user
Including Domain Admin, Enterprise Admin, krbtgt, or non-existent users
With any group membership
Valid for any duration
Works on any Kerberos-enabled service

The domain trusts the ticket because KRBTGT is the root trust anchor of Kerberos authentication.

🧭 2. Why Golden Tickets Are So Dangerous — Hastinapura Parallel





























Mahabharata ExampleGolden Ticket EquivalentForging the king’s sealForging the KRBTGT keyArmy obeys false ordersDomain Controllers accept forged TGTsImpersonate generals or ministersImpersonate any AD user or adminControl over entire war strategyControl over entire domain authenticationImpossible to detect by appearanceKerberos cannot distinguish forged tickets
Once the KRBTGT key is compromised:

The kingdom (domain) is lost unless the seal (KRBTGT keys) is reset.


🎬 3. Animation Placeholder
[GIF Placeholder: “Attacker steals KRBTGT hash → forges TGT → becomes Domain Admin → accesses everything”]

Scene 1 → Attacker gains DC access  
Scene 2 → Extracts KRBTGT hash  
Scene 3 → Generates Golden Ticket with fake user  
Scene 4 → Accesses all servers  
Scene 5 → Blue team tries logon monitoring → nothing suspicious  
Scene 6 → KRBTGT reset restores trust  


🧠 4. Core Concepts (Simple + Deep)

⭐ 4.1 KRBTGT = Kerberos Root of Trust
KRBTGT account signs all Kerberos tickets in the domain.
If attacker steals its key → attacker becomes Kerberos itself.

⭐ 4.2 Golden Tickets Bypass:

Password expiration
Account lockout
MFA
Smartcard requirement
Group membership checks
SIEM detection (mostly)
Login attempts

Because they are self‑signed with the KRBTGT key.

⭐ 4.3 Golden Tickets Are Valid Until KRBTGT Is Reset Twice
One reset is not enough — Kerberos retains previous version for replication consistency.
Best practice:

Reset KRBTGT twice, 12–24 hours apart
Ensure domain replication is stable


⭐ 4.4 How Attackers Steal KRBTGT
Requires Domain Controller-level compromise, typically through:

DCSync attack
DC Shadow
Pass‑the-Hash on a DC account
Memory dump of LSASS on DC
Backup extraction (ntds.dit)
Replication abuse
Privilege escalation chains

Modern Microsoft privileged access guidance highlights that DC compromise is one of the highest-risk privileged access pathways in an enterprise environment. [github.com]

🕸 5. Golden Ticket Attack Flow (Mermaid Diagram)
sequenceDiagram  participant Attacker  participant DC as Domain Controller  participant KRBTGT as KRBTGT Account  participant Services as Domain Services  Attacker->>DC: DCSync / Hash Extraction  DC-->>Attacker: KRBTGT Hash (NTLM/AES)  Attacker->>Attacker: Generate Golden Ticket (Forged TGT)  Attacker->>Services: Present TGT as Domain Admin  Services-->>Attacker: Full Access Granted (Trusted)Show more linesDomain ServicesKRBTGT AccountDomain ControllerAttackerDomain ServicesKRBTGT AccountDomain ControllerAttacker#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-thickness-normal {stroke-width:1px}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .actor {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 text.actor > tspan {fill:blackstroke:none;}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .actor-line {stroke:rgb(218, 206, 243)}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .messageLine0 {stroke-width:1.5stroke-dasharray:none;stroke:rgb(51, 51, 51);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .messageLine1 {stroke-width:1.5stroke-dasharray:2, 2;stroke:rgb(51, 51, 51);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 #arrowhead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .sequenceNumber {fill:white}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 #sequencenumber {fill:rgb(51, 51, 51)}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 #crosshead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .messageText {fill:rgb(51, 51, 51)stroke:none;}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .labelBox {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .labelText, #mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .labelText > tspan {fill:blackstroke:none;}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .loopText, #mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .loopText > tspan {fill:blackstroke:none;}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .loopLine {stroke-width:2pxstroke-dasharray:2, 2;stroke:rgb(218, 206, 243);fill:rgb(218, 206, 243);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .note {stroke:rgb(170, 170, 51)fill:rgb(255, 245, 173);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .noteText, #mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .noteText > tspan {fill:blackstroke:none;}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .activation0 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .activation1 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .activation2 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .actorPopupMenu {position:absolute}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .actorPopupMenuPanel {position:absolutefill:rgb(236, 236, 255);box-shadow:rgba(0, 0, 0, 0.2) 0px 8px 16px 0px;filter:drop-shadow(rgba(0, 0, 0, 0.4) 3px 5px 2px);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .actor-man line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .actor-man circle, #mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);stroke-width:2px;}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .error-icon{fill:#552222;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .error-text{fill:#552222;stroke:#552222;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-thickness-normal{stroke-width:1px;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .marker{fill:#333333;stroke:#333333;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .marker.cross{stroke:#333333;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 p{margin:0;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .actor{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 text.actor>tspan{fill:black;stroke:none;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .actor-line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 #arrowhead path{fill:#333;stroke:#333;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .sequenceNumber{fill:white;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 #sequencenumber{fill:#333;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 #crosshead path{fill:#333;stroke:#333;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .messageText{fill:#333;stroke:none;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .labelBox{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .labelText,#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .labelText>tspan{fill:black;stroke:none;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .loopText,#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .loopText>tspan{fill:black;stroke:none;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .note{stroke:#aaaa33;fill:#fff5ad;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .noteText,#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .noteText>tspan{fill:black;stroke:none;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .actorPopupMenu{position:absolute;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .actorPopupMenuPanel{position:absolute;fill:#ECECFF;box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .actor-man line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 .actor-man circle,#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;stroke-width:2px;}#mermaid-9cb7def4-0085-475c-91d2-2a1237b8d578 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}DCSync / Hash ExtractionKRBTGT Hash (NTLM/AES)Generate Golden Ticket (Forged TGT)Present TGT as Domain AdminFull Access Granted (Trusted)

🔧 6. How Attackers Actually Do It (Lab‑Only Demonstration)
⚠️ For isolated testing labs ONLY.

✔ 6.1 Steal KRBTGT Hash via DCSync
PowerShellmimikatz.exelsadump::dcsync /user:krbtgtShow more lines

✔ 6.2 Generate Golden Ticket
PowerShellkerberos::golden /user:fakeAdmin /domain:contoso.local /sid:S-1-5-21-111-222-333 /krbtgt:<HASH> /groups:512Show more lines
Groups:

512 – Domain Admins
518 – Schema Admins
519 – Enterprise Admins


✔ 6.3 Use Ticket
PowerShellkerberos::ptt golden_ticket.kirbiShow more lines
Now attacker IS Domain Admin.

⚔️ 7. Real‑World Golden Ticket Incidents

🛑 7.1 APT Persistence
Advanced threat groups often inject Golden Tickets to maintain multi‑year stealth access.

🛑 7.2 Decommissioned Accounts
Attackers forge TGTs for deleted accounts — makes Blue Team suspicious but helpless.

🛑 7.3 Unlimited Lifetime Tickets
Attackers set validity to 10 years, bypassing ticket TTL.

🛑 7.4 Fake Lateral Movement
Attackers can impersonate any user to mislead investigation.

🛡 **8. Defense Strategy —
“The seal must be guarded, rotated, and protected.”**

⭐ 8.1 Protect Domain Controllers
Because DC compromise enables Golden Ticket attacks.
Microsoft’s model: Tier‑0 must be extremely isolated.
 [github.com]
Actions:

No admin logons from non‑PAWs
Patch DCs aggressively
Harden LSASS (RunAsPPL)
Block internet access
Enable Credential Guard on servers where possible


⭐ 8.2 Implement Tier‑0 Isolation
DC admin accounts never log onto:

Workstations
Application servers
Jump boxes without PAW policies

Strict tiering is mandated under modern EA Model hardening.
 [github.com]

⭐ 8.3 Monitor for DCSync Attempts
Alerts for:

Directory Replication Services (DRS) replication request
4662 with replication rights
Unauthorized accounts with DS-Replication-Get-Changes


⭐ 8.4 KRBTGT Account Rotation (Critical)
Reset twice, 12–24 hours apart.

⭐ 8.5 Enforce AES‑only Kerberos
Prevents weak encryption for forged tickets.

⭐ 8.6 Harden Privileged Access Pathways

Use PAWs
Use JIT/JEA/PIM
Avoid always-on DA accounts
Protect admin credentials from exposure


⭐ 8.7 Deploy Microsoft Defender for Identity (MDI)
Detects:

DCSync
Suspicious Kerberos activity
Unusual ticket creation
Lateral movement patterns


🔧 9. Blue Team Quick Commands
KRBTGT Password Last Set
PowerShellGet-ADUser krbtgt -Properties "pwdLastSet"Show more lines
View Replication Rights on Domain
PowerShellGet-ADPermission -Identity "DC=contoso,DC=local" | where {$_.ExtendedRights -match "Replication"}Show more lines
Monitor Ticket Lifetimes
PowerShellklistShow more lines

🧵 10. Mind Map (Placeholder)
Golden Ticket
 ├─ DC Compromise
 │   ├─ DCSync
 │   ├─ LSASS Dump
 │   ├─ ntds.dit Extraction
 ├─ KRBTGT Hash Theft
 ├─ Ticket Forgery
 ├─ Unlimited Access
 ├─ Defenses
 │   ├─ Tier-0 Protection
 │   ├─ KRBTGT Rotation
 │   ├─ Monitoring (MDI)
 │   ├─ JIT/JEA/PIM
 │   ├─ AES-Only
 └─ Attack Surface Hardening


📚 References


Microsoft Enterprise Access Model — privileged access pathways and the security of identity infrastructure.
 [github.com]


Clean Source Principle & Tier‑0 protection insights (Quest Blog on Tiering).
 [github.com]
