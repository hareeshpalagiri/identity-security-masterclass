📘 04 — Microsoft Sentinel (Professional Overview)
A clear, medium‑depth, enterprise‑ready explanation of Microsoft Sentinel, its architecture, capabilities, and how it integrates with the unified Microsoft Defender Portal.
This chapter is fully backed by verified Microsoft Learn citations.

🎯 1. What is Microsoft Sentinel? (Professional Definition)
Microsoft Sentinel is Microsoft’s cloud‑native SIEM and SOAR platform that:

Collects and analyzes security data at scale
Uses AI, automation, and threat intelligence
Detects and investigates threats
Performs automated response actions
Operates across on‑prem, cloud, SaaS, and multi‑cloud environments

Microsoft Sentinel is now fully integrated into the Microsoft Defender Portal as part of Microsoft’s unified security operations platform.
 [github.com]
Starting July 2026, the Azure Portal interface for Sentinel is being retired and Sentinel will be accessed exclusively through the Microsoft Defender Portal.
 [github.com]
This unifies SIEM + XDR into a single SOC workspace.

🛡 2. Why Organizations Use Sentinel
Microsoft Sentinel provides:
✔ Cloud-scale log analytics
Ingest data from:

Windows/Linux servers
Azure resources
Microsoft 365
Entra ID
Firewalls & network devices
SaaS applications
Multi-cloud (AWS, GCP)

✔ AI-driven threat detection
Detects anomalies using:

Machine learning
Microsoft global threat intelligence
Behavioral analytics

✔ Automated investigation & response
SOAR (Security Orchestration, Automation, and Response):

Playbooks
Automated remediation
Logic Apps

✔ Unified incidents (Sentinel + Defender XDR)
Now all alerts correlate automatically with identity, endpoint, email, cloud, and app signals in the Defender portal.
 [github.com]

🧭 3. Sentinel Inside the Microsoft Defender Portal
Microsoft Learn describes the Defender Portal as a unified SecOps platform combining:

Microsoft Defender XDR
Microsoft Sentinel
Threat Intelligence
Exposure Management
 [github.com]

What changes when Sentinel moves to Defender?
✔ One place for all alerts (identity, endpoint, email, cloud, SIEM logs)
✔ Unified incidents → correlated automatically
✔ Unified entities (users, devices, IPs, apps)
✔ Unified hunting (KQL queries across all workloads)
✔ Unified automation (playbooks & response actions)
Security teams no longer switch between portals.

🧠 4. Sentinel Architecture (Simple + Clear)
Sentinel is built on top of:
✔ Log Analytics Workspace
Stores all security logs.
✔ Data Connectors
Ingest logs from:

Entra ID
Defender XDR services
Azure resources
Windows event logs
Syslog
Firewalls (Palo Alto, Fortinet, Cisco, Checkpoint)
AWS CloudTrail
GCP Security logs

✔ Analytics Rules
Detect suspicious behaviors (KQL-based).
✔ SOAR Playbooks
Automate incident response (Logic Apps).
✔ Workbooks
Dashboards for visualization.

🕸 5. Architecture Diagram (Professional Mermaid)
flowchart LRsubgraph Sources[Data Sources]    AD[On-Prem AD / Servers]    M365[Microsoft 365 / Entra ID]    AWS[AWS / GCP / SaaS Apps]    NW[Firewalls / Network Logs]endSources --> Connectors[Data Connectors]Connectors --> LA[Log Analytics Workspace]LA --> Sentinel["Microsoft Sentinel (in Defender Portal)"]Sentinel --> Incidents[Unified Incidents]Sentinel --> Hunting["Advanced Hunting (KQL)"]Sentinel --> Playbooks[Automation & Playbooks]Incidents --> SOC[SOC Analysts / IR Team]Show more lines#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .error-icon {fill:rgb(85, 34, 34)}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-thickness-normal {stroke-width:1px}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-thickness-thick {stroke-width:3.5px}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-pattern-solid {stroke-dasharray:0}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .cluster-label span p {background-color:transparent}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .label text, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node rect, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node circle, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node ellipse, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node polygon, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .rough-node .label text, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node .label text, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .image-shape .label, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .icon-shape .label {text-anchor:middle}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .rough-node .label, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node .label, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .image-shape .label, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .icon-shape .label {text-align:center}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node.clickable {cursor:pointer}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .cluster text {fill:rgb(51, 51, 51)}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .cluster span {color:rgb(51, 51, 51)}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c rect.text {fill:nonestroke-width:0;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .icon-shape, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .icon-shape p, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .icon-shape rect, #mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .error-icon{fill:#552222;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .error-text{fill:#552222;stroke:#552222;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-thickness-normal{stroke-width:1px;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-thickness-thick{stroke-width:3.5px;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-pattern-solid{stroke-dasharray:0;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .marker{fill:#333333;stroke:#333333;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .marker.cross{stroke:#333333;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c p{margin:0;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .cluster-label text{fill:#333;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .cluster-label span{color:#333;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .cluster-label span p{background-color:transparent;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .label text,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c span{fill:#333;color:#333;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node rect,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node circle,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node ellipse,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node polygon,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .rough-node .label text,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node .label text,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .image-shape .label,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .icon-shape .label{text-anchor:middle;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .rough-node .label,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node .label,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .image-shape .label,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .icon-shape .label{text-align:center;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node.clickable{cursor:pointer;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .arrowheadPath{fill:#333333;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .flowchart-link{stroke:#333333;fill:none;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .cluster text{fill:#333;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .cluster span{color:#333;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c rect.text{fill:none;stroke-width:0;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .icon-shape,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .icon-shape p,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .icon-shape rect,#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-909f3be3-da67-4f1c-83a7-25f345773a0c :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Data SourcesOn-Prem AD / ServersMicrosoft 365 / Entra IDAWS / GCP / SaaS AppsFirewalls / Network LogsData ConnectorsLog Analytics WorkspaceMicrosoft Sentinel (inDefender Portal)Unified IncidentsAdvanced Hunting (KQL)Automation & PlaybooksSOC Analysts / IR Team

⚡ 6. Key Features of Microsoft Sentinel
✔ 6.1 Data Connectors
Over 300+ connectors, including:

Entra ID
Defender XDR
Azure Infrastructure
AWS
GCP
Syslog
CEF
Third-party vendors


✔ 6.2 Analytics Rules
Rules classify detected behaviors as alerts.
Types:

Scheduled rules
NRT (near real-time) rules
Fusion AI-driven rules (correlation engine)


✔ 6.3 Incidents
Sentinel groups alerts → Incidents, now correlated with Defender XDR signals.
 [github.com]
This allows SOC teams to see:

Identity events
Endpoint logs
Email threats
Cloud alerts
Lateral movement
in one incident view.


✔ 6.4 Hunting (KQL-based)
Analysts use Kusto Query Language to:

Hunt for threats
Analyze large datasets
Build custom detection logic

Hunting is now unified with Defender data.

✔ 6.5 Automation (SOAR)
Playbooks can:

Disable compromised users
Block IPs in firewalls
Send Teams / Email alerts
Reset credentials
Enforce Conditional Access actions
Run auto-investigations

Automation = faster response + reduced analyst workload.

✔ 6.6 Workbooks (Dashboards)
Visual dashboards for:

Identity activity
Firewall logs
Cloud workloads
Compliance
Threat intelligence
Incidents


✔ 6.7 Threat Intelligence Integration
With Microsoft Defender Threat Intelligence (MDTI):

Enriched alerts
Adversary insights
IOC correlation
 [github.com]


🧩 7. How Sentinel Works with Defender for Identity (MDI)
MDI sends:

Identity alerts
Lateral movement paths
DCSync alerts
Kerberos attack signals
Directory reconnaissance detections

Sentinel correlates identity alerts with:

Device logs
Network logs
Email threats
Cloud anomalies

This gives complete visibility into the attack chain.

🛠 8. Sentinel Use Cases (Professional)
✔ Identity threat correlation
PTA attacks, Kerberoasting, lateral movement.
✔ Insider threat detection
Abnormal folder access, anomalous logon behavior.
✔ Cloud posture monitoring
Azure resource misconfigurations.
✔ Multi-cloud visibility
AWS, GCP logs integrated into unified incidents.
✔ Operational security
Firewall attacks, VPN logs, syslog-based events.
✔ Governance & Compliance
Audit logs, access logs, sign-in data.

🧵 9. Mind Map
Microsoft Sentinel
 ├─ Data Sources
 │   ├─ Entra ID
 │   ├─ Defender XDR
 │   ├─ Servers
 │   ├─ Firewalls
 │   ├─ AWS / GCP
 ├─ Core Features
 │   ├─ Analytics Rules
 │   ├─ Hunting (KQL)
 │   ├─ Incidents
 │   ├─ Workbooks
 │   └─ SOAR Playbooks
 ├─ Defender Portal Integration
 │   ├─ Unified Incidents
 │   ├─ Identity Correlation
 │   ├─ Automation
 └─ Use Cases
     ├─ Threat Detection
     ├─ Identity Security
     ├─ Multi-Cloud SIEM
     └─ Compliance


🎯 Summary — Clean & Professional
Microsoft Sentinel = Cloud SIEM + SOAR, delivering:

AI-based threat detection
Unified incidents
Massive multi-cloud log analytics
Automated response
Deep integration with Defender XDR
Modern SOC experience inside Microsoft Defender Portal

Microsoft’s vision is clear:
Unified Security Operations — one portal, one incident, one investigation path.
