📘 04 — Active Directory Certificate Services (AD CS)
PKI for identity: CAs, templates, enrollment, revocation, and hardening — GitBook Ready

🏹 Mahabharata Story Analogy (Strategic Only)
Picture Hastinapura’s seal office that forges royal signets used across the kingdom to prove who’s who and what’s genuine.

The offline royal mint = Offline Root CA (ultimate trust, rarely powered on).
The daily seal desk = Issuing CA (signs most requests).
Heralds = enrollment services (web/RPC/SCEP) that carry petitions.
Notice boards with revocation lists = CRL/OCSP so subjects can check if a seal is still valid.
Secure the mint, restrict who can request which seals, and publish revocations reliably — or impostors will roam free. [techcommun...rosoft.com], [learn.microsoft.com]


🔐 1. AD CS in one paragraph (Simple Definition)
Active Directory Certificate Services (AD CS) is the Windows Server role that issues and manages X.509 certificates for encryption, signing, and authentication. It includes Certification Authorities (root/subordinate; enterprise/standalone), Web/Enrollment services, Online Responder (OCSP), and Network Device Enrollment Service (NDES/SCEP), enabling automated issuance via templates and AD integration. [learn.microsoft.com], [learn.microsoft.com]

🧭 2. Architecture at a glance

Two‑tier hierarchy: Offline Root CA (trust anchor) signs online Issuing CA(s); this is the most common, secure and manageable design. Keep the root off network, publish its CRL on schedule, and use the issuing CA for day‑to‑day certificates. [techcommun...rosoft.com], [techcommun...rosoft.com]
Enterprise vs Standalone CA: Enterprise CAs integrate with AD (templates, autoenrollment, smart card sign‑in), while Standalone CAs don’t use templates and typically require manual approval. [learn.microsoft.com]
Critical publication points: CDP (CRL Distribution Points) and AIA (Authority Information Access) must be reachable and kept fresh; certificate validation breaks if CRLs expire or endpoints go down. [techcommun...rosoft.com], [learn.microsoft.com]


🎬 3. Animation Placeholder
(Add later using GIF/Notebook‑LLM)
[Animation Placeholder: "Two-tier PKI lifecycle"]
Scene 1 → Offline Root signs Issuing CA
Scene 2 → Issuing CA signs user/computer/server certs via templates
Scene 3 → Clients check AIA (chain) + CDP/OCSP (revocation)
Scene 4 → Hardening: template scoping, EPA on web endpoints, auditing


🧠 4. Core Components (Simple + Deep)
4.1 Certification Authorities

Root CA (often Standalone, offline) → signs only the issuing CA(s) and publishes long‑lived CRLs. Do not keep it on the network. [techcommun...rosoft.com], [techcommun...rosoft.com]
Issuing CA (Enterprise, online) → uses certificate templates and AD to automate enrollment and renewal. [learn.microsoft.com]

4.2 Enrollment paths

RPC/DCOM enrollment (classic) and Web/CES endpoints for domain or remote clients. NDES/SCEP enables non‑domain devices (routers, MDM/Intune devices) to get certs. [learn.microsoft.com], [learn.microsoft.com]
Autoenrollment via GPO for users/computers: enables issuance/renewal at scale. [learn.microsoft.com]

4.3 Revocation checking

CRLs (HTTP/LDAP/file) must be published reliably; OCSP provides real‑time status via the Online Responder role and an OCSP Response Signing certificate. [techcommun...rosoft.com], [learn.microsoft.com]


🧩 5. Templates & Autoenrollment (What to configure, and why it matters)

Templates define subject, validity, EKUs, issuance requirements (e.g., Manager approval, authorized signatures), and permissions (Enroll/Autoenroll/Read). These drive who can request what, for which purpose, and how approval happens. [learn.microsoft.com]
Autoenrollment (GPO):

Computer Configuration → Public Key Policies → Certificate Services Client – Auto‑Enrollment = Enabled, Renew expired, Update pending, Update templates. Repeat under User Configuration as needed. [learn.microsoft.com]
Common pitfall: with Manager approval templates, ensure the autoenrollment policy revisits pending→issued state so clients retrieve approved certs automatically. [en.ittrip.xyz]


Web server/SSL or NPS/EAP‑TLS: prefer duplicating modern v2+ templates (not legacy v1) and granting minimal Enroll/Autoenroll permissions to scoped groups only. [4sysops.com]


🌐 6. CRL / AIA / OCSP — Keep validation fast and reliable

Plan CDP/AIA URLs (HTTP paths, DNS names, overlapping CRL validity) and monitor expirations. If CRLs expire or locations are down, validation fails. [techcommun...rosoft.com]
Configure CDP/AIA properly on CA properties (Extensions tab), publish to HTTP paths clients can reach, and include the right “Include in…” checkboxes for chain building and delta CRLs. [learn.microsoft.com]
OCSP (Online Responder) improves revocation freshness; set the AIA OCSP URL and issue the OCSP Response Signing template to the responder. [learn.microsoft.com], [petenetlive.com]


Scaling tip (optional): Host CDP/AIA on highly available web endpoints (on‑prem + cloud) or DFS+IIS pattern for resiliency and low latency. [pkisolutions.com]


📡 7. Device Certificates with NDES/SCEP (Routers, MDM/Intune, IoT)

NDES is Microsoft’s SCEP RA that brokers cert requests from devices without AD credentials to your CA. It runs as an IIS ISAPI app, generates OTPs, submits/retrieves certs, and delivers them back to devices. [learn.microsoft.com]
Intune + SCEP: use the Intune Certificate Connector; newer strong mapping requirements (KB5014754) add a SAN URL tag to tie the cert to a device/user SID. Ensure your CA supports it (AD CS updated with KB5014754). [learn.microsoft.com]
Service account option for NDES (recommended) requires permissions on CA/template and IIS_IUSRS membership; configure SPN if using a CNAME/LB name. [learn.microsoft.com]


⚔️ 8. Modern Attack Paths & What to Fix (Before red teams find it)
8.1 Template abuse (ESC1–ESC3 and friends)

ESC1 — template allows requester‑supplied subject/SAN + has client‑auth EKUs + broad Enroll → attacker requests a cert as any user and authenticates. Mitigate: remove Supply in request, restrict EKUs, require manager approval, scope permissions. [specterops.io], [netscylla.com]
ESC2/ESC3 — overly permissive EKUs (AnyPurpose) or Enrollment Agent misuse to enroll on behalf of privileged users. Mitigate: restrict EKUs, require approval, add Enrollment Agent restrictions at CA, and lock down who holds CRA EKU. [specterops.io], [github.com]


Defender for Identity can assess insecure templates/CA ACLs (e.g., ESC7/ESC8/ESC11) and recommend fixes. [learn.microsoft.com]

8.2 Web endpoint NTLM relay (ESC8 / PetitPotam chains)

AD CS Web Enrollment/CES endpoints can be targeted by NTLM relay (e.g., coerced auth via EFSRPC → relay to AD CS → issue DC cert). Mitigate: Enable Extended Protection for Authentication (EPA), Require SSL, and ideally disable NTLM for those sites. See KB5005413. [support.mi...rosoft.com]
Community and vendor guidance reinforce EPA and limiting DC outbound/coercion vectors for PetitPotam. [truesec.com], [success.tr...dmicro.com]

8.3 Strong certificate mapping changes (KB5014754 era)

Post‑KB5014754, Windows pushes strong mapping to reduce weak SAN‑based impersonation; Intune SCEP profiles add a SAN URL tag bound to SID. Plan for mapping modes and avoid disabling enforcement. [learn.microsoft.com]


🛡 9. Hardening Checklist (Practical Steps)
9.1 PKI design & CA security

Two‑tier with offline root; strictly control root ceremonies and CRL publication. [techcommun...rosoft.com], [techcommun...rosoft.com]
Treat AD CS servers as Tier‑0; audit CA/DB access, enable role separation, and regularly review template ACLs. [techcommun...rosoft.com]

9.2 Templates & issuance

Minimize templates that permit requester‑supplied subject/SAN; for any that must, add manager approval and limit Enroll to scoped groups. [specterops.io]
For Enrollment Agent, apply CA‑level Enrollment Agent restrictions; keep CRA holders minimal and monitored. [github.com]

9.3 Web endpoints (IIS)

For Certsrv/CES/NDES, Require SSL and EPA, prefer Negotiate(Kerberos) over NTLM or disable NTLM, and review app‑pool/service account hardening. [support.mi...rosoft.com]

9.4 Enrollment channels

Keep RPC enrollment with packet privacy enforced (IF_ENFORCEENCRYPTICERTREQUEST) to prevent relays on the RPC interface (ESC11). [learn.microsoft.com]

9.5 Revocation publishing

Host CDP/AIA on highly available HTTP endpoints; monitor CRL expirations; add OCSP where latency or freshness matters. [techcommun...rosoft.com], [learn.microsoft.com]

9.6 Key archival (for encryption keys)

If you archive private keys (e.g., for S/MIME/EFS), configure KRA certificates and understand lifecycle: only KRAs present at archival time can decrypt that item later. Separate CA manager (retrieve blob) vs KRA (decrypt). [learn.microsoft.com], [techcommun...rosoft.com]


🧩 10. Smart Card, Mapping & UPN

Windows smart‑card sign‑in requires specific cert properties (UPN in SAN, smart‑card logon EKU, etc.) and a valid KDC certificate in the domain. [learn.microsoft.com]
For Microsoft Entra CBA and hybrid scenarios, Windows decides which UPN to send and may rely on hints; ensure UPNs and mappings are consistent. [learn.microsoft.com]


🔧 11. Quick Admin Snippets (Copy‑ready)

Enable computer & user autoenrollment (GPO)

Plain TextGPO → Computer Configuration → Policies → Windows Settings → Security Settings → Public Key Policies  ▸ Certificate Services Client – Auto‑Enrollment = Enabled     [x] Renew expired, update pending, remove revoked     [x] Update certificates that use certificate templates(Repeat under User Configuration if needed)Show more lines
 [learn.microsoft.com]

Harden RPC enrollment interface (ESC11)

BATcertutil -setreg CA\InterfaceFlags +IF_ENFORCEENCRYPTICERTREQUESTnet stop certsvc & net start certsvcShow more lines
 [learn.microsoft.com]

Web endpoints (IIS) — EPA + Require SSL (ESC8/PetitPotam)


Enable Extended Protection for Authentication (EPA) on Certsrv/CES sites and Require SSL; prefer Negotiate:Kerberos. [support.mi...rosoft.com]


OCSP AIA URL example (on CA Properties → Extensions)


Add http://pki.contoso.com/ocsp and check “Include in the online certificate status protocol (OCSP) extension.” [petenetlive.com]


CDP/AIA baseline


Publish CRLs to http://pki.contoso.com/pki/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl and include in CDP extension of issued certs. [learn.microsoft.com]


NDES basics


Install NDES, run as a service account with Enroll on the NDES template; protect the IIS app and OTP flow with TLS. [learn.microsoft.com], [learn.microsoft.com]


Key archival


Issue KRA cert(s), enable Archive subject’s encryption private key on relevant templates, and remember KRA presence is not retroactive. [itprotoday.com], [techcommun...rosoft.com]


🧵 12. Mind Map (Placeholder)
(Will be converted to GIF later)
AD CS
 ├─ Design: Offline Root → Issuing CA(s)
 ├─ Enrollment:
 │   ├─ RPC/DCOM, Web (CES), NDES/SCEP
 │   └─ Autoenrollment via GPO
 ├─ Control plane:
 │   ├─ Templates (EKUs, issuance, permissions)
 │   └─ CA & template ACLs (tight)
 ├─ Validation:
 │   ├─ AIA (chain)
 │   └─ CDP (CRL) + OCSP (Online Responder)
 ├─ Security:
 │   ├─ EPA on web endpoints (ESC8)
 │   ├─ Strong mapping (KB5014754 path)
 │   ├─ RPC packet privacy (ESC11)
 │   └─ Key archival with KRA


References (selected)

AD CS overview, roles & features. [learn.microsoft.com], [learn.microsoft.com]
CA types (enterprise/standalone), root/subordinate. [learn.microsoft.com]
Two‑tier design & offline root guidance. [techcommun...rosoft.com], [techcommun...rosoft.com]
Autoenrollment (GPO) configuration. [learn.microsoft.com]
CDP/AIA & CRL availability best practices. [techcommun...rosoft.com], [learn.microsoft.com]
OCSP/Online Responder. [learn.microsoft.com]
NDES/SCEP overview & Intune strong mapping. [learn.microsoft.com], [learn.microsoft.com]
PetitPotam/ESC8 mitigations (EPA/Require SSL/disable NTLM). [support.mi...rosoft.com]
Template abuse (ESC1–ESC3) background & mitigations. [specterops.io], [github.com]
RPC enrollment packet privacy (ESC11). [learn.microsoft.com]
Key archival & KRA lifecycle. [learn.microsoft.com], [techcommun...rosoft.com]
Smart card requirements & Entra CBA UPN behavior. [learn.microsoft.com], [learn.microsoft.com]
