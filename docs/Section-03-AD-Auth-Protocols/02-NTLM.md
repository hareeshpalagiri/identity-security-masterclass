📘 02 — NTLM (Fallback, Risks & Hardening)
A simple, deep, story‑based explanation using strategic Mahabharata analogies — GitBook Ready

🏹 Mahabharata Story Analogy (Strategic Only)
Imagine a temporary pass system used only when royal seals (Kerberos tickets) aren’t available. It’s quick and works when roads are broken or the courier can’t reach the command post — but guards cannot verify the gate is genuine.
That is NTLM in Windows: a challenge‑response fallback that can still move people through—but attackers can relay or reuse the proof to sneak in. [learn.microsoft.com], [techcommun...rosoft.com]

🔐 1. What is NTLM? (Simple Definition)
NTLM (NT LAN Manager) is a family of Windows challenge‑response authentication protocols (LANMAN, NTLMv1, NTLMv2). It authenticates users/computers by proving knowledge of a password hash without sending the password itself. In Active Directory domains, Kerberos is preferred; NTLM persists for workgroups, local logon on non‑DCs, or when Kerberos negotiation fails. [learn.microsoft.com]

Microsoft is deprecating and moving to disable NTLM by default in future Windows releases via a three‑phase roadmap: enhanced auditing → Kerberos improvements (IAKerb, Local KDC) → NTLM disabled by default (re‑enable via policy if needed). [techcommun...rosoft.com], [bleepingcomputer.com], [expertinsights.com]


🧭 2. Why NTLM Matters — Hastinapura Example





















When it lingers (risk)With modern controls (safer)No server authentication → easy to relay credentials to an attacker‑controlled serverSMB signing, LDAP signing + channel binding add integrity & bind TLS to the handshake, blunting relaysWeak crypto heritage → pass‑the‑hash, replay, brute‑force on captured hashesPrefer Kerberos; audit + restrict NTLM; block NTLM over SMB; enable secure defaults in newer buildsHidden dependencies in legacy appsNew auditing (Win 11 24H2/Server 2025+) shows who/why/where NTLM was chosen, easing migration
 [learn.microsoft.com], [support.mi...rosoft.com], [learn.microsoft.com], [support.mi...rosoft.com]

🎬 3. Animation Placeholder
(Add later using GIF/Notebook‑LLM)
[Animation Placeholder: "Why NTLM is risky"]
Scene 1 → Client proves identity with hash (challenge–response)
Scene 2 → Attacker relays proof to target server (no server auth) → access granted
Scene 3 → Defenses appear: SMB signing, LDAP signing + channel binding, NTLM auditing & blocking
Scene 4 → Kerberos-first flow replaces NTLM fallback


🧠 4. Core Concepts (Simple + Deep)
How NTLM works (at a glance)

Server sends challenge → client responds with a value derived from the password hash → server/DC validates. [techcommun...rosoft.com]
Unlike Kerberos, no mutual authentication → client can’t verify server identity → relay risk. [techcommun...rosoft.com]

Where NTLM still appears

Workgroups, local accounts, legacy apps, or Kerberos negotiation failures. [learn.microsoft.com]

Why it’s risky

Relay (no server auth), pass‑the‑hash, and hash disclosure issues (recent CVEs). [support.mi...rosoft.com], [cyberpress.org]

Roadmap & posture shift

Microsoft is deprecating NTLM and moving toward Kerberos‑first with features (IAKerb, Local KDC) and enhanced auditing, then disabled‑by‑default in future Windows. [techcommun...rosoft.com], [bleepingcomputer.com], [expertinsights.com]


🗺 5. Where NTLM Fallback Happens (and How to See It)
A) Discover NTLM in your environment (Domain/Servers/Clients)
Enable NTLM auditing (Group Policy → Security Options):

Network security: Restrict NTLM: Audit NTLM authentication in this domain → Enable all (DCs).
Network security: Restrict NTLM: Audit Incoming NTLM Traffic → Enable auditing for all accounts.
Network security: Restrict NTLM: Outgoing NTLM traffic to remote servers → Audit all.
Check Applications and Services Logs → Microsoft → Windows → NTLM → Operational for Event IDs 8001/8002/8003/8004 (client/server/DC). [learn.microsoft.com], [itprotoday.com]


New Windows 11 24H2 / Windows Server 2025 auditing adds who/why/where NTLM was used to speed remediation. [support.mi...rosoft.com]

B) Detect NTLMv1 (must go)
Audit for NTLMv1 via Security Event 4624 (Package Name = NTLM V1) and domain‑wide NTLM logs. [learn.microsoft.com]
C) Track LDAP and SMB paths that trigger NTLM

LDAP apps not using signing/TLS, or devices that don’t support Kerberos. [support.mi...rosoft.com], [learn.microsoft.com]
SMB shares where clients aren’t using Kerberos or SMB signing isn’t enforced. [learn.microsoft.com]


🔧 6. NTLM Hardening — Practical Steps (with modern defaults)

Goal: Kerberos‑first, NTLM only where absolutely necessary — and cryptographically protected paths when it occurs.

6.1 Prefer Kerberos via Negotiate
Update apps to use Negotiate (SPNEGO) so Windows selects Kerberos first (falls back to NTLM only if needed). [learn.microsoft.com], [windowsforum.com]
6.2 Enforce SMB Signing (breaks many NTLM relay paths)

In Windows 11 24H2: inbound & outbound SMB signing required by default; Windows Server 2025 requires outbound by default. Validate/adjust per guidance. [learn.microsoft.com], [learn.microsoft.com]
Signing protects against tampering/relay; don’t disable unless absolutely necessary. [learn.microsoft.com]

6.3 Enforce LDAP Signing + Channel Binding (CBT/EPA)

Enable LDAP signing and LDAP channel binding on DCs to stop tamper/relay, including common AD CS relay chains. [support.mi...rosoft.com], [learn.microsoft.com]
Microsoft’s KB and hardening series explain why both signing and channel binding are needed. [support.mi...rosoft.com], [techcommun...rosoft.com]

6.4 Audit → Restrict → Block NTLM (phased)

Start with Audit policies (above), then move to Restrict/Block using Restrict NTLM GPOs (Incoming/Outgoing, per‑domain and per‑member server), with server exceptions only where required. [learn.microsoft.com], [4sysops.com]
New BlockNTLMv1SSO control (Win 11 24H2/Server 2025) provides Audit/Enforce for NTLMv1‑derived credentials. [support.mi...rosoft.com], [4sysops.com]

6.5 Block NTLM over SMB (client)

Newer builds add SMB NTLM blocking (client‑side) to prevent coerced NTLM to malicious servers; allow explicit exceptions if absolutely needed. [argonsys.com]

6.6 Plan for Microsoft’s “Disable by default” timeline

Follow the three‑phase roadmap (audit → Kerberos enhancements → disabled‑by‑default) announced by Microsoft. [techcommun...rosoft.com], [bleepingcomputer.com]


⚔️ 7. Attacks & Defenses (What red teams exploit, how to stop it)
🛑 Common Attacks

NTLM Relay (e.g., to LDAP/SMB/HTTP) — exploit no server auth; coercion techniques (PrinterBug, PetitPotam) force devices to authenticate, then relay to privileged services. Mitigation: SMB signing; LDAP signing + channel binding; EPA on AD CS web roles; block NTLM where possible. [support.mi...rosoft.com], [vaadata.com]
Pass‑the‑Hash — stolen NTLM hashes used to authenticate without cracking the password. Mitigation: minimize NTLM, harden endpoints, disable NTLM where possible. [learn.microsoft.com]
NTLM hash disclosure CVEs (e.g., CVE‑2025‑24054) — coerce Windows to leak NTLMv2 hashes via crafted files; patch promptly. [cyberpress.org], [heise.de]

🛡 Effective Defenses

SMB signing defaults (Win 11 24H2/Server 2025). [learn.microsoft.com], [learn.microsoft.com]
LDAP signing + channel binding (with EPA) — especially for AD CS web endpoints per KB5005413. [support.mi...rosoft.com], [support.mi...rosoft.com]
Audit, then block with Restrict‑NTLM policies, and use new enhanced NTLM auditing to find dependencies. [support.mi...rosoft.com], [learn.microsoft.com]
Kerberos‑first via Negotiate; phase to disable‑by‑default posture. [learn.microsoft.com], [techcommun...rosoft.com]


🔧 8. Quick Commands & Policy Paths (Copy‑ready)
🔹 View NTLM audit stream (clients/servers/DCs)
Event Viewer → Applications and Services Logs → Microsoft → Windows → NTLM → Operational
Look for Event IDs 8001, 8002, 8003, 8004. [learn.microsoft.com]
🔹 Enable NTLM audit (GPO)
Computer Configuration
  └─ Windows Settings
     └─ Security Settings
        └─ Local Policies
           └─ Security Options
              • Network security: Restrict NTLM: Audit NTLM authentication in this domain = Enable all
              • Network security: Restrict NTLM: Audit Incoming NTLM Traffic = Enable auditing for all accounts
              • Network security: Restrict NTLM: Outgoing NTLM traffic to remote servers = Audit all

 [itprotoday.com]
🔹 Enforce LDAP protections (DCs)

LDAP signing (reject unsigned SASL/simple over cleartext). [learn.microsoft.com]
LDAP channel binding (CBT/EPA) to bind auth to TLS session. [support.mi...rosoft.com], [learn.microsoft.com]

🔹 SMB signing (defaults vary by OS)
Review/align with latest defaults (e.g., Win 11 24H2: inbound + outbound required; Server 2025: outbound required). [learn.microsoft.com], [learn.microsoft.com]
🔹 Move apps to Negotiate (Kerberos‑first)
Update authentication package from “NTLM” to “Negotiate” in code/app configs so AD can choose Kerberos. [learn.microsoft.com]
🔹 (Optional) Identify NTLMv1 usage
Check Security → 4624 → Package Name (NTLM only): NTLM V1. [learn.microsoft.com]

🧵 9. Mind Map (Placeholder)
(Will be converted to GIF later)
NTLM (Fallback)
 ├─ Where it appears (workgroup, local, Kerberos fail)
 ├─ Why risky (no server auth → relay; hash theft)
 ├─ Visibility (NTLM auditing 8001/2/3/4; 4624 details)
 ├─ Controls:
 │   ├─ Negotiate (Kerberos-first)
 │   ├─ SMB signing (default on 11 24H2/Server 2025)
 │   ├─ LDAP signing + channel binding (EPA)
 │   ├─ Restrict/Block NTLM (GPO, BlockNtlmv1SSO)
 └─ Roadmap:
     ├─ Audit now
     ├─ Kerberos enhancements (IAKerb, Local KDC)
     └─ Disable-by-default (future Windows)


References (selected)

NTLM overview & where it’s used (Kerberos preferred; NTLM in workgroups/local logon; audit & restrict tooling). [learn.microsoft.com]
NTLM vs Kerberos (no server auth → relay risk). [techcommun...rosoft.com]
Microsoft roadmap to disable NTLM by default (phased: audit → Kerberos enhancements → disable). [techcommun...rosoft.com], [bleepingcomputer.com], [expertinsights.com]
Enhanced NTLM auditing (Win 11 24H2/Server 2025). [support.mi...rosoft.com]
Audit events & policies (8001–8004; Restrict‑NTLM). [learn.microsoft.com], [learn.microsoft.com]
SMB signing changes & defaults (Windows 11 24H2/Server 2025). [learn.microsoft.com], [learn.microsoft.com]
LDAP signing & channel binding (CBT/EPA) hardening guidance and rationale. [support.mi...rosoft.com], [learn.microsoft.com]
AD CS NTLM relay mitigations (PetitPotam & EPA). [support.mi...rosoft.com]
NTLM deprecation background & migration (Negotiate). [windowsforum.com]
