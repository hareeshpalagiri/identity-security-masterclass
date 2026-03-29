🏹 **Mahabharata Strategic Analogy —
“Not every warrior enters every tent.”**
In the Pandava army:

Sacred temples, weapon forges, and command tents were restricted zones
Only warriors with the right varna, rank, or authorization could enter
Lower‑ranked soldiers could not wander inside command areas
Messages flowed downward, never upward without scrutiny
The clean source principle was absolute:
High-value strategy must NEVER touch low‑trust environments

This is the Tiered Admin Model in cybersecurity:

Tier‑0 (identity plane) is like the command tent.
Tier‑1 (server plane) is the weapons arena.
Tier‑2 (workstations) are the general camp.

The rule:
T0 → T1 → T2 (allowed)
T2 → T1 → T0 (never allowed)
Because one careless login on a compromised tent can collapse the kingdom.
 [learn.microsoft.com], [blog.quest.com]

🔐 1. What Is the Tiered Model? (Simple Definition)
The Tiered Administration Model separates all identities, machines, and privileges in AD into three trust zones to stop credential exposure:





























TierPlaneExamplesSecurity LevelTier 0Identity & controlDCs, PKI, Entra Connect/AD FS, KRBTGT, schema adminsHighestTier 1ServersFile servers, SQL, application serversHighTier 2UsersWorkstations, VDI, helpdesk endpointsMedium
Rule:
A Tier‑0 credential must never touch a Tier‑1 or Tier‑2 system.
A Tier‑1 credential must never touch Tier‑2.
 [blog.quest.com]

🧭 2. Why Tiering Exists — Hastinapura Example
⭐ Enemy infiltrates the outer tents (Tier‑2)
→ steals a generic messenger badge
→ walks into the weapons area (Tier‑1)
→ overhears plans
→ tries entering command tent (Tier‑0)
If there is no tier separation, attackers escalate until they reach the throne.
Exactly like an AD breach:

























Without TieringWith TieringDomain Admin logs into a user deviceBlocked by logon restrictionsHelpdesk machines contain cached high‑priv credsNever possibleMalware on a workstation steals DA tokenPAW + tier rules = no DA token presentOne phish = whole domainOne phish = limited to Tier‑2 only
 [blog.quest.com]

🎬 3. Animation Placeholder
[Animation Placeholder: "A soldier from outer tent attempts to enter command tent → blocked"]
Scene 1: T2 warrior tries stepping into T1 → blocked  
Scene 2: T1 tries stepping into T0 → blocked  
Scene 3: T0 → T1 → T2 flow allowed  
Scene 4: Malware tries stealing DA credential from workstation → unable (no Tier‑0 creds present)


🧠 4. Core Concepts (Simple + Deep)
4.1 The Clean Source Principle
High-privileged credentials must never be exposed to lower-trust systems.
 [blog.quest.com]
4.2 Allowed vs Blocked Control Paths

Allowed: T0 → T1 → T2
Blocked: T2 → T1 → T0

This ensures breach containment.
4.3 Tier Boundaries Must Be Technical (Not Policy-Only)

Logon rights
Network boundaries
Authentication policies
PAWs
Group scoping
GPO isolation

4.4 AD Tiering is NOT replaced by EAM
Microsoft clarified:

Tiered Model still required under Enterprise Access Model (EAM).
It is not deprecated.
 [blog.quest.com]


🕸 5. Tiered Admin Architecture Diagram (Mermaid)
Parse error on line 17:
...W1  S1 --> W2  W1 -x S1  W1 -x DC  S
---------------------^
Expecting 'SEMI', 'NEWLINE', 'EOF', 'AMP', 'START_LINK', 'LINK', 'LINK_ID', got 'NODE_STRING'flowchart TD  subgraph T2[ Tier 2 – Workstations / Users ]    W1[Helpdesk PC]    W2[Employee Laptop]  end  subgraph T1[ Tier 1 – Servers / Apps ]    S1[File Server]    S2[Web / App Server]  end  subgraph T0[ Tier 0 – Identity & Control ]    DC[Domain Controller]    PKI[AD CS]    AADC[Entra Connect]  end  %% Allowed flow: Downward  DC --> S1 --> W1  S1 --> W2  %% Blocked upward flows:  W1 -x S1  W1 -x DC  S1 -x DC  classDef tier0 fill:#c7eaff,stroke:#005a9e,color:#000;  classDef tier1 fill:#d3ffd9,stroke:#0b8a46,color:#000;  classDef tier2 fill:#f2f2f2,stroke:#999,color:#000;  class T0 tier0;  class T1 tier1;  class T2 tier2;Show more lines

🔧 6. Real‑World Implementation (Practical Steps)
6.1 Create Tier OUs (mandatory)
OU=Tier0
OU=Tier1
OU=Tier2
OU=PAWs

6.2 Create Tiered Admin Groups
SG_Tier0_Admins
SG_Tier1_Admins
SG_Tier2_Admins

6.3 Enforce Logon Restrictions via GPO

























TierAllow LogonDeny LogonT0SG_Tier0_AdminsEveryone elseT1SG_Tier1_AdminsT0, T2T2SG_Tier2_AdminsT0, T1
 [ravenswood...nology.com]
6.4 Require PAWs for Tier‑0
PAWs prevent T0 credentials from appearing on unsafe devices.
 [blog.quest.com]
6.5 Protected Users + Authentication Policy Silos
Prevents:

Token replay
NTLM fallback
Weak crypto usage

6.6 Use JIT/JEA/PIM for Time‑Bound Privilege
No more permanent DA membership.

⚔️ 7. Attack Scenarios This Model Prevents

























AttackPrevented BecausePass‑the‑Hash from helpdesk PCTier‑0 creds never touch that PCLateral movement from workstation → server → DCUpward logon paths blockedService account escalationTier boundaries + scope restrictionsPhishing → DA compromiseNo DA tokens on Tier‑2 endpoints
 [blog.quest.com]

🛡 8. Defense Strategies — “Pandava Command Discipline”
Mandatory

Tier OUs + GPO logon policies
PAWs for all Tier‑0 accounts
LAPS on all servers/workstations
JIT + PIM for elevation
Protected Users group
Kerberos-only for Tier‑0 and Tier‑1

Recommended

Dedicated admin forests for extremely high-risk orgs
Tier‑aware network ACLs
Admin SD Holder reviews


🔧 9. Quick Commands (Copy‑ready)
Check logon rights
PowerShellsecedit /export /cfg C:\temp\secpol.infSelect-String C:\temp\secpol.inf -Pattern "SeInteractiveLogonRight|SeRemoteInteractiveLogonRight"Show more lines
Check your Kerberos tickets
PowerShellklistShow more lines
Check which group you are effectively in
PowerShellwhoami /groupsgpresult /rShow more lines

🧵 10. Mind Map (Placeholder)
Tiered Admin Model
 ├─ Clean Source Principle
 ├─ Tier0 (Identity)
 ├─ Tier1 (Servers)
 ├─ Tier2 (Workstations)
 ├─ PAWs
 ├─ Logon Restrictions
 ├─ JIT/JEA/PIM
 └─ Monitoring & Alerts


📚 References

Microsoft Enterprise Access Model (modern privileged‑access strategy)
 [learn.microsoft.com]
Tiered Model hardening & clean source principle
 [blog.quest.com]
Logon restriction enforcement (GPO‑based)
 [ravenswood...nology.com]
