📘 01 — Kerberos Authentication
A simple, deep, story‑based explanation using strategic Mahabharata analogies — GitBook Ready

🏹 Mahabharata Story Analogy (Strategic Only)
At Hastinapura’s battle camps, no warrior shouts passwords across valleys.
Instead, a central command post issues sealed passes.
A warrior shows the pass at each tent to move without re‑proving identity.

Command post = KDC (Key Distribution Center) — the authority that issues tickets. [github.com]
Sealed pass to visit many tents = Ticket‑Granting Ticket (TGT) enabling SSO. [github.com]
Pass for a specific tent = Service Ticket tied to that service’s identity (SPN). [support.mi...rosoft.com]

Just like passes avoid repeated secrets, Kerberos enables secure, ticket‑based access.

🔐 1. What is Kerberos? (Simple Definition)
Kerberos is an authentication protocol used by Active Directory where a trusted KDC (on Domain Controllers) issues tickets that clients present to services — enabling single sign‑on without sending passwords repeatedly. [github.com]

Modern note (hybrid): Microsoft Entra Kerberos allows cloud‑joined devices to get Kerberos tickets for on‑prem resources (Entra acting as a cloud KDC) — useful in hybrid SSO. [github.com]


🧭 2. Why Kerberos Matters — Hastinapura Example

























Without Kerberos (weak)With Kerberos (strong)Passwords sent often → risk of theftTickets represent identity; passwords not sent repeatedlyNo single source of trustKDC is a central trust for issuing/verifying ticketsHard to scale SSOTGT lets users request multiple service tickets (SSO)Easier replay / no mutual checksAuthenticators & timestamps reduce replay; mutual auth supported
(In AD, Kerberos is the default authentication; mutual authentication + tickets make it robust.) [github.com]

🎬 3. Animation Placeholder
(Add later using GIF/Notebook‑LLM)
[Animation Placeholder: "Kerberos in Hastinapura"]
Scene 1 → Warrior obtains sealed pass at command post (AS-REQ/AS-REP → TGT)
Scene 2 → Warrior asks command post for a specific tent pass (TGS-REQ/REP → Service Ticket)
Scene 3 → Warrior shows the tent pass and enters (AP-REQ/REP)
Labels → KDC, Tickets, SPN, no passwords on the wire


🧠 4. Core Components of Kerberos (Simple + Deep)
KDC (on Domain Controllers)
Issues TGTs (Authentication Service) and service tickets (Ticket‑Granting Service). [github.com]
Tickets

TGT: proves you’ve authenticated; used to request service tickets (SSO). [github.com]
Service Ticket: for a specific service instance (identified by SPN). [support.mi...rosoft.com]

SPN (Service Principal Name)
A unique identifier for a service (e.g., HTTP/app.corp.local, MSSQLSvc/sql01.corp.local:1433). Must be unique and registered on the account running the service (computer or user). [support.mi...rosoft.com], [trustedsec.com]
Ports
Kerberos uses TCP/UDP 88 between clients and KDCs (DCs). [cordero.me]
Ticket Lifetime (policy)
Default service ticket lifetime is commonly 600 minutes (10 hours) (Kerberos Policy in domain). [learn.microsoft.com]

🗺 5. Kerberos Flow (AS → TGS → AP)
sequenceDiagram    participant C as Client    participant K as KDC (AS/TGS)    participant S as Service (SPN=HTTP/app.corp.local)    C->>K: AS-REQ (Initial auth)    K-->>C: AS-REP (TGT)    C->>K: TGS-REQ (TGT + SPN)    K-->>C: TGS-REP (Service Ticket)    C->>S: AP-REQ (Presents Service Ticket)    S-->>C: AP-REP (optional mutual auth)Show more linesService (SPN=HTTP/app.corp.local)KDC (AS/TGS)ClientService (SPN=HTTP/app.corp.local)KDC (AS/TGS)Client#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-thickness-normal {stroke-width:1px}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .actor {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 text.actor > tspan {fill:blackstroke:none;}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .actor-line {stroke:rgb(218, 206, 243)}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .messageLine0 {stroke-width:1.5stroke-dasharray:none;stroke:rgb(51, 51, 51);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .messageLine1 {stroke-width:1.5stroke-dasharray:2, 2;stroke:rgb(51, 51, 51);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 #arrowhead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .sequenceNumber {fill:white}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 #sequencenumber {fill:rgb(51, 51, 51)}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 #crosshead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .messageText {fill:rgb(51, 51, 51)stroke:none;}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .labelBox {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .labelText, #mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .labelText > tspan {fill:blackstroke:none;}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .loopText, #mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .loopText > tspan {fill:blackstroke:none;}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .loopLine {stroke-width:2pxstroke-dasharray:2, 2;stroke:rgb(218, 206, 243);fill:rgb(218, 206, 243);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .note {stroke:rgb(170, 170, 51)fill:rgb(255, 245, 173);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .noteText, #mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .noteText > tspan {fill:blackstroke:none;}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .activation0 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .activation1 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .activation2 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .actorPopupMenu {position:absolute}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .actorPopupMenuPanel {position:absolutefill:rgb(236, 236, 255);box-shadow:rgba(0, 0, 0, 0.2) 0px 8px 16px 0px;filter:drop-shadow(rgba(0, 0, 0, 0.4) 3px 5px 2px);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .actor-man line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .actor-man circle, #mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);stroke-width:2px;}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .error-icon{fill:#552222;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .error-text{fill:#552222;stroke:#552222;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-thickness-normal{stroke-width:1px;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .marker{fill:#333333;stroke:#333333;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .marker.cross{stroke:#333333;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 p{margin:0;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .actor{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 text.actor>tspan{fill:black;stroke:none;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .actor-line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 #arrowhead path{fill:#333;stroke:#333;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .sequenceNumber{fill:white;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 #sequencenumber{fill:#333;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 #crosshead path{fill:#333;stroke:#333;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .messageText{fill:#333;stroke:none;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .labelBox{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .labelText,#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .labelText>tspan{fill:black;stroke:none;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .loopText,#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .loopText>tspan{fill:black;stroke:none;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .note{stroke:#aaaa33;fill:#fff5ad;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .noteText,#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .noteText>tspan{fill:black;stroke:none;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .actorPopupMenu{position:absolute;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .actorPopupMenuPanel{position:absolute;fill:#ECECFF;box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .actor-man line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 .actor-man circle,#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;stroke-width:2px;}#mermaid-8e4c3485-b8e0-4252-b4db-09f4eacad8e5 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}AS-REQ (Initial auth)AS-REP (TGT)TGS-REQ (TGT + SPN)TGS-REP (Service Ticket)AP-REQ (Presents Service Ticket)AP-REP (optional mutual auth)
Why it works: the client proves identity once, then uses the TGT to obtain service‑specific tickets — no password re‑entry on every access. [github.com], [github.com]

🔧 6. Kerberos in Real IT Systems
🔹 Check SPNs (troubleshoot NTLM fallback)
PowerShellsetspn -L SERVER01                 # list SPNs on computer accountsetspn -L CORP\svc-webapp          # list SPNs on service accountsetspn -S HTTP/app.corp.local CORP\svc-webapp   # add SPN (unique)Show more lines
(SPNs must be registered on the account running the service; duplicates break Kerberos.) [trustedsec.com]
🔹 See user’s tickets on a workstation / server
PowerShellklist             # lists TGT + service ticketsklist purge       # clears tickets (force fresh acquisition)Show more lines
🔹 Enforce modern crypto & policy (examples)

Prefer AES; disable legacy RC4 where compatible. [zensec.org]
Keep service ticket lifetime ≈ 10 hours unless risk/business requires otherwise. [learn.microsoft.com]

🔹 Hybrid SSO (cloud to on‑prem)

Consider Microsoft Entra Kerberos for cloud‑joined devices to access on‑prem resources with Kerberos (cloud KDC capability). [github.com]


⚔️ 7. Kerberos in Cybersecurity
🛑 Attacks


Kerberoasting (T1558.003) — An attacker with any domain user requests service tickets for SPN accounts and cracks them offline (especially if RC4/weak passwords).
Mitigate: strong passwords for service accounts, AES‑only, monitor anomalous TGS requests. [zensec.org], [techcommun...rosoft.com]


AS‑REP Roasting — If a user has “Do not require Kerberos preauthentication” enabled, an attacker can obtain an AS‑REP and crack it offline.
Mitigate: enable pre‑auth for all users; continuously monitor exceptions. [learn.microsoft.com], [pentestpad.com]


🛡 Defenses

Enforce AES; remove RC4 where possible, rotate service account creds. [zensec.org]
Kerberos FAST / Armoring — protects pre‑authentication exchanges; foundation for claims/compound auth; introduced in Windows Server 2012+. [port135.com], [stigviewer.com]
SPN hygiene — ensure SPN uniqueness / correctness (setspn); avoid aliases without matching SPNs. [trustedsec.com]
Ports & reachability — ensure TCP/UDP 88 to DCs to avoid NTLM fallback. [cordero.me]
Reasonable lifetimes — keep default service ticket lifetime (~600 min) unless specific risks dictate otherwise. [learn.microsoft.com]


🧵 8. Mind Map (Placeholder)
(Will be converted to GIF later)
Kerberos Mind Map:
  - KDC (AS/TGS)
  - Tickets (TGT, Service Tickets)
  - SPN
  - Ports (88/TCP-UDP)
  - Policy (lifetimes)
  - Hybrid (Entra Kerberos)
  - Attacks (Kerberoast, AS-REP roast)
  - Defenses (AES-only, FAST, SPN hygiene)


🔗 9. What Comes Next? (Smooth Transition)
Now that you know how tickets prove identity securely, the next question is:

What happens when Kerberos is not available and Windows falls back?

Historically, environments used NTLM — simpler, but weaker and prone to relay/pass‑the‑hash style risks.
Next chapter:
👉 Chapter 02 — NTLM (Fallback protocol, weaknesses, and hardening)

References (selected)

Kerberos roles, flows, SSO in Windows/AD: Microsoft/industry deep dives. [github.com], [github.com]
SPN definition & setspn usage: Microsoft Learn. [support.mi...rosoft.com], [trustedsec.com]
Kerberos ports (88/TCP, UDP): Microsoft guidance. [cordero.me]
Service ticket lifetime default (600 minutes): Microsoft policy reference. [learn.microsoft.com]
Kerberoasting (T1558.003): MITRE/CISA. [zensec.org], [techcommun...rosoft.com]
AS‑REP Roasting: Microsoft / industry guidance. [learn.microsoft.com], [pentestpad.com]
Kerberos FAST/Armoring & claims: Microsoft/industry. [port135.com], [stigviewer.com]
Entra Kerberos (hybrid): Microsoft Learn. [github.com]
