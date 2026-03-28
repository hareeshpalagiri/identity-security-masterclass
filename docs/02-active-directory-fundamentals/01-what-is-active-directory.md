📘 Section 02 — Active Directory (On-Premise)

Chapter 01 — What Is Active Directory?

🔰 1. Introduction
Active Directory (AD) is Microsoft’s on‑premises directory service that provides the foundation for identity, authentication, and authorization inside a Windows enterprise network.
It stores and manages information about:

Users
Computers
Groups
Printers
Service accounts
Security policies

AD ensures that the right users get the right access to the right resources at the right time — securely and consistently.

🏛️ 2. Why Active Directory Exists
Before AD, organizations struggled with:

Local user accounts on every machine
No central authentication
No centralized policies
Manual access control
Difficult auditing and compliance

Active Directory solved these problems by introducing centralized identity management.

🧠 3. The Core Purpose of AD
✔ Centralized Authentication
Users log in once to AD, then access resources across the domain.
✔ Centralized Authorization
Permissions are managed via groups and policies.
✔ Administrative Control
Admins can manage thousands of devices and users from one place.
✔ Security Enforcement
Policies like password rules, software deployment, device restrictions.
✔ Directory Services
Applications can query AD for user and group information.

🏗️ 4. Active Directory Architecture Overview
Active Directory is a hierarchical directory structure.
It consists of:
1. Forest
The entire AD environment (top-level security boundary).
2. Domains
Administrative boundaries inside a forest.
Example:
corp.company.com
emea.company.com
apac.company.com

3. Organizational Units (OUs)
Logical containers used to organize objects:

Users
Computers
Service Accounts
Groups

4. Domain Controllers (DCs)
Servers that store and replicate the AD database (NTDS.dit).
5. AD Database
Stores all objects, attributes, passwords (hashed), and configurations.

🌐 5. Key Components of AD
Domain Controller (DC)

Handles login authentication
Issues Kerberos tickets
Replicates directory data to other DCs

Global Catalog (GC)

Partial read-only copy of all objects in the forest
Used for logons and universal group membership

FSMO Roles
Five special roles that ensure consistency:

Schema Master
Domain Naming Master
PDC Emulator
RID Master
Infrastructure Master

Sites & Replication

Defines physical network layout
Optimizes replication between DCs


🔑 6. How Authentication Works (High-Level)
Windows uses Kerberos by default:
User → Domain Controller → Receives Ticket Granting Ticket (TGT)
User → Requests service → Gets Service Ticket → Access granted

If Kerberos fails, AD falls back to NTLM (older, less secure).

🧩 7. What Objects AD Manages
Users

Human accounts
Service accounts

Groups

Security groups
Distribution groups

Computers

Workstations
Servers
Domain‑joined devices

Policies

Group Policy Objects (GPOs)
Security baselines

Other Objects

Printers
Contacts
Shared folders


🛡️ 8. Why AD Is Important for Security
✔ Access Control
All access — file shares, applications, servers — goes through AD.
✔ Policy Enforcement
AD controls password policies, MFA extensions (via ADFS), device restrictions.
✔ Attack Target
Because AD is powerful, attackers heavily target it.
Compromise of AD = Compromise of the entire organization.
✔ Integration
AD integrates with:

Windows
Linux (via LDAP / Kerberos)
Applications
Authentication systems
Cloud (Entra Connect)


🔥 9. Modern Challenges with Active Directory
While AD is mature and widely trusted, today’s challenges include:

Hybrid identity complexity
NTLM still in use
Privileged access risks
Kerberoasting attacks
DCSync attacks
Domain Admin overuse
Lack of audit logging

Organizations must continuously monitor, secure, and harden AD.

🧾 10. Summary
Active Directory is the core identity and access platform for on‑premises infrastructure.
It provides:

Central identity store
Authentication
Authorization
Security enforcement
Policy management

Although cloud identity platforms like Entra ID are gaining dominance, AD remains foundational for most hybrid enterprises.
