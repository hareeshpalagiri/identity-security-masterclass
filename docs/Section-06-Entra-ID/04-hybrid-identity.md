📘 06.04 — Hybrid Identity (PHS, PTA, Seamless SSO, Cloud Sync)

A simple, deep, Mahabharata-aligned explanation of how on‑prem Active Directory connects to Microsoft Entra ID.

🏹 **Mahabharata Analogy —
“Bridging two kingdoms with a sacred alliance.”**
In the Mahabharata:

The Pandavas controlled Indraprastha, and
The Panchalas controlled Kampilya.

Two great kingdoms…
Two sets of warriors…
Two councils, two laws.
But to defeat the Kauravas, the two kingdoms formed a single, unified alliance, sharing:

identity (who belongs to which clan),
access (who can enter which war tent),
trusted messengers, and
joint command.

This is Hybrid Identity:

The alliance between on‑prem Active Directory (AD) and Microsoft Entra ID (cloud identity) to create a single unified identity for users and devices.

Hybrid Identity ensures:
✔ One identity → works on‑premises AND in the cloud
✔ One login → SSO across apps
✔ One security policy → Conditional Access, MFA, Zero Trust
✔ One source of truth → synchronized identity
Microsoft defines Hybrid Identity as identity that spans both on‑prem and cloud resources.
 [acefekay.w...dpress.com]

🔐 1. What is Hybrid Identity? (Simple Definition)
Hybrid Identity is an architecture where:

Identities originate in on‑prem AD,
Synchronize to Microsoft Entra ID, and
Are authenticated using PHS, PTA, or federation.

Hybrid Identity enables:

Cloud Single Sign-On (SSO)
MFA & Conditional Access
Access to Microsoft 365 & SaaS apps
Secure modern authentication
Cloud-based governance

Microsoft Entra supports Hybrid Identity under its device and identity integration features.
 [acefekay.w...dpress.com]

🧭 2. Why Hybrid Identity Exists — Hastinapura Logic





























Ancient ScenarioModern IdentityTwo kingdoms needed a trusted bridgeOn‑prem AD + Cloud Entra IDMessengers verified using shared sealsSync uses secure hash/signatureAlliance made armies stronger togetherHybrid identity enables AD + Cloud appsUnified command minimized confusionUnified identity = one login, one policyAllies must trust each otherCloud & on‑prem must trust identity
Hybrid Identity solves the question:
“How does a user who exists in AD access cloud apps securely?”

🧠 3. The Three Hybrid Identity Models (Based on Microsoft Learn)
Microsoft Entra ID supports multiple sign‑in methods depending on the hybrid identity configuration.
 [acefekay.w...dpress.com]

⭐ 3.1 Password Hash Synchronization (PHS)
Most common, simplest, most reliable.
How it works:

AD password hash is hashed again
Securely synced to Entra ID
Auth happens in the cloud (fast & highly available)

Pros:

Simple
No on‑prem dependency
Best for Conditional Access
No special infra
Supports MFA

Cons:

Org must be comfortable syncing password hashes

Use Case:
99% of Microsoft 365 customers.

⭐ 3.2 Pass-Through Authentication (PTA)
Cloud delegates authentication to on‑prem AD.
How it works:

Cloud forwards login request to on‑prem Authentication Agent
Users authenticate with on‑prem AD password
No password hash stored in cloud

Pros:

Password never leaves on‑prem
Works well for strict password policies

Cons:

Requires on‑prem infra
Adds dependency during login

Use Case:
Organizations requiring on-premise password validation.

⭐ 3.3 Federation (Legacy / ADFS)
Oldest method — mostly replaced by PHS/PTA.
How it works:

Entra ID redirects users to ADFS
ADFS validates credentials
ADFS issues SAML token to cloud

Pros:

Supports old compliance requirements
Custom claim rules

Cons:

Heavy infra
Expensive
Outdated
High attack surface
Most organizations moving away

Use Case:
Legacy-only. Consider migrating to PHS/PTA.

⭐ BONUS: Cloud Sync (Lightweight Sync Engine)
Microsoft’s Cloud Sync is a modern replacement for Azure AD Connect in many scenarios:

Lightweight agent
Multi‑forest support
No SQL
Simple updates
Cloud‑driven orchestration

BUT:
Supports only PHS & PTA, not federation.
Cloud Sync is part of Entra’s hybrid identity ecosystem.
 [acefekay.w...dpress.com]

🕸 4. Hybrid Identity Architecture Diagram
flowchart TDAD[On-Prem Active Directory] -->|Sync via AAD Connect or Cloud Sync| EntraID[Microsoft Entra ID]subgraph SignInMethods  PHS[Password Hash Sync]  PTA[Pass-Through Auth]  FED["Federation (ADFS)"]endEntraID --> PHSEntraID --> PTAEntraID --> FEDPHS --> CloudApps["Cloud Apps\n(M365, Azure, SaaS)"]PTA --> CloudAppsFED --> CloudAppsShow more lines#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-thickness-normal {stroke-width:1px}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .cluster-label span p {background-color:transparent}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .label text, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node rect, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node circle, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node ellipse, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node polygon, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .rough-node .label text, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node .label text, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .image-shape .label, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .icon-shape .label {text-anchor:middle}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .rough-node .label, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node .label, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .image-shape .label, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .icon-shape .label {text-align:center}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node.clickable {cursor:pointer}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .cluster text {fill:rgb(51, 51, 51)}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .cluster span {color:rgb(51, 51, 51)}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 rect.text {fill:nonestroke-width:0;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .icon-shape, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .icon-shape p, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .icon-shape rect, #mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .error-icon{fill:#552222;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .error-text{fill:#552222;stroke:#552222;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-thickness-normal{stroke-width:1px;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .marker{fill:#333333;stroke:#333333;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .marker.cross{stroke:#333333;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 p{margin:0;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .cluster-label text{fill:#333;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .cluster-label span{color:#333;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .cluster-label span p{background-color:transparent;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .label text,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 span{fill:#333;color:#333;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node rect,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node circle,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node ellipse,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node polygon,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .rough-node .label text,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node .label text,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .image-shape .label,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .icon-shape .label{text-anchor:middle;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .rough-node .label,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node .label,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .image-shape .label,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .icon-shape .label{text-align:center;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node.clickable{cursor:pointer;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .arrowheadPath{fill:#333333;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .flowchart-link{stroke:#333333;fill:none;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .cluster text{fill:#333;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .cluster span{color:#333;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 rect.text{fill:none;stroke-width:0;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .icon-shape,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .icon-shape p,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .icon-shape rect,#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-9d0cf4b8-604f-4575-9a1b-626226462c20 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}SignInMethodsSync via AAD Connect or Cloud SyncOn-Prem Active DirectoryMicrosoft Entra IDPassword Hash SyncPass-Through AuthFederation (ADFS)Cloud Apps\n(M365, Azure,SaaS)

🔧 5. Seamless SSO (For PHS & PTA)
Seamless SSO signs users in automatically on domain-joined PCs without passwords.
How it works:

Kerberos ticket from AD
Browser silently authenticates
Entra ID verifies device + user
No popup → instant login

Requirements:

PHS or PTA
Domain-joined PC
Seamless SSO configured in Azure AD Connect


🔥 6. Cloud Kerberos Trust (The Future of Hybrid Identity)
Modern authentication using Entra ID as the trust anchor for on‑prem Kerberos.
Benefits:

No ADFS
No certificate trust
Simplified WHfB deployment
Works with Hybrid Azure AD Join

Microsoft recognizes device identity as essential for hybrid authentication.
 [acefekay.w...dpress.com]

🛡 7. Security Benefits of Hybrid Identity
✔ Conditional Access for AD-synced users
Device compliance, risk-based access, geolocation.
✔ MFA enforcement
Regardless of on‑prem password.
✔ Zero Trust
Integrates signals across cloud & on-prem.
✔ Identity Protection
Risk-based identity detection.
 [github.com]
✔ PIM (Privileged Identity Management)
JIT admin access for synced users.

🧵 8. Mind Map
Hybrid Identity
 ├─ Sync Engine
 │   ├─ Azure AD Connect
 │   └─ Cloud Sync
 ├─ Sign-in Methods
 │   ├─ Password Hash Sync (PHS)
 │   ├─ Pass-through Authentication (PTA)
 │   └─ Federation (ADFS)
 ├─ Enhancements
 │   ├─ Seamless SSO
 │   └─ Cloud Kerberos Trust
 ├─ Zero Trust Controls
 │   ├─ MFA
 │   ├─ CA
 │   ├─ Identity Protection
 └─ Migration Path


🎯 Summary
Hybrid Identity is the bridge between:

The legacy identity world (Active Directory)
The modern cloud identity world (Entra ID)

It enables:

Unified identity
Secure authentication
Seamless SSO
Zero Trust enforcement
Cloud access for AD users

Most organizations use PHS, many use PTA, and federation is fading.
Cloud Sync + Cloud Kerberos Trust represent the future of hybrid identity.

