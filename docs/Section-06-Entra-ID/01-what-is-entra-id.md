📘 06.01 — What is Entra ID?
A simple, deep, Mahabharata‑inspired introduction to Microsoft’s Cloud Identity Platform.

🏹 **Mahabharata Analogy —
“The king who governs many kingdoms from one central throne.”**
In ancient Bharat:

A Maharaja ruled multiple regions (kingdoms, tribes, states).
Each region had its own warriors, temples, boundaries… but
Identity, authority, and access flowed from one central throne in Hastinapura.
This central authority ensured:

who can enter which palace,
who can access which weapon hall,
who can command which division,
who can speak in royal court,
how outsiders are treated.



This is exactly what Microsoft Entra ID does in the modern digital world:

Entra ID is the “cloud identity king” that governs identity, authentication, and access across apps, devices, cloud services, and hybrid environments.

It is the central source of truth for identity in Microsoft cloud and hybrid systems.

🔐 1. What is Microsoft Entra ID? (Simple Definition)
Microsoft Entra ID is Microsoft’s cloud‑based identity and access management (IAM) platform that:

Manages user identities
Controls authentication and Single Sign-On (SSO)
Protects sign-ins using MFA, Conditional Access, Identity Protection
Manages access to Microsoft 365, Azure, and thousands of SaaS apps
Enables hybrid identity with on‑prem Active Directory
Secures devices, apps, workloads, external users, and APIs

✔ It is the new name for Azure Active Directory (Azure AD).
Microsoft rebranded it in 2023 and expanded it into the broader Microsoft Entra family.
 [learn.microsoft.com], [it.ie]

🌐 2. Why Microsoft Introduced Entra ID
Because the identity world changed:

Organizations use cloud, on‑prem, hybrid, multicloud
Identities now include apps, workloads, devices, contractors, partners
Attacks increasingly target identity, not networks
Zero Trust requires:

Verify identity
Check device
Enforce policies
Monitor continuously



Entra ID became the foundation of the Microsoft Entra lineup:
✔ Entra ID (IAM)
✔ Entra Permissions Management
✔ Entra Verified ID
✔ Entra ID Governance
✔ Entra Internet/Private Access
 [learn.microsoft.com]

🧠 3. What Entra ID Replaces in Traditional AD





























Traditional AD RoleEntra ID EquivalentDomain ControllersCloud identity fabric (no servers needed)Kerberos/NTLMOAuth, OIDC, SAMLGroup Policy (partial)Conditional Access + IntuneWorkstation joinAzure AD Join / Hybrid JoinAuthenticationCloud-based token issuance
Entra ID does NOT replace on‑prem Active Directory —
instead, it becomes the identity plane for all cloud apps and integrates with AD using Hybrid Identity.

📌 4. Key Components of Entra ID (Simple & Clear)
✔ Users & Groups
Manage people, admins, security groups, and dynamic groups.
✔ Apps & SSO
Connect thousands of SaaS apps with SSO, federation, or provisioning.
✔ Authentication
Modern token-based auth (OAuth 2.0, OIDC, SAML).
 [docs.azure.cn]
✔ Conditional Access
Zero Trust engine enforcing:

device compliance
MFA requirement
risk-based access
 [learn.microsoft.com]

✔ Multi-Factor Authentication
Phone, authenticator app, biometrics, FIDO keys.
✔ Identity Protection
Detects risky sign-ins using ML-driven signals.
 [it.ie]
✔ Privileged Identity Management (PIM)
Just-in-time admin roles.
✔ Device Identity
Join or register devices for compliance and secure access.
 [learn.microsoft.com]
✔ Hybrid Identity
Sync users from on‑prem Active Directory via Azure AD Connect.
 [learn.microsoft.com]

🕸 5. Entra ID Architecture (Mermaid Diagram)
flowchart TD    U[Users / Devices / External Guests]    subgraph EntraID[Microsoft Entra ID]        A["Authentication<br/>(OAuth, OIDC, SAML)"]        B[Conditional Access Policies]        C[Identity Protection]        D[SSO & App Access]        E[PIM & RBAC]    end    Apps[SaaS Apps / Microsoft 365 / Azure / On-prem Apps via App Proxy]    U --> A    A --> B    B --> C    B --> D    D --> Apps    E --> AppsShow more lines#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-thickness-normal {stroke-width:1px}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .cluster-label span p {background-color:transparent}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .label text, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node rect, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node circle, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node ellipse, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node polygon, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .rough-node .label text, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node .label text, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .image-shape .label, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .icon-shape .label {text-anchor:middle}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .rough-node .label, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node .label, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .image-shape .label, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .icon-shape .label {text-align:center}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node.clickable {cursor:pointer}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .cluster text {fill:rgb(51, 51, 51)}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .cluster span {color:rgb(51, 51, 51)}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 rect.text {fill:nonestroke-width:0;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .icon-shape, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .icon-shape p, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .icon-shape rect, #mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .error-icon{fill:#552222;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .error-text{fill:#552222;stroke:#552222;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-thickness-normal{stroke-width:1px;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .marker{fill:#333333;stroke:#333333;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .marker.cross{stroke:#333333;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 p{margin:0;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .cluster-label text{fill:#333;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .cluster-label span{color:#333;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .cluster-label span p{background-color:transparent;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .label text,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 span{fill:#333;color:#333;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node rect,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node circle,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node ellipse,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node polygon,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .rough-node .label text,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node .label text,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .image-shape .label,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .icon-shape .label{text-anchor:middle;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .rough-node .label,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node .label,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .image-shape .label,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .icon-shape .label{text-align:center;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node.clickable{cursor:pointer;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .arrowheadPath{fill:#333333;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .flowchart-link{stroke:#333333;fill:none;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .cluster text{fill:#333;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .cluster span{color:#333;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 rect.text{fill:none;stroke-width:0;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .icon-shape,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .icon-shape p,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .icon-shape rect,#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-80525ebe-4f9c-463f-b006-a7f4e0c69ee1 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Microsoft Entra IDUsers / Devices / ExternalGuestsAuthentication(OAuth, OIDC, SAML)Conditional Access PoliciesIdentity ProtectionSSO & App AccessPIM & RBACSaaS Apps / Microsoft 365 /Azure / On-prem Apps viaApp Proxy

🧭 6. Entra ID vs Azure AD — What Changed?
✔ Nothing breaks
✔ No migration needed
✔ Same APIs, Graph, endpoints, auth models
✔ New naming + more capabilities under “Microsoft Entra”
Entra ID is simply:

Azure AD + new features + new name + new identity product family alignment
 [learn.microsoft.com], [netcomlearning.com]


🛡 7. Why Entra ID Matters for Zero Trust
Zero Trust =
Never trust → Always verify → Continuously monitor
Entra ID provides:

Strong identity verification
Device-based access control
Identity risk detection
Least privilege via PIM
Secure access to cloud + hybrid apps

Microsoft recommends Entra ID as the core control plane for Zero Trust.
 [learn.microsoft.com]

🔧 8. Where Entra ID Is Used
Entra ID identity underpins access to:

Microsoft 365
Azure Portal
Azure VMs, Functions, Storage
Power Platform
Dynamics 365
Third-party SaaS apps (Salesforce, ServiceNow, Zoom, etc.)
On-prem apps via App Proxy
Hybrid apps via Kerberos/Cloud Trust

 [m365corner.com]

🎯 9. Summary (Simple)
Entra ID is:

The cloud identity king
The center of Microsoft’s Zero Trust
The successor to Azure AD
The identity provider for Microsoft 365, Azure, SaaS apps
The bridge between AD and cloud
The future of enterprise authentication
