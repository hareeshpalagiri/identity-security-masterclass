📘 04 — Pass-Through Authentication (PTA)
Medium‑depth explanation with Mahabharata‑aligned storytelling — GitBook Ready.

🏹 **Mahabharata Analogy —
“The royal messenger verifies identity only at the king’s court.”**
In ancient times:

When an allied warrior arrived at a kingdom,
the guards did not validate his identity themselves.
Instead, they sent a trusted messenger to the king’s court:

“Is this warrior truly from your kingdom?”


Only after the king confirmed his identity
were the gates opened.

This is exactly how Pass‑Through Authentication (PTA) works:

Entra ID does NOT validate the user’s password in the cloud.
Instead, it sends the authentication request back to your on‑prem AD
to verify the password against Domain Controllers.

The cloud becomes a gateway →
The domain controllers remain the “king’s court.”

🔐 1. What Is Pass‑Through Authentication? (Simple Definition)
Pass‑Through Authentication (PTA) is a hybrid sign‑in method where:

Users enter their password on the Entra ID cloud login page
BUT the password is validated on‑premises
Using a lightweight PTA Agent installed on your servers
Which forwards the encrypted password to Active Directory Domain Services (AD DS)

PTA ensures:

The password never lives in the cloud
Real-time verification happens in AD
Users get SSO-like behavior without ADFS


🧠 2. How PTA Works (Medium Depth)
Here is the exact PTA flow:

⭐ Step 1 — User enters login at login.microsoftonline.com
Password is encrypted locally using public key of PTA service.

⭐ Step 2 — Entra ID forwards encrypted credentials
No plaintext password ever travels.

⭐ Step 3 — PTA Agent picks up the request
Agent runs on an on‑prem server (can deploy multiple for HA).

⭐ Step 4 — Agent decrypts password using private key
Stored securely in the agent.

⭐ Step 5 — Agent validates password with AD DS
Against Domain Controllers using Kerberos/NTLM.

⭐ Step 6 — Result sent back to Entra ID
Success → Entra ID issues tokens
Failure → Access denied
No password ever gets stored or synced to the cloud.

🕸 3. PTA Login Workflow (Mermaid Diagram)
sequenceDiagram    participant User    participant Entra as Entra ID    participant PTAAgent as PTA Agent (On-Prem)    participant DC as Domain Controller    User->>Entra: Login + Password (Encrypted)    Entra->>PTAAgent: Send Auth Request    PTAAgent->>PTAAgent: Decrypt Password    PTAAgent->>DC: Validate Credentials    DC-->>PTAAgent: Success/Failure    PTAAgent-->>Entra: Response    Entra-->>User: Token Issued / DeniedShow more linesDomain ControllerPTA Agent (On-Prem)Entra IDUserDomain ControllerPTA Agent (On-Prem)Entra IDUser#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-thickness-normal {stroke-width:1px}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .actor {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 text.actor > tspan {fill:blackstroke:none;}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .actor-line {stroke:rgb(218, 206, 243)}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .messageLine0 {stroke-width:1.5stroke-dasharray:none;stroke:rgb(51, 51, 51);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .messageLine1 {stroke-width:1.5stroke-dasharray:2, 2;stroke:rgb(51, 51, 51);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 #arrowhead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .sequenceNumber {fill:white}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 #sequencenumber {fill:rgb(51, 51, 51)}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 #crosshead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .messageText {fill:rgb(51, 51, 51)stroke:none;}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .labelBox {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .labelText, #mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .labelText > tspan {fill:blackstroke:none;}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .loopText, #mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .loopText > tspan {fill:blackstroke:none;}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .loopLine {stroke-width:2pxstroke-dasharray:2, 2;stroke:rgb(218, 206, 243);fill:rgb(218, 206, 243);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .note {stroke:rgb(170, 170, 51)fill:rgb(255, 245, 173);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .noteText, #mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .noteText > tspan {fill:blackstroke:none;}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .activation0 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .activation1 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .activation2 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .actorPopupMenu {position:absolute}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .actorPopupMenuPanel {position:absolutefill:rgb(236, 236, 255);box-shadow:rgba(0, 0, 0, 0.2) 0px 8px 16px 0px;filter:drop-shadow(rgba(0, 0, 0, 0.4) 3px 5px 2px);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .actor-man line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .actor-man circle, #mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);stroke-width:2px;}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .error-icon{fill:#552222;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .error-text{fill:#552222;stroke:#552222;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-thickness-normal{stroke-width:1px;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .marker{fill:#333333;stroke:#333333;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .marker.cross{stroke:#333333;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 p{margin:0;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .actor{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 text.actor>tspan{fill:black;stroke:none;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .actor-line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 #arrowhead path{fill:#333;stroke:#333;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .sequenceNumber{fill:white;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 #sequencenumber{fill:#333;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 #crosshead path{fill:#333;stroke:#333;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .messageText{fill:#333;stroke:none;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .labelBox{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .labelText,#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .labelText>tspan{fill:black;stroke:none;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .loopText,#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .loopText>tspan{fill:black;stroke:none;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .note{stroke:#aaaa33;fill:#fff5ad;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .noteText,#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .noteText>tspan{fill:black;stroke:none;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .actorPopupMenu{position:absolute;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .actorPopupMenuPanel{position:absolute;fill:#ECECFF;box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .actor-man line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 .actor-man circle,#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;stroke-width:2px;}#mermaid-0824ca7b-9299-4579-87c9-b952ef5d42a7 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Login + Password (Encrypted)Send Auth RequestDecrypt PasswordValidate CredentialsSuccess/FailureResponseToken Issued / Denied

⚡ 4. Why Organizations Choose PTA
✔ Password never leaves on‑prem AD
Ideal for strict regulatory environments.
✔ Cloud login page + on‑prem validation
Best balance between cloud experience + on‑prem ownership.
✔ No ADFS required
PTA replaces ADFS for most scenarios.
✔ Works fully with Conditional Access
Because cloud still issues the tokens.
✔ Simple & lightweight

No federation servers
No load balancers
No SQL
Just multiple PTA agents for high availability.


🔐 5. PTA vs PHS vs Federation (Medium Depth)





















































FeaturePTAPHSADFSPassword ValidationOn‑premCloudOn‑premPassword Stored in Cloud❌ No✔ Rehashed❌ NoCloud DependencyMediumLowLowOn‑Prem DependencyHighLowVery highComplexityLowVery lowVery highConditional Access Support✔ Full✔ FullPartialIdeal ForRegulated orgs99% orgsLegacy only
Bottom Line:
PTA is the best choice when compliance requires password validation to remain on‑premises,
but ADFS is too heavy and unnecessary.

🖥 6. PTA Agent Requirements
✔ Install on Windows Server (domain joined)
✔ Outbound internet only (no inbound firewall rules)
✔ Multiple agents for failover & load distribution
✔ Minimal system impact
✔ Azure AD Connect must be present in the environment
Agents can be installed on existing servers like:

AD Connect server
Member servers
Management servers


🔧 7. Key PTA Features
✔ High Availability
Install 3–5 agents — Entra ID load‑balances automatically.
✔ Encryption
Credentials are encrypted before leaving client/browser.
✔ Real-Time Validation
No sync delay (unlike password sync).
✔ Works with Seamless SSO
Which you will cover in the next chapter.

⚠️ 8. PTA Limitations
❌ Requires on‑prem availability
If on‑prem network or DCs are down → logins fail.
❌ Higher operational dependency
Compared to PHS (which can run even if AD is down).
❌ Not ideal for cloud‑first environments
Remote workforce depends on your on-prem infrastructure.

🌉 9. When PTA Is the Right Choice
Use PTA if:

Compliance requires password to never reside in the cloud
You’re moving away from ADFS
You still have a heavy on‑prem presence
You have investments in AD DS policies
Identity governance is performed on‑prem

For most other cases, PHS is simpler and more resilient.

🧠 10. Mind Map
Pass-Through Authentication
 ├─ Purpose
 │   ├─ On-prem password validation
 │   ├─ No cloud password sync
 ├─ Flow
 │   ├─ User → Entra ID
 │   ├─ Encrypted password
 │   ├─ PTA Agent → AD DS
 │   ├─ Validation result
 ├─ Benefits
 │   ├─ Compliance
 │   ├─ Works with CA + MFA
 │   ├─ Lightweight alternative to ADFS
 ├─ Limitations
 │   ├─ Dependency on DC availability
 └─ When To Use
     ├─ Strict compliance
     ├─ Not cloud-first
     └─ ADFS replacement


🎯 Summary
Pass‑Through Authentication is:

secure
lightweight
compliance-friendly
simple to maintain
integrated with all modern cloud security (MFA, CA, Identity Protection)

It allows users to sign in through the cloud
while keeping password validation on-prem.
PTA is ideal when organizations need on‑prem control,
but want to avoid the complexity of ADFS
and benefit from modern Entra ID authentication.
