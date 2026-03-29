📘 02 — Privileged Access Workstations (PAWs)
A simple, deep, story‑driven explanation with Mahabharata‑aligned strategy — GitBook‑Ready

🏹 **Mahabharata Story Analogy —
“Commanders never used ordinary tents or weapons.”**
In the Mahabharata war:

The commanders (Bhishma, Drona, Arjuna, Krishna’s charioteer role)
never walked into regular soldier tents
They had separate war chariots, guarded, purified, and used ONLY for command duty
Weapons of high value (Divyastras) were kept in sacred, isolated areas
No commander performed strategy from common camps
Even interacting with ordinary tents was considered tactically dangerous

Why?
Because one poisoned arrow, one spy, or one careless entry to the wrong tent
could compromise the entire war strategy.
This is the philosophy behind Privileged Access Workstations (PAWs):

A PAW is the modern commander’s chariot — used ONLY for privileged tasks, isolated from danger, hardened beyond normal endpoints.

 [github.com]

🔐 1. What Are PAWs? (Simple Definition)
A Privileged Access Workstation (PAW) is a dedicated, hardened, isolated computer
used ONLY for administrative or high‑privilege tasks.
It is NOT a normal workstation.
It does NOT open email, browse the internet, install random apps, or run daily office work.
A PAW provides:

Stronger OS hardening
WDAC/AppLocker allow‑listing
Dedicated admin identity
No exposure to phishing/malware vectors
Network isolation to Tier‑0 resources only

Microsoft’s privileged access strategy places PAWs as a non‑negotiable requirement for protecting Tier‑0 assets like DCs, PKI, AADC, and root identities.
 [github.com]

🧭 2. Why PAWs Exist — Hastinapura Example

























Without PAWs (danger)With PAWs (safe)Domain Admin logs into a normal laptop → malware steals tokenTier‑0 admins can log in only from PAW → token never exposedAdmin checks mail on the same device used to manage DCsPAW doesn’t allow mail or browser → no spear‑phish entryHelpdesk system fully compromised → attacker harvests privileged credsHelpdesk (Tier‑2) and DC‑admin (Tier‑0) devices are physically separatedPhishing → RMM → full domain compromisePAW prevents RMM agents and shadow IT apps
💡 PAWs ensure: even if Tier‑2 is compromised, Tier‑0 survives.
 [github.com]

🎬 3. Animation Placeholder
[Animation Placeholder: "Admin tries using email on PAW → blocked; PAW connects only to DC; malware attempt fails"]
Scene 1: Normal workstation filled with apps/phishing
Scene 2: PAW shows only admin tools and hardening banners
Scene 3: Malware attempts LSASS dump → blocked by Credential Guard/WDAC
Scene 4: PAW → DC (secured path), Normal PC → DENIED


🧠 4. Core Concepts (Simple + Deep)
4.1 PAW = Isolation
Just like Arjuna’s chariot was sacred and restricted, PAWs cannot mingle with untrusted environments.

No email
No internet browsing
No general productivity tools
No plugins
No user account logins

4.2 PAW = Hardened Platform

BitLocker
Secure Boot
Credential Guard (if applicable)
Attack Surface Reduction
No local admin rights for user
Strict WDAC / AppLocker allow‑listing

4.3 PAW = Least Privilege Device Access
A PAW can only access:

Domain Controllers
PKI servers
Entra Connect / AD FS
Admin portals

No “browsing SharePoint”, no “checking WhatsApp web”, no “downloading tools”.
 [github.com]

🕸 5. PAW Architecture (Mermaid Diagram)
flowchart TD  PAW[Privileged Access Workstation<br/>Hardened, Isolated, WDAC/AppLocker] -->|Only Tier-0 access| T0[Domain Controllers<br/>PKI<br/>AADC/AD FS]  PAW -.blocked.-> INTERNET[Internet / Email / SaaS]  PAW -.blocked.-> T1T2[Servers + Workstations]  classDef blue fill:#d0e7ff,stroke:#0074c2,color:#000;  classDef red fill:#ffe5e5,stroke:#b30000,color:#000;  class PAW,T0 blue;  class INTERNET,T1T2 red;Show more lines#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .error-icon {fill:rgb(85, 34, 34)}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-thickness-normal {stroke-width:1px}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-thickness-thick {stroke-width:3.5px}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-pattern-solid {stroke-dasharray:0}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .cluster-label span p {background-color:transparent}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .label text, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node rect, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node circle, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node ellipse, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node polygon, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .rough-node .label text, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node .label text, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .image-shape .label, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .icon-shape .label {text-anchor:middle}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .rough-node .label, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node .label, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .image-shape .label, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .icon-shape .label {text-align:center}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node.clickable {cursor:pointer}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .cluster text {fill:rgb(51, 51, 51)}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .cluster span {color:rgb(51, 51, 51)}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac rect.text {fill:nonestroke-width:0;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .icon-shape, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .icon-shape p, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .icon-shape rect, #mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .blue rect {fill:rgb(208, 231, 255)stroke:rgb(0, 116, 194);color:rgb(0, 0, 0);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .blue polygon {fill:rgb(208, 231, 255)stroke:rgb(0, 116, 194);color:rgb(0, 0, 0);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .blue ellipse {fill:rgb(208, 231, 255)stroke:rgb(0, 116, 194);color:rgb(0, 0, 0);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .blue circle {fill:rgb(208, 231, 255)stroke:rgb(0, 116, 194);color:rgb(0, 0, 0);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .blue path {fill:rgb(208, 231, 255)stroke:rgb(0, 116, 194);color:rgb(0, 0, 0);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .blue tspan {fill:rgb(0, 0, 0)}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .red rect {fill:rgb(255, 229, 229)stroke:rgb(179, 0, 0);color:rgb(0, 0, 0);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .red polygon {fill:rgb(255, 229, 229)stroke:rgb(179, 0, 0);color:rgb(0, 0, 0);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .red ellipse {fill:rgb(255, 229, 229)stroke:rgb(179, 0, 0);color:rgb(0, 0, 0);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .red circle {fill:rgb(255, 229, 229)stroke:rgb(179, 0, 0);color:rgb(0, 0, 0);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .red path {fill:rgb(255, 229, 229)stroke:rgb(179, 0, 0);color:rgb(0, 0, 0);}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .red tspan {fill:rgb(0, 0, 0)}
#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .error-icon{fill:#552222;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .error-text{fill:#552222;stroke:#552222;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-thickness-normal{stroke-width:1px;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-thickness-thick{stroke-width:3.5px;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-pattern-solid{stroke-dasharray:0;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .marker{fill:#333333;stroke:#333333;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .marker.cross{stroke:#333333;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac p{margin:0;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .cluster-label text{fill:#333;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .cluster-label span{color:#333;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .cluster-label span p{background-color:transparent;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .label text,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac span{fill:#333;color:#333;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node rect,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node circle,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node ellipse,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node polygon,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .rough-node .label text,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node .label text,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .image-shape .label,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .icon-shape .label{text-anchor:middle;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .rough-node .label,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node .label,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .image-shape .label,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .icon-shape .label{text-align:center;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node.clickable{cursor:pointer;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .arrowheadPath{fill:#333333;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .flowchart-link{stroke:#333333;fill:none;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .cluster text{fill:#333;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .cluster span{color:#333;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac rect.text{fill:none;stroke-width:0;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .icon-shape,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .icon-shape p,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .icon-shape rect,#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .blue rect{fill:#d0e7ff!important;stroke:#0074c2!important;color:#000!important;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .blue polygon{fill:#d0e7ff!important;stroke:#0074c2!important;color:#000!important;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .blue ellipse{fill:#d0e7ff!important;stroke:#0074c2!important;color:#000!important;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .blue circle{fill:#d0e7ff!important;stroke:#0074c2!important;color:#000!important;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .blue path{fill:#d0e7ff!important;stroke:#0074c2!important;color:#000!important;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .blue tspan{fill:#000!important;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .red rect{fill:#ffe5e5!important;stroke:#b30000!important;color:#000!important;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .red polygon{fill:#ffe5e5!important;stroke:#b30000!important;color:#000!important;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .red ellipse{fill:#ffe5e5!important;stroke:#b30000!important;color:#000!important;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .red circle{fill:#ffe5e5!important;stroke:#b30000!important;color:#000!important;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .red path{fill:#ffe5e5!important;stroke:#b30000!important;color:#000!important;}#mermaid-b2f67ffa-4baa-4302-a7fc-ea8f7f6854ac .red tspan{fill:#000!important;}Only Tier-0 accessblockedblockedPrivileged AccessWorkstationHardened, Isolated,WDAC/AppLockerDomain ControllersPKIAADC/AD FSInternet / Email / SaaSServers + Workstations

🔧 6. PAW Implementation (Practical Steps)
6.1 Create PAW OU
OU=PAWs,DC=domain,DC=com

6.2 Configure PAW GPO / Intune Profile

Disable Internet access
Disable consumer apps
Disable non‑admin tools
Enable BitLocker
Enable Secure Boot
Enable Device Guard / WDAC
Enable Credential Guard
Enable Microsoft Defender + ASR rules
Enforce firewall lockdown

6.3 Allow‑listing (Mandatory)
Only approved admin tools allowed:

























CategoryExamplesDirectory toolsADUC, ADSI Edit, RSAT-AD-PowerShellIdentity toolsgMSA manager, certutil, pkiviewTroubleshootingeventvwr, PowerShell (Constrained)CustomJEA endpoints
6.4 Tier‑Scoped Logon
PAWs → allow ONLY Tier‑0 admin identities.
All Tier‑1 / Tier‑2 identities → DENY.

⚔️ 7. Attack Scenarios PAWs Neutralize
🛑 Pass‑the‑Hash from compromised workstation
No Tier‑0 creds ever log into Tier‑2 endpoints → hash never exists on compromised machine.
🛑 Credential theft via LSASS dumping
PAWs + WDAC + Credential Guard → protected LSASS, minimal footprint.
🛑 Phishing → RMM takeover → DC compromise
PAWs do NOT allow email, browser, or RMM agents.
🛑 Token replay & session hijack
PAWs block untrusted network paths and enforce hardened logon.

🛡 8. Defense Strategy — “Bhishma’s Discipline”
Must‑Have

PAWs for ALL Tier‑0 admins
Admins NEVER log into Tier‑0 systems from daily PCs
WDAC/AppLocker enforcement
BitLocker + Secure Boot
No internet, no email
Tier‑0 logon restrictions (no T0 on T1/T2)

Recommended

Smart card / FIDO2 for PAW login
JEA for least‑privileged PowerShell
Admin SIEM watchlist monitoring PAW activity


🔧 9. Quick Commands (Copy‑Paste)
Check what GPOs applied
PowerShellgpresult /rShow more lines
Check allowed applications
PowerShellGet-AppLockerPolicy -Effective -XmlShow more lines
Verify no internet
PowerShellTest-NetConnection www.microsoft.comShow more lines
Check Defender Tamper Protection
PowerShellGet-MpComputerStatus | Select RealTimeProtectionEnabled, TamperProtectionEnabledShow more lines

🧵 10. Mind Map (Placeholder)
PAW
 ├─ Isolation
 ├─ Hardened OS
 ├─ WDAC/AppLocker
 ├─ No Internet / No Email
 ├─ Tier-0 Only Logon
 ├─ Defender + ASR
 ├─ Credential Guard
 ├─ Verification & Monitoring


📚 References

Microsoft Privileged Access Strategy & Enterprise Access Model
 [github.com]
Tiered administration & clean source principle (Quest/Microsoft blogs)
 [github.com]
Logon restriction patterns for Tier‑0 isolation
