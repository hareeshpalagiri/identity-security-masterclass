Chapter 07 — Active Directory Trusts

🔰 1. Introduction
Active Directory Trusts enable authentication and authorization across different domains or forests.
They define how identities from one security boundary can access resources in another.
Trusts are essential in environments where organizations have:

Multiple domains
Multiple forests
Mergers & acquisitions
Partner/third-party collaboration
Isolated business units needing limited access


🧠 2. What Is a Trust?
A trust is a security relationship that allows authentication requests to flow between two AD domains or forests.
Simple definition:

A Trust = One domain/forest trusting another domain/forest’s ability to authenticate users.

Example:
If DomainA trusts DomainB, then users from DomainB can access resources in DomainA (if permissions allow).

🏛️ 3. Why Trusts Exist
Trusts solve:

Cross-domain authentication
Centralized resource access
Legacy multi-domain architecture
Distributed business units
Gradual migration to another forest
AD consolidation projects

Example real-world needs:

Company A acquires Company B
Two forests need limited sharing
Subsidiaries need access to central HR system
Migration from old forest to new forest (side-by-side migration)


🔐 4. Key Concepts: Direction & Scope
4.1 Trust Direction
A trust can be:
➡ One-way Trust

Domain A → trusts Domain B
Users from B can access A
Users from A CANNOT access B

↔ Two-way Trust

Both domains trust each other
Authentication flows both ways


4.2 Trust Scope
A trust can be:
Forest-wide

All domains in Forest A trust all domains in Forest B
Easier to manage
Larger attack surface

External (Domain-level Only)

Domain A ⇄ Domain B
Does NOT include full forest
Limited, more secure


🧩 5. Types of Active Directory Trusts
5.1 Parent–Child Trust

Automatically created
Two-way, transitive
Example:
corp.local
    ↳ sales.corp.local



5.2 Tree–Root Trust

Automatically created
Connects two domain trees in the same forest
Two-way, transitive
Example:
corp.local
hr.company.local



5.3 External Trust

Manually created
One-way or two-way
Non-transitive
Used with older/legacy domains or in partial-trust situations
Example:
Contoso.com → Fabrikam.com



5.4 Forest Trust

Manually created
One-way or two-way
Transitive across forests
Strongly used in enterprise mergers
Example:
Forest A (HQ) ↔ Forest B (Subsidiary)



5.5 Shortcut Trust

Manually created
Two domains inside a complex forest path
Used to speed up authentication
Example:
US.corp.com ⇄ APAC.corp.com



5.6 Realm Trust (Kerberos Realm)

Used to trust non-Windows Kerberos realms (e.g., Linux MIT Kerberos)
One-way or two-way
Flexible integration with UNIX environments


🛂 6. Transitive vs. Non‑Transitive Trusts
Transitive Trust

Trust extends beyond two domains
Example:
A trusts B  
B trusts C  
→ A implicitly trusts C



Non‑Transitive Trust

Only between specified domains
No automatic extension
Example:
A ↔ B  
C is not included




🔐 7. Authentication Flow in Trusts (Simplified)
When a user from Domain B accesses a resource in Domain A:
1. User logs into Domain B
2. Domain B issues Kerberos TGT
3. Domain A checks Trust with Domain B
4. Domain A validates identity using Domain B’s DC
5. Access granted if permissions exist

This is called the Kerberos Referral Process.

🛡️ 8. Security Risks in AD Trusts
Trusts expand the attack surface.
⚠ 1. SID Filtering Bypass
If not enabled, attacker can forge SIDs to escalate privileges.
⚠ 2. Kerberos Golden Ticket Across Trusts
A compromised domain can issue TGTs that work in the trusted domain.
⚠ 3. DCSync Across Forest Trusts
If trust is not properly restricted, replication rights can leak.
⚠ 4. Unmonitored Trust Flow
Attackers use trusts to pivot laterally.

🔧 9. Hardening AD Trusts
🔹 Enable SID Filtering
Prevents SID spoofing.
🔹 Disable Unused Trusts
Remove stale or legacy trusts.
🔹 Use Selective Authentication
Instead of trusting entire domain/forest:

Trust only specific users/groups
Applies “Allowed to Authenticate” ACL

🔹 Restrict Admins Across Trusts
Avoid giving Domain Admin rights across forests.
🔹 Monitor Trust-related Events
Event ID 4713 — Kerberos policy change
Event ID 4769 — TGS request anomalies across trust
Event ID 4624 — Authentication from external domain

🔹 Block NTLM Across Trusts
NTLM across forests is insecure.
Use:

Kerberos only
LDAPs
Secure channels


🔍 10. Trust Scenarios & Real-World Use Cases
⭐ Scenario 1 — Company Merger
Forest Trust used between two companies.
Gradual migration happens without downtime.
⭐ Scenario 2 — Partner Access**
External Trust created only for project resources.
⭐ Scenario 3 — Complex Forest Structure**
Shortcut Trust reduces authentication latency.
⭐ Scenario 4 — Legacy System Integration**
Realm Trust connects AD with Linux Kerberos realm.

📊 11. Visual Summary Diagram
Forest A                           Forest B
----------- Trust Relationship -----------
  Domain A1  ←—— two-way ——→  Domain B1
      |                           |
  Domain A2                   Domain B2

Users in A can authenticate in B (and vice versa)
depending on trust direction + permissions.


🧾 12. Summary
Active Directory Trusts enable collaboration across domains and forests by allowing identity authentication to cross security boundaries.
Trusts must be designed carefully because they affect:

Authentication flow
Attack paths
Lateral movement
Enterprise architecture
Security monitoring

Properly configured and monitored, AD trusts empower hybrid and multi-domain organizations while maintaining security.
