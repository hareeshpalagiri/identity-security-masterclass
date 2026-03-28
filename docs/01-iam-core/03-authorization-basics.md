📘 03 — Authorization Basics
Deciding “What you can access” after authentication
Mahabharata Strategic Storytelling + Modern IAM Concepts

🏹 Mahabharata Story Opener — “Inside the Walls of Hastinapura”
In Hastinapura, proving your identity allowed you to enter the gate —
but what you could access after entering depended on your role, lineage, trust level, and permissions.
Examples:

Abhimanyu could enter certain formations but not exit others → partial access
Karna had access conflicts (raised in one house, loyal to another) → identity misalignment
Bhishma could access war councils, royal chambers, armory → privileged identity
Ordinary warriors could not enter strategic war rooms
Shakuni manipulated access to influence decisions → access misuse
Vidura ensured only the right people entered political chambers → governance

This is exactly how Authorization works in modern security.

🔐 1. What is Authorization? (Simple Definition)
Authorization is the mechanism that decides:

“What resources can this authenticated identity access?”

If authentication answers:

Who are you?

Authorization answers:

What can you do?


🧠 2. Why Authorization Matters (Simple + Deep)
Without authorization:

Everyone could access everything
Sensitive systems would be exposed
Privileged misuse would be easy
Insider threats would explode
Attackers could move laterally freely

Same in Hastinapura:

If any warrior could enter Rajya Sabha, chaos would follow
If Duryodhana could access Kunti’s chambers, risk of misuse rises
If Ashwatthama were granted access without limits → uncontrolled destruction
If Shakuni could access war plans → strategic breach

Authorization = properly controlled permissions.

🧩 3. Authorization Models Explained
✔ Role-Based Access Control (RBAC)
Permissions assigned based on role.
Mahabharata Analogy:
Roles determine access:

Commander (Bhishma) → access to war room
Advisor (Vidura) → political chambers
Warrior (Arjuna) → battlefield access
Messenger → limited halls

Example in AD/Entra ID:

“Security Admin”
“Global Reader”
“Exchange Admin”
“Virtual Machine Contributor”


✔ Attribute-Based Access Control (ABAC)
Access based on attributes:

Department = Finance
Location = Bangalore
Device = Compliant
Risk = Low

Analogy:
Only warriors with combination of:

lineage (attribute)
duty (attribute)
allegiance (attribute)
are allowed into specific areas.


✔ Discretionary Access Control (DAC)
Owner decides who gets access.
Analogy:
A warrior controls who may enter their personal tent.

✔ Mandatory Access Control (MAC)
Strict, system‑enforced levels.
Analogy:
War councils enforce fixed levels:
No matter who you are, you cannot bypass.

🎬 4. Animation Placeholder (Add later)
[GIF Placeholder: "Arjuna enters palace → allowed rooms shown, restricted rooms blocked"]
- Show identity proven at gate
- Show map of rooms with allowed/restricted signs
- Show privileged access with Bhishma-type metaphor


🏛 5. How Authorization Works in Real IAM Systems
Authorization happens through:
🔹 AD Security Groups
PowerShellAdd-ADGroupMember -Identity "Finance-Team" -Members hareeshShow more lines
🔹 ACLs (Access Control Lists)
File/folder/server permissions.
🔹 RBAC (Azure & Applications)
PowerShellaz role assignment create --assignee <ID> --role "Virtual Machine Contributor" --scope <vm-resource>Show more lines
🔹 Conditional Access Policies

If device = compliant → allow
If risk = high → block

🔹 PAM / PIM (Privileged Access Management)
Time‑bound elevation → prevents Bhishma‑like permanent privilege.

📊 6. Authorization Flow Diagram (Mermaid)
flowchart TD    A[Authenticated User] --> B{Check Role?}    B -->|Yes| C[Access Granted]    B -->|No| D[Check Policy Attributes]    D -->|Match| C    D -->|Mismatch| E[Access Denied]Show more lines#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-thickness-normal {stroke-width:1px}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .cluster-label span p {background-color:transparent}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .label text, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node rect, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node circle, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node ellipse, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node polygon, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .rough-node .label text, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node .label text, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .image-shape .label, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .icon-shape .label {text-anchor:middle}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .rough-node .label, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node .label, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .image-shape .label, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .icon-shape .label {text-align:center}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node.clickable {cursor:pointer}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .cluster text {fill:rgb(51, 51, 51)}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .cluster span {color:rgb(51, 51, 51)}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 rect.text {fill:nonestroke-width:0;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .icon-shape, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .icon-shape p, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .icon-shape rect, #mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .error-icon{fill:#552222;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .error-text{fill:#552222;stroke:#552222;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-thickness-normal{stroke-width:1px;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .marker{fill:#333333;stroke:#333333;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .marker.cross{stroke:#333333;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 p{margin:0;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .cluster-label text{fill:#333;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .cluster-label span{color:#333;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .cluster-label span p{background-color:transparent;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .label text,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 span{fill:#333;color:#333;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node rect,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node circle,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node ellipse,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node polygon,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .rough-node .label text,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node .label text,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .image-shape .label,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .icon-shape .label{text-anchor:middle;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .rough-node .label,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node .label,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .image-shape .label,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .icon-shape .label{text-align:center;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node.clickable{cursor:pointer;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .arrowheadPath{fill:#333333;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .flowchart-link{stroke:#333333;fill:none;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .cluster text{fill:#333;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .cluster span{color:#333;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 rect.text{fill:none;stroke-width:0;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .icon-shape,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .icon-shape p,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .icon-shape rect,#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-4d433333-c071-4e02-b57a-d6707517b1c4 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}YesNoMatchMismatchAuthenticated UserCheck Role?Access GrantedCheck Policy AttributesAccess Denied

⚔️ 7. How Attackers Exploit Authorization
1. Privilege Creep (Ashwatthama)
Users accumulate permissions over time.
2. Over‑privileged accounts (Bhishma)
Standing admin rights.
3. Insider threats (Duryodhana)
Authorized identity misusing access.
4. Social engineering (Shakuni)
Tricks someone into granting access.
5. ACL/Group Misconfigurations
Attackers love broad permissions like:

“Everyone: Full Control”
“Domain Users: Read All”

6. Lateral Movement
Weak authorization boundaries allow attackers to pivot.

🛡 8. Authorization Defense Strategy (Simple + Effective)
✔ Least Privilege
No warrior should have more access than necessary.
✔ Just‑In‑Time Admin Access
Give temporary privilege when needed.
✔ Access Reviews
Like Vidura periodically reviewing who can enter which hall.
✔ Group Cleanup
Remove old group memberships.
✔ Segmentation
War council rooms separate from general chambers.
✔ Block legacy permissions
No “Everyone, Full Control”.

🧵 9. Mind Map (Placeholder)
Authorization Mind Map:
  - RBAC (Bhishma, Arjuna)
  - ABAC (Attributes)
  - ACLs
  - Privilege Creep (Ashwatthama)
  - Insider Threat (Duryodhana)
  - Segmentation
  - Access Reviews (Vidura)


🔗 10. Transition to Chapter 04 — SSO & Federation
Once identity is authenticated and authorized inside Hastinapura,
what happens when:

Warriors travel to other kingdoms?
Alliances need cross‑boundary access?

Similarly, modern users need to sign in across multiple apps/domains.
This leads to:
👉 Chapter 04 — SSO & Federation
(Using Mahabharata’s “alliances between kingdoms” analogy to explain cross-domain identity trust)
