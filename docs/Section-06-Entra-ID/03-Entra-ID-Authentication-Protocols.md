📘 03 — Entra ID Authentication Protocols (OAuth2, OIDC, SAML)


🏹 **Mahabharata Analogy —
“From handwritten scrolls to divine seals of authentication.”**
In ancient Bharat:

Messengers traveled between kingdoms with scrolls containing commands.
Over time, scrolls evolved into royal seals, mudras, and insignias
— cryptographic identity proofs.
These seals allowed:

verification of the messenger,
authorization to access war rooms,
trust between kingdoms.



This evolution mirrors modern identity:

Passwords = scrolls (easy to steal, forge, or intercept)
OAuth/OIDC/SAML tokens = divine seals (digitally signed, secure, verifiable)

Microsoft Entra ID uses modern authentication protocols to issue such “divine identity tokens.”
 [learn.microsoft.com]

🔐 1. What Are Authentication Protocols? (Simple Definition)
Authentication protocols define how apps verify identity.
Microsoft Entra ID supports:
✔ OAuth 2.0 — Authorization framework
✔ OpenID Connect (OIDC) — Authentication built on OAuth
✔ SAML 2.0 — XML-based enterprise federation
✔ Legacy integrations — LDAP, Kerberos, RADIUS (for compatibility)
 [learn.microsoft.com]
These protocols help Entra ID issue secure tokens instead of relying on passwords.

🧭 2. Why Modern Authentication Exists
Passwords are:

reused
phished
stolen
replayed
brute-forced

Legacy protocols don’t support:

MFA
Conditional Access
Passwordless
Device trust
Zero Trust

Modern authentication (OAuth/OIDC/SAML) solves this by issuing secure, signed, short-lived tokens, validated cryptographically.

🧠 3. OAuth 2.0 (Authorization Protocol)
OAuth = “What can this app do?”
OIDC = “Who is the user?”
Microsoft Learn describes OAuth2 as consisting of four parties:
authorization server, client app, resource owner, resource server.
 [learn.microsoft.com]
Entra ID = Authorization Server.
OAuth issues:

Access Tokens (JWT) → For APIs
Refresh Tokens → To obtain new access tokens silently
 [learn.microsoft.com]

💡 Real-world examples:

Microsoft Graph
Outlook API
Teams API
Any custom API protected by Entra ID


⭐ 4. OpenID Connect (OIDC) — Authentication Layer on OAuth 2.0
OIDC adds identity to OAuth2.
Microsoft Learn describes OIDC as providing:

ID Tokens (JWT)
Authentication
Claims (email, name, tenant, groups)
 [learn.microsoft.com]

✔ ID Token = “Who are you?”
Contains:

sub (unique user ID)
Issuer (iss)
Expiry (exp)
Audience (aud)
Username, email

✔ Access Token = “What can you access?”
Used for API calls.
OIDC is used for:

Modern web apps
Mobile apps
Single-page apps
Microsoft 365 sign-in
Sign-in with "Login with Microsoft"


⭐ 5. SAML 2.0 — Enterprise Federation
SAML = older enterprise SSO mechanism, still widely used.
Microsoft Learn shows SAML as a supported authentication integration under Entra ID.
 [learn.microsoft.com]
Characteristics:

XML-based
Uses SAML Assertions instead of JWT
Browser-based redirects
Ideal for:

SAP
Salesforce
Workday
Older enterprise apps



SAML remains popular for legacy/enterprise workloads.

🎬 6. Modern Authentication Flow (Mermaid Diagram)
sequenceDiagram  participant User  participant App  participant EntraID as Entra ID (Authorization Server)  participant API  User->>App: Sign in request  App->>EntraID: OAuth/OIDC Authorization Request  EntraID->>User: Login + MFA  User->>EntraID: Credentials / Token Binding  EntraID-->>App: ID Token (OIDC) + Access Token (OAuth2)  App->>API: Send Access Token  API-->>App: Resource Access GrantedShow more linesAPIEntra ID (Authorization Server)AppUserAPIEntra ID (Authorization Server)AppUser#mermaid-33442374-4f05-45db-9d1e-34b263028a80 {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;fill:rgb(51, 51, 51);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-animation-slow {stroke-dashoffset:900animation-duration:50s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-animation-fast {stroke-dashoffset:900animation-duration:20s;animation-timing-function:linear;animation-delay:0s;animation-iteration-count:infinite;animation-direction:normal;animation-fill-mode:none;animation-play-state:running;animation-name:dash;animation-timeline:auto;animation-range-start:normal;animation-range-end:normal;stroke-linecap:round;stroke-dasharray:9, 5;}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .error-icon {fill:rgb(85, 34, 34)}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .error-text {fill:rgb(85, 34, 34)stroke:rgb(85, 34, 34);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-thickness-normal {stroke-width:1px}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-thickness-thick {stroke-width:3.5px}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-pattern-solid {stroke-dasharray:0}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-thickness-invisible {stroke-width:0fill:none;}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-pattern-dashed {stroke-dasharray:3}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-pattern-dotted {stroke-dasharray:2}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .marker {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .marker.cross {stroke:rgb(51, 51, 51)}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 svg {font-family:"trebuchet ms", verdana, arial, sans-seriffont-size:16px;}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 p {margin-top:0pxmargin-right:0px;margin-bottom:0px;margin-left:0px;}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .actor {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 text.actor > tspan {fill:blackstroke:none;}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .actor-line {stroke:rgb(218, 206, 243)}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .messageLine0 {stroke-width:1.5stroke-dasharray:none;stroke:rgb(51, 51, 51);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .messageLine1 {stroke-width:1.5stroke-dasharray:2, 2;stroke:rgb(51, 51, 51);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 #arrowhead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .sequenceNumber {fill:white}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 #sequencenumber {fill:rgb(51, 51, 51)}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 #crosshead path {fill:rgb(51, 51, 51)stroke:rgb(51, 51, 51);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .messageText {fill:rgb(51, 51, 51)stroke:none;}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .labelBox {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .labelText, #mermaid-33442374-4f05-45db-9d1e-34b263028a80 .labelText > tspan {fill:blackstroke:none;}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .loopText, #mermaid-33442374-4f05-45db-9d1e-34b263028a80 .loopText > tspan {fill:blackstroke:none;}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .loopLine {stroke-width:2pxstroke-dasharray:2, 2;stroke:rgb(218, 206, 243);fill:rgb(218, 206, 243);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .note {stroke:rgb(170, 170, 51)fill:rgb(255, 245, 173);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .noteText, #mermaid-33442374-4f05-45db-9d1e-34b263028a80 .noteText > tspan {fill:blackstroke:none;}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .activation0 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .activation1 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .activation2 {fill:rgb(244, 244, 244)stroke:rgb(102, 102, 102);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .actorPopupMenu {position:absolute}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .actorPopupMenuPanel {position:absolutefill:rgb(236, 236, 255);box-shadow:rgba(0, 0, 0, 0.2) 0px 8px 16px 0px;filter:drop-shadow(rgba(0, 0, 0, 0.4) 3px 5px 2px);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .actor-man line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .actor-man circle, #mermaid-33442374-4f05-45db-9d1e-34b263028a80 line {stroke:rgb(218, 206, 243)fill:rgb(236, 236, 255);stroke-width:2px;}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80 :root {--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif}
#mermaid-33442374-4f05-45db-9d1e-34b263028a80{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .error-icon{fill:#552222;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .error-text{fill:#552222;stroke:#552222;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-thickness-normal{stroke-width:1px;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .marker{fill:#333333;stroke:#333333;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .marker.cross{stroke:#333333;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 p{margin:0;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .actor{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 text.actor>tspan{fill:black;stroke:none;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .actor-line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 #arrowhead path{fill:#333;stroke:#333;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .sequenceNumber{fill:white;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 #sequencenumber{fill:#333;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 #crosshead path{fill:#333;stroke:#333;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .messageText{fill:#333;stroke:none;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .labelBox{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .labelText,#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .labelText>tspan{fill:black;stroke:none;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .loopText,#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .loopText>tspan{fill:black;stroke:none;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .note{stroke:#aaaa33;fill:#fff5ad;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .noteText,#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .noteText>tspan{fill:black;stroke:none;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .actorPopupMenu{position:absolute;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .actorPopupMenuPanel{position:absolute;fill:#ECECFF;box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .actor-man line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 .actor-man circle,#mermaid-33442374-4f05-45db-9d1e-34b263028a80 line{stroke:hsl(259.6261682243, 59.7765363128%, 87.9019607843%);fill:#ECECFF;stroke-width:2px;}#mermaid-33442374-4f05-45db-9d1e-34b263028a80 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}Sign in requestOAuth/OIDC Authorization RequestLogin + MFACredentials / Token BindingID Token (OIDC) + Access Token (OAuth2)Send Access TokenResource Access Granted

🔧 7. Token Types in Entra ID
According to Microsoft identity platform docs:
Bearer tokens are JWTs used to authenticate and authorize access.
 [learn.microsoft.com]
✔ ID Token (OIDC)
Used to authenticate the user.
✔ Access Token (OAuth2)
Used to authorize API access.
✔ Refresh Token
Used to obtain new tokens.

🛡 8. Conditional Access + MFA + Identity Protection
These only work with modern authentication.
Legacy protocols do not support these controls.
Microsoft Learn confirms that Conditional Access is built on top of Entra ID authentication signals.
 [acefekay.w...dpress.com]
Modern protocols enable:

Risk-based authentication
Device compliance checks
Passwordless authentication
Zero Trust enforcement


📡 9. Legacy Authentication Integration (Compatibility)
Microsoft Entra supports integration with several legacy protocols:

Kerberos / Windows Auth
LDAP
Header-based auth
RADIUS
 [learn.microsoft.com]

These integrations help organizations migrate old apps to cloud identity.

🔥 10. Comparing OAuth, OIDC, and SAML















































FeatureOAuth2OIDCSAMLPurposeAuthorizationAuthenticationAuthenticationTokenAccess Token (JWT)ID Token (JWT)SAML Assertion (XML)Best ForAPIsModern appsEnterprise legacySupported By Entra ID✔✔✔MFA/CA✔✔✔Passwordless✔✔Limited

🧵 11. Mind Map
Authentication Protocols
 ├─ OAuth 2.0
 │   ├─ Access Token (JWT)
 │   ├─ Refresh Token
 │   └─ API authorization
 ├─ OpenID Connect (OIDC)
 │   ├─ ID Token (JWT)
 │   ├─ Claims
 │   └─ User authentication
 ├─ SAML 2.0
 │   ├─ SAML Assertion
 │   ├─ XML-based
 │   └─ Enterprise SSO
 ├─ Legacy Integration
 │   ├─ Kerberos
 │   ├─ LDAP
 │   └─ RADIUS
 └─ Zero Trust
     ├─ MFA
     ├─ Conditional Access
     ├─ Identity Protection
     └─ Passwordless


🎯 Summary
Microsoft Entra ID supports three major modern authentication protocols:

OAuth2 — authorization
OIDC — authentication
SAML — enterprise federation

These enable:

MFA
Conditional Access
Passwordless
Zero Trust
Secure API access
Modern and legacy app support

This chapter prepares you for the next two major areas:
→ 04-Entra-ID-Security-Hardening.md
→ 05-Users-Groups-Devices.md
