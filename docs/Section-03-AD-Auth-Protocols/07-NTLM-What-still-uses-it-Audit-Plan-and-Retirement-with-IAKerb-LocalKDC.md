📘 Section 03 — AD Authentication Protocols
Chapter 07 — NTLM: What still uses it, how to audit it, and a phased retirement plan (with IAKerb/Local KDC)
(Medium Depth, aligned with earlier AD chapters)

🔰 1) Introduction
NTLM is a legacy Windows challenge–response authentication protocol. It still appears in modern estates due to fallbacks, legacy devices/apps, and non‑domain scenarios. This chapter covers:

What still uses NTLM (practical inventory)
How to audit NTLM usage (events, policies, and signals)
A phased retirement plan to minimize or eliminate NTLM
Where IAKerb and Local KDC can help you keep Kerberos even when the client cannot reach a domain controller


🧠 2) Why It Matters

NTLM lacks strong mutual authentication and is vulnerable to relay and pass‑the‑hash techniques.
NTLM frequently appears when Kerberos breaks (SPN/DNS/time issues), so removing NTLM forces you to fix the real causes.
Auditors increasingly expect a roadmap to deprecate NTLM and evidence that you’re monitoring and restricting it.


🧩 3) Core Concepts (Quick Ref)

NTLMv2 — the only acceptable variant when you can’t avoid NTLM (v1/LM must be disabled).
Fallback — Windows “Negotiate” chooses Kerberos first; if it fails, it falls back to NTLM.
IAKerb — a Kerberos extension where the application server proxies to the KDC on behalf of the client; helps when clients cannot contact a KDC directly (firewalls/DMZ).
Local KDC (LKDC) — a host‑local Kerberos KDC implementation (platform/vendor‑specific) that can satisfy Kerberos for local/isolated scenarios, reducing reliance on NTLM.
Signing/EPA/CBT — protocol hardening (SMB/LDAP signing, HTTP Extended Protection, Channel Binding) that breaks NTLM relay and encourages Kerberos.


🏗️ 4) How NTLM Shows Up (and Why Kerberos Didn’t)
Common sources still using NTLM:

NAS / filers / printers / scanners that only speak NTLM or lack proper SPN/Kerberos config
Legacy apps on IIS/HTTP configured for “NTLM” instead of “Negotiate (Kerberos)”
Proxies/WAFs terminating auth with NTLM for intranet SSO
Workgroup or non‑domain joined machines using local accounts
RDP/WinRM/SMB when SPNs are wrong, there’s time drift, or duplicate SPNs
Cross‑network/perimeter where clients cannot reach a KDC (firewall/DMZ)

Kerberos typically fails due to:
SPN errors, DNS/SRV issues, time skew (±5 min), unsupported cipher suites (RC4/AES mismatch), or application misconfiguration (forcing NTLM).

🔐 5) Security Risks / Common Attack Patterns

NTLM Relay: Adversary relays a victim’s NTLM handshake to another service to gain access (especially where signing or EPA/CBT isn’t enforced).
Pass‑the‑Hash (PtH): Using the NT hash to authenticate without knowing the password.
Downgrade/Fallback: Attack paths that force NTLM by breaking Kerberos pre‑conditions.
Lack of mutual auth: Easier to spoof endpoints versus Kerberos with service tickets/SPNs.


🛡️ 6) Hardening & Best Practices (Baseline)
Kill legacy variants

Refuse LM/NTLMv1 everywhere (GPO/registry).
Enforce NTLMv2 only if NTLM is unavoidable.

Force strong channel protections

SMB: Require signing (client/server “always”).
LDAP (DCs): Require signing and channel binding.
HTTP/IIS: Prefer Negotiate (Kerberos); enable Extended Protection for Authentication (EPA); bind to SPNs.
Disable WDigest, deploy Credential Guard on endpoints.

Prefer Kerberos everywhere

Fix SPNs/DNS/time first.
Use gMSA for services; prefer AES over RC4.
For “can’t‑reach‑KDC” scenarios, explore IAKerb or Local KDC patterns (details below).


🛠️ 7) Operations — Audit, Events & Troubleshooting
A) Turn on NTLM auditing (domain‑wide)
Group Policy → Security Options → Network security: Restrict NTLM: Audit NTLM authentication in this domain → Enable
(Do this before you deny/disable NTLM.)
B) Collect the right events

On DCs/servers (Security log):

4776 — NTLM authentication to a DC
4624 — Successful logon → Authentication Package: NTLM (watch Logon Type; 3 = network)
4625 — Failed logon (with NTLM package details)


(Optional) Applications and Services Logs → Microsoft → Windows → NTLM/Operational (if present in your build)
SMB/LDAP/IIS logs for signing/EPA/CBT status (to spot relay‑prone endpoints)

C) Hunting ideas

Top NTLM callers by host/app/user
NTLM against DCs (should be minimal; alert on spikes)
NTLM where Kerberos is expected (per app/URL/share)
HTTP/IIS services returning WWW‑Authenticate: NTLM without Negotiate

D) First‑aid troubleshooting

Kerberos expected but NTLM used → check SPN, DNS, time sync, cipher config on the service account.
DC sees many 4776 from one host → isolate and analyze app/agent on that host.
SMB/LDAP shows no signing → enable signing/CBT and test (this will also break relays).


🧭 8) Phased NTLM Retirement Plan (Pragmatic)

Goal: Maximize Kerberos, constrain NTLM to audited exceptions only, then enforce.

Phase 1 — Visibility (2–4 weeks)

Enable “Audit NTLM authentication in this domain”.
Centralize 4776/4624/4625 to SIEM.
Build a Top NTLM sources report (hosts, apps, device types).
Identify Kerberos‑should‑be cases: SMB shares, IIS sites, LDAP binds.

Phase 2 — Fix Kerberos (4–8 weeks)

SPN hygiene (setspn -L <account>): add missing, remove duplicates.
DNS/time: fix drift (±5 minutes) and SRV records.
HTTP/IIS: switch to Negotiate, add SPNs for HTTP/host, enable EPA.
SMB/LDAP: enforce signing and CBT; test clients.
Service accounts: move to gMSA, prefer AES; drop RC4.
Perimeter/DMZ: if clients cannot reach KDCs, evaluate IAKerb or Kerberos proxy; for special platforms, evaluate Local KDC options.

Phase 3 — Contain NTLM (2–6 weeks)

Domain policy: Refuse LM & NTLMv1; allow only NTLMv2 where needed.
Restrict NTLM (domain GPOs):

Start with Audit, then move to Deny in scoped OUs.
Maintain a documented exceptions list (explicit allowlist by SPN/host).


Network: segment NTLM‑only devices (NAS/printers) behind proxies or limited VLANs.

Phase 4 — Enforce (ongoing)

Switch Restrict NTLM to Deny domain‑wide (except approved exceptions).
Block outbound NTLM from Tier‑0/Tier‑1 servers.
Quarterly review: remove stale exceptions; keep the SIEM dashboards live.


🧩 9) Where IAKerb & Local KDC Fit (to avoid NTLM)
Problem: Some clients can’t reach a KDC (firewalls/DMZ/isolated networks), so they fall back to NTLM.
Better option: Keep Kerberos by introducing a proxy or local KDC model.
IAKerb (Kerberos with server proxy)

The application server (that can reach a DC) proxies the client’s Kerberos exchanges to the KDC.
Useful when client → DC is blocked, but server ↔ DC is allowed.
Net effect: client still gets Kerberos, not NTLM.
Actions: Confirm app/server stack supports IAKerb (SSPI/GSS), ensure SPNs are correct, and DC reachability exists from the server.

Local KDC (LKDC)

A host‑local KDC implementation (varies by platform/vendor) that can issue/validate tickets for a local realm or tightly scoped use cases.
Useful for appliance‑style or isolated environments, reducing the need for NTLM or plaintext binds.
Actions: Check your OS/vendor docs for LKDC support and realm mapping; integrate with your directory if supported; test ticket issuance and service validation.


Tip: In perimeter scenarios, you can also evaluate Kerberos over HTTP (KDC proxy) patterns where available; the objective is the same—keep Kerberos, avoid NTLM.


🧱 10) Configuration Cheat‑Sheet (quick copy)
Refuse LM/NTLMv1; require NTLMv2
Plain Textreg isn’t fully supported. Syntax highlighting is based on Plain Text.; Domain/Local Policy → Security Options → LAN Manager auth level; Send NTLMv2 response only. Refuse LM & NTLM[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa]"LmCompatibilityLevel"=dword:00000005Show more lines
SMB signing (client & server “always”)

Computer Configuration → Windows Settings → Security Settings → Local Policies → Security Options

Microsoft network client: Digitally sign communications (always) → Enabled
Microsoft network server: Digitally sign communications (always) → Enabled



LDAP hardening (DCs)

Domain controller: LDAP server signing requirements → Require signing
Domain controller: LDAP server channel binding token → Required

Restrict NTLM (domain)

Audit first → then Deny (with explicit exceptions).
Keep a version‑controlled exceptions register.


🧾 11) Summary

NTLM persists due to legacy devices/apps and Kerberos pre‑req failures.
Start with auditing, fix Kerberos hygiene (SPN/DNS/time/ciphers), and enforce signing/EPA/CBT to kill relays.
Use IAKerb, Local KDC, or Kerberos proxy patterns to preserve Kerberos where direct KDC access isn’t possible.
Move from Audit → Contain → Enforce, leaving documented exceptions only.
