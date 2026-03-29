📘 02 — Entra ID Architecture & Topology


🏹 **Mahabharata Analogy —
“Understanding the Kingdom’s Map Before Entering the Great War.”**
In the Mahabharata:

Hastinapura was the central kingdom
Around it were sub‑kingdoms, tribes, provinces, border states
Each region had:

unique leaders (roles),
local administrative groups,
shared alliances,
governed temples and armies.



But all regions obeyed one central royal authority,
and all warriors needed this map to understand the hierarchy of power.
Entra ID has a similar map.
Users, groups, apps, tenants, directories, roles, and resources all form a hierarchical topology.
Understanding this “kingdom map” is essential before learning authentication, devices, hybrid identity, and Conditional Access.

🔐 1. What Is Microsoft Entra ID? (Cloud Directory Architecture)
Microsoft Entra ID is Microsoft’s cloud‑based directory and identity management service that:

Stores identities
Controls authentication
Manages access to cloud/on‑prem apps
Secures users, groups, devices, apps, workloads
Acts as the foundation of Microsoft’s identity product family
 [acefekay.w...dpress.com]

Every Microsoft 365 or Azure tenant automatically includes an Entra ID directory.
 [github.com]
It replaces traditional AD domain controllers with a fully cloud‑managed identity platform.

🧭 2. The Three-Layer Architecture of Entra ID (High Level)
Here is the simplest way to understand Entra ID:
Tenant  →  Directory  →  Objects (Users, Groups, Apps, Devices, Service Principals)

Microsoft Learn describes this as a multitenant, cloud-based directory that stores and manages identity objects.
 [acefekay.w...dpress.com]
Let’s break it down.

🏰 3. Tenants — “The Kingdom”
A tenant is your entire cloud identity boundary.

Each tenant represents an organization
Created automatically when you sign up for Microsoft 365, Azure, or Entra products
Has a unique global ID
All identities and resources inside belong to this tenant


In Mahabharata terms:
The tenant = Hastinapura (the kingdom).

Every tenant begins with a default domain like:
contoso.onmicrosoft.com

 [github.com]
Admins can add custom domains (example.com).

🗂️ 4. Directory — “The Royal Ledger”
The directory inside a tenant contains:

Users
Groups
Service Principals
Devices
Enterprise apps
Application registrations
Roles & permissions

Entra ID is described by Microsoft as combining core directory services, app access management, and identity protection into one identity store.
 [acefekay.w...dpress.com]

👥 5. Identity Objects — “The Citizens of the Kingdom”
The directory contains several object types.
✔ Users
Human users — employees, admins, guests.
 [acefekay.w...dpress.com]
✔ Groups
Security groups, M365 groups, dynamic groups.
 [windows-ac...ectory.com]
✔ Devices
Azure AD Joined, Hybrid Joined, Registered.
 [acefekay.w...dpress.com]
✔ Service Principals
Identity for an application or service.
 [acefekay.w...dpress.com]
✔ Applications
Entra ID supports:

App registrations
Enterprise apps
SSO
API access
 [acefekay.w...dpress.com]

✔ Roles & Administrators
Role-Based Access Control (RBAC) defines admin permissions.
 [acefekay.w...dpress.com]

🕸 6. Entra ID Architecture Diagram (Mermaid)
flowchart TDTenant[Microsoft Entra Tenant<br/>contoso.onmicrosoft.com] --> Directory[Directory]Directory --> Users[Users]Directory --> Groups[Groups]Directory --> Devices[Devices]Directory --> Apps[Applications & Service Principals]Directory --> Roles[Admin Roles & RBAC]Apps --> CloudApps[SaaS Apps / M365 / Azure Resources]Show more lines#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .error-icon {fill:rgb(85, 34, 34)}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-thickness-normal {stroke-width:1px}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-thickness-thick {stroke-width:3.5px}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-pattern-solid {stroke-dasharray:0}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .cluster-label span p {background-color:transparent}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .label text, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node rect, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node circle, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node ellipse, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node polygon, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .rough-node .label text, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node .label text, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .image-shape .label, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .icon-shape .label {text-anchor:middle}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .rough-node .label, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node .label, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .image-shape .label, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .icon-shape .label {text-align:center}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node.clickable {cursor:pointer}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .cluster text {fill:rgb(51, 51, 51)}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .cluster span {color:rgb(51, 51, 51)}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af rect.text {fill:nonestroke-width:0;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .icon-shape, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .icon-shape p, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .icon-shape rect, #mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .error-icon{fill:#552222;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .error-text{fill:#552222;stroke:#552222;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-thickness-normal{stroke-width:1px;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-thickness-thick{stroke-width:3.5px;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-pattern-solid{stroke-dasharray:0;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .marker{fill:#333333;stroke:#333333;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .marker.cross{stroke:#333333;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af p{margin:0;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .cluster-label text{fill:#333;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .cluster-label span{color:#333;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .cluster-label span p{background-color:transparent;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .label text,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af span{fill:#333;color:#333;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node rect,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node circle,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node ellipse,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node polygon,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .rough-node .label text,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node .label text,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .image-shape .label,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .icon-shape .label{text-anchor:middle;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .rough-node .label,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node .label,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .image-shape .label,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .icon-shape .label{text-align:center;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node.clickable{cursor:pointer;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .arrowheadPath{fill:#333333;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .flowchart-link{stroke:#333333;fill:none;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .cluster text{fill:#333;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .cluster span{color:#333;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af rect.text{fill:none;stroke-width:0;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .icon-shape,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .icon-shape p,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .icon-shape rect,#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-bbc2f4d2-487b-4e26-b44c-b2983686d1af :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Microsoft Entra Tenantcontoso.onmicrosoft.comDirectoryUsersGroupsDevicesApplications & ServicePrincipalsAdmin Roles & RBACSaaS Apps / M365 / AzureResources

🔑 7. Identity Access Flow (How Objects Interact)
When a user signs into an application:

User authenticates
Entra ID validates credentials (passwordless, MFA, risk-based)
Directory checks:

Group memberships
Device compliance
Conditional Access
Risk signals
 [acefekay.w...dpress.com]


Entra ID issues tokens (OAuth/OIDC/SAML)
 [github.com]
App verifies token
Access granted

This unified identity engine is core to Zero Trust.
 [github.com]

🔐 8. Topology Building Blocks

⭐ 8.1 Tenants (Org-level boundary)

One company = one tenant
Multi-tenant organizations share identity across tenants
 [acefekay.w...dpress.com]


⭐ 8.2 Directories (Identity storage)
Each tenant has one directory storing identity objects.

⭐ 8.3 Entra ID Domain Services (AAD DS)
For legacy apps that require:

Kerberos
NTLM
LDAP
Group Policy

Managed domain services provided in the cloud.
 [github.com]

🌍 9. Multi-Tenant Identity in Entra
Entra ID supports:

Cross-tenant collaboration
Guest access (B2B)
External identities
Multi-tenant cloud apps
 [acefekay.w...dpress.com]

This allows apps to trust identities across tenants — crucial for SaaS environments.

🛡 10. Security Built Into Topology
Microsoft Entra ID includes built-in protections at every layer:
✔ MFA
✔ Conditional Access
✔ Identity Protection
✔ RBAC for admin roles
✔ Device compliance
✔ App governance
 [acefekay.w...dpress.com], [github.com]
These controls form Microsoft’s Zero Trust identity foundation.
 [github.com]

🧵 11. Mind Map
Entra ID Architecture
 ├─ Tenant (Identity Boundary)
 ├─ Directory (Object Store)
 │   ├─ Users
 │   ├─ Groups
 │   ├─ Devices
 │   ├─ Apps & Service Principals
 │   ├─ Roles
 ├─ Domain Services (AAD DS)
 ├─ Multi-Tenant Access
 └─ Security Controls
     ├─ Conditional Access
     ├─ MFA
     ├─ Identity Protection
     └─ RBAC


🎯 Summary
Entra ID consists of:

Tenants (kingdoms)
Directories (ledger of identities)
Objects (users, groups, devices, apps)
Roles (administrators)
Hybrid + cloud identity integrations
Security controls enforcing Zero Trust

This chapter gives the foundational map you need before learning:

Application management (next chapter)
Hybrid identity
Conditional Access
Entra ID governance
Migration strategies
