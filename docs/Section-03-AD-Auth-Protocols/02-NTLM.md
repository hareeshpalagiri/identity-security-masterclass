Chapter 02 — NTLM (Medium Depth)

🔰 1) What is NTLM?
NTLM (NT LAN Manager) is a legacy challenge‑response authentication protocol used by Windows for authenticating users and computers. It predates Kerberos and is still encountered when:

A device/app doesn’t support Kerberos
Kerberos fails (SPN/DNS/time issues) and Negotiate falls back to NTLM
Workgroup or local account authentication is used
Legacy applications, NAS devices, printers, or proxies only speak NTLM

NTLM has several variants:

LM (LanMan) — obsolete, do not use
NTLMv1 — legacy, do not use
NTLMv2 — stronger, but still vulnerable to credential relay and pass‑the‑hash without additional protections


🧠 2) How NTLM Works (Challenge‑Response)
NTLM doesn’t send passwords over the wire. Instead, it performs a challenge‑response using the client’s NT hash of the password.
High‑level flow (NTLMSSP):
[1] Client → Server: NEGOTIATE (capabilities)
[2] Server → Client: CHALLENGE (server nonce)
[3] Client → Server: AUTHENTICATE (response computed with user's NT hash)

Server forwards to a DC (if needed) → DC validates response → Success/Failure

If accepted, the server issues a logon session and grants access per ACLs.

🧩 3) Where You’ll Still See NTLM

SMB access to servers/NAS that lack Kerberos/SPN setup
IIS/HTTP apps configured for NTLM instead of Negotiate (Kerberos)
Proxies/WAFs performing NTLM for intranet SSO
Workgroup machines / local admin logons
Legacy devices (copiers, scanners, KVMs) that only support NTLM


Tip: If Kerberos should be used but you see NTLM, suspect SPN, DNS, time skew, or duplicate SPNs.


🛡️ 4) Security Weaknesses (and Why to Move Away)

Pass‑the‑Hash (PtH): Access using the NT hash without knowing the password
NTLM Relay: Adversary relays a victim’s NTLM authentication to another service to gain access (especially when signing isn’t required)
Downgrade risks: Apps misconfigured to prefer NTLM over Kerberos
Weaker crypto in LM/NTLMv1; even NTLMv2 is still relay‑prone without extra protections
Lack of mutual authentication (by default) compared to Kerberos

Bottom line: Prefer Kerberos. Where NTLM is unavoidable, enforce compensating controls.

🧾 5) Event IDs & Quick Troubleshooting
On Domain Controllers / Servers (Security log):

























Event IDMeaningNotes4624Successful logon“Authentication Package: NTLM”; watch Logon Type (3 = network)4625Failed logonLook for Status/Substatus & package NTLM4776NTLM authentication to DCKey event for DC validation of NTLM creds

Kerberos‑vs‑NTLM quick hint: If expected Kerberos is missing and you see 4776/NTLM, troubleshoot SPN/DNS/time.


⚙️ 6) Hardening NTLM — Minimum Requirements
6.1 Disable legacy LM/NTLMv1
Group Policy (or local security policy):
Computer Configuration → Windows Settings → Security Settings → Local Policies → Security Options

Network security: LAN Manager authentication level →
Send NTLMv2 response only. Refuse LM & NTLM
Network security: Do not store LAN Manager hash value on next password change → Enabled

Equivalent registry (example):
MermaidNo diagram type detected matching given configuration for text: ; Refuse LM & NTLMv1; require NTLMv2
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa]
"LmCompatibilityLevel"=dword:00000005; Refuse LM & NTLMv1; require NTLMv2[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa]"LmCompatibilityLevel"=dword:00000005Show more lines
6.2 Require signing & protection on key protocols

SMB signing (server & client):

Microsoft network server: Digitally sign communications (always) → Enabled
Microsoft network client: Digitally sign communications (always) → Enabled


LDAP signing and channel binding (DCs):

Domain controller: LDAP server signing requirements → Require signing
Domain controller: LDAP server channel binding token → Required


IIS/HTTP apps: enable Extended Protection for Authentication (EPA) and use Negotiate (Kerberos)

6.3 Constrain or block NTLM where possible
Domain‑level policies under Security Options → Network security: Restrict NTLM:

Audit NTLM authentication in this domain → Enable auditing (first)
Restrict NTLM: Incoming NTLM traffic → Deny all (after baselining)
Restrict NTLM: Outgoing NTLM traffic to remote servers → Deny all / Add exceptions only where necessary


Phased approach is critical (see Section 9).

6.4 Protect credentials & endpoints

Windows Defender Credential Guard for LSASS credential protection
LAPS / gMSA for local & service account secrets
Disable WDigest (unless explicitly required)
Use Privileged Access Workstations / PAW for admins


🔍 7) Detecting NTLM Misuse (SOC Playbook)
Indicators to alert on

Spike in 4776 from a single host
Many 4624 (Type 3) across many servers with NTLM package from one workstation
SMB/LDAP connections without signing (where required)
Authentication from non‑Windows devices using NTLM into DCs

Sample hunting ideas (SIEM‑agnostic)

NTLM where Kerberos is expected (same user hitting many resources using NTLM)
NTLM to LDAP on DCs without signing (should be blocked)
NTLM to HTTP on sensitive internal apps (migrate to Kerberos/EPA)


🧪 8) Troubleshooting: “Why did this fall back to NTLM?”

SPN missing/incorrect — App/server SPN not registered to the right account
Duplicate SPN — Two accounts own the same SPN → Kerberos fails
Time skew — Client/Server/DC time drift > 5 min
DNS/SRV issues — Client can’t locate KDC
Client/Server etypes mismatch — Server/service account doesn’t support AES
Application misconfigured — HTTP/IIS using NTLM only; proxy removes Negotiate header

Fix pattern:

Validate SPN with setspn -L <account>
Check time/NTP on client, server, DC
Ensure Negotiate is offered and Kerberos is preferred
Verify encryption types on service accounts (prefer AES)


🚧 9) Practical Plan to Eliminate (or Contain) NTLM
Phase 1 — Visibility

Enable “Audit NTLM authentication in this domain” on DCs
Collect 4776/4624/4625 centrally (SIEM)
Identify top NTLM sources (hosts, apps, devices)

Phase 2 — Fix & Migrate

Migrate apps to Negotiate/Kerberos; configure SPNs
For devices that only support NTLM (NAS/printers), isolate via network segmentation or application proxies
Enforce SMB/LDAP signing and HTTP EPA

Phase 3 — Contain

Set LAN Manager level to refuse LM & NTLMv1 everywhere
Turn on SMB signing required; LDAP signing + CBT required
Block NTLM outbound from servers that should never use it

Phase 4 — Enforce

Restrict NTLM domain policies: move from Audit → Deny (with explicit exceptions list)
Re‑baseline periodically; remove stale exceptions


🧱 10) Configuration Cheat‑Sheet (GPO Paths)
Computer Configuration → Windows Settings → Security Settings → Local Policies → Security Options

Network security: LAN Manager authentication level → Send NTLMv2 only; Refuse LM & NTLM
Network security: Do not store LAN Manager hash value → Enabled
Network security: Restrict NTLM: Audit NTLM authentication in this domain → Enable (then Deny)
Microsoft network server/client: Digitally sign communications (always) → Enabled
Domain controller: LDAP server signing requirements → Require signing
Domain controller: LDAP server channel binding token → Required


🧾 11) Summary

NTLM is legacy. Prefer Kerberos for mutual auth and stronger protections.
When NTLM is unavoidable, eliminate LM/NTLMv1, enforce signing/EPA, and restrict NTLM domain‑wide with a phased plan.
Monitor 4776/4624/4625, look for relays and PtH behavior, and keep SPNs/time/DNS healthy to avoid unintended fallback to NTLM.
