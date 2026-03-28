📘 06 — Zero Trust
A modern security model, retold through the strategic lens of Mahabharata’s battlefield wisdom.

🏹 **Mahabharata Story Opener —
"Trust No One Blindly on the Battlefield"**
In the great war:

Warriors disguised themselves
Secret alliances formed
Insider manipulation existed (e.g., Shakuni’s tactics)
Some warriors switched sides
Trusted individuals were compromised by emotion, anger, or revenge

Therefore, the Pandava camp never trusted ANYONE blindly —
not even known warriors.
Every person was continuously verified:

Intent
Identity
Weapon control
Alignment
Movement patterns

This is the essence of Zero Trust in cybersecurity:

Never trust. Always verify. Continuously validate.

Even if someone is inside the network, they must still prove legitimacy.

🔐 1. What is Zero Trust? (Simple Definition)
Zero Trust is a security model that assumes:

Nothing is trusted automatically,
Everything must be verified continuously,
Access is granted only with strict checks,
Every action is monitored.

It is the modern replacement for the old
“trusted internal network → untrusted external network” mindset.

🧠 2. Why Zero Trust Exists (Simple + Deep)
Traditional security mindset:
“If you are inside the network, you are trusted.”
This failed when:

Remote work grew
Cloud services became external
Attackers compromised internal machines
Identity attacks (phishing, token theft) exploded

Just like Hastinapura realized that:

Even familiar warriors might be compromised
Insider threat (Duryodhana) is deadly
Manipulators (Shakuni) weaken trust
Privilege abuse (Ashwatthama) causes damage
Masked attackers can bypass blind trust

Zero Trust fixes this weakness.

📌 3. Core Principles of Zero Trust
Zero Trust is built on six principles, each mapped to Mahabharata’s strategic behaviors.

🔷 1. Verify Explicitly
Always authenticate and authorize —
even if the user or device is internal.
Mahabharata Analogy:
Every warrior entering the Pandava camp was checked every time,
even if it was Arjuna returning from a mission.

🔷 2. Use Least Privilege Access
Give minimal access required.
Analogy:
Not every warrior could access the war council.
Only commanders (Bhishma-like roles) had higher privilege.

🔷 3. Assume Breach
Act as if attackers are already inside.
Analogy:
During the war, Pandavas always planned as if spies already infiltrated.

🔷 4. Micro-Segmentation
Break the environment into small trust zones.
Analogy:
Different weapon halls, chambers, and tents —
each protected separately.

🔷 5. Device Health Verification
Only allow secure, compliant devices.
Analogy:
Weapons were inspected before entering the war camp.

🔷 6. Continuous Monitoring
Track every action.
Analogy:
Sanjaya continuously observing battlefield events
is the perfect representation of real-time telemetry.

🎬 4. Animation Placeholder (Add Later)
[GIF Placeholder: "Warrior enters → verified → micro-zones → re-validation → monitored by Sanjaya"]

You can generate a clean animation later using NotebookLLM.

🕸 5. Zero Trust Architecture (Mermaid Diagram)
flowchart TD    A[User or Device] --> B{Authenticate?}    B -->|Yes| C[Least Privilege Policy Enforcement]    B -->|No| D[Access Denied]    C --> E{Device Compliant?}    E -->|Yes| F[Microsegment Access]    E -->|No| D    F --> G[Continuous Monitoring]    G --> H{Risk Detected?}    H -->|Yes| D    H -->|No| I[Access Continues With Re-Auth]Show more lines#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-thickness-normal {stroke-width:1px}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .label {font-family:"trebuchet ms", verdana, arial, sans-serifcolor:rgb(51, 51, 51);}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .cluster-label text {fill:rgb(51, 51, 51)}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .cluster-label span {color:rgb(51, 51, 51)}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .cluster-label span p {background-color:transparent}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .label text, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 span {fill:rgb(51, 51, 51)color:rgb(51, 51, 51);}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node rect, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node circle, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node ellipse, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node polygon, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node path {fill:rgb(236, 236, 255)stroke:rgb(147, 112, 219);stroke-width:1px;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .rough-node .label text, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node .label text, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .image-shape .label, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .icon-shape .label {text-anchor:middle}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node .katex path {fill:rgb(0, 0, 0)stroke:rgb(0, 0, 0);stroke-width:1px;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .rough-node .label, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node .label, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .image-shape .label, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .icon-shape .label {text-align:center}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node.clickable {cursor:pointer}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .root .anchor path {stroke-width:0stroke:rgb(51, 51, 51);fill:rgb(51, 51, 51);}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .arrowheadPath {fill:rgb(51, 51, 51)}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edgePath .path {stroke:rgb(51, 51, 51)stroke-width:2px;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .flowchart-link {stroke:rgb(51, 51, 51)fill:none;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edgeLabel {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edgeLabel p {background-color:rgba(232, 232, 232, 0.8)}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edgeLabel rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .labelBkg {background-color:rgba(232, 232, 232, 0.5)}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .cluster rect {fill:rgb(255, 255, 222)stroke:rgb(170, 170, 51);stroke-width:1px;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .cluster text {fill:rgb(51, 51, 51)}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .cluster span {color:rgb(51, 51, 51)}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 div.mermaidTooltip {position:absolutetext-align:center;max-width:200px;padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;font-family:"trebuchet ms", verdana, arial, sans-serif;font-size:12px;background-image:initial;background-position-x:initial;background-position-y:initial;background-size:initial;background-repeat:initial;background-attachment:initial;background-origin:initial;background-clip:initial;background-color:rgb(249, 255, 236);border-top-width:1px;border-right-width:1px;border-bottom-width:1px;border-left-width:1px;border-top-style:solid;border-right-style:solid;border-bottom-style:solid;border-left-style:solid;border-top-color:rgb(170, 170, 51);border-right-color:rgb(170, 170, 51);border-bottom-color:rgb(170, 170, 51);border-left-color:rgb(170, 170, 51);border-image-source:initial;border-image-slice:initial;border-image-width:initial;border-image-outset:initial;border-image-repeat:initial;border-top-left-radius:2px;border-top-right-radius:2px;border-bottom-right-radius:2px;border-bottom-left-radius:2px;pointer-events:none;z-index:100;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .flowchartTitleText {text-anchor:middlefont-size:18px;fill:rgb(51, 51, 51);}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 rect.text {fill:nonestroke-width:0;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .icon-shape, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .image-shape {background-color:rgba(232, 232, 232, 0.8)text-align:center;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .icon-shape p, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .image-shape p {background-color:rgba(232, 232, 232, 0.8)padding-top:2px;padding-right:2px;padding-bottom:2px;padding-left:2px;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .icon-shape rect, #mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .image-shape rect {opacity:0.5background-color:rgba(232, 232, 232, 0.8);fill:rgba(232, 232, 232, 0.8);}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .label-icon {display:inline-blockheight:1em;overflow-x:visible;overflow-y:visible;vertical-align:-0.125em;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node .label-icon path {fill:currentcolorstroke:revert;stroke-width:revert;}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .error-icon{fill:#552222;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .error-text{fill:#552222;stroke:#552222;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-thickness-normal{stroke-width:1px;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .marker{fill:#333333;stroke:#333333;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .marker.cross{stroke:#333333;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 p{margin:0;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .cluster-label text{fill:#333;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .cluster-label span{color:#333;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .cluster-label span p{background-color:transparent;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .label text,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 span{fill:#333;color:#333;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node rect,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node circle,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node ellipse,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node polygon,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .rough-node .label text,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node .label text,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .image-shape .label,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .icon-shape .label{text-anchor:middle;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .rough-node .label,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node .label,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .image-shape .label,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .icon-shape .label{text-align:center;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node.clickable{cursor:pointer;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .root .anchor path{fill:#333333!important;stroke-width:0;stroke:#333333;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .arrowheadPath{fill:#333333;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .flowchart-link{stroke:#333333;fill:none;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edgeLabel{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edgeLabel p{background-color:rgba(232,232,232, 0.8);}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .edgeLabel rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .cluster text{fill:#333;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .cluster span{color:#333;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 rect.text{fill:none;stroke-width:0;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .icon-shape,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .image-shape{background-color:rgba(232,232,232, 0.8);text-align:center;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .icon-shape p,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .image-shape p{background-color:rgba(232,232,232, 0.8);padding:2px;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .icon-shape rect,#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .image-shape rect{opacity:0.5;background-color:rgba(232,232,232, 0.8);fill:rgba(232,232,232, 0.8);}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#mermaid-bb4e5309-cc00-40ba-98b1-8a083f396f83 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}YesNoYesNoYesNoUser or DeviceAuthenticate?Least Privilege PolicyEnforcementAccess DeniedDevice Compliant?Microsegment AccessContinuous MonitoringRisk Detected?Access Continues WithRe-Auth

🛠 6. Real-World Zero Trust Configurations
✔ Enforce MFA Everywhere
Portal → Conditional Access → New Policy → Require MFA
✔ Enforce Device Compliance
Conditional Access →
Grant access only to compliant / hybrid-joined devices.
✔ Block Legacy Authentication
Legacy protocols bypass Zero Trust.
PowerShellSet-AuthenticationPolicy -BlockLegacyAuth $trueShow more lines
✔ Enable Risk-Based Conditional Access

Sign-in Risk
User Risk
Session Risk

✔ Implement Micro-Segmentation
Azure:

Network Security Groups
App Gateway WAF
Private Endpoints

AD:

Tiered Administration Model

✔ Deploy Defender for Identity
Monitors lateral movement & identity compromise.

⚔️ 7. Attack Scenarios Zero Trust Prevents
🚫 Pass-the-Hash
Continuous verification + device trust stops reuse of stolen tokens.
🚫 Password Spraying
MFA blocks the attack path.
🚫 Compromised Internal Machines
Assume breach → checks prevent lateral movement.
🚫 Token Replay
Conditional Access + POP tokens detect anomalies.
🚫 Insider Threat
Access reviews + least privilege reduce attack blast radius.

🛡 8. Defense Strategies in Zero Trust

MFA mandatory
Passwordless authentication
Device compliance enforcement
Micro-segmentation
Risk-based policies
Identity protection alerts
Continuous monitoring (Sanjaya model)
Privileged access control (PAM + Zero Trust together)

Think of this as Vidura’s governance + Sanjaya's visibility + Bhishma’s discipline in one system.

🧵 9. Mind Map Placeholder
Zero Trust Mind Map:
  - Verify Explicitly
  - Least Privilege
  - Assume Breach
  - Device Health
  - Micro-Segmentation
  - Continuous Monitoring
  - Identity + Network + Device integration


🔗 10. Transition to Chapter 07 — Audit & Logging
Zero Trust is powerful, but one question remains:

“How do we SEE what is happening inside the environment?”

Just as Sanjaya narrated every move on the battlefield with perfect clarity,
modern cybersecurity relies on logging, auditing, and monitoring.
So your next chapter:
👉 Chapter 07 — Audit & Logging
(Identity events, AD logs, Entra logs, SIEM integration)
