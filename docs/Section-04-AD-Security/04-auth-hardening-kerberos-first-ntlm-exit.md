📘 04 — Authentication Hardening (Kerberos‑first & NTLM Exit)
A simple, deep, story‑driven chapter using Mahabharata strategy — GitBook Ready

🏹 **Mahabharata Story Analogy —
“Verify the banner before allowing entry.”**
On the Kurukshetra battlefield:

Soldiers wore similar armor
Enemy spies disguised themselves as friendly warriors
Camps relied not on appearance, but on:

Banner verification
Voice recognition
Secret codes
Divine identification marks



Any warrior entering the Pandava camp had to prove:
✔ Identity
✔ Legitimacy
✔ Intent
✔ Allegiance
Even if someone looked legitimate, they were never trusted blindly.
This is the principle of Kerberos, the modern “trusted banner protocol”.
And NTLM is the old unverified “appearance check” that attackers exploit.

🔐 1. What Is Kerberos‑First? (Simple Definition)
Kerberos‑first authentication ensures that applications, servers, and clients always use Kerberos (secure, mutual authentication) instead of falling back to NTLM (legacy, relay‑vulnerable).
Kerberos-first means:

Prefer Negotiate → Kerberos
Fix SPNs so servers can be identified
Configure browsers for WIA (Kerberos SSO)
Reduce NTLM usage → audit → block (in phases)
Hardening SMB, LDAP, HTTP to never fall back silently

Why?
Because Microsoft is moving toward disabling NTLM by default in future Windows versions, using a three‑phase plan:
Audit → Kerberos Enhancements → NTLM Disabled by Default.
 [learn.microsoft.com]

🧭 2. Why Kerberos‑First Matters — Mahabharata Example





























Problem (old world – NTLM)Solution (new world – Kerberos)No mutual verification (easy to impersonate a guard)Mutual authentication (both sides prove identity)Kerberos negotiation fails → silent NTLM fallbackExplicit Kerberos enforcement ("verify the banner")Attackers relay NTLM to privileged servicesKerberos tickets are bound to the service (SPN) making relays far harderWeak crypto (RC4 legacy)Kerberos uses AES + FAST armoringRemote users stuck with NTLMKDC Proxy (Kerberos over HTTPS 443) removes NTLM need
Kerberos‑first brings discipline and verification, like Pandavas vetting every warrior entering camp.
 [cyberpress.org], [github.com]

🎬 3. Animation Placeholder
[Animation Placeholder: "Kerberos-first vs. NTLM Fallback"]

Scene 1 → User tries accessing intranet site  
Scene 2 → SPN found → Kerberos ticket issued → SSO success  
Scene 3 → SPN missing → NTLM fallback → relay attack triggers  
Scene 4 → Fix SPN + enforce Negotiate  
Scene 5 → All flows → Kerberos-first → NTLM blocked


🧠 4. Core Concepts (Simple + Deep)

⭐ 4.1 Kerberos Requires SPNs (Identity of Service)
Kerberos needs SPNs (Service Principal Names):
HTTP/app.company.com
cifs/fileserver01
ldap/dc01

If missing or duplicated → Kerberos fails → NTLM fallback.
 [cyberpress.org]

⭐ 4.2 Negotiate Chooses Kerberos FIRST
Only if Kerberos fails does Windows consider NTLM.
Thus, fixing the environment ensures NTLM is never needed.

⭐ 4.3 Browsers Must Allow Kerberos for Web SSO
Edge/Chrome require:

AuthServerAllowlist
AuthNegotiateDelegateAllowlist (if delegation needed)

to do Kerberos SSO.
 [github.com]

⭐ 4.4 SMB NTLM Blocking (Modern Feature)
Windows 11 and Server 2025 support:
✔ Client-side NTLM blocking
✔ Exception lists for legacy hosts
 [windowstechno.com]

⭐ 4.5 KDC Proxy (KKDCP) for Remote Kerberos
Kerberos over HTTPS 443 removes dependency on DC reachability.
 [calcomsoftware.com], [cybersecur...tynews.com]

⭐ 4.6 Kerberos Enhancements

RC4 removal → AES-only
FAST (Kerberos armoring) → protects pre-auth
 [pkisolutions.com], [techcommun...rosoft.com]


🕸 5. Kerberos‑First Flow (Mermaid Diagram)
sequenceDiagram  participant User  participant Browser  participant KDC  participant Server  User->>Browser: Access https://intranet  Browser->>Server: GET / (Negotiate)  Server-->>Browser: 401 Negotiate  Browser->>KDC: TGS-REQ (SPN: HTTP/intranet)  KDC-->>Browser: TGS-REP (Kerberos Ticket)  Browser->>Server: Authorization: Negotiate <Kerberos>  Server-->>Browser: 200 OK (SSO Success)Show more linesServerKDCBrowserUserServerKDCBrowserUser#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-thickness-normal {stroke-width:1px}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .actor {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 text.actor > tspan {fill:blackstroke:none;}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .actor-line {stroke:rgb(218, 206, 243)}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .messageLine0 {stroke-width:1.5stroke-dasharray:none;stroke:rgb(51, 51, 51);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .messageLine1 {stroke-width:1.5stroke-dasharray:2, 2;stroke:rgb(51, 51, 51);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 #arrowhead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .sequenceNumber {fill:white}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 #sequencenumber {fill:rgb(51, 51, 51)}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 #crosshead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .messageText {fill:rgb(51, 51, 51)stroke:none;}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .labelBox {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .labelText, #mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .labelText > tspan {fill:blackstroke:none;}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .loopText, #mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .loopText > tspan {fill:blackstroke:none;}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .loopLine {stroke-width:2pxstroke-dasharray:2, 2;stroke:rgb(218, 206, 243);fill:rgb(218, 206, 243);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .note {stroke:rgb(170, 170, 51)fill:rgb(255, 245, 173);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .noteText, #mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .noteText > tspan {fill:blackstroke:none;}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .activation0 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .activation1 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .activation2 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .actorPopupMenu {position:absolute}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .actorPopupMenuPanel {position:absolutefill:rgb(236, 236, 255);box-shadow:rgba(0, 0, 0, 0.2) 0px 8px 16px 0px;filter:drop-shadow(rgba(0, 0, 0, 0.4) 3px 5px 2px);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .actor-man line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .actor-man circle, #mermaid-28cd8d08-f409-4d40-a745-a5555c215971 line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);stroke-width:2px;}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-28cd8d08-f409-4d40-a745-a5555c215971{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .error-icon{fill:#552222;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .error-text{fill:#552222;stroke:#552222;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-thickness-normal{stroke-width:1px;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .marker{fill:#333333;stroke:#333333;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .marker.cross{stroke:#333333;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 p{margin:0;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .actor{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 text.actor>tspan{fill:black;stroke:none;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .actor-line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 #arrowhead path{fill:#333;stroke:#333;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .sequenceNumber{fill:white;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 #sequencenumber{fill:#333;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 #crosshead path{fill:#333;stroke:#333;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .messageText{fill:#333;stroke:none;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .labelBox{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .labelText,#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .labelText>tspan{fill:black;stroke:none;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .loopText,#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .loopText>tspan{fill:black;stroke:none;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .note{stroke:#aaaa33;fill:#fff5ad;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .noteText,#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .noteText>tspan{fill:black;stroke:none;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .actorPopupMenu{position:absolute;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .actorPopupMenuPanel{position:absolute;fill:#ECECFF;box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .actor-man line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 .actor-man circle,#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;stroke-width:2px;}#mermaid-28cd8d08-f409-4d40-a745-a5555c215971 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Access https://intranetGET / (Negotiate)401 NegotiateTGS-REQ (SPN: HTTP/intranet)TGS-REP (Kerberos Ticket)Authorization: Negotiate <Kerberos>200 OK (SSO Success)
If SPN missing → fallback to NTLM → vulnerable.

🔧 6. Practical Hardening Steps (Copy‑Ready)

✔ 6.1 Fix SPNs (Most Important)
PowerShellsetspn -S HTTP/intranet.contoso.com CONTOSO\svc_iissetspn -X     # Find duplicatesShow more lines
 [cyberpress.org]

✔ 6.2 IIS → Prefer Kerberos
Settings → Windows Authentication → Providers:
Negotiate
NTLM

Order matters.
 [cyberpress.org]

✔ 6.3 Edge/Chrome Policies for Kerberos SSO
Example:
AuthServerAllowlist = *.contoso.com
AuthNegotiateDelegateAllowlist = intranet.contoso.com

 [github.com]

✔ 6.4 Enable SMB NTLM Blocking
Use:

Block all NTLM except approved servers
Gradually reduce exception list
 [windowstechno.com]


✔ 6.5 Deploy KDC Proxy (Remote Kerberos)
If remote workers cannot reach DCs:

Deploy KDC Proxy (KKDCP) on RD Gateway/AVD
Tunnel Kerberos over 443
 [calcomsoftware.com], [cybersecur...tynews.com]


✔ 6.6 Enforce LDAP Signing & Channel Binding
Prevents NTLM-to-LDAP relay attacks.
 [github.com]

✔ 6.7 Enable Kerberos FAST (Armoring)
Protects Kerberos pre-auth traffic.
 [techcommun...rosoft.com]

✔ 6.8 RC4 → AES Migration
Identify RC4 usage and modernize.
 [pkisolutions.com]

✔ 6.9 NTLM Audit → Restrict → Block
Same phased plan Microsoft published.
 [learn.microsoft.com]

⚔️ 7. What Attacks Kerberos‑First Prevents





























AttackWhy It DiesNTLM Relay (SMB/LDAP/HTTP)No NTLM = no relayPass‑the‑HashKerberos doesn’t accept raw NTLM hashesNTLM downgradeNegotiate → Kerberos enforcedService spoofingKerberos mutual auth prevents fake serversMisconfigured SPNsAuditing reveals fallback hotspots
Kerberos-first dramatically reduces lateral movement and credential replay.

🛡 8. Defense Strategy — “Verify Every Banner, Always”
Mandatory

SPN fixes everywhere
IIS Negotiate ordering
Browser WIA policies
LDAP signing + CBT
SMB NTLM block
Kerberos-only for Tier‑0 & Tier‑1

Recommended

KDC Proxy for remote SSO
Certificate-based logon (smartcard/FIDO)
FAST armoring
Audit → block NTLM gradually


🔧 9. Quick Commands (Copy‑Paste)
View Kerberos tickets
PowerShellklistShow more lines
Check SPN duplication
PowerShellsetspn -XShow more lines
Check if NTLM used recently
PowerShellGet-WinEvent -LogName "Microsoft-Windows-NTLM/Operational" | select -f 20Show more lines
Test SMB NTLM block
PowerShellGet-SmbClientConfigurationShow more lines

🧵 10. Mind Map (Placeholder)
Kerberos-first
 ├─ SPN hygiene
 ├─ Negotiate ordering
 ├─ Browser policies
 ├─ SMB NTLM blocking
 ├─ LDAP signing + CBT
 ├─ KDC Proxy
 ├─ FAST armoring
 ├─ AES crypto
 └─ NTLM deprecation (audit → restrict → block)


📚 References


Advancing Windows Security: NTLM Disabled by Default
 [learn.microsoft.com]


IIS Windows Authentication: Negotiate/SPNs
 [cyberpress.org]


Browser WIA Policies (Edge/Chrome)
 [github.com]


SMB NTLM Blocking
 [windowstechno.com]


KDC Proxy (KKDCP) guidance
 [calcomsoftware.com], [cybersecur...tynews.com]


Kerberos FAST, RC4 retirement, AES upgrade
 [techcommun...rosoft.com], [pkisolutions.com]
