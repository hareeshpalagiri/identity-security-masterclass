📘 06.03 — Device Identity & Join Models (Azure AD / Entra ID Devices)


🏹 **Mahabharata Analogy —
“Every warrior needed a recognized mark before entering the war camp.”**
In the Mahabharata:

Warriors carried royal marks, weapons, or divine identifiers that proved loyalty
The Pandava camp would verify the warrior’s identity AND their equipment before entry
A warrior with:

unknown weapon → questioned
no royal mark → denied
forged symbol → treated as an enemy



This is Device Identity in Entra ID:

Your device must present a trusted identity before accessing apps, data, or cloud resources.
Not just “who you are,” but “who your device is” also matters.

Modern Zero Trust:
“Never trust a device blindly — always verify it.”
 [acefekay.w...dpress.com]

🔐 1. What Is Device Identity? (Simple Definition)
Device identity is the unique, cloud‑trusted identity assigned to a device by Microsoft Entra ID, enabling:

Authentication
Conditional Access policies
Compliance checks
SSO (Single Sign-On)
Passwordless sign‑in
Zero Trust enforcement

Entra ID supports different device join states, each representing an identity model.
 [acefekay.w...dpress.com]

🌐 2. Why Device Identity Exists (Hastinapura Logic)

























Battlefield LogicModern Identity LogicWarrior identity alone was not enoughUser identity alone is not enoughWeapon authenticity verifiedDevice authenticity verifiedWrong warrior with right badge = dangerCompromised device with valid password = breachRules applied based on warrior + weaponConditional Access applies: user + device
This reflects Microsoft’s Zero Trust:
device trust + user trust + session trust.
 [acefekay.w...dpress.com]

🧠 3. The Three Device Join Types in Entra ID (Simple → Deep)
Microsoft Entra documentation defines multiple device identity models including Azure AD Join, Hybrid Join, and device registration.
 [acefekay.w...dpress.com]

⭐ 3.1 Azure AD Join (Cloud‑Only Devices)
Used for:

Cloud‑first organizations
Intune-managed devices
Windows 10/11 in cloud‑native environments

Identity: Device is joined directly to Entra ID.
Benefits:

True cloud SSO
Works with MFA, CA, compliance
Passwordless sign-in
Deep integration with Intune

Typical scenario:
Modern laptops enrolled from home/office → no AD domain required.

⭐ 3.2 Hybrid Azure AD Join (Domain + Cloud)
Used for:

Environments with on‑prem AD + Entra ID
Want to use modern authentication while preserving AD
Require GPO-based management

Identity: Device is domain‑joined (on-prem AD) AND registered in Entra ID.
Benefits:

Supports legacy on-prem apps
Enables Conditional Access + SSO in cloud
Bridge between AD and cloud

Typical scenario:
Enterprise laptops managed by AD/GPO but also accessing cloud apps.

⭐ 3.3 Azure AD Registered (Personal Devices)
Used for:

BYOD (Bring Your Own Device)
Mobile phones
Personal laptops

Identity:
Device is registered, not joined.
User signs in with Entra ID account inside apps (Work Account → Account > Access Work or School).
Benefits:

App-level SSO
Conditional Access (limited)
Suitable for contractors/partners

BUT:
Cannot apply organizational device policies like full Intune compliance or domain policies.

⭐ NEW MODEL: Cloud Kerberos Trust (Windows 11 / Entra)**
Microsoft added a new join model for hybrid authentication:

Authenticate to domain resources using Entra ID credentials without ADFS or certificate-based trust.

This is part of Entra’s device identity and hybrid access strategy.
 [acefekay.w...dpress.com]
Why it matters:

No ADFS needed
No certificate trust needed
Simpler Hybrid Join model
Supports Windows Hello for Business
Kerberos tickets issued using cloud auth

This simplifies hybrid identity dramatically.

🕸 4. Device Join Models — Diagram
flowchart TDUser[User] --> Device[Device Identity]subgraph EntraID[Microsoft Entra ID]    AADJ[Azure AD Join]    HYBRID[Hybrid Azure AD Join]    REG[Azure AD Registered]endDevice --> AADJDevice --> HYBRIDDevice --> REGAADJ --> CloudApps[Cloud Apps & SSO]HYBRID --> CloudAppsHYBRID --> OnPremApps[On-Prem AD Apps]REG --> LimitedAccess[Limited Access / BYOD]Show more lines#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .error-icon {fill:rgb(85, 34, 34)}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-thickness-normal {stroke-width:1px}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-thickness-thick {stroke-width:3.5px}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-pattern-solid {stroke-dasharray:0}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .cluster-label span p {background-color:transparent}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .label text, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node rect, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node circle, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node ellipse, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node polygon, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .rough-node .label text, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node .label text, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .image-shape .label, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .icon-shape .label {text-anchor:middle}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .rough-node .label, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node .label, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .image-shape .label, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .icon-shape .label {text-align:center}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node.clickable {cursor:pointer}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .cluster text {fill:rgb(51, 51, 51)}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .cluster span {color:rgb(51, 51, 51)}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d rect.text {fill:nonestroke-width:0;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .icon-shape, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .icon-shape p, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .icon-shape rect, #mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .error-icon{fill:#552222;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .error-text{fill:#552222;stroke:#552222;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-thickness-normal{stroke-width:1px;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-thickness-thick{stroke-width:3.5px;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-pattern-solid{stroke-dasharray:0;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .marker{fill:#333333;stroke:#333333;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .marker.cross{stroke:#333333;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d p{margin:0;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .cluster-label text{fill:#333;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .cluster-label span{color:#333;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .cluster-label span p{background-color:transparent;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .label text,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d span{fill:#333;color:#333;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node rect,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node circle,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node ellipse,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node polygon,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .rough-node .label text,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node .label text,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .image-shape .label,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .icon-shape .label{text-anchor:middle;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .rough-node .label,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node .label,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .image-shape .label,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .icon-shape .label{text-align:center;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node.clickable{cursor:pointer;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .arrowheadPath{fill:#333333;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .flowchart-link{stroke:#333333;fill:none;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .cluster text{fill:#333;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .cluster span{color:#333;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d rect.text{fill:none;stroke-width:0;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .icon-shape,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .icon-shape p,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .icon-shape rect,#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-4d8b8c29-eb65-4bc7-a4ca-aae47f47332d :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Microsoft Entra IDUserDevice IdentityAzure AD JoinHybrid Azure AD JoinAzure AD RegisteredCloud Apps & SSOOn-Prem AD AppsLimited Access / BYOD

🧭 5. Comparing Join Models (Simple Table)





























Join TypeOwnershipBest ForTrust LevelAzure AD JoinOrganizationCloud-first devicesHighestHybrid JoinOrganizationMixed AD + CloudVery HighAzure AD RegisteredUser (BYOD)Personal devicesMedium

🔧 6. How Identity Works in Each Join Type

✔ Azure AD Join

Device joins Entra ID
Device gets Primary Refresh Token (PRT)
Enables seamless SSO to cloud apps
Conditional Access checks:

Device compliance
Risk
User context




✔ Hybrid Join

Device joins Active Directory
Syncs to Entra ID via:

Azure AD Connect
Or Cloud Sync


Gains cloud identity (Device object in Entra ID)
Supports:

SSO to cloud
Kerberos for on-prem
Conditional Access




✔ Azure AD Registered

User signs in to app/work account
Device registers key in Entra ID
Provides:

SSO inside apps
Basic Conditional Access


Not suitable for privileged users or admins


🔥 7. Which Join Model Should You Use? (Recommended Strategy)

























ScenarioUse ModelCloud-first, IntuneAzure AD JoinLegacy on-prem apps + cloudHybrid JoinBYOD, mobile, contractorsAzure AD RegisteredPasswordless + Hybrid + SSOAzure AD Join OR Hybrid Join with Cloud Kerberos Trust

🛡 8. Security Considerations (Zero Trust)
Device identity is central to Conditional Access policies in Entra ID.
 [acefekay.w...dpress.com]
Enforce:

MFA + compliant device
Block access from unmanaged devices
Device risk policies
Passwordless authentication
Least privilege on admin accounts (PAWs should be AADJ or Hybrid Joined)


🧵 Mind Map
Device Identity
 ├─ Azure AD Join
 ├─ Hybrid Azure AD Join
 ├─ Azure AD Registered
 ├─ Cloud Kerberos Trust
 ├─ Primary Refresh Token
 ├─ Conditional Access
 ├─ Compliance
 └─ Zero Trust Access


🎯 Summary

Device identity is central in Entra ID & Zero Trust.
Three join models: Azure AD Join, Hybrid Join, Azure AD Registered.
Cloud Kerberos Trust simplifies hybrid authentication.
Modern SSO relies on device trust (PRT).
Entra ID uses device identity to enforce Conditional Access policies.
