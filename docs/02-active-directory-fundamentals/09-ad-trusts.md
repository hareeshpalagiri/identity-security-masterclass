📘 Chapter 08 — Active Directory Trusts
How separate AD domains & forests form secure relationships — explained simply with enterprise clarity & strategic analogies.

🏹 **Mahabharata Strategic Opener —
“Alliances Between Kingdoms”**
In ancient times, different kingdoms such as Hastinapura, Panchala, Matsya, and others formed alliances:


Some alliances were strong and transitive —
“If Hastinapura trusts Panchala, it also trusts Matsya because Panchala trusts them.”


Some alliances were limited and non‑transitive —
“Hastinapura trusts Gandhara, but this trust does NOT extend to other kingdoms.”


Some alliances required selective access — only certain warriors or envoys were allowed entry.


This is exactly how Active Directory Trusts work.
Trusts control which domains and forests can authenticate users from each other and under what rules.

🔵 1. What is an AD Trust? (Simple Definition)
An Active Directory Trust is a secure relationship that allows:

Users in one domain/forest to be authenticated by another domain/forest.

Trusts enable:

Cross‑domain logons
Shared applications
Centralized authentication
Resource access across AD boundaries


🟧 2. Why Trusts Exist
Without trusts:

Users must have separate accounts in each domain
Apps cannot authenticate users from other domains
Cross‑forest collaboration becomes impossible

With trusts:

One identity → multiple domains
Company mergers & acquisitions can integrate quickly
Resource sharing becomes easy
Security boundaries remain intact


🏗 3. Trust Types (Simple + Clean)
Active Directory supports two major families:

A) Direction

One‑Way Trust
Domain A → trusts → Domain B
But B does NOT trust A.

Analogy:
Hastinapura accepts warriors from Panchala,
but Panchala does NOT accept warriors from Hastinapura.

Two‑Way Trust
Both domains trust each other.

This is the most common configuration inside a forest.

B) Scope


Domain Trusts
Between domains in the same forest
Automatic, transitive, two‑way.


Forest Trusts
Between two separate forests
Must be created manually.


External Trusts
Legacy trusts with NT‑style domains or standalone forests.


Shortcut Trusts
Improve authentication performance between distant domains
inside a large forest.



🔀 4. Transitive vs Non‑Transitive Trusts
Transitive Trust
If A trusts B and B trusts C → A trusts C.
Used inside all modern forests.
Non‑Transitive Trust
Trust does NOT extend automatically.
Used for:

External Trusts
Some Forest Trust cases


🔐 5. Authentication Flow (Simple Overview)
When a user from Domain A tries to access Domain B:

User authenticates to their home DC
Home DC issues Kerberos ticket
A referral is made to Domain B’s KDC
Domain B authorizes resources based on:

Group membership
SID history
Selective authentication rules



(This is a simplified flow — enough for your book.)

📡 6. Selective Authentication (Zero‑Trust Style Permission)
Selective authentication ensures:

Users from the trusted domain must be explicitly allowed to authenticate to resources.

This is used in high‑security cross‑forest situations.
Analogy:
A kingdom accepts an envoy, but only certain envoys can enter royal chambers.

🧱 7. SID Filtering (Protection Against Abuse)
SID Filtering prevents attackers from:

Adding fake privileged SIDs
Escalating across trust boundaries
Abusing foreign security principals

SID filtering is enabled by default on external and forest trusts.

🔧 8. DNS Requirements for Trusts
Trusts rely heavily on DNS:

Each domain must resolve the other domain’s DNS
Use conditional forwarders
Or stub zones
Or forest‑wide resolution

Microsoft emphasizes DNS planning before creating site or trust topology.
 [github.com]

📊 9. Diagram — How Trusts Work (Mermaid)
flowchart LR    A[Domain A Users] -->|Authenticate| B[Domain A DC]    B -->|Referral via Trust| C[Domain B DC]    C -->|Authorize Access| D[Resource in Domain B]Show more lines#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-thickness-normal {stroke-width:1px}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .cluster-label span p {background-color:transparent}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .label text, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node rect, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node circle, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node ellipse, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node polygon, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .rough-node .label text, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node .label text, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .image-shape .label, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .icon-shape .label {text-anchor:middle}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .rough-node .label, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node .label, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .image-shape .label, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .icon-shape .label {text-align:center}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node.clickable {cursor:pointer}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .cluster text {fill:rgb(51, 51, 51)}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .cluster span {color:rgb(51, 51, 51)}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 rect.text {fill:nonestroke-width:0;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .icon-shape, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .icon-shape p, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .icon-shape rect, #mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .error-icon{fill:#552222;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .error-text{fill:#552222;stroke:#552222;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-thickness-normal{stroke-width:1px;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .marker{fill:#333333;stroke:#333333;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .marker.cross{stroke:#333333;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 p{margin:0;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .cluster-label text{fill:#333;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .cluster-label span{color:#333;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .cluster-label span p{background-color:transparent;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .label text,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 span{fill:#333;color:#333;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node rect,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node circle,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node ellipse,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node polygon,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .rough-node .label text,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node .label text,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .image-shape .label,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .icon-shape .label{text-anchor:middle;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .rough-node .label,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node .label,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .image-shape .label,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .icon-shape .label{text-align:center;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node.clickable{cursor:pointer;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .arrowheadPath{fill:#333333;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .flowchart-link{stroke:#333333;fill:none;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .cluster text{fill:#333;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .cluster span{color:#333;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 rect.text{fill:none;stroke-width:0;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .icon-shape,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .icon-shape p,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .icon-shape rect,#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-1af78ff4-39f3-44d3-bd4f-cc7f29848440 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}AuthenticateReferral via TrustAuthorize AccessDomain A UsersDomain A DCDomain B DCResource in Domain B

🏢 10. Enterprise Scenario — Two Companies Integrate
Scenario:
Company A acquires Company B.

CompanyA.local
CompanyB.local

They want:

Company B users → access Company A resources
Company A helpdesk → manage Company B accounts
Shared applications across forests

✔ Step 1 — DNS Forwarding
Add conditional forwarders:
CompanyA.local → DNS resolves CompanyB.local  
CompanyB.local → DNS resolves CompanyA.local

✔ Step 2 — Decide Trust Type
Most common:
Forest trust — Two‑Way, Transitive
✔ Step 3 — Security Settings

Enable Selective Authentication if high security
Keep SID Filtering enabled
Review access on per‑resource basis

✔ Step 4 — Test Authentication

Logon from CompanyB user to CompanyA shared folder
Validate Kerberos delegation
Check event logs

✔ Step 5 — Gradual Integration

ADMT (optional) for account migration
Conditional access policies across forests


🧵 11. When to Use Which Trust (Quick Decision Table)





























SituationBest Trust TypeTwo domains in same forestBuilt‑in Parent/Child (automatic)Access between two forestsForest TrustOld NT4 domain integrationExternal TrustAuthentication slow across large forestShortcut TrustHighly sensitive cross‑forest accessForest Trust + Selective Authentication

🔚 12. Summary
You now understand:

What trusts are
Why they exist
Types of trusts
Transitive vs non‑transitive
Direction (one‑way vs two‑way)
Selective authentication (important in real companies)
SID filtering
DNS requirements
Authentication flow (simple overview)
Enterprise acquisition example

This chapter is intentionally “medium‑depth” to match your book style.
