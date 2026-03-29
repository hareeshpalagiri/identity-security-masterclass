🎯 Purpose of Section‑09
This section teaches how to monitor, detect, and respond to identity‑centric threats using:

Windows Event Logging
Active Directory advanced auditing
Microsoft Defender for Identity (MDI)
Microsoft Sentinel (SIEM)
IR Playbooks & response procedures

Monitoring is the backbone of security.
Without reliable logs → nothing can be detected, correlated, or investigated.
This section teaches you how to establish a complete identity threat visibility pipeline across:

Domain Controllers
Windows servers
Entra ID
SIEM
XDR
Identity sensors
Incident response mechanisms


🗂 Files in This Section
01 — Windows Event IDs
01-Windows-Event-IDs.md
A complete reference of critical event IDs used for detection, threat hunting, and IR.
Includes categories for authentication, privilege escalation, Kerberos attacks, object access, and persistence.

02 — AD Audit Configuration
02-AD-Audit-Configuration.md
Explains how to correctly configure Active Directory auditing using:

Advanced audit policy
SACLs
DC-level logging
GPO audit configuration
Defender for Identity prerequisites
This is the foundation for SOC visibility.


03 — Defender for Identity
03-Defender-for-Identity.md
A professional overview of Microsoft Defender for Identity, including:

Identity-based threat detection
Lateral movement path discovery
Directory reconnaissance monitoring
Integration with the Microsoft Defender portal
Identity posture assessments
Unified identity incidents across M365
Based on Microsoft’s modern ITDR model.


04 — Microsoft Sentinel
04-Microsoft-Sentinel.md
A complete overview of Sentinel as a cloud-native SIEM + SOAR, covering:

Unified incidents with Defender XDR
Log analytics
Data connectors
KQL hunting
Playbooks (automation)
Multi-cloud monitoring
Full migration to Defender Portal (2026 roadmap)


05 — Incident Response (IR) Playbooks
05-IR-Playbooks.md (You will generate next)
Contains clear IR workflows for identity attacks:

Kerberoasting
Pass-the-Hash
DCSync
Golden Ticket
Lateral Movement
Account compromise response
Sentinel automation playbooks
SOC triage guidance


🧵 Section‑09 Mind Map
Monitoring & IR
 ├─ Windows Logging
 │   ├─ Event IDs
 │   └─ Logon/Process/DS Events
 ├─ AD Auditing
 │   ├─ GPO audit config
 │   ├─ SACLs
 │   └─ DC auditing
 ├─ Identity Detection
 │   └─ Defender for Identity
 ├─ SIEM
 │   └─ Microsoft Sentinel
 ├─ XDR Integrations
 └─ Incident Response
     ├─ Playbooks
     └─ Automation


🔥 What You’ll Learn From Section‑09
By the end of this section, you will know:
✔ How to enable full auditing in AD
✔ How to read critical Event IDs for threat detection
✔ How to detect identity attacks with Defender for Identity
✔ How Sentinel performs:

correlation
hunting
orchestration
unified incident response

✔ How to build real-world IR playbooks for identity attacks
✔ How to operate a SOC using the Microsoft Defender Portal
This section transforms you from an identity engineer → to a detection/IR-ready professional.
