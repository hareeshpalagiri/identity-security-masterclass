📘 03 — LDAP & LDAPS (Directory Binds, Signing, Channel Binding, Hardening)
A simple, deep, story‑based explanation using strategic Mahabharata analogies — GitBook Ready

🏹 Mahabharata Story Analogy (Strategic Only)
Think of scribes carrying scrolls between palaces (apps) and the royal archive (directory).

Plain parchment and open courtyards = unsigned, cleartext LDAP — easy to tamper with.
A sealed envelope = LDAP signing — the scribe can’t alter the scroll undetected.
A sealed envelope tied to a specific courier route = LDAP channel binding — even if someone builds a fake courtyard (TLS “man‑in‑the‑middle”), the seal proves it belongs to this secure route only. [learn.microsoft.com], [windows-ac...ectory.com]


🔐 1. What is LDAP / LDAPS? (Simple Definition)
LDAP (Lightweight Directory Access Protocol) lets applications read and update directory data (users, groups, policies). It operates over TCP 389 by default. LDAPS is LDAP over SSL/TLS on TCP 636, establishing encryption as soon as the connection starts. [learn.microsoft.com]
In Windows AD, security can be strengthened with LDAP signing (cryptographic integrity for SASL binds) and LDAP channel binding (binds the application‑layer authentication to the underlying TLS session to prevent relay/MITM). [learn.microsoft.com]

🧭 2. Why LDAP Matters — Hastinapura Example





















Without protectionsWith protectionsSimple binds over cleartext can expose credentials; unsigned SASL binds can be modified by an attacker in transit.Enforce LDAP signing so DCs reject unsigned SASL and simple binds over non‑TLS; prefer LDAPS for encryption. [community....eworks.com]TLS termination/re‑encryption by a malicious middlebox can still enable LDAP relay even if signing seems “on.”Add LDAP channel binding (CBT/EPA) so the bind is tied to that TLS tunnel, blocking relays/MITM. [windows-ac...ectory.com], [learn.microsoft.com]Hard to see who/what is using weak binds.Directory Service logs (e.g., 2887/2889) & newer CBT events help you discover and enforce safely. [community....eworks.com], [wafaicloud.com]

🎬 3. Animation Placeholder
(Add later using GIF/Notebook‑LLM)
[Animation Placeholder: "From cleartext to sealed route"]
Scene 1 → App → DC (LDAP simple bind over 389) → credentials visible (risk)
Scene 2 → App → DC (SASL bind unsigned) → tamper risk
Scene 3 → Enable Signing → scribe’s scroll sealed (tamper-evident)
Scene 4 → Enable Channel Binding → seal is tied to this TLS route (relay blocked)


🧠 4. Core Components (Simple + Deep)
Binds and Mechanisms

Simple bind: sends credentials; must be wrapped in TLS (LDAPS/StartTLS) or it risks exposure. [windows-ac...ectory.com]
SASL bind (Negotiate/Kerberos/NTLM/Digest): can be signed so the DC verifies message integrity end‑to‑end. [learn.microsoft.com]

LDAP Signing

When enforced on DCs, the server rejects unsigned SASL binds and rejects simple binds over cleartext. This prevents replay/tamper and is a recommended baseline. [community....eworks.com]

LDAP Channel Binding (CBT/EPA)

Binds the application‑layer auth to the TLS session using a Channel Binding Token so an attacker who tries to terminate and re‑establish TLS can’t re‑use the client’s authentication — closes a key relay loophole. [windows-ac...ectory.com], [learn.microsoft.com]

Policy & Events

Microsoft’s hardening guidance (ADV190023 / KB4520412) explains why signing & channel binding together matter and adds CBT auditing events (3039–3041) to help you plan enforcement. [wafaicloud.com]
DCs log 2887 (daily summary of insecure binds) and 2889 (client detail for unsigned binds) to identify sources before enforcing. [community....eworks.com]


🔀 5. Bind Patterns You’ll See (and What to Do)
flowchart LR    A[App/Client] -- LDAP 389 (simple) --> B[DC]    A -. LDAPS 636 (TLS) .-> B    A == SASL/Negotiate (Kerb/NTLM) ==> B    style A fill:#eaf2ff,stroke:#4c7bd9    style B fill:#f5f5f5,stroke:#999Show more lines#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-thickness-normal {stroke-width:1px}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .cluster-label span p {background-color:transparent}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .label text, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node rect, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node circle, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node ellipse, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node polygon, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .rough-node .label text, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node .label text, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .image-shape .label, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .icon-shape .label {text-anchor:middle}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .rough-node .label, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node .label, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .image-shape .label, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .icon-shape .label {text-align:center}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node.clickable {cursor:pointer}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .cluster text {fill:rgb(51, 51, 51)}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .cluster span {color:rgb(51, 51, 51)}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 rect.text {fill:nonestroke-width:0;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .icon-shape, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .icon-shape p, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .icon-shape rect, #mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .error-icon{fill:#552222;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .error-text{fill:#552222;stroke:#552222;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-thickness-normal{stroke-width:1px;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .marker{fill:#333333;stroke:#333333;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .marker.cross{stroke:#333333;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 p{margin:0;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .cluster-label text{fill:#333;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .cluster-label span{color:#333;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .cluster-label span p{background-color:transparent;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .label text,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 span{fill:#333;color:#333;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node rect,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node circle,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node ellipse,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node polygon,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .rough-node .label text,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node .label text,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .image-shape .label,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .icon-shape .label{text-anchor:middle;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .rough-node .label,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node .label,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .image-shape .label,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .icon-shape .label{text-align:center;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node.clickable{cursor:pointer;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .arrowheadPath{fill:#333333;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .flowchart-link{stroke:#333333;fill:none;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .cluster text{fill:#333;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .cluster span{color:#333;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 rect.text{fill:none;stroke-width:0;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .icon-shape,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .icon-shape p,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .icon-shape rect,#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-8ace1982-d1c4-4dab-8190-1571096cb8d4 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}LDAP 389 (simple)LDAPS 636 (TLS)SASL/Negotiate (Kerb/NTLM)App/ClientDC

Simple bind over 389 → block (or only allow if wrapped by StartTLS); prefer 636/LDAPS or SASL with signing. [community....eworks.com]
SASL bind (Negotiate) → enforce LDAP signing so tampering is detected; then add channel binding to defeat relays via TLS termination. [learn.microsoft.com], [windows-ac...ectory.com]


🔧 6. LDAP Hardening — Practical Steps
6.1 Discover current usage

On DCs, enable eventing to spot insecure binds:

2887 summary daily; 2889 shows source IP/identity for unsigned binds (set “LDAP Interface Events” diagnostic to 2). [community....eworks.com]


For channel binding readiness, use CBT audit events (3039–3041) from the KB to find clients that will fail when enforcing CBT/EPA. [wafaicloud.com]

6.2 Enforce LDAP signing (Domain Controllers)

Group Policy → Computer Configuration → Policies → Windows Settings → Security Settings → Local Policies → Security Options →
Domain controller: LDAP server signing requirements = Require signing (after review of 2889 findings). [community....eworks.com]

6.3 Enable LDAP channel binding (CBT/EPA)

Apply channel binding on DCs so TLS and the auth exchange are cryptographically bound; Microsoft’s hardening series details why both signing & channel binding are necessary and how to stage enforcement safely. [windows-ac...ectory.com]
Microsoft’s KB centralizes CBT policy references and the monitoring events to help you audit‑then‑enforce. [wafaicloud.com]

6.4 Use LDAPS where possible

Prefer port 636 (or StartTLS) to encrypt the entire session immediately; this prevents credential exposure for simple bind and protects directory data-in-transit. [learn.microsoft.com]

6.5 Monitor and iterate

Keep watching 2887/2889 (bind quality) and CBT audit events; remediate devices and apps until the logs are clean, then flip enforcement. [wafaicloud.com], [community....eworks.com]


⚔️ 7. Common Attack Paths & Effective Defenses
🛑 Attacks

LDAP simple bind over cleartext → credentials visible to intercept; remediation is LDAPS/signing. [community....eworks.com]
LDAP relay via TLS termination (even when “signing” appears present in parts of the path) → remediation is channel binding (CBT/EPA) to tie the auth to the TLS session. [windows-ac...ectory.com]

🛡 Defenses

Enforce LDAP signing (reject unsigned SASL, simple over clear). [community....eworks.com]
Enforce LDAP channel binding (EPA/CBT) to prevent relays/MITM. [learn.microsoft.com]
Maintain LDAPS with correct certificates on DCs. (Port 636; immediate TLS). [learn.microsoft.com]


🔧 8. Quick Admin Snippets (Copy‑ready)

A) Find unsigned binds (DC)
Event Viewer → Applications and Services Logs → Directory Service


Event ID 2887 (daily summary of insecure binds)
Event ID 2889 (client IP/identity for unsigned binds; requires diagnostic level 2) [community....eworks.com]


B) Watch CBT readiness
Check NTLM/Directory Service logs for CBT audit events (3039–3041) (added via security updates in support of ADV190023). [wafaicloud.com]


C) Enforce DC policy (after audit)

GPO → Computer Configuration
   → Windows Settings → Security Settings
   → Local Policies → Security Options
      ▸ Domain controller: LDAP server signing requirements = Require signing

 [community....eworks.com]

D) Ports


LDAP: 389/TCP (StartTLS optional)
LDAPS: 636/TCP (TLS from connect) [learn.microsoft.com]


🧵 9. Mind Map (Placeholder)
(Will be converted to GIF later)
LDAP/LDAPS
 ├─ Binds: Simple vs SASL (Negotiate/Kerberos/NTLM)
 ├─ Ports: 389 (LDAP), 636 (LDAPS)
 ├─ Hardening:
 │   ├─ LDAP signing (reject unsigned & clear)
 │   └─ LDAP channel binding (CBT/EPA)
 ├─ Events:
 │   ├─ 2887/2889 (insecure/unsigned bind sources)
 │   └─ 3039–3041 (CBT auditing)
 └─ Process:
     1) Audit → 2) Fix clients/apps → 3) Enforce signing → 4) Enforce CBT


References (selected)

LDAP signing & channel binding (how/why; ports) — Microsoft Learn. [learn.microsoft.com]
Hardening rationale: why both signing and CBT are needed — Microsoft TechCommunity series. [windows-ac...ectory.com]
KB4520412 (ADV190023) — LDAP channel binding + signing requirements; CBT auditing events (3039–3041). [wafaicloud.com]
Enable and audit LDAP signing (events 2887/2889; policy path) — Microsoft troubleshooting doc.
