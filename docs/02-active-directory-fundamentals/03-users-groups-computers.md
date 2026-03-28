📘 Chapter 03 — Users, Groups & Computers
The living entities inside an Active Directory domain, explained through organizational strategy and ancient kingdom structure.

🏹 **Mahabharata Story Opener —
“The Warriors, Councils & War Engines of a Kingdom”**
Inside Hastinapura’s kingdom:

Warriors (Arjuna, Bhima, Duryodhana) = Users
Councils (war councils, advisory groups) = Groups
War Chariots & Elephants (battle resources) = Computers/Devices
Roles & duties were clearly defined
Permissions differed based on clan, role, responsibility
Resources were assigned only to authorized members

Active Directory works the same way.
Inside a domain:

Users = the people
Groups = teams/departments
Computers = machines registered under the domain
Permissions = controlled by group memberships

Understanding Users, Groups & Computers is essential to mastering AD.

🔐 1. AD Users (Simple + Deep)
An AD User is any identity representing a person or service.
Types of AD Users:

Human Users → employees, admins, service desk
Service Accounts → run apps, services
Administrator Accounts → domain admins, delegated admins

Mahabharata Mapping:

Arjuna, Bhima, Nakula → individual user identities
Drona → privileged user
Shakuni → malicious user (insider)
A disguised warrior → user identity with altered attributes

User Object Attributes (Important):

sAMAccountName → logon name
userPrincipalName → cloud-friendly login
memberOf → group memberships
accountExpires
pwdLastSet
userAccountControl

Create user via PowerShell:
PowerShellNew-ADUser -Name "Arjuna" -SamAccountName "arjuna" -AccountPassword (Read-Host -AsSecureString) -Enabled $trueShow more lines

🫂 2. AD Groups — The Councils & Teams
Groups simplify permissions by assigning rights to teams instead of individuals.
Mahabharata Mapping:

War council → Security Group
Small tactical unit → Distribution Group
Royal advisory group → Privileged Group

Types of AD Groups:


Security Groups
Used for assigning permissions


Distribution Groups
Used for email lists


Group Scopes:





















ScopeMeaningDomain LocalPermissions inside a single domainGlobalUsers from same domainUniversalMultiple domains (forest-wide)
Example analogy:
A Universal Group = united council of warriors from multiple kingdoms.
PowerShell Example:
PowerShellNew-ADGroup -Name "Hastinapura-WarCouncil" -GroupScope Global -GroupCategory SecurityShow more lines

💻 3. AD Computers — Devices of the Domain
A Computer object represents:

A workstation
A server
A laptop
A virtual machine

Analogy:
Just like different war machines (chariots, elephants, armors) were registered under specific commanders,
domain computers belong to OUs and follow domain policies.
Key things about computer objects:

They authenticate using a machine account (ends with $)
They change passwords every 30 days
They receive GPOs based on their OU location

Example:
PowerShellAdd-Computer -DomainName corp.local -OUPath "OU=Servers,DC=corp,DC=local"Show more lines

🧩 4. AGDLP Model — The Strategy of Structured Access
One of the most important AD models:
A  = Accounts  
G  = Global Groups  
DL = Domain Local Groups  
P  = Permissions  

Meaning:

Assign users to Global Groups
Global Groups go into Domain Local Groups
Domain Local is assigned permissions

Mahabharata Analogy:

Individual warriors → Global Groups
Councils → Domain Local Groups
Access to chambers, weapons, councils → Permissions

Mermaid Diagram
PowerShellgraph LR    A[Users] --> B[Global Groups]    B --> C[Domain Local Groups]    C --> D[Permissions on Resources]Show more lines

🧠 5. Understanding OU Placement
Where you place objects in AD affects:

Group Policy application
Delegation of rights
Security boundaries (soft)

Example OU Structure:
OU=Users
OU=Admins
OU=Servers
OU=Workstations

Separate warriors by role, clan, responsibility.

🛠 6. Commands You Will Use Often
✔ List all users:
PowerShellGet-ADUser -Filter * -Properties *Show more lines
✔ List all groups:
PowerShellGet-ADGroup -Filter *Show more lines
✔ Add user to group:
PowerShellAdd-ADGroupMember -Identity "WarCouncil" -Members "arjuna"Show more lines
✔ View computer object:
PowerShellGet-ADComputer -Identity "HSTN-SRV01" -Properties *Show more lines

⚔️ 7. Attack Scenarios Related to Users, Groups & Computers
1. Credential Harvesting
Stealing user passwords or hashes.
2. Kerberoasting
Targeting service accounts.
3. Over-permission groups
When “Everyone” or “Domain Users” has access → like letting any warrior into a strategic chamber.
4. Privilege Creep
Users keep getting added to new groups but old ones not removed.
5. Shadow Admins
Users who indirectly gain admin rights through nested groups.
6. Misconfigured computer objects
Machines placed in wrong OUs → GPO bypass.

🛡 8. Defense Strategies

Enforce strong RBAC
Use AGDLP properly
Clean unused groups
Review memberships regularly
Use PAWs (Privileged Access Workstations)
Enforce workstation/server separation
Rotate service account passwords (use gMSA)

Mahabharata Strategy:
Vidura handled governance →
make sure your “Vidura” (governance) reviews access frequently.

🧵 9. Mind Map Placeholder
Users, Groups & Computers Mind Map:
 - Users
 - Privileged Users
 - Groups (Security / Distribution)
 - AGDLP Model
 - OU Placement
 - Computer Accounts
 - Service Accounts
 - Attack Paths
 - Defense Strategies


🔗 10. Transition to Chapter 04 — Group Policy (GPO)
Now that we know who exists inside the kingdom (users),
which councils they belong to (groups),
and what devices they use (computers),
the next question becomes:

“How are rules applied across the entire kingdom?”

In AD terms:
GPO = the lawbook of the kingdom.
Next module:
👉 Chapter 04 — Group Policy (GPO)
