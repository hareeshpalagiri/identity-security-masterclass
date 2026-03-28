📘 05 — Privileged Access Management (PAM)
Controlling powerful identities using Mahabharata’s strategic characters.

🏹 **Mahabharata Story Opener —
“The Power of Bhishma & the Danger of Ashwatthama”**
In Hastinapura, some individuals held immense authority:
Bhishma

Commanded armies
Trusted by everyone
Bound by vows
Used his power responsibly
Represented controlled privileged access

Ashwatthama

Powerful but impulsive
Used power recklessly
Acted without accountability
Became a threat to everyone
Represented privilege creep & uncontrolled admin access

PAM in cybersecurity exists to create Bhishmas, not Ashwatthamas.
Privileged access must be:

Controlled
Monitored
Time-bound
Audited
Granted only when needed
Revoked after use

This is the heart of PAM.

🔐 1. What is Privileged Access Management? (Simple Definition)
PAM controls and secures powerful accounts that can:

manage systems
change configurations
access sensitive data
create users
reset passwords
run administrative tasks

Privileged roles are the biggest targets for attackers.

🧠 2. Why PAM is Critical (Simple + Deep)
Privileged accounts are like:

Bhishma → stable, disciplined, controlled
Ashwatthama → dangerous when unchecked
Drona → powerful but with emotional weaknesses
Shakuni → manipulates those in power

Modern attackers aim for:
“Get domain admin → get everything.”
Without PAM:

Attackers escalate privileges
Insider threats misuse power
Privilege creep goes unnoticed
No accountability exists
Compromised admin account = total breach


👑 3. Types of Privileged Accounts
1. Domain Admins (Highest Power)
Access to entire AD environment.
2. Enterprise Admins
Cross-domain administration.
3. Local Administrator Accounts
Often reused passwords → attacker goldmine.
4. Service Accounts
Often have high privileges and rarely monitored.
5. Application Admins
Azure, AWS, M365 admin roles.
6. Device Admins
Manage system configurations.
These accounts require stronger controls than normal identities.

🕸 4. Privilege Creep (Ashwatthama Effect)
Privilege creep happens when:

Users change roles
Old access never removed
Gradually become over‑privileged

Like Ashwatthama:

More freedom
No accountability
Hard to control
Causes massive destruction
Becomes an unpredictable threat

This happens in organizations literally every day.

🎬 5. Animation Placeholder
[GIF Placeholder: "Bhishma receiving temporary blessed weapons → Ashwatthama hoarding weapons over time → visualizing privilege creep vs. controlled privileges"]


🛠 6. Real-World PAM Implementations
✔ Privileged Identity Management (PIM) in Entra ID
Grant just‑in‑time (JIT) admin access.
Steps:

Identity → Privileged Identity Management
My Roles → Eligible Roles
Activate: provides temporary privilege
Requires justification
Requires MFA
Auto-expiry after time


✔ LAPS (Local Administrator Password Solution)
Randomizes local admin passwords.
PowerShell example:
PowerShellGet-AdmPwdPassword -ComputerName "Server01"Show more lines

✔ gMSA (Group Managed Service Accounts)
Service accounts with automatic password rotation.
Creation:
PowerShellNew-ADServiceAccount -Name WebApp01 -DNSHostName WebApp01.corp.local -PrincipalsAllowedToRetrieveManagedPassword "IISServers"Show more lines

✔ Break‑Glass Accounts
Emergency accounts stored offline for disaster recovery.

Must NOT be used regularly
Require strict monitoring


📊 7. PAM Architecture (Mermaid Diagram)
flowchart TD    A[Request Privilege] --> B{PIM Approval?}    B -->|Yes| C["Activate Role (Time-bound)"]    B -->|No| D[Deny Access]    C --> E[Perform Admin Task]    E --> F[Auto-Expiry of Privilege]Show more lines#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-thickness-normal {stroke-width:1px}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .cluster-label span p {background-color:transparent}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .label text, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node rect, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node circle, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node ellipse, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node polygon, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .rough-node .label text, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node .label text, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .image-shape .label, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .icon-shape .label {text-anchor:middle}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .rough-node .label, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node .label, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .image-shape .label, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .icon-shape .label {text-align:center}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node.clickable {cursor:pointer}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .cluster text {fill:rgb(51, 51, 51)}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .cluster span {color:rgb(51, 51, 51)}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 rect.text {fill:nonestroke-width:0;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .icon-shape, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .icon-shape p, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .icon-shape rect, #mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .error-icon{fill:#552222;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .error-text{fill:#552222;stroke:#552222;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-thickness-normal{stroke-width:1px;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .marker{fill:#333333;stroke:#333333;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .marker.cross{stroke:#333333;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 p{margin:0;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .cluster-label text{fill:#333;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .cluster-label span{color:#333;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .cluster-label span p{background-color:transparent;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .label text,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 span{fill:#333;color:#333;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node rect,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node circle,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node ellipse,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node polygon,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .rough-node .label text,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node .label text,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .image-shape .label,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .icon-shape .label{text-anchor:middle;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .rough-node .label,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node .label,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .image-shape .label,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .icon-shape .label{text-align:center;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node.clickable{cursor:pointer;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .arrowheadPath{fill:#333333;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .flowchart-link{stroke:#333333;fill:none;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .cluster text{fill:#333;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .cluster span{color:#333;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 rect.text{fill:none;stroke-width:0;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .icon-shape,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .icon-shape p,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .icon-shape rect,#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-4d0f833d-162e-44c2-9ae3-a0fec4df9686 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}YesNoRequest PrivilegePIM Approval?Activate Role (Time-bound)Deny AccessPerform Admin TaskAuto-Expiry of Privilege

⚔️ 8. How Attackers Target Privileged Accounts
1. Pass-the-Hash / Pass-the-Ticket
Steal credentials or tokens → escalate to domain admin.
2. Kerberoasting
Crack service accounts → escalate.
3. Golden Ticket
Forged TGT = infinite power.
4. Shadow Admins
Hidden privileged accounts:

Members of ACLs
Delegated rights
gMSA misconfigurations

5. Abuse of stale privileges
Privilege creep = easy target.
6. Social engineering
Shakuni tricking legitimate high-privilege users.

🛡 9. Defense Strategies
✔ Just-in-Time (JIT) Access
Short, temporary admin sessions.
✔ Just-Enough-Administration (JEA)
Limit what admin can do.
✔ Tiered Administration Model
Separate admin accounts per tier.
✔ MFA for ALL privileged accounts
Mandatory.
✔ Logging & Monitoring (Sanjaya metaphor)
Track:

role activations
elevation failures
suspicious privileged actions

✔ Access Review (Vidura metaphor)
Periodic validation of correct privileges.

🧵 10. Mind Map Placeholder
PAM Mind Map:
 - Privileged Accounts
 - PIM/JIT
 - LAPS
 - gMSA
 - Privilege Creep
 - Shadow Admins
 - Attack Techniques
 - Defense Model
 - Governance (Vidura)


🔗 11. Transition to Chapter 06 — Zero Trust
Once privileged accounts are controlled, the next logical question is:

“How do we secure everything so that NOTHING is trusted automatically?”

This leads to Zero Trust —
a strategy similar to:

Never trusting Shakuni
Always verifying even known identities
Continuous validation (like Sanjaya & Vidura together)

Next chapter:
👉 Chapter 06 — Zero Trust
