📘 CHAPTER 05 — DNS & DHCP in Active Directory (Complete Masterclass Edition)
(Fully rewritten + complete + includes enterprise examples and multi‑site design)

🏛 1. Why DNS & DHCP Matter in Active Directory
Microsoft states that:

Active Directory Domain Services rely entirely on DNS for DC locator, authentication, replication, and service discovery. [github.com]

DHCP provides the network identity (IP, DNS settings, gateway) that clients need to:

join the domain
locate Domain Controllers
authenticate using Kerberos
apply Group Policies
access enterprise resources

DNS + DHCP = foundation of identity + networking.

🌐 2. DNS Fundamentals in AD (Clean & Complete)
AD uses DNS for:
✔ DC Locator
Clients find domain controllers using SRV records like:
_ldap._tcp.dc._msdcs.corp.local

✔ Kerberos Authentication
Kerberos requires DNS to find KDC servers.
✔ Replication
DCs use DNS to locate replication partners.
(Multi-site replication reference:) [github.com]
✔ Global Catalog Discovery
Uses:
_gc._tcp.corp.local

✔ Name Resolution
Every AD object is referenced by DNS name, not IP.

🧠 3. How DNS is Stored in AD (AD‑Integrated Zones)
DNS zones in AD are stored in:

DomainDNSZones partition
ForestDNSZones partition

Replicated using multi-master AD replication across sites.
 [github.com]
Advantages:

No need for secondary zones
Automatic replication
Secure updates
Supports multi-site


🔁 4. DNS Relay / Forwarding (What You Actually Meant by “DNS Replay”)
“DNS replay” is not a technical term.
The correct concept is DNS Relay / Forwarding.
DNS servers forward unknown queries to:

Upstream DNS
Conditional forwarders (other internal domains/forests)
Cloud resolvers

Forwarders are crucial in multi-forest / multi‑site setups.
 [github.com]
Types of Forwarders:

Standard forwarders
Conditional forwarders
Stub zones
Root hints


🏙 5. How DNS Works in Multi‑Site AD
Multi-site DNS must consider:

Site-to-site replication
Local DC preference
WAN latency
Failover behavior

Multi‑site planning discussed in DNS design guides.
 [github.com], [github.com]
✔ Behavior:

Clients always use local DNS servers first
SRV records are site-aware
Replication follows AD site link schedules
If local DNS fails → use DNS from another site
(as recommended in enterprise DNS setups) [github.com]


🕸 6. DNS Multi-Site Flow (Diagram)
flowchart TD    A[Client in Site A] --> B[Local DNS/DC]    B -->|Local zone data| C[Immediate Answer]    B -->|Not found| D[Conditional Forwarder]    D --> E[Remote Site DNS/DC]    E --> B    B --> AShow more lines#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .error-icon {fill:rgb(85, 34, 34)}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-thickness-normal {stroke-width:1px}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-thickness-thick {stroke-width:3.5px}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-pattern-solid {stroke-dasharray:0}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .cluster-label span p {background-color:transparent}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .label text, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node rect, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node circle, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node ellipse, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node polygon, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .rough-node .label text, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node .label text, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .image-shape .label, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .icon-shape .label {text-anchor:middle}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .rough-node .label, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node .label, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .image-shape .label, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .icon-shape .label {text-align:center}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node.clickable {cursor:pointer}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .cluster text {fill:rgb(51, 51, 51)}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .cluster span {color:rgb(51, 51, 51)}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d rect.text {fill:nonestroke-width:0;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .icon-shape, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .icon-shape p, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .icon-shape rect, #mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .error-icon{fill:#552222;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .error-text{fill:#552222;stroke:#552222;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-thickness-normal{stroke-width:1px;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-thickness-thick{stroke-width:3.5px;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-pattern-solid{stroke-dasharray:0;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .marker{fill:#333333;stroke:#333333;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .marker.cross{stroke:#333333;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d p{margin:0;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .cluster-label text{fill:#333;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .cluster-label span{color:#333;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .cluster-label span p{background-color:transparent;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .label text,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d span{fill:#333;color:#333;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node rect,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node circle,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node ellipse,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node polygon,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .rough-node .label text,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node .label text,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .image-shape .label,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .icon-shape .label{text-anchor:middle;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .rough-node .label,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node .label,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .image-shape .label,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .icon-shape .label{text-align:center;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node.clickable{cursor:pointer;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .arrowheadPath{fill:#333333;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .flowchart-link{stroke:#333333;fill:none;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .cluster text{fill:#333;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .cluster span{color:#333;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d rect.text{fill:none;stroke-width:0;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .icon-shape,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .icon-shape p,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .icon-shape rect,#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-52eb862d-5c6e-492d-86f1-9e96f2c2f13d :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Local zone dataNot foundClient in Site ALocal DNS/DCImmediate AnswerConditional ForwarderRemote Site DNS/DC

🚨 7. DHCP Fundamentals in AD
DHCP assigns:

IP address
Subnet mask
DNS servers
Domain name
Gateway

Clients MUST receive correct DNS servers (AD DNS),
NOT external DNS (breaks AD DS).

⚙️ 8. DHCP DORA: FULL Enterprise Explanation
D — Discover
Client sends broadcast to find DHCP server.
O — Offer
DHCP server proposes IP + options.
R — Request
Client asks for a specific offer.
A — Acknowledge
DHCP grants the lease.

📡 9. DHCP Relay (IP Helper) — Required in ALL Enterprises
DHCP broadcasts do not cross VLANs/subnets.
Network devices must forward DHCP packets:
Example (Cisco):
interface Vlan10
 ip helper-address 10.10.1.10

DHCP Relay is needed when:

Centralized DHCP
Multi-site DHCP
Remote offices
VLAN segmentation


🏢 **10. Enterprise Scenario
New Office Acquisition — Complete Workflow**
This section combines DNS + DHCP + AD Sites.
Company acquires new office in Chennai.
You must integrate this office into AD + network.

🔷 Step 1 — Define Network Subnets (Network Team)
Users      10.60.10.0/24  
Servers    10.60.20.0/24  
Wi-Fi      10.60.30.0/24  
Gateway    10.60.10.1  


🔷 Step 2 — Add Subnet to AD Sites
Using AD Sites & Services:
Site: Chennai-Office  
Subnet: 10.60.10.0/24 → Chennai-Office

This ensures site-aware DC locator.

🔷 Step 3 — Deploy Two Domain Controllers (with DNS)
CHN-DC01 → 10.60.10.11  
CHN-DC02 → 10.60.10.12  

DNS zones replicate via multi-master AD replication.
 [github.com]

🔷 Step 4 — DNS Configuration (Enterprise Best Practices)
Based on multi-site DNS recommendations.
 [github.com]
CHN-DC01 DNS settings:
Primary   : CHN-DC02  
Secondary : 127.0.0.1  
Tertiary  : Bangalore-DC01  

CHN-DC02 DNS settings:
Primary   : CHN-DC01  
Secondary : 127.0.0.1  

Clients get DNS from DHCP:
DNS1: 10.60.10.11  
DNS2: 10.60.10.12


🔷 Step 5 — Configure DHCP Relay
On core switch/router:
ip helper-address 10.10.1.10

DHCP server at HQ handles Chennai clients.

🔷 Step 6 — Create DHCP Scope for Chennai
Scope: 10.60.10.0/24  
Router: 10.60.10.1  
DNS:    10.60.10.11, 10.60.10.12  
Lease:  8 days  
Options: 003 Router, 006 DNS, 015 Domain Name


🔷 Step 7 — Validate End‑to‑End Behavior
Expected behavior:
✔ DHCP
Client receives IP, DNS, gateway.
✔ DNS
Client resolves:
_ldap._tcp.CHENNAI._sites.dc._msdcs.corp.local

(DC Locator)
 [github.com]
✔ Authentication
Local DC handles login.
✔ Replication
Changes flow from Chennai → Bangalore via AD Site Links.

🗺 11. Combined DNS + DHCP Workflow (Master Diagram)
flowchart TD    C[Client Joins Network] --> DORA[DHCP Relay / DORA Process]    DORA --> IP[IP + DNS Assigned]    IP --> DNS[DNS Query to Local DC]    DNS --> SRV[DC Locator SRV Lookup]    SRV --> AUTH[Local Authentication]    AUTH --> REPL[AD Replication Across Sites]Show more lines#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-thickness-normal {stroke-width:1px}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .cluster-label span p {background-color:transparent}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .label text, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node rect, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node circle, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node ellipse, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node polygon, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .rough-node .label text, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node .label text, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .image-shape .label, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .icon-shape .label {text-anchor:middle}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .rough-node .label, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node .label, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .image-shape .label, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .icon-shape .label {text-align:center}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node.clickable {cursor:pointer}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .cluster text {fill:rgb(51, 51, 51)}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .cluster span {color:rgb(51, 51, 51)}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 rect.text {fill:nonestroke-width:0;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .icon-shape, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .icon-shape p, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .icon-shape rect, #mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .error-icon{fill:#552222;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .error-text{fill:#552222;stroke:#552222;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-thickness-normal{stroke-width:1px;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .marker{fill:#333333;stroke:#333333;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .marker.cross{stroke:#333333;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 p{margin:0;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .cluster-label text{fill:#333;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .cluster-label span{color:#333;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .cluster-label span p{background-color:transparent;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .label text,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 span{fill:#333;color:#333;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node rect,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node circle,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node ellipse,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node polygon,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .rough-node .label text,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node .label text,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .image-shape .label,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .icon-shape .label{text-anchor:middle;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .rough-node .label,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node .label,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .image-shape .label,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .icon-shape .label{text-align:center;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node.clickable{cursor:pointer;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .arrowheadPath{fill:#333333;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .flowchart-link{stroke:#333333;fill:none;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .cluster text{fill:#333;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .cluster span{color:#333;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 rect.text{fill:none;stroke-width:0;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .icon-shape,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .icon-shape p,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .icon-shape rect,#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-0dd51b3c-e4b4-4b83-8f20-2945ff9e1082 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Client Joins NetworkDHCP Relay / DORA ProcessIP + DNS AssignedDNS Query to Local DCDC Locator SRV LookupLocal AuthenticationAD Replication Across Sites

🧵 12. Key Security Considerations
DNS

Secure dynamic updates
DNS scavenging
Reducing stale records
Conditional forwarders for partner forests

DHCP

DHCP snooping
IP source guard
Rogue DHCP detection

AD Multi-Site

Prefer local authentication
Avoid single-site DNS dependency
Validate replication

