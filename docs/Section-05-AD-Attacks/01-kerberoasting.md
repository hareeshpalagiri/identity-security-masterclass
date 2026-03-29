🏹 **Mahabharata Story Analogy —
“Stealing the Commander’s Insignia to Forge Orders”**
In the Mahabharata:

Some spies tried to steal royal seals
With the seal, they could issue fake commands
These commands looked legitimate because the seal was valid
But the enemy would forge the orders using that stolen insignia

This is Kerberoasting:

Attackers request service tickets (TGS) from AD,
extract the encrypted part containing the service account’s key,
and then crack it offline to recover the password.

Just like forging orders using a stolen commander’s seal.

🔐 1. What Is Kerberoasting? (Simple Definition)
Kerberoasting is an attack where:

The attacker requests a Kerberos Service Ticket (TGS) for a service account.
The ticket contains data encrypted using the service account’s NTLM hash (derived from its password).
The attacker extracts this encrypted blob.
The attacker cracks it offline to recover the service account password.

Why it works:
Service accounts often have weak, old, never‑rotated, or non‑complex passwords, making cracking feasible.
Popular tools:
Rubeus, Impacket, Invoke-Kerberoast.

🧭 2. Why Kerberoasting Matters — Hastinapura Example

























ScenarioInterpretationA warrior publicly displays their royal sealService accounts SPNs are publicly queryable in ADAnyone can request a stamped orderAnyone with domain access can request a service ticketSeal is captured, forged to produce fake commandsTicket is cracked offline → password recoveredForged command unlocks strategic areasCracked password grants server takeover, lateral movement, or domain privilege
In other words:

The enemy doesn’t break into the fort — they rewrite the orders carried out by the fort itself.


🎬 3. Animation Placeholder
[GIF Placeholder: "Attacker requests TGS → extracts hash → cracks offline → becomes service account"]

Scene 1 → Attacker enumerates SPNs  
Scene 2 → Requests TGS from DC  
Scene 3 → Extracts encrypted ticket blob  
Scene 4 → Cracks using hashcat  
Scene 5 → Logs in as the service account → lateral movement  


🧠 4. Core Concepts (Simple + Deep)

⭐ 4.1 Kerberos SPNs → The Public Royal Seals
Service accounts with SPNs can be enumerated easily:
setspn -Q */*

This gives attackers a complete list of roastable targets.

⭐ 4.2 Kerberos TGS Tickets Are “Encrypt‑with‑Hash”
Service Ticket (TGS) contains:

Encrypted service session key
Encryption done with NTLM hash of service account

If password is weak → TGS encryption cracks easily.

⭐ 4.3 Offline Cracking = No Detection
Once attacker gets the TGS hash:

They take it offline
No AD logs
No lockouts
No throttling
No SIEM events

AD never knows password cracking is happening.

⭐ 4.4 High‑Value Targets

SQL Service Accounts
IIS App Pool Identities
Backup service accounts
Legacy service accounts
Any service running under “user” accounts
Accounts with SPNs + Domain Admin (misconfig)


🕸 5. Kerberoasting Flow (Mermaid Diagram)
sequenceDiagram  participant Attacker  participant DC as Domain Controller (KDC)  participant SVC as Service Account  Attacker->>DC: SPN Enumeration (LDAP Query)  Attacker->>DC: TGS-REQ for SPN (HTTP/SQL/File)  DC-->>Attacker: TGS-REP (Encrypted with SVC NTLM Hash)  Attacker->>Attacker: Extract TGS Hash (Rubeus/Impacket)  Attacker->>Attacker: Offline Crack (Hashcat)  Attacker->>SVC: Authenticate with Cracked Password  SVC-->>Attacker: Privileged Access / Lateral MovementShow more linesService AccountDomain Controller (KDC)AttackerService AccountDomain Controller (KDC)Attacker#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-thickness-normal {stroke-width:1px}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .actor {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 text.actor > tspan {fill:blackstroke:none;}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .actor-line {stroke:rgb(218, 206, 243)}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .messageLine0 {stroke-width:1.5stroke-dasharray:none;stroke:rgb(51, 51, 51);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .messageLine1 {stroke-width:1.5stroke-dasharray:2, 2;stroke:rgb(51, 51, 51);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 #arrowhead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .sequenceNumber {fill:white}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 #sequencenumber {fill:rgb(51, 51, 51)}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 #crosshead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .messageText {fill:rgb(51, 51, 51)stroke:none;}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .labelBox {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .labelText, #mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .labelText > tspan {fill:blackstroke:none;}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .loopText, #mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .loopText > tspan {fill:blackstroke:none;}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .loopLine {stroke-width:2pxstroke-dasharray:2, 2;stroke:rgb(218, 206, 243);fill:rgb(218, 206, 243);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .note {stroke:rgb(170, 170, 51)fill:rgb(255, 245, 173);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .noteText, #mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .noteText > tspan {fill:blackstroke:none;}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .activation0 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .activation1 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .activation2 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .actorPopupMenu {position:absolute}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .actorPopupMenuPanel {position:absolutefill:rgb(236, 236, 255);box-shadow:rgba(0, 0, 0, 0.2) 0px 8px 16px 0px;filter:drop-shadow(rgba(0, 0, 0, 0.4) 3px 5px 2px);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .actor-man line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .actor-man circle, #mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);stroke-width:2px;}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .error-icon{fill:#552222;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .error-text{fill:#552222;stroke:#552222;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-thickness-normal{stroke-width:1px;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .marker{fill:#333333;stroke:#333333;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .marker.cross{stroke:#333333;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 p{margin:0;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .actor{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 text.actor>tspan{fill:black;stroke:none;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .actor-line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 #arrowhead path{fill:#333;stroke:#333;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .sequenceNumber{fill:white;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 #sequencenumber{fill:#333;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 #crosshead path{fill:#333;stroke:#333;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .messageText{fill:#333;stroke:none;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .labelBox{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .labelText,#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .labelText>tspan{fill:black;stroke:none;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .loopText,#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .loopText>tspan{fill:black;stroke:none;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .note{stroke:#aaaa33;fill:#fff5ad;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .noteText,#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .noteText>tspan{fill:black;stroke:none;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .actorPopupMenu{position:absolute;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .actorPopupMenuPanel{position:absolute;fill:#ECECFF;box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .actor-man line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 .actor-man circle,#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;stroke-width:2px;}#mermaid-e044a107-0c3b-4004-b44e-351cd74b7f38 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}SPN Enumeration (LDAP Query)TGS-REQ for SPN (HTTP/SQL/File)TGS-REP (Encrypted with SVC NTLM Hash)Extract TGS Hash (Rubeus/Impacket)Offline Crack (Hashcat)Authenticate with Cracked PasswordPrivileged Access / Lateral Movement

🔧 6. Hands‑On Attack Walkthrough (For Lab Only)
⚠️ Use only in lab environments.

✔ 6.1 Enumerate SPNs
PowerShellsetspn -Q */*Show more lines
or via PowerShell:
PowerShellGet-ADUser -Filter {ServicePrincipalName -ne $null} -Properties ServicePrincipalNameShow more lines

✔ 6.2 Request TGS
PowerShellRubeus.exe kerberoastShow more lines
or Impacket:
ShellGetUserSPNs.py contoso.local/user:pass -requestShow more lines

✔ 6.3 Crack offline
Shellhashcat -m 13100 hashfile.txt rockyou.txtShow more lines
Mode 13100 = Kerberos 5 TGS‐Rep etype 23.

⚔️ 7. Real Attack Examples
🛑 7.1 Weak SQL Service Account
SQL service account with password Summer2020!
→ cracked in seconds
→ full SQL instance hijack
→ extract domain credentials → escalate

🛑 7.2 Web App Running as Domain Admin (worst case)
Yes — many orgs mistakenly run services under Domain Admin.
Kerberoasting = instant domain compromise.

🛑 7.3 Legacy Account Never Rotated for Years
Older accounts often use RC4 or NTLM hashing → crack speed is extremely fast.

🛡 8. Defense Strategy — “Strengthen the Royal Seals”

⭐ 8.1 Strongest Passwords for Service Accounts
Minimum:

25+ characters
Randomly generated
Rotated regularly
No reuse


⭐ 8.2 Use Managed Accounts

gMSA (Group Managed Service Accounts)
Auto-managed keys
Not roastable
No password cracking possible

This is the best defense.

⭐ 8.3 Remove Unnecessary SPNs
Many SPNs exist because:

Old apps
Decommissioned servers
Bad configurations

Every SPN = potential roasting target.

⭐ 8.4 Enforce AES Encryption (Disable RC4)
AES slow to crack → dramatically increases difficulty.
PowerShellSet-ADUser svc_sql -KerberosEncryptionType AES256Show more lines

⭐ 8.5 Tier Service Accounts
Service accounts in:

Tier‑0 → extremely sensitive
Tier‑1 → servers/apps
Tier‑2 → workstations (rare)

Apply Tier boundaries to their usage.

⭐ 8.6 Monitor TGS Requests
Use Defender for Identity or SIEM:

Spike in TGS requests
TGS for high-value service accounts
Mismatched user → unusual service requests


⭐ 8.7 Disable DES and RC4
Ensure domain functional level supports it.

⭐ 8.8 Rotate High‑Value Service Account Passwords Regularly
Especially:

SQL
IIS
Backup
SCCM
Monitoring tools


🔧 9. Quick Commands (Blue Team)
Check which accounts have SPNs:
PowerShellGet-ADUser -Filter {ServicePrincipalName -ne $null} -Properties ServicePrincipalNameShow more lines
Check account encryption type:
PowerShellGet-ADUser svc_sql -Properties msDS-SupportedEncryptionTypesShow more lines
Enforce AES:
PowerShellSet-ADUser svc_sql -KerberosEncryptionType AES256Show more lines
Check for stale SPNs:
PowerShellsetspn -Q */* > allspns.txtShow more lines

🧵 10. Mind Map (Placeholder)
Kerberoasting
 ├─ SPN Discovery
 ├─ TGS Request
 ├─ Extract Ticket
 ├─ Offline Crack
 ├─ Priv Escalation
 ├─ Defenses
 │   ├─ gMSA
 │   ├─ Strong Passwords
 │   ├─ AES Only
 │   ├─ SPN Cleanup
 │   ├─ Monitoring
 │   ├─ Tiering
 └─ Attack Surface Reduction


📚 References


Kerberos & SPNs fundamentals (Microsoft Docs)
https://learn.microsoft.com/windows-server/security/kerberos/kerberos-authentication-overview


Attack behavior and mitigations (Microsoft Security Blog)
https://microsoft.com/security/blog


Kerberoasting research papers (various cybersecurity conferences)
