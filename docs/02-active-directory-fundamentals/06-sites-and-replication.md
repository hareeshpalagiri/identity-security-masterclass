📘 Chapter 06 — Sites & Replication (Medium Depth, Enterprise Friendly)
How Active Directory replicates directory data efficiently across locations.

🏹 Mahabharata Strategic Story Opener —
“Different Camps, One Army”
In the Kurukshetra war, armies were spread across multiple camps:

Each camp had its own commanders & warriors
Camps were placed based on geography
Messages between camps traveled with different speeds
Leaders ensured information reached every camp accurately and consistently

This is exactly how Active Directory Sites & Replication work:

Each site = a geographic location
DCs inside a site communicate quickly
DCs across sites communicate slower
Replication ensures every site stays synchronized


🔵 1. What is an AD Site? (Simple Definition)
A Site in Active Directory represents:

A group of well-connected IP subnets.

Its purpose is to:

Help clients find the nearest DC
Optimize authentication
Control replication traffic
Improve performance across geographies

This definition is consistent with Microsoft Learn and AD site references.
 [windows-ac...ectory.com]

🟩 2. What Are Subnets? (Simple Explanation)
A Subnet tells AD which IP ranges belong to which site.
Example:
10.10.0.0/24  → Bangalore-Site  
10.20.0.0/24  → Mumbai-Site  

Clients use their IP address to determine their site.
This ensures authentication happens locally, not across WAN.

🟦 3. What is AD Replication? (Medium Depth)
Replication keeps all Domain Controllers synchronized with:

Users
Computers
Groups
Password changes
Group Policies

AD replication happens through connection objects created by the KCC (Knowledge Consistency Checker).
 [learn.microsoft.com]

🟠 4. Intra‑Site vs Inter‑Site Replication
Microsoft and enterprise sources highlight two replication modes:
 [petri.com]

4.1 Intra‑Site Replication (within same site)

Very fast
Low latency
Happens automatically every 15 seconds by default
No compression
Ideal for LAN

Analogy:
“Within the same camp, messengers communicate constantly.”

4.2 Inter‑Site Replication (between sites)

Slower
Controlled by schedules
Default: 180 minutes (3 hours)
Data is compressed to save WAN bandwidth
 [petri.com]

Analogy:
“Messages between distant camps take longer and are scheduled.”

🧩 5. What Are Site Links? (Basic Only)
A Site Link defines:

Which sites replicate with each other
The path replication follows
The schedule
The cost (priority)

Site links represent the network connection between locations.
 [dispersednet.com]

🔧 6. How Clients Choose the Nearest Domain Controller (DC Locator)
Clients query DNS SRV records such as:
_ldap._tcp.<site>._sites.dc._msdcs.domain.com

This ensures:

Users authenticate against local DCs
GPOs apply faster
WAN links aren’t overloaded

This behavior is documented in Microsoft’s DNS/AD DS guidance.
 [github.com]

📊 7. Simple Visual Diagram (Mermaid)
flowchart TD    A[Client Subnet: 10.10.0.0/24] --> B[Mapped to Bangalore Site]    A2[Client Subnet: 10.20.0.0/24] --> C[Mumbai Site]    B --> D[DC01 Bangalore]    C --> E[DC01 Mumbai]    D <-->|Intersite Replication| EShow more lines#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-thickness-normal {stroke-width:1px}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .cluster-label span p {background-color:transparent}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .label text, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node rect, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node circle, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node ellipse, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node polygon, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .rough-node .label text, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node .label text, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .image-shape .label, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .icon-shape .label {text-anchor:middle}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .rough-node .label, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node .label, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .image-shape .label, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .icon-shape .label {text-align:center}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node.clickable {cursor:pointer}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .cluster text {fill:rgb(51, 51, 51)}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .cluster span {color:rgb(51, 51, 51)}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 rect.text {fill:nonestroke-width:0;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .icon-shape, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .icon-shape p, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .icon-shape rect, #mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .error-icon{fill:#552222;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .error-text{fill:#552222;stroke:#552222;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-thickness-normal{stroke-width:1px;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .marker{fill:#333333;stroke:#333333;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .marker.cross{stroke:#333333;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 p{margin:0;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .cluster-label text{fill:#333;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .cluster-label span{color:#333;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .cluster-label span p{background-color:transparent;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .label text,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 span{fill:#333;color:#333;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node rect,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node circle,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node ellipse,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node polygon,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .rough-node .label text,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node .label text,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .image-shape .label,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .icon-shape .label{text-anchor:middle;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .rough-node .label,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node .label,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .image-shape .label,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .icon-shape .label{text-align:center;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node.clickable{cursor:pointer;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .arrowheadPath{fill:#333333;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .flowchart-link{stroke:#333333;fill:none;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .cluster text{fill:#333;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .cluster span{color:#333;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 rect.text{fill:none;stroke-width:0;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .icon-shape,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .icon-shape p,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .icon-shape rect,#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-c896bcd7-a4af-4f21-a0d5-727d1c3ae8d5 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Intersite ReplicationClient Subnet:10.10.0.0/24Mapped to Bangalore SiteClient Subnet:10.20.0.0/24Mumbai SiteDC01 BangaloreDC01 Mumbai

🏢 8. REAL Enterprise Scenario (Medium Depth)
Scenario:
Your company has 2 offices:

Bangalore (HQ)
Hyderabad (New Branch)

Step 1 — Network Team gives subnets
Bangalore: 10.10.0.0/24  
Hyderabad: 10.20.0.0/24

Step 2 — Create Sites in AD
Bangalore-Site  
Hyderabad-Site

Step 3 — Add subnets to sites
10.10.0.0/24 → Bangalore-Site  
10.20.0.0/24 → Hyderabad-Site  

Step 4 — Place DCs
BLR-DC01 → Bangalore-Site  
HYD-DC01 → Hyderabad-Site

Step 5 — Site Link
Default-Site-Link: Bangalore ↔ Hyderabad

Outcome:

Hyderabad clients authenticate locally to HYD-DC01
Replication between BLR‑DC01 and HYD‑DC01 happens every 3 hours
(Default inter-site schedule per AD replication defaults)
 [petri.com]
WAN traffic is optimized
GPOs apply quickly
Authentication is fast


🛡 9. Key Benefits of Sites & Replication
🚀 Performance
Local authentication is much faster.
📉 Reduced WAN load
Inter-site replication is scheduled + compressed.
🧭 Accurate DC selection
Clients always find the nearest DC.
🔐 Better security
Less cross-site traffic reduces exposure.
