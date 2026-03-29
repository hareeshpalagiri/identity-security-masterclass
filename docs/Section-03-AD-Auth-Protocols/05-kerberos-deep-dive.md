📘 05 — Kerberos Deep‑Dive (tickets, SPNs, PAC, delegation, IAKerb, Local KDC, and modern hardening)
A simple, deep, story‑based explanation using strategic Mahabharata analogies — GitBook Ready

🏹 Mahabharata Story Analogy (Strategic Only)
Think of Kerberos as Hastinapura’s sealed travel‑orders system.

A central royal registrar (KDC) issues a pass (TGT) after verifying identity. [learn.microsoft.com]
The traveler exchanges that pass for destination‑specific orders (service tickets) to enter temples, granaries, or archives. [learn.microsoft.com]
Each order contains a privilege scroll (PAC) listing the bearer’s clans and roles, so gatekeepers can decide “what you may do” without calling the registrar again. [learn.microsoft.com]
Occasionally, a herald (front‑end service) must act on your behalf to another hall — that’s delegation — but only to named halls under strict conditions. [learn.microsoft.com]


🔐 1. What is Kerberos? (Simple Definition)
Kerberos v5 is the default Windows domain authentication protocol that uses tickets issued by a Key Distribution Center (KDC) to provide mutual authentication between users and services without sending passwords on the wire. 
Windows extends Kerberos with authorization data (PAC), Service Principal Names (SPNs) for targeting services, and delegation mechanisms for tiered apps. [learn.microsoft.com] [learn.microsoft.com], [learn.microsoft.com], [learn.microsoft.com]

🧭 2. Ticket Anatomy: TGT, Service Ticket & PAC

TGT (Ticket‑Granting Ticket): Issued after initial sign‑in, it lets the client request service tickets without re‑entering secrets. [learn.microsoft.com]
Service ticket (TGS): Presented to the target service; includes the PAC so the service can build an access token locally. [learn.microsoft.com]
PAC (Privilege Attribute Certificate): Holds SIDs and group memberships; PAC validity is verified (PAC signature checked) during access, and Microsoft has tightened validation in recent updates to address CVE‑2024‑26248/29056. [learn.microsoft.com], [support.mi...rosoft.com]


🎬 3. Animation Placeholder
(Add later using GIF/Notebook‑LLM)
[Animation Placeholder: "A day in the life of a Kerberos ticket"]
Scene 1 → Logon → TGT from KDC
Scene 2 → Request TGS for HTTP/app → ticket contains PAC
Scene 3 → Service validates PAC → builds access token
Scene 4 → Front end uses constrained delegation to back end


🧩 4. SPNs (Service Principal Names) — Targeting the Right Service
SPNs are unique identifiers (e.g., HTTP/app.contoso.com) stored on the service account that let the KDC find the right principal when issuing a ticket; correct SPN registration is essential for Kerberos to work (and to avoid NTLM fallback). 
Manage SPNs with setspn and ensure uniqueness; stale or duplicate SPNs cause ticketing failures and may open doors to Kerberoasting if misused. [learn.microsoft.com] [learn.microsoft.com], [4sysops.com]

🧠 5. Delegation (S4U) — Acting on a User’s Behalf
Kerberos supports constrained delegation so a front‑end service can act as a user only to specific back‑end SPNs using S4U2proxy, and — if protocol transition is enabled — it can map non‑Kerberos logons into Kerberos via S4U2self. 
Resource‑based constrained delegation (RBCD) moves control to the back‑end service (msDS‑AllowedToActOnBehalfOfOtherIdentity), enabling cross‑domain scenarios with less central admin involvement. 
Microsoft provides step‑by‑step KCD/RBCD configuration and troubleshooting guidance (including SPN setup and “Kerberos‑only” vs “protocol transition”). [learn.microsoft.com] [learn.microsoft.com], [learn.microsoft.com]

Red‑team context: Unconstrained delegation is dangerous; prefer KCD/RBCD and keep delegations tightly scoped to the minimum SPNs. [learn.microsoft.com]


🌐 6. When DC Line‑of‑Sight Breaks: IAKerb, Local KDC & KDC Proxy

IAKerb lets a client without direct DC connectivity proxy Kerberos messages through a server that does have DC line‑of‑sight, removing a classic reason for NTLM fallback. [techcommun...rosoft.com]
A Local KDC enables Kerberos for local accounts by leveraging the local SAM, again shrinking NTLM dependency; these features are part of Microsoft’s Kerberos‑first roadmap. [techcommun...rosoft.com], [expertinsights.com]
KDC Proxy (KKDCP) tunnels Kerberos over HTTPS to a DC, useful for Remote Desktop/Azure Virtual Desktop and segmented networks; Microsoft documents the protocol and deployment patterns. [learn.microsoft.com], [learn.microsoft.com]


⚙️ 7. Modern Hardening (2024–2026): Encryption, Armoring, PAC & NTLM Exit
7.1 Stronger encryption — RC4 → AES
Microsoft is flipping Kerberos defaults to AES‑SHA1 and phasing out RC4, with official guidance to audit and remediate RC4 usage ahead of enforcement. 
Industry coverage and Microsoft comms indicate enforcement phases in 2026, with audit then enforcement and removal of rollback, so identify legacy accounts/devices that still rely on RC4 now. [learn.microsoft.com] [securityweek.com], [neowin.net]
7.2 Kerberos Armoring (FAST)
FAST/Armoring creates a protected tunnel for pre‑auth and ticket exchanges, mitigating manipulation and some roasting techniques; enable via Group Policy on KDC and clients in modern domains. 
Microsoft documentation and community guidance position armoring as a prerequisite for secure claims/compound auth features as well. [hub.trimar...curity.com], [docs.oneidentity.com] [learn.microsoft.com], [enowsoftware.com]
7.3 PAC validation hardening
Microsoft’s 2024–2025 updates enforced stronger PAC signature validation to mitigate spoofing and cross‑forest issues; move to Enforced mode after updating DCs and clients. [support.mi...rosoft.com]
7.4 NTLM deprecation → Kerberos‑first
Microsoft’s three‑phase plan: enhanced NTLM auditing (now), then IAKerb + Local KDC to close gaps, then disable network NTLM by default in future Windows releases, with explicit re‑enable controls. [techcommun...rosoft.com]

🔒 8. Practical Hardening Checklist (Kerberos‑first)

Inventory & fix SPNs: Remove duplicates; register HTTP/host aliases properly (both short/FQDN) to avoid NTLM fallback. [learn.microsoft.com]
Prefer KCD/RBCD over unconstrained delegation, and scope allowed SPNs narrowly; review msDS‑AllowedToDelegateTo and msDS‑AllowedToActOnBehalfOfOtherIdentity regularly. [learn.microsoft.com]
Enable FAST (Kerberos armoring) KDC‑wide and client‑wide once your forest supports it; validate app compatibility. [hub.trimar...curity.com]
Disable RC4 where possible; run Microsoft’s RC4 usage audits and ensure service accounts have AES keys (rotate old passwords). [learn.microsoft.com]
Harden PAC validation: complete client/DC patching and switch to Enforced after reviewing audit events. [support.mi...rosoft.com]
Plan for IAKerb/Local KDC in remote, local‑account, or segmented scenarios to remove NTLM gaps. [techcommun...rosoft.com]
Use KDC Proxy for external/remote RDP/AVD Kerberos where DC ports aren’t exposed. [learn.microsoft.com]


🔧 9. Quick Admin Snippets (Copy‑ready)

A) List & fix SPNs (examples)

Shell# List SPNs on an accountsetspn -L SVC_WebApp            # review existing mappings# Add HTTP SPNs (short + FQDN) to a service accountsetspn -S HTTP/app.contoso.com CONTOSO\svc_websetspn -S HTTP/APP CONTOSO\svc_webShow more lines
(Ensure uniqueness; duplicates cause ticket failures.) [learn.microsoft.com]

B) Find accounts configured for KCD (PowerShell snippets)

PowerShellGet-ADUser -Filter {msDS-AllowedToDelegateTo -like '*'} -Properties msDS-AllowedToDelegateTo,TrustedToAuthForDelegationGet-ADComputer -Filter {msDS-AllowedToDelegateTo -like '*'} -Properties msDS-AllowedToDelegateTo,TrustedToAuthForDelegationShow more lines
(Review Kerberos‑only vs Protocol Transition, and narrow target SPNs.) [compass-security.com]

C) Enable Kerberos armoring (FAST) via GPO


KDC: Computer Configuration → Policies → Administrative Templates → System → KDC → Fail unarmored authentication requests (enforce). [docs.oneidentity.com]
Clients: Computer Configuration → Policies → Administrative Templates → System → Kerberos → Kerberos client support for claims, compound auth, and Kerberos armoring (enable). [hub.trimar...curity.com]


D) Detect & remediate RC4 usage (prepare for 2026 enforcement)
Follow Microsoft’s guide to audit Event Logs and update accounts to AES‑SHA1; disable RC4 where feasible. [learn.microsoft.com]


E) PAC validation hardening
Patch DCs/clients to April 2024 or later and progress to Enforced mode per KB5037754. [support.mi...rosoft.com]


F) KDC Proxy (KKDCP) references
Use KKDCP to proxy Kerberos over HTTPS (e.g., RDS/AVD scenarios). [learn.microsoft.com], [learn.microsoft.com]


🧵 10. Mind Map (Placeholder)
(Will be converted to GIF later)
Kerberos Deep‑Dive
 ├─ Tickets: TGT, TGS (+ PAC)
 │   └─ PAC validation hardening (2024–25)
 ├─ SPNs: registration, uniqueness
 ├─ Delegation:
 │   ├─ Constrained (S4U2self/S4U2proxy)
 │   └─ RBCD (cross-domain friendly)
 ├─ Kerberos in tough topologies:
 │   ├─ IAKerb (no DC line-of-sight)
 │   ├─ Local KDC (local accounts via Kerberos)
 │   └─ KDC Proxy (HTTPS tunneling)
 └─ Hardening:
     ├─ RC4 → AES defaults (2026)
     ├─ FAST/Armoring
     └─ NTLM deprecation → Kerberos-first


References (selected)

Constrained & resource‑based constrained delegation (S4U2proxy/S4U2self) — Microsoft Learn and GitHub docs. [learn.microsoft.com], [github.com]
KCD configuration/troubleshooting — SPN and delegation setup guidance. [learn.microsoft.com], [learn.microsoft.com]
PAC structure & validation — MS‑PAC and MS‑APDS; PAC hardening KB. [learn.microsoft.com], [learn.microsoft.com], [support.mi...rosoft.com]
SPN management — setspn usage and best practices. [learn.microsoft.com]
IAKerb & Local KDC — Windows IT Pro blog and coverage of Kerberos‑first roadmap. [techcommun...rosoft.com], [4sysops.com]
KDC Proxy (KKDCP) — Protocol spec and AVD/RDS guidance. [learn.microsoft.com], [learn.microsoft.com]
RC4 → AES hardening — Detect/remediate RC4 usage; 2026 rollout reporting. [learn.microsoft.com], [securityweek.com]
Kerberos armoring (FAST) — What it is, why, and how to enable. [hub.trimar...curity.com], [docs.oneidentity.com]
