📘 08 — Azure AD Connect & Hybrid Identity Synchronization

🏹 **Mahabharata Analogy —
“Building the sacred bridge between two great kingdoms.”**
In the Mahabharata:

Hastinapura (Kauravas)
Indraprastha (Pandavas)

…were two powerful kingdoms with different rules, armies, temples, and citizens.
But during diplomatic missions, royal marriages, alliances, and war preparations, they needed a secure, trusted bridge that allowed:

exchange of warriors,
communication between rulers,
recognition of identities,
and flow of resources.

This is exactly what Azure AD Connect and Hybrid Identity do:

They build the sacred bridge between on-prem Active Directory and cloud Entra ID, ensuring one identity works everywhere.

Microsoft defines Hybrid Identity as an identity that spans on-premises and cloud, using authentication and sync protocols to unify identity.
 [github.com]

🔐 1. What Is Azure AD Connect? (Simple Definition)
Azure AD Connect is Microsoft’s directory synchronization and hybrid identity engine used to:

sync identities from Active Directory to Entra ID,
enable Single Sign-On,
orchestrate PHS (Password Hash Sync) or PTA (Pass-through Authentication),
integrate on-prem and cloud authentication flows.

It is the foundation of Hybrid Identity, enabling both cloud and on-prem apps to trust the same identity.
Microsoft Learn describes Azure AD Connect as part of Entra’s integration with authentication and sync protocols.
 [github.com]

🧠 2. Why Azure AD Connect Exists (Hastinapura Logic)





























Ancient NeedAzure AD Connect FunctionUnity between kingdomsUnity between AD & Entra IDShared recognition of warriorsOne identity across cloud + on-premConsistent messages between rulersConsistent user attributes everywhereValidating who belongs to which kingdomSync UPNs, groups, attributesMaintaining loyalty & trustSecure authentication in cloud
Hybrid identity ensures:

Users sign in once → get access everywhere.


🏛 3. The Three Hybrid Identity Sign-In Models
Described by Microsoft Entra architecture guidance.
 [github.com]
⭐ 3.1 Password Hash Synchronization (PHS)
Most common, simplest, most recommended.

AD password hash → re-hashed → synced to Entra
Cloud authenticates the user
No dependency on on-prem infrastructure

✔ Best for:

99% of organizations
Zero Trust
Conditional Access
MFA everywhere
Cloud-first identity


⭐ 3.2 Pass-through Authentication (PTA)
Cloud sends login to on-prem agent to validate password.

No password hash stored in cloud
On-prem AD remains the “source of truth”

✔ Best for:

Strict regulatory environments
Password policies enforced on-prem


⭐ 3.3 Federation (ADFS / Ping / Okta)
Oldest model — heavy infrastructure.

Cloud redirects to ADFS
ADFS authenticates user
Issues token back to cloud

❌ Not recommended today
Most orgs are migrating away from federation to PHS/PTA.

🔧 4. Directory Synchronization Flow (High Level)
Azure AD Connect synchronizes:

Users
Groups
Contacts
Hashes
Device objects (Hybrid Join)
Attributes (UPN, proxyAddresses, etc.)

It ensures cloud & on-prem identities stay consistent.

🕸 5. Hybrid Identity Architecture (Mermaid Diagram)
flowchart LRAD[On-Prem Active Directory] -->|Sync via Azure AD Connect| Entra[Microsoft Entra ID]subgraph Sign-In Methods  PHS[Password Hash Sync]  PTA[Pass-Through Authentication]  FED[Federation / ADFS]endEntra --> PHSEntra --> PTAEntra --> FEDPHS --> CloudApps[Microsoft 365 / Azure / SaaS Apps]PTA --> CloudAppsFED --> CloudAppsShow more lines#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .error-icon {fill:rgb(85, 34, 34)}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-thickness-normal {stroke-width:1px}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-thickness-thick {stroke-width:3.5px}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-pattern-solid {stroke-dasharray:0}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .cluster-label span p {background-color:transparent}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .label text, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node rect, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node circle, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node ellipse, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node polygon, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .rough-node .label text, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node .label text, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .image-shape .label, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .icon-shape .label {text-anchor:middle}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .rough-node .label, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node .label, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .image-shape .label, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .icon-shape .label {text-align:center}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node.clickable {cursor:pointer}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .cluster text {fill:rgb(51, 51, 51)}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .cluster span {color:rgb(51, 51, 51)}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb rect.text {fill:nonestroke-width:0;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .icon-shape, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .icon-shape p, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .icon-shape rect, #mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .error-icon{fill:#552222;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .error-text{fill:#552222;stroke:#552222;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-thickness-normal{stroke-width:1px;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-thickness-thick{stroke-width:3.5px;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-pattern-solid{stroke-dasharray:0;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .marker{fill:#333333;stroke:#333333;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .marker.cross{stroke:#333333;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb p{margin:0;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .cluster-label text{fill:#333;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .cluster-label span{color:#333;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .cluster-label span p{background-color:transparent;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .label text,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb span{fill:#333;color:#333;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node rect,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node circle,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node ellipse,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node polygon,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .rough-node .label text,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node .label text,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .image-shape .label,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .icon-shape .label{text-anchor:middle;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .rough-node .label,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node .label,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .image-shape .label,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .icon-shape .label{text-align:center;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node.clickable{cursor:pointer;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .arrowheadPath{fill:#333333;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .flowchart-link{stroke:#333333;fill:none;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .cluster text{fill:#333;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .cluster span{color:#333;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb rect.text{fill:none;stroke-width:0;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .icon-shape,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .icon-shape p,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .icon-shape rect,#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-b4356f16-8b18-400c-9b09-5afc2cca32bb :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Sign-In MethodsSync via Azure AD ConnectOn-Prem Active DirectoryMicrosoft Entra IDPassword Hash SyncPass-ThroughAuthenticationFederation / ADFSMicrosoft 365 / Azure /SaaS Apps

⚡ 6. Seamless SSO (Adds True SSO to PHS/PTA)
Seamless SSO uses Kerberos on internal networks to sign in users automatically.
How it works:

User logs into domain-joined PC
Kerberos ticket is issued
Browser automatically signs the user in
Entra ID accepts the ticket + cloud session begins

Useful for organizations without ADFS.

🌩 7. Cloud Sync (Lightweight Azure AD Connect Replacement)
Microsoft’s new Cloud Sync offers:

Lightweight agent
Cloud-controlled sync
Multi-forest support
No SQL dependency
Fast updates

Cloud Sync supports:

PHS
PTA
Device writeback (limited)

This is part of Microsoft’s modernization of authentication and sync integration.
 [github.com]

🎯 8. Device Identity in Hybrid Identity
Azure AD Connect also enables:

Hybrid Azure AD Join
Device writeback (for PHS/PTA scenarios)
Certificate trust (older WHfB model)
Cloud Kerberos Trust (latest WHfB model)

Microsoft Learn defines device identity & join types under Entra ID’s device capabilities.
 [learn.microsoft.com]
Cloud Kerberos Trust = Future of Hybrid Identity

No ADFS needed
No certificate trust needed
Simplifies passwordless authentication
Issues Kerberos tickets from cloud credentials


🛡 9. Security Hardening for Azure AD Connect
✔ Enforce least privilege
Azure AD Connect server must only be managed by Tier‑0 admins.
✔ Isolate the sync server

No internet browsing
No email
No user access

✔ Use the latest build
Security patches are frequent.
✔ Enable password writeback
Allows cloud-initiated resets (via SSPR) to sync back.
✔ Protect PTA Agents
They process live passwords → must be monitored.
✔ Disable unnecessary features
E.g., avoid Exchange hybrid if not needed.

🔍 10. Troubleshooting Insights
Common issues:

Attribute filtering errors
UPN mismatch
Duplicate proxyAddresses
Sync rule conflicts
Stale objects
AD inconsistencies

Microsoft’s documentation outlines these as standard troubleshooting categories.
 [github.com]

🧵 11. Mind Map
Azure AD Connect
 ├─ Sync Engine
 │   ├─ Users
 │   ├─ Groups
 │   ├─ Attributes
 ├─ Authentication
 │   ├─ PHS
 │   ├─ PTA
 │   └─ Federation
 ├─ Enhancements
 │   ├─ Seamless SSO
 │   ├─ Cloud Sync
 │   ├─ Cloud Kerberos Trust
 ├─ Device Identity
 │   ├─ Hybrid AAD Join
 │   ├─ Device Writeback
 ├─ Security
 │   ├─ Tier-0 Isolation
 │   ├─ Least Privilege
 │   ├─ Hardening Sync Server
 └─ Monitoring


🎯 Summary
Azure AD Connect is the identity bridge between ON‑PREM Active Directory and CLOUD Entra ID.
It:

Synchronizes users, groups, devices
Enables modern sign-in with PHS/PTA
Supports Seamless SSO
Provides hybrid identity consistency
Powers Zero Trust and modern authentication
Integrates with device trust & passwordless models

