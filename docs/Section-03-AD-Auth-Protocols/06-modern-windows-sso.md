📘 06 — Modern Windows SSO Patterns (Negotiate/SPNEGO, CredSSP, and Web SSO bridges)
A simple, deep, story‑based explanation using strategic Mahabharata analogies — GitBook Ready

🏹 Mahabharata Story Analogy (Strategic Only)
Imagine palace messengers carrying sealed introductions that let you pass from one hall to another without re‑introducing yourself each time.

The usher who decides which seal to present — Kerberos or a fallback — is Negotiate/SPNEGO. [learn.microsoft.com], [rfc-editor.org]
When you must hand your credentials to a chamberlain so inner rooms trust you once inside, that’s CredSSP (RDP’s pre‑auth + credential delegation over TLS). [learn.microsoft.com]
And when the outer gate uses cloud tokens but the inner hall wants Kerberos, you add a bridge (KCD via AD FS Web Application Proxy or Microsoft Entra Application Proxy). [learn.microsoft.com], [learn.microsoft.com]


🔐 1) Negotiate / SPNEGO — “Pick the strongest, fall back if needed”
Negotiate is a Security Support Provider (SSP) that sits atop SSPI and chooses Kerberos by default (if the target is identified by SPN/UPN/NetBIOS), with NTLM as fallback when Kerberos can’t be used. 
For HTTP, browsers and servers use the “Negotiate” auth‑scheme that encapsulates SPNEGO tokens; when Kerberos is selected, you get Windows Integrated Authentication (WIA) without re‑typing credentials. 
On IIS, enable Windows Authentication and ensure Providers → Negotiate appears above NTLM so Kerberos is tried first; also ensure proper HTTP/host SPNs for the site identity (pool account or machine). 
SPNs matter: if the KDC can’t find a matching SPN for the hostname, the client tends to present NTLM via Negotiate, which breaks true SSO and some delegation scenarios. [learn.microsoft.com] [rfc-editor.org] [woshub.com], [techcommun...rosoft.com] [serverfault.com]
Browser configuration tips (WIA): Add your site to Intranet/Trusted Sites, enable Integrated Windows Authentication, and (for Edge/Chrome) configure AuthServerAllowlist / AuthNegotiateDelegateAllowlist so the browser is willing to send Kerberos tokens. 
Note that ASP.NET Core documents WIA behavior and the requirement to downgrade to HTTP/1.1 during the challenge phase; once authenticated, HTTP/2 can resume. [learn.microsoft.com], [documentat...eprism.com] [learn.microsoft.com]

🧳 2) CredSSP — RDP’s SSO workhorse (TLS + SPNEGO + credential delegation)
CredSSP (Credential Security Support Provider) is a protocol that combines TLS for the outer channel and Kerberos/NTLM via SPNEGO inside, then securely forwards user credentials to the server for single‑sign‑on (e.g., launching tools inside an RDP session without extra prompts). 
In the RDP stack, CredSSP is indicated by HYBRID/HYBRID_EX negotiation flags and always begins with a TLS handshake, after which Kerberos (or NTLM) authenticates the user and binds to the TLS session. [learn.microsoft.com], [github.com] [learn.microsoft.com]
Security note (must‑do): In 2018 Microsoft fixed CVE‑2018‑0886, a CredSSP RCE; environments must patch clients/servers and set the “Encryption Oracle Remediation” policy to avoid vulnerable handshakes (common RDP error text references this remediation). 
The CredSSP protocol spec is public (MS‑CSSP) for implementers and shows the credential delegation semantics (not the same as Kerberos constrained delegation). [support.mi...rosoft.com], [woshub.com] [learn.microsoft.com]

🌉 3) Web SSO bridges — Cloud tokens outside, Kerberos tickets inside
3.1 AD FS Web Application Proxy (WAP) preauthentication
WAP with AD FS preauth issues a claims token at the edge, then obtains a Kerberos ticket to the backend app (Integrated Windows Authentication) so users get SSO while the app still sees Kerberos. [learn.microsoft.com]
3.2 Microsoft Entra Application Proxy + KCD
Microsoft Entra Application Proxy can front an on‑prem app and use Kerberos Constrained Delegation (KCD) to impersonate the user against the internal site, delivering SSO after cloud preauth (Conditional Access/MFA apply on the cloud side). 
Docs include end‑to‑end flow and prerequisites (IWA backend, SPNs, domain‑joined connector, proper delegation lists), plus troubleshooting articles. [learn.microsoft.com] [learn.microsoft.com], [github.com]

☁️ 4) Modern SSO building blocks: WAM/WebView2 and Entra Kerberos


WAM (Web Account Manager) is Windows’ broker that MSAL‑based apps call to acquire tokens, enabling device/OS‑level SSO, Conditional Access, FIDO/Hello, and silent token acquisition with the OS account. [learn.microsoft.com]


As of late 2025/2026, Windows 11 can host WAM sign‑ins in WebView2, aligning app sign‑in UX with Chromium and improving compatibility for modern auth and passwordless. [techcommun...rosoft.com], [winaero.com]


Microsoft Entra Kerberos for Azure Files issues Kerberos tickets from Entra ID so devices (including cloud‑only identities) can access SMB file shares without DC line‑of‑sight; the feature is in preview with explicit prerequisites. [learn.microsoft.com]


Cloud Kerberos Trust also underpins SSO to on‑prem resources for Entra‑joined devices (e.g., WHfB with cloud trust) — a key pattern when moving to Kerberos‑first without heavy hybrid join. [headsinthecloud.blog], [maximerastello.com]



🧭 5) Patterns you’ll deploy (and how to choose)








































PatternUse whenKey requirementsNegotiate (HTTP SPNEGO)Intranet web apps on IIS/ASP.NET Core where you want silent WIAIIS Windows Auth + Negotiate first, correct SPNs, browser allowlists (Edge/Chrome), and Trusted Sites/Intranet zone. [woshub.com], [learn.microsoft.com], [documentat...eprism.com]CredSSP (RDP/NLA SSO)Admin RDP sessions and seamless tool launches inside RDPPatch for CVE‑2018‑0886 and enforce Encryption Oracle Remediation policy. [support.mi...rosoft.com]AD FS WAP preauthPublish an IWA app externally with federation at the edgeAD FS relying party, WAP, backend over Kerberos, optional compound auth/claims when needed. [learn.microsoft.com], [learn.microsoft.com]Entra App Proxy + KCDCloud preauth + on‑prem Kerberos backend SSO (no VPN)Domain‑joined Connector, KCD configured, correct SPNs, app supports IWA. [learn.microsoft.com]WAM + WebView2Consistent app sign‑in UX on Windows 11 with modern webWindows cumulative update (KB5072033+) and WebView2 runtime present. [techcommun...rosoft.com]Entra Kerberos (Azure Files)SMB shares with Entra identities, no DC line‑of‑sightStorage account configured for Entra Kerberos, meet preview prerequisites. [learn.microsoft.com]

🔒 6) Hardening checklist (Kerberos‑first without surprises)

Prefer Kerberos via Negotiate: keep Negotiate first, maintain SPNs, and configure browsers for WIA; this avoids NTLM fallback. [learn.microsoft.com], [woshub.com]
Track the NTLM exit ramp: Microsoft is phasing out NTLM (audit → compatibility fixes like IAKerb/Local KDC → disabled by default in future Windows), so reduce dependencies now. [calcomsoftware.com]
Keep CredSSP patched: enforce Encryption Oracle Remediation and ensure both clients/servers are current to prevent RDP failures and exposure. [support.mi...rosoft.com]
Be precise with KCD: scope delegation only to necessary SPNs and validate no duplicate SPNs exist to avoid ticketing failures. [learn.microsoft.com]
Browser posture matters: use AuthServerAllowlist / DelegateAllowlist for Edge/Chrome, and add sites to Intranet/Trusted Sites for automatic logon. [documentat...eprism.com], [learn.microsoft.com]


🎬 7) Animation Placeholder
(Add later using GIF/Notebook‑LLM)
[Animation Placeholder: "Bridging tokens and tickets"]
Scene 1 → Browser → IIS (Negotiate: Kerberos) → silent WIA
Scene 2 → MSTSC → TLS → CredSSP (Kerberos) → tools run without prompts
Scene 3 → Cloud login (OIDC/SAML) → App Proxy → KCD to backend
Scene 4 → Windows app → WAM (WebView2) → token → resource


🔧 8) Quick Admin Snippets (Copy‑ready)

A) IIS: prefer Kerberos

PowerShell# Enable Windows Authentication and order providers# IIS Manager → Site → Authentication → Enable "Windows Authentication"# Providers → Move "Negotiate" to the top (above NTLM)``Show more lines
(Negotiate chooses Kerberos when SPN/UPN is present; NTLM is fallback.) [woshub.com], [learn.microsoft.com]

B) Register HTTP SPNs for a custom app pool identity

BATsetspn -S HTTP/webportal.contoso.com CONTOSO\svc_iissetspn -S HTTP/webportal CONTOSO\svc_iissetspn -X   :: check for duplicatesShow more lines
(SPNs must be unique; duplicates break Kerberos and cause NTLM fallback.) [woshub.com]

C) Edge/Chrome allowlists for WIA

Plain Textreg isn’t fully supported. Syntax highlighting is based on Plain Text.Windows Registry Editor Version 5.00[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Edge]"AuthServerAllowlist"="webportal.contoso.com""AuthNegotiateDelegateAllowlist"="webportal.contoso.com"[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome]"AuthServerAllowlist"="webportal.contoso.com""AuthNegotiateDelegateAllowlist"="webportal.contoso.com"Show more lines
(Allows SPNEGO/Negotiate and delegation to trusted hosts.) [documentat...eprism.com]

D) CredSSP “Encryption Oracle Remediation” (Group Policy path)
Computer Configuration → Administrative Templates → System → Credentials Delegation → Encryption Oracle Remediation (set to Mitigated or Force Updated Clients, after patching). [support.mi...rosoft.com]


E) Entra App Proxy + KCD (high‑level)

Plain Text1) Publish app via Entra App Proxy (Pre‑Auth = Entra ID)2) Configure SSO method = Integrated Windows Authentication (KCD)3) On connector's AD account: grant delegation "to specified services"   (HTTP/backend.contoso.com) and verify SPNs on backendShow more lines
(Cloud preauth + on‑prem Kerberos with KCD.) [learn.microsoft.com]

F) MSAL + WAM on Windows (value props)

C#// MSAL calls WAM for OS-brokered SSO; supports Hello/FIDO and CA// See: Microsoft.Identity.Client + WAM integration docsShow more lines
(WAM is the Windows broker enabling fast SSO with OS accounts.) [learn.microsoft.com]

🧵 9) Mind Map (Placeholder)
(Will be converted to GIF later)
Modern Windows SSO
 ├─ Negotiate/SPNEGO → Kerberos-first (fallback NTLM)
 │   └─ IIS provider order + SPNs + browser allowlists
 ├─ CredSSP → TLS + SPNEGO + credential delegation (RDP)
 │   └─ Patch CVE-2018-0886 (encryption oracle remediation)
 ├─ Web SSO bridges
 │   ├─ AD FS WAP preauth → Kerberos to backend
 │   └─ Entra App Proxy + KCD
 └─ Modern blocks
     ├─ WAM + WebView2 sign-in on Windows 11
     └─ Entra Kerberos (Azure Files) / Cloud Kerberos Trust


References (selected)

Negotiate (SSPI) & SPNEGO (HTTP “Negotiate”) — Microsoft docs and RFC 4559. [learn.microsoft.com], [rfc-editor.org]
IIS Kerberos/WIA configuration & SPNs — Windows OS Hub and IIS Support Blog. [woshub.com], [techcommun...rosoft.com]
Browser WIA allowlists / AD FS WIA user‑agents — Microsoft Learn and Blue Prism/Specops examples. [learn.microsoft.com], [documentat...eprism.com], [specopssoft.com]
CredSSP protocol & RDP usage — MS‑RDPBCGR and MS‑CSSP. [learn.microsoft.com], [learn.microsoft.com]
CredSSP CVE‑2018‑0886 remediation — Microsoft Support and NVD/CVE records. [support.mi...rosoft.com], [nvd.nist.gov]
AD FS WAP preauth (claims edge → Kerberos backend). [learn.microsoft.com]
Microsoft Entra Application Proxy + KCD — How‑to and GitHub docs. [learn.microsoft.com], [github.com]
WAM (broker) & WebView2 sign‑ins — Identity platform/WAM docs and Windows IT Pro Blog. [learn.microsoft.com], [techcommun...rosoft.com]
Entra Kerberos (Azure Files) — Microsoft Learn preview guidance. [learn.microsoft.com]
NTLM deprecation roadmap (Kerberos‑first) — Windows IT Pro Blog. [calcomsoftware.com]
