Kerberos Authentication (Windows AD)

🏹 Story opener — “Trusted passes between allied camps”
On the battlefield, allied camps do not shout passwords across valleys. Instead, a trusted command post issues sealed entry passes. A warrior presents the pass at each gate to move between tents and command rooms, without re‑proving identity every time.
This is Kerberos in modern networks: a Key Distribution Center (KDC) issues tickets that the client presents to services to prove identity—no passwords sent around repeatedly. [cherry-security.com]

🔐 1) What Kerberos is (simple definition)
Kerberos is an authentication protocol for Active Directory that uses tickets from a trusted KDC (on domain controllers) so users and computers can authenticate securely and then access multiple services via single sign‑on. In Windows, the KDC exposes two roles: Authentication Service (AS) and Ticket‑Granting Service (TGS). [cherry-security.com]

Modern note: Microsoft has also introduced Microsoft Entra Kerberos so cloud‑joined devices can obtain Kerberos tickets for on‑prem apps in hybrid scenarios (Entra acting as a cloud KDC). [learn.microsoft.com]


🧭 2) Why enterprises use Kerberos

No clear‑text passwords on the network; tickets represent identity. [linkedin.com]
Mutual authentication and replay protections via timestamps & authenticators. [cherry-security.com]
SSO experience: a TGT allows requesting new service tickets without re‑auth. [linkedin.com]


🧩 3) Core building blocks (Windows AD)

KDC on DCs: issues TGTs (AS) and service tickets (TGS). [cherry-security.com]
SPN (Service Principal Name): unique name that identifies a service instance and ties it to a service account—required for Kerberos to find the right key to encrypt the ticket. [learn.microsoft.com]
Ports: Kerberos uses TCP/UDP 88 between clients and KDCs. [learn.microsoft.com]
Ticket lifetimes: default service ticket lifetime is commonly 600 minutes (10 hours) via domain Kerberos policy (can be tuned). [learn.microsoft.com]


🔁 4) How Kerberos works in AD (step‑by‑step)
(a) Logon / get the TGT (AS‑REQ / AS‑REP)

Client sends AS‑REQ to KDC.
KDC validates and returns AS‑REP with a TGT for the user (and a session key).
This TGT is encrypted by the KDC and cannot be read by clients or services. [linkedin.com], [cherry-security.com]

(b) Request access to a service (TGS‑REQ / TGS‑REP)

Client presents the TGT + target SPN to KDC (TGS‑REQ).
KDC issues a service ticket (TGS‑REP) encrypted with the service account’s key (from the SPN). [learn.microsoft.com], [cherry-security.com]

(c) Access the service (AP‑REQ / AP‑REP)

Client connects to the service and presents the service ticket.
Service validates and (optionally) replies with AP‑REP for mutual auth. [cherry-security.com]

Diagram — Ticket flow (Mermaid)
sequenceDiagram    participant U as User/Client    participant KDC as KDC (AS/TGS)    participant S as Service (SPN=HTTP/app.corp.local)    U->>KDC: AS-REQ (I need a TGT)    KDC-->>U: AS-REP (TGT + session key)    U->>KDC: TGS-REQ (TGT + SPN=HTTP/app.corp.local)    KDC-->>U: TGS-REP (Service Ticket)    U->>S: AP-REQ (Service Ticket)    S-->>U: AP-REP (optional, mutual auth)Show more linesService (SPN=HTTP/app.corp.local)KDC (AS/TGS)User/ClientService (SPN=HTTP/app.corp.local)KDC (AS/TGS)User/Client#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-thickness-normal {stroke-width:1px}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .actor {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 text.actor > tspan {fill:blackstroke:none;}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .actor-line {stroke:rgb(218, 206, 243)}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .messageLine0 {stroke-width:1.5stroke-dasharray:none;stroke:rgb(51, 51, 51);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .messageLine1 {stroke-width:1.5stroke-dasharray:2, 2;stroke:rgb(51, 51, 51);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 #arrowhead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .sequenceNumber {fill:white}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 #sequencenumber {fill:rgb(51, 51, 51)}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 #crosshead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .messageText {fill:rgb(51, 51, 51)stroke:none;}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .labelBox {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .labelText, #mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .labelText > tspan {fill:blackstroke:none;}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .loopText, #mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .loopText > tspan {fill:blackstroke:none;}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .loopLine {stroke-width:2pxstroke-dasharray:2, 2;stroke:rgb(218, 206, 243);fill:rgb(218, 206, 243);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .note {stroke:rgb(170, 170, 51)fill:rgb(255, 245, 173);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .noteText, #mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .noteText > tspan {fill:blackstroke:none;}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .activation0 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .activation1 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .activation2 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .actorPopupMenu {position:absolute}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .actorPopupMenuPanel {position:absolutefill:rgb(236, 236, 255);box-shadow:rgba(0, 0, 0, 0.2) 0px 8px 16px 0px;filter:drop-shadow(rgba(0, 0, 0, 0.4) 3px 5px 2px);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .actor-man line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .actor-man circle, #mermaid-7f344254-253b-48e4-8881-7f2e453b4837 line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);stroke-width:2px;}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-7f344254-253b-48e4-8881-7f2e453b4837{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .error-icon{fill:#552222;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .error-text{fill:#552222;stroke:#552222;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-thickness-normal{stroke-width:1px;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .marker{fill:#333333;stroke:#333333;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .marker.cross{stroke:#333333;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 p{margin:0;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .actor{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 text.actor>tspan{fill:black;stroke:none;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .actor-line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 #arrowhead path{fill:#333;stroke:#333;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .sequenceNumber{fill:white;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 #sequencenumber{fill:#333;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 #crosshead path{fill:#333;stroke:#333;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .messageText{fill:#333;stroke:none;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .labelBox{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .labelText,#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .labelText>tspan{fill:black;stroke:none;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .loopText,#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .loopText>tspan{fill:black;stroke:none;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .note{stroke:#aaaa33;fill:#fff5ad;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .noteText,#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .noteText>tspan{fill:black;stroke:none;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .actorPopupMenu{position:absolute;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .actorPopupMenuPanel{position:absolute;fill:#ECECFF;box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .actor-man line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 .actor-man circle,#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;stroke-width:2px;}#mermaid-7f344254-253b-48e4-8881-7f2e453b4837 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}AS-REQ (I need a TGT)AS-REP (TGT + session key)TGS-REQ (TGT + SPN=HTTP/app.corp.local)TGS-REP (Service Ticket)AP-REQ (Service Ticket)AP-REP (optional, mutual auth)

🧾 5) SPNs in practice (what to get right)

Register SPNs on the account running the service (computer or user).
SPNs must be unique—duplicates break Kerberos and cause NTLM fallback.
setspn is the supported tool for reading/writing SPNs and fixing mismatches. [learn.microsoft.com], [learn.microsoft.com]


Example SPNs: HTTP/app.corp.local, MSSQLSvc/sql01.corp.local:1433, cifs/fs01.corp.local [learn.microsoft.com]


⚙️ 6) Quick enterprise configuration checklist

Ensure clients/DCs can reach TCP/UDP 88 (Kerberos) and standard AD ports. [learn.microsoft.com]
Verify SPNs for tier‑1 apps (IIS/HTTP, CIFS, MSSQLSvc) using setspn -L. [learn.microsoft.com]
Keep ticket lifetimes at recommended defaults (e.g., service ticket ~10 hours) unless there’s a strong reason to reduce/extend. [learn.microsoft.com]
Prefer AES (disable RC4 where possible) to harden tickets. (Background in Kerberoasting references below). [attack.mitre.org]
For hybrid, consider Microsoft Entra Kerberos for cloud‑joined devices accessing on‑prem resources. [learn.microsoft.com]


🧨 7) Common attack paths (what red teams exploit)
Kerberoasting (T1558.003)
Attackers with any domain user can request service tickets for SPN accounts and crack them offline (especially if RC4 or weak passwords are in use). Mitigate with strong service account passwords, AES‑only, and monitoring. [attack.mitre.org], [cisa.gov]
AS‑REP Roasting
If a user has “Do not require Kerberos preauthentication” enabled, an attacker can request an AS‑REP and crack it offline. Mitigate by enabling pre‑auth for all users and monitoring for exceptions. [techcommun...rosoft.com], [jumpcloud.com]

References include Microsoft’s Defender for Identity guidance and industry write‑ups. [techcommun...rosoft.com], [jumpcloud.com]


🛡️ 8) Defenses that actually move the needle

Enforce AES encryption; disable RC4 where compatible. (Reduces crackable material in tickets.) [attack.mitre.org]
Kerberos FAST / Armoring: protect pre‑authentication exchanges and enable advanced claims/compound auth; introduced in Windows Server 2012+. [learn.microsoft.com], [enowsoftware.com]
SPN hygiene: keep SPNs unique, tied to correct accounts; fix duplicates with setspn. [learn.microsoft.com]
Right ports, right paths: ensure 88/TCP,88/UDP to DCs; avoid firewall breaks that cause NTLM fallback. [learn.microsoft.com]
Ticket policy: keep reasonable lifetimes (service tickets ~600 minutes default) and renewals; shorter when risk dictates. [learn.microsoft.com]


🧪 9) Quick verification & troubleshooting

klist to view TGT and service tickets on a client. (General Windows admin practice; no citation needed)
If an app keeps falling back to NTLM, verify SPN exists & DNS name matches the SPN the client composes. [learn.microsoft.com]
Confirm port 88 reachability to DCs. [learn.microsoft.com]


🎬 10) Animation placeholder (for NotebookLLM later)
[Animation: "Kerberos in 20 seconds"]
Frames:
1) User → KDC (AS-REQ/REP) → TGT received
2) TGT → KDC with SPN (TGS-REQ/REP) → Service ticket received
3) Client → Service (AP-REQ/REP) → Access granted
Labels on 88/TCP-UDP, SPN lookup, and “no password on the wire”


🧵 11) Mind map placeholder
Kerberos
 ├─ KDC (AS/TGS)
 ├─ Tickets (TGT, Service Ticket)
 ├─ SPN (service mapping)
 ├─ Ports (88/TCP-UDP)
 ├─ Policy (lifetimes)
 ├─ Attacks (Kerberoast, AS-REP roast)
 └─ Defenses (AES only, FAST, SPN hygiene)


✅ Summary
Kerberos delivers secure, ticket‑based SSO in AD: clients obtain a TGT once, then request per‑service tickets tied to SPNs, over port 88, with lifetimes governed by domain policy. Correct SPN management, AES‑only, and FAST/Armoring minimize common attack paths (Kerberoasting, AS‑REP roasting). [learn.microsoft.com], [learn.microsoft.com], [enowsoftware.com], [attack.mitre.org]

Key references

Microsoft Learn: SPNs and setspn (format, uniqueness, management) [learn.microsoft.com], [learn.microsoft.com]
Kerberos process & roles in Windows/AD (KDC, AS/TGS, SPN usage) [cherry-security.com]
Entra Kerberos for hybrid cloud SSO [learn.microsoft.com]
Default service ticket lifetime (600 minutes) policy reference [learn.microsoft.com]
Kerberoasting (T1558.003) descriptions and implications (MITRE/CISA) [attack.mitre.org], [cisa.gov]
Kerberos FAST/Armoring guidance and value in modern AD [learn.microsoft.com], [enowsoftware.com]
Kerberos port/AD firewall considerations (88/TCP-UDP) [learn.microsoft.com]
