📘 Chapter 04 — Group Policy (GPO)
How kingdoms enforce laws — and how Active Directory enforces policies.

🏹 **Mahabharata Story Opener —
“The Laws of Hastinapura”**
In Hastinapura, not even the strongest warrior could act against established laws:

Bhishma obeyed vows and rules even if it went against his emotions
Warriors followed battlefield rules (Dharma‑Yuddha)
Councils issued kingdom‑wide orders
Clans had their own internal rules
Breaking rules led to consequences

This is exactly what Group Policy (GPO) does in Active Directory:

It defines rules, security settings, and behavior for every user and computer in the domain — automatically and consistently.

GPO = the lawbook of the AD kingdom.

🔐 1. What is Group Policy? (Simple Definition)
Group Policy is a system in Active Directory used to:

configure
secure
control
restrict
standardize

the behavior of users and computers across the domain.
It is one of the MOST powerful features in Active Directory.

📌 2. Why GPO Exists (Simple + Deep)
Without GPO, computers would behave like:

warriors with no discipline
everyone setting their own rules
passwords with no policies
devices misconfigured
security depending on individual choice

With GPO:

password policies become uniform
software can be deployed automatically
security baselines are enforced
devices follow standard hardening
attackers cannot bypass rules easily

GPO brings order, just like Hastinapura’s enforced laws.

🧱 3. How GPO Works (High-Level Concept)

Policies are created
Policies are linked to an OU / Domain
Users & computers receive policies
Domain controllers deliver policies
Devices apply settings at startup/login

Mahabharata analogy:
Laws created by the kingdom council →
Sent across districts →
People must follow them or face consequences.

🌳 4. GPO Hierarchy — LSDOU Explained
Order of GPO processing:
L → S → D → OU






























LevelMeaningAnalogyLLocal MachineRules inside a warrior’s personal hutSSiteRules for the entire regionDDomainLaws of HastinapuraOUOrganizational UnitRules for specific clans
Later rules override earlier ones.

📊 5. GPO Processing Flow (Mermaid Diagram)
flowchart TD    A[Local Policy] --> B[Site Policy]    B --> C[Domain Policy]    C --> D[OU Policy]    D --> E[Resultant Set of Policy]Show more lines#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .error-icon {fill:rgb(85, 34, 34)}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-thickness-normal {stroke-width:1px}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-thickness-thick {stroke-width:3.5px}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-pattern-solid {stroke-dasharray:0}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .cluster-label span p {background-color:transparent}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .label text, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node rect, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node circle, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node ellipse, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node polygon, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .rough-node .label text, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node .label text, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .image-shape .label, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .icon-shape .label {text-anchor:middle}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .rough-node .label, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node .label, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .image-shape .label, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .icon-shape .label {text-align:center}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node.clickable {cursor:pointer}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .cluster text {fill:rgb(51, 51, 51)}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .cluster span {color:rgb(51, 51, 51)}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c rect.text {fill:nonestroke-width:0;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .icon-shape, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .icon-shape p, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .icon-shape rect, #mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .error-icon{fill:#552222;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .error-text{fill:#552222;stroke:#552222;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-thickness-normal{stroke-width:1px;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-thickness-thick{stroke-width:3.5px;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-pattern-solid{stroke-dasharray:0;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .marker{fill:#333333;stroke:#333333;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .marker.cross{stroke:#333333;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c p{margin:0;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .cluster-label text{fill:#333;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .cluster-label span{color:#333;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .cluster-label span p{background-color:transparent;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .label text,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c span{fill:#333;color:#333;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node rect,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node circle,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node ellipse,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node polygon,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .rough-node .label text,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node .label text,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .image-shape .label,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .icon-shape .label{text-anchor:middle;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .rough-node .label,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node .label,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .image-shape .label,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .icon-shape .label{text-align:center;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node.clickable{cursor:pointer;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .arrowheadPath{fill:#333333;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .flowchart-link{stroke:#333333;fill:none;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .cluster text{fill:#333;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .cluster span{color:#333;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c rect.text{fill:none;stroke-width:0;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .icon-shape,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .icon-shape p,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .icon-shape rect,#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-304e4794-cc12-475f-8c56-fea01f5bb22c :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Local PolicySite PolicyDomain PolicyOU PolicyResultant Set of Policy
Final applied result = RSoP.

🛠 6. Real-World Group Policy Configuration
✔ Open Group Policy Management
gpmc.msc

✔ Create a GPO
Right-click domain / OU →
“Create a GPO in this domain, and Link it here…”
✔ Edit GPO
Right-click → Edit
✔ Common Settings to Configure
Password Policy
Computer Config → Policies → Windows Settings → Security Settings → Account Policies → Password Policy

Disable USB devices
Computer Config → Admin Templates → System → Removable Storage Access

Deploy Software
Computer Config → Policies → Software Settings → Software Installation

Harden RDP
Computer Config → Admin Templates → Windows Components → Remote Desktop Services


🧾 7. GPO Linking — A Crucial Concept
GPOs don’t apply unless linked to:

Domain
Site
OU

Best practice:

Do NOT link GPOs at the root unless required
Use OUs for targeted control
Avoid complex nesting

Mahabharata analogy:
Different clans receive different battle rules.

🛡 8. Security GPOs — Hardening the Domain
Examples:
✔ Disable LM & NTLM
Prevents NTLM relay
Network Security: LAN Manager Authentication Level → Send NTLMv2 response only  

✔ Enable Firewall
Default inbound/outbound restrictions.
✔ Audit Logging
Success + failure events.
✔ Disable SMBv1
Mitigates ransomware.
✔ Microsoft Security Baselines
Import via Security Compliance Toolkit.

⚔️ 9. How Attackers Abuse GPO
Attackers LOVE misconfigured GPO.
1. GPO Abuse via Delegations
If helpdesk has control → attacker can hijack.
2. GPO Password Exposure
Old “cpassword” in GPP stored passwords →
decrypted in seconds.
3. Malicious Startup Scripts
Insert malware through GPO scripts.
4. GPO-induced Backdoors
Use GPO to disable antivirus/firewall.
5. RSoP Enumeration
Attackers enumerate applied policies to understand security posture.
Mahabharata analogy:
If the kingdom lawmaker (Vidura role) is compromised,
the WHOLE kingdom falls.

🛡 10. Defense Strategies

Limit GPO editing rights
Use Role-Based Delegation
Enable GPO change auditing
Avoid using Domain Admin for routine GPO work
Block inheritance where needed
Use WMI filtering carefully
Deploy tiered admin model
Switch to modern Intune policies for cloud devices

GPO is powerful — treat it like Bhishma's command authority.

🧵 11. Mind Map Placeholder
GPO Mind Map:
  - LSDOU
  - Policy Linking
  - Security Hardening
  - Administrative Templates
  - Delegation
  - GPO Abuse Techniques
  - Defense Strategies


🔗 12. Transition to Chapter 05 — DNS & DHCP in AD
After laws (GPO) come the communication systems.
In a kingdom:

Messengers
Couriers
Signaling systems
Army communications

In AD:

DNS = how objects find each other
DHCP = how systems get addresses & join the network

Next chapter:
👉 Chapter 05 — DNS & DHCP in AD
(How identity systems communicate inside the kingdom)
