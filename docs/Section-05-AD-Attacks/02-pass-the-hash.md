📘 02 — Pass‑the‑Hash (Using Stolen Hashes as Passwords)
A simple, deep, battlefield‑style explanation with Mahabharata analogies — GitBook Ready

🏹 **Mahabharata Story Analogy —
“Using the royal seal without knowing the mantra.”**
In the Mahabharata:

A royal seal allowed entry into certain war councils
The holder did not need to know the secret mantras,
only possess the physical seal
If an enemy stole the seal, they could impersonate the rightful person
The Pandavas recognized this threat and implemented strict boundaries
(verifying the warrior, checking allegiance, ensuring right‑to‑enter)

This is Pass‑the‑Hash (PtH):

Attackers don’t need your password —
they just need the NTLM hash (the “seal”).
With the hash, they authenticate without cracking it.

A stolen seal → forged entry.
A stolen hash → forged identity.

🔐 1. What Is Pass‑the‑Hash? (Simple Definition)
Pass‑the‑Hash is a technique where an attacker:

Steals a user’s NTLM hash from memory, disk, SAM database, LSASS, or credential material
Uses the hash directly to authenticate to remote systems
Never needs the actual plaintext password

The hash acts as the credential.
PtH is possible because Windows still accepts NTLM authentication tokens produced using the hash.
 [github.com]

🧭 2. Why PtH Works — Hastinapura Parallel

























Mahabharata ScenarioAD EquivalentA stolen royal seal gives access to restricted tentsA stolen NTLM hash gives access to remote loginSeal does not require knowing divine mantrasHash does not require knowing the passwordEnemy can impersonate the commanderAttacker becomes the user / adminSeal found in outer tents → dangerousAdmin logs into low-tier workstation → disastrous
Why it succeeds:

Windows caches credentials
Admins log into unsafe endpoints
LSASS stores reusable secrets
NTLM is still enabled for compatibility
No MFA or device verification on network protocols

 [github.com]

🎬 3. Animation Placeholder
[GIF Placeholder: "Attacker steals NTLM hash → reuses hash → authenticates as victim"]

Scene 1: Compromised workstation  
Scene 2: Attacker dumps LSASS hash  
Scene 3: Uses hash with Pass-the-Hash tool  
Scene 4: Logs into server as Domain Admin  
Scene 5: Full domain compromise  


🧠 4. Core Concepts (Simple + Deep)

⭐ 4.1 Hash ≠ Password
But Windows allows it to authenticate through NTLM challenge-response.
The server verifies the hash → not the password.

⭐ 4.2 Credential Types Stored in LSASS
LSASS may store:

NTLM hashes
Kerberos TGTs
Session keys
Cached credentials
SSP secrets

These can be dumped using tools like:

Mimikatz
Procdump + pypykatz
Task Manager’s memory dump (if unprotected)


⭐ 4.3 Perfect for Lateral Movement
Once attacker gets the hash, they can move sideways:
Workstation → Server → Domain Controller

Especially deadly when:

Admin logged into workstation
LAPS not configured
Legacy protocols enabled
No tiering in place


⭐ 4.4 PtH Needs Only ONE Successful Credential Theft
A single stolen admin hash can lead to entire forest compromise.

🕸 5. Pass‑the‑Hash Attack Flow (Mermaid Diagram)
Mermaidflowchart TDA[Compromised Workstation] --> B[Dump LSASS / Hash Extraction]B --> C[NTLM Hash Obtained]C --> D[Use Hash with PtH Tools]D --> E[Remote Auth to Server/Share]E --> F[Lateral Movement / Elevation]Show more lines

🔧 6. Attack Demonstration (For Lab Only)
⚠️ For educational testing in isolated labs only.

✔ 6.1 Dump LSASS
PowerShellprocdump -ma lsass.exe lsass.dmpShow more lines
OR using Mimikatz:
PowerShellmimikatz.exeprivilege::debugsekurlsaShow more lines

✔ 6.2 Use Hash for Authentication
Example with Impacket:
Shellwmiexec.py contoso.local/user@server -hashes :aad3b435b51404eeaad3b435b51404eeShow more lines
Example with evil-winrm:
Shellevil-winrm -i server -u Administrator -H <NTLM_HASH>Show more lines
No password needed.

⚔️ 7. Real‑World PtH Attack Scenarios

🛑 Scenario 1 — “Admin logged into compromised PC”

Attacker steals DA hash
Uses hash to access DC
Full domain takeover
No password cracking needed


🛑 Scenario 2 — “Service account running on workstation”

Hash extracted
Service account often has high privileges
Attackers escalate quickly


🛑 Scenario 3 — “Local admin reused everywhere”

Same hash across machines
Compromise one machine → compromise all


🛑 Scenario 4 — “NTLM allowed + SMB signing disabled”

Perfect for relay + PtH combo attacks


🛡 **8. Defense Strategy —
“Never allow the commander’s seal to leave the sanctum.”**

⭐ 8.1 Use PAWs for Admin Work (Mandatory)
Admins NEVER log into:

Workstations
Browsers
Email clients
Tier‑2 machines

PAWs ensure admin hashes never land on unsafe machines.
 [github.com]

⭐ 8.2 Enforce Tiered Access Model
Tier‑0 admins → only on Tier‑0 machines
Tier‑1 admins → only on Tier‑1 machines
Tier‑2 admins → only on Tier‑2 machines
 [github.com]

⭐ 8.3 Enable Credential Guard
Protects LSASS secrets.

⭐ 8.4 Disable NTLM Wherever Possible
NTLM enables PtH → Kerberos‑first prevents it.
 [github.com]

⭐ 8.5 LAPS (Rotate Local Admin Passwords)
Stops hash reuse across machines.

⭐ 8.6 Protected Users Group
Prevents NTLM usage entirely for sensitive accounts.

⭐ 8.7 Harden SMB

SMB signing
Disable SMBv1
Prevent NTLM fallback


⭐ 8.8 Use JIT/JEA/PIM
Reduce standing admin privileges → shrink PtH surface.

⭐ 8.9 Endpoint Isolation

No RDP inbound on workstations
No WinRM from Tier‑2 to Tier‑1
Firewall segmentation


🔧 9. Blue Team Quick Commands
Check if Credential Guard is enabled:
PowerShellGet-CimInstance -ClassName Win32_DeviceGuardShow more lines
Check SMB signing:
PowerShellGet-SmbServerConfiguration | Select EnableSecuritySignature, RequireSecuritySignatureShow more lines
Find accounts with NTLM enabled:
PowerShellGet-ADUser -LDAPFilter "(userAccountControl:1.2.840.113556.1.4.803:=1048576)"Show more lines
Check local admin reuse:
PowerShellGet-LocalGroupMember AdministratorsShow more lines

🧵 10. Mind Map (Placeholder)
Pass-the-Hash
 ├─ LSASS Dump
 ├─ NTLM Hash Extraction
 ├─ Remote Authentication
 ├─ Lateral Movement
 ├─ Defenses
 │   ├─ PAWs
 │   ├─ Tiering
 │   ├─ Credential Guard
 │   ├─ Disable NTLM
 │   ├─ LAPS
 │   ├─ SMB Signing
 │   ├─ Protected Users
 └─ Attack Surface Reduction


📚 References


Microsoft Enterprise Access Model (privileged access hardening)
 [github.com]


Clean Source Principle & Tiered Model (Quest blog)
 [github.com]
