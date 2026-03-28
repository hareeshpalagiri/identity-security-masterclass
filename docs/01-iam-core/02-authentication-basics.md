📘 02 — Authentication Basics
(Understanding how users prove who they are — through the lens of Hastinapura’s gate security)

🏹 Mahabharata Story Opener — “The Gate of Hastinapura”
Before anyone enters the city of Hastinapura, they must pass through well-guarded gates.

Warriors state their name & lineage
Gatekeepers verify their clan, symbols, reputation
Some require secret phrases or tokens
High‑risk situations trigger extra checks
Unknown travelers face strict validation

This is exactly how Authentication works in cybersecurity.
Authentication = The digital gatekeeper that verifies identity.

🔐 1. Simple Definition
Authentication is the process of proving your identity before accessing a system.
In IAM terms:

“Authentication answers the question: Who are you?”


🧠 2. Why Authentication Exists (Simple + Deep)
Without authentication, anyone could:

Log in as anyone
Access internal systems
Impersonate privileged users
Trigger security incidents

Just like in Hastinapura:

Letting any archer walk into the palace without verifying if he is Arjuna → dangerous.
Letting Ashwatthama enter with unchecked weaponry → privilege misuse.
Letting Shakuni in without verification → social engineering attack.

Strong authentication prevents identity misuse.

🔍 3. Types of Authentication (Explained simply)
✔ 1. Something you know

Passwords
PIN

Like knowing a secret phrase used at the gate.
✔ 2. Something you have

Authenticator app
Smart card
Hardware token

Like having a royal seal or identity token.
✔ 3. Something you are

Biometrics (face, fingerprint)

Like recognizing a warrior by appearance & unique traits.
✔ 4. Somewhere you are

Geo-location
IP range

Like entering from a trusted gate or territory.
✔ 5. Something you do

Behavior analysis

Like identifying a warrior by unique archery style.

🎬 4. Animation Placeholder
(Will be generated later)
[GIF Placeholder: "Warrior approaching gate → identity proof → verification → access granted/denied"]

You will create:
- A warrior arriving
- Gatekeeper checking identity
- Applying MFA (extra check)
- Allow/Deny animation


🏛 5. Classical vs Modern Authentication
📌 5.1 Traditional (Weak) Authentication

Password-only
Easily guessed
Reusable
Prone to attacks

Mahabharata analogy:
Letting anyone in who just says “I am from Pandava camp.”
📌 5.2 Modern (Strong) Authentication

Multifactor authentication (MFA)
Passwordless
Device-bound credentials
Certificate-based login

Analogy:
Only allowing entry if a warrior shows identity token + lineage code.

🔁 6. Kerberos & NTLM (High-Level Foundation)
Deep dive will happen in Section 03, but here is the basics:
NTLM (Old, Weak)

Challenge-response
Vulnerable to relay attacks
Fallback protocol

Analogy:
A guard who allows people through based on verbal claims — easy to fool.
Kerberos (Modern AD Authentication)

Ticket-based
Secure
Uses KDC
Harder to replay

Analogy:
Gatekeeper issues a signed entry pass (ticket) from the royal authority.
Mermaid Diagram
sequenceDiagram    participant User    participant KDC    participant Server    User->>KDC: Requests identity validation    KDC->>User: Issues Ticket    User->>Server: Presents Ticket    Server->>User: Access GrantedShow more linesServerKDCUserServerKDCUser#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-thickness-normal {stroke-width:1px}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .actor {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 text.actor > tspan {fill:blackstroke:none;}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .actor-line {stroke:rgb(218, 206, 243)}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .messageLine0 {stroke-width:1.5stroke-dasharray:none;stroke:rgb(51, 51, 51);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .messageLine1 {stroke-width:1.5stroke-dasharray:2, 2;stroke:rgb(51, 51, 51);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 #arrowhead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .sequenceNumber {fill:white}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 #sequencenumber {fill:rgb(51, 51, 51)}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 #crosshead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .messageText {fill:rgb(51, 51, 51)stroke:none;}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .labelBox {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .labelText, #mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .labelText > tspan {fill:blackstroke:none;}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .loopText, #mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .loopText > tspan {fill:blackstroke:none;}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .loopLine {stroke-width:2pxstroke-dasharray:2, 2;stroke:rgb(218, 206, 243);fill:rgb(218, 206, 243);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .note {stroke:rgb(170, 170, 51)fill:rgb(255, 245, 173);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .noteText, #mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .noteText > tspan {fill:blackstroke:none;}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .activation0 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .activation1 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .activation2 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .actorPopupMenu {position:absolute}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .actorPopupMenuPanel {position:absolutefill:rgb(236, 236, 255);box-shadow:rgba(0, 0, 0, 0.2) 0px 8px 16px 0px;filter:drop-shadow(rgba(0, 0, 0, 0.4) 3px 5px 2px);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .actor-man line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .actor-man circle, #mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);stroke-width:2px;}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .error-icon{fill:#552222;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .error-text{fill:#552222;stroke:#552222;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-thickness-normal{stroke-width:1px;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .marker{fill:#333333;stroke:#333333;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .marker.cross{stroke:#333333;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 p{margin:0;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .actor{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 text.actor>tspan{fill:black;stroke:none;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .actor-line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 #arrowhead path{fill:#333;stroke:#333;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .sequenceNumber{fill:white;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 #sequencenumber{fill:#333;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 #crosshead path{fill:#333;stroke:#333;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .messageText{fill:#333;stroke:none;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .labelBox{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .labelText,#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .labelText>tspan{fill:black;stroke:none;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .loopText,#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .loopText>tspan{fill:black;stroke:none;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .note{stroke:#aaaa33;fill:#fff5ad;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .noteText,#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .noteText>tspan{fill:black;stroke:none;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .actorPopupMenu{position:absolute;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .actorPopupMenuPanel{position:absolute;fill:#ECECFF;box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .actor-man line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 .actor-man circle,#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;stroke-width:2px;}#mermaid-1a43ce7c-ab05-485f-ac98-ea14806f8708 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Requests identity validationIssues TicketPresents TicketAccess Granted

🔧 7. Real-World Authentication Configurations
✔ Check user login method in AD (Event Viewer)
Security Log → Event ID 4624 / 4625
Shows whether user used:

NTLM
Kerberos
Local auth

✔ Force NTLM blocking via GPO
Computer Config → Policies → Windows Settings → Security Settings → Local Policies → Security Options

Network Security: Restrict NTLM: NTLM authentication in this domain → Deny All

✔ Enable MFA in Entra ID
Portal → Identity → Users → Authentication Methods → Require MFA
✔ Enable Passwordless (FIDO2)
Portal → Identity → Authentication Methods → FIDO2 Security Key → Enable

⚔️ 8. How Attackers Abuse Authentication
1. Password Spraying

Trying few common passwords across many accounts
Analogy:
Shakuni testing multiple simple “entry phrases” on different gates.

2. Credential Stuffing
Using leaked passwords from other sites.
3. NTLM Relay
Intercepting and reusing authentication requests.
Analogy:
Impersonating a messenger by reusing someone’s identity token.
4. Pass-the-Hash
Using password hash to authenticate without password.
5. Kerberoasting
Requesting ticket for a service account and cracking it offline.
6. MFA Fatigue Attack
Bombarding a user with MFA push requests.

🛡 9. Defensive Controls
Enable MFA everywhere
Stops 99% of attacks.
Disable NTLM wherever possible
Prevents relays & pass-the-hash.
Enforce Conditional Access

Location
Device compliance
Risk-based conditions

Passwordless Auth

FIDO2
Windows Hello for Business

Strong Kerberos Config

AES encryption
LDAP signing
Disable RC4


🧵 10. Mind Map (Placeholder)
(To animate later)
Authentication Mind Map:
  - Passwords
  - MFA
  - Kerberos
  - NTLM
  - Certificates
  - Passwordless
  - Attack techniques
  - Defense strategies


🔗 11. Transition to Chapter 03 — Authorization
Now that you understand how users prove who they are,
the next step is:

“After entering Hastinapura, what can the user access?”

Even if a warrior proves identity:

Abhimanyu cannot enter Kaurava war room
Karna cannot enter Pandava private chambers
Only Bhishma, Drona, Vidura have privileged access

This leads us to:
👉 Chapter 03 — Authorization (RBAC, ABAC, permissions, groups, ACLs)
