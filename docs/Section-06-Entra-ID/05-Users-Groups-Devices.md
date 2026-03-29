📘 05 — Users, Groups & Devices in Entra ID
A simple → deep, Mahabharata‑inspired guide to core identity objects in Microsoft Entra ID (Azure AD).

🏹 **Mahabharata Analogy —
“Understanding Warriors, Armies, and Their Chariots.”**
In the Mahabharata:

Warriors = individual identities
Armies/divisions = groups
Chariots & divine vehicles = devices

Each warrior needed:

A personal identity (name, lineage, role)
Membership inside a division or sena (Yoddha, Maharathi, Atirathi)
A trusted chariot/weapon to fight

The Pandavas meticulously managed:

Who is a warrior?
Which sena they belong to?
Which vehicle they use?
Who controls which division?

This is exactly how Microsoft Entra ID organizes its identity ecosystem:

Users = Warriors
Groups = Armies
Devices = Chariots

Understanding these three object types is critical before learning Conditional Access, Zero Trust, or Access Governance.

🔐 1. What Are Identity Objects in Entra ID? (Simple Definition)
Microsoft Entra ID is a cloud-based directory that manages users, groups, devices, apps, and roles.
 [learn.microsoft.com]
The objects covered in this chapter:
✔ Users — human or service identities
✔ Groups — collective identity containers
✔ Devices — machines with identity (AADJ / Hybrid / Registered)
These objects form the core building blocks of authentication, authorization, and device-based access policies.

🧭 2. USERS — “The Warriors of the Identity Kingdom”
Users represent human or workload identities in the directory.
Microsoft Entra documentation defines Users as directory objects representing people or services that authenticate through Entra ID.
 [learn.microsoft.com]
✔ Types of Users





















User TypeDescriptionMember UsersEmployees inside the organizationGuest Users (B2B)External partners invited via B2BService AccountsNon-human identities (automation, scripts)

✔ Key Properties of a User

UPN (User Principal Name)
Immutable ID
Authentication methods
Assigned licenses
Group memberships
Role assignments
Device associations
Sign-in logs


✔ User Lifecycle in Modern Identity

Provision (HR, SCIM, sync, or manual)
Activate (assign licenses, MFA setup)
Operate (SSO, apps, devices)
Govern (reviews, PIM, access control)
Offboard (block sign-in, delete, remove groups)


🛡 3. GROUPS — “The Armies & War Divisions”
Groups allow Entra ID admins to manage access at scale.
Microsoft Entra documentation highlights security groups and Microsoft 365 groups as primary grouping mechanisms for identity/permission management.
 [learn.microsoft.com]
✔ Types of Groups

























Group TypeUsed ForSecurity GroupsApp access, RBAC, Conditional AccessMicrosoft 365 GroupsCollaboration (Teams, SharePoint)Dynamic GroupsAuto-membership based on rulesDistribution ListsEmail-based communication

✔ Dynamic Group Examples

All devices with OS = Windows 11
All users with JobTitle = Manager
All devices marked as compliant

Dynamic groups reduce manual burden through rules.

✔ Why Groups Matter
Groups control:

App access
Permissions
Licensing
Conditional Access targeting
Privileged identity boundaries


🖥 4. DEVICES — “The Chariots & Divine Vehicles”
Devices represent hardware trusted by Entra ID.
Microsoft Entra ID documentation describes Device identity and Join types (Azure AD Join, Hybrid Join, Registered) as a core part of securing user/device access.
 [learn.microsoft.com]
✔ Types of Device Identities





















Device TypePurposeAzure AD JoinedOrg-owned cloud-first devicesHybrid AAD JoinedOn-prem AD + Entra ID syncedAzure AD RegisteredPersonal/BYOD devices

✔ Device Identity Enables:

SSO
MFA strengthening
Conditional Access
Device compliance
Intune MDM/MAM
Passwordless authentication
Cloud Kerberos Trust
Zero Trust device-based access controls


🕸 5. Users, Groups, Devices — Relationship Diagram
flowchart TDUser[User Identity<br/>Member / Guest] --> Groups[Groups<br/>Security / M365 / Dynamic]User --> Devices[Devices<br/>AADJ / Hybrid / Registered]Groups --> Apps[Applications & Resources]Devices --> Access[Conditional Access & Compliance]Access --> AppsShow more lines#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .error-icon {fill:rgb(85, 34, 34)}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-thickness-normal {stroke-width:1px}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-thickness-thick {stroke-width:3.5px}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-pattern-solid {stroke-dasharray:0}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .cluster-label span p {background-color:transparent}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .label text, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node rect, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node circle, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node ellipse, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node polygon, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .rough-node .label text, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node .label text, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .image-shape .label, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .icon-shape .label {text-anchor:middle}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .rough-node .label, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node .label, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .image-shape .label, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .icon-shape .label {text-align:center}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node.clickable {cursor:pointer}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .cluster text {fill:rgb(51, 51, 51)}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .cluster span {color:rgb(51, 51, 51)}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d rect.text {fill:nonestroke-width:0;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .icon-shape, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .icon-shape p, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .icon-shape rect, #mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .error-icon{fill:#552222;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .error-text{fill:#552222;stroke:#552222;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-thickness-normal{stroke-width:1px;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-thickness-thick{stroke-width:3.5px;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-pattern-solid{stroke-dasharray:0;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .marker{fill:#333333;stroke:#333333;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .marker.cross{stroke:#333333;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d p{margin:0;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .cluster-label text{fill:#333;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .cluster-label span{color:#333;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .cluster-label span p{background-color:transparent;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .label text,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d span{fill:#333;color:#333;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node rect,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node circle,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node ellipse,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node polygon,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .rough-node .label text,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node .label text,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .image-shape .label,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .icon-shape .label{text-anchor:middle;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .rough-node .label,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node .label,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .image-shape .label,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .icon-shape .label{text-align:center;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node.clickable{cursor:pointer;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .arrowheadPath{fill:#333333;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .flowchart-link{stroke:#333333;fill:none;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .cluster text{fill:#333;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .cluster span{color:#333;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d rect.text{fill:none;stroke-width:0;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .icon-shape,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .icon-shape p,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .icon-shape rect,#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-c6c59d23-3f2d-431d-87c9-aa98886f5c2d :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}User IdentityMember / GuestGroupsSecurity / M365 / DynamicDevicesAADJ / Hybrid / RegisteredApplications & ResourcesConditional Access &Compliance

🔐 6. Entra ID Roles — “The Royal Titles & Permissions”
Microsoft Entra ID uses Role-Based Access Control (RBAC) to assign least-privilege administrator permissions.
 [learn.microsoft.com]
✔ Important Roles

Global Administrator
Security Administrator
Conditional Access Administrator
User Administrator
Privileged Role Administrator
Application Administrator

✔ Use PIM for all roles
PIM (Privileged Identity Management) adds:

Just-in-time elevation
Approval workflows
Risk-based activation
 [community....eworks.com]


🔐 7. Identity + Device + Group = Access (Zero Trust Formula)
Microsoft Learn confirms Conditional Access evaluates user, device, and risk signals.
 [learn.microsoft.com]
Zero Trust Access Equation:
Access = User Identity
        + Device Identity
        + Group Membership
        + App Sensitivity
        + Real-Time Risk

Example decision:

“Allow access ONLY IF
the user is trusted AND
the device is compliant AND
the app is approved AND
risk is low.”


🧬 8. Best Practices for Managing Users, Groups & Devices
✔ Users

Enforce MFA
Enable Identity Protection
Use passwordless authentication
Assign least-privilege roles
Remove dormant accounts

✔ Groups

Prefer security groups over individual assignments
Use dynamic groups wherever possible
Restrict permission inheritance
Review group membership regularly

✔ Devices

Require compliant devices via Conditional Access
Prefer Azure AD Join for cloud-first
Deploy Intune for MDM/MAM
Enforce Secure Boot, BitLocker
Block legacy, unmanaged devices


🧵 9. Mind Map
Users-Groups-Devices
 ├─ Users
 │   ├─ Member
 │   ├─ Guest
 │   ├─ Service Accounts
 ├─ Groups
 │   ├─ Security Groups
 │   ├─ M365 Groups
 │   ├─ Dynamic Groups
 ├─ Devices
 │   ├─ Azure AD Joined
 │   ├─ Hybrid AAD Joined
 │   ├─ Registered (BYOD)
 ├─ RBAC Roles
 └─ Zero Trust (User + Device + Risk)


🎯 Summary
Microsoft Entra ID organizes identity using three core object types:
✔ Users → the warriors
✔ Groups → the armories/divisions
✔ Devices → the warrior’s chariots
These identities interact to enforce:

Authentication
Authorization
Conditional Access
Zero Trust security
Device compliance
Application access
Governance

Understanding these objects is essential before learning:
06 — App Registration & Enterprise Applications
