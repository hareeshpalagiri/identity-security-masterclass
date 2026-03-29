📘 Section 08 — Hybrid Identity

Chapter 06 — Hybrid Azure AD Join (Hybrid Identity Device Model)


🔰 1) Introduction
Hybrid Azure AD Join enables on‑premises Active Directory–joined Windows devices to register with Microsoft Entra ID, giving them a cloud identity alongside their traditional AD identity.
This dual registration allows:

Seamless SSO to cloud apps
Conditional Access on device compliance
Modern authentication (OAuth / OIDC)
Intune integration
Device-based access policies

Hybrid Azure AD Join is the most common enterprise device identity model during cloud transition.

🧠 2) Why Hybrid Azure AD Join Matters
Enterprises adopting Zero Trust need to know who the user is and what the device is. On-prem AD alone cannot provide device posture or cloud identity signals.
Hybrid Azure AD Join enables:
✔ Modern authentication for domain-joined devices
Tokens include device claims, enabling CA and MFA.
✔ Seamless SSO across hybrid environments
Kerberos → Entra ID token → Cloud apps.
✔ Conditional Access enforcement
You can require:

Compliant device
Hybrid join
Device risk checks

✔ Device inventory consolidation
Device appears in:

Local AD
Entra ID
Intune (if enrolled)

✔ Smooth transition to cloud-only device join
Hybrid AD Join is often an interim step before moving to Azure AD Join.

🧩 3) How Hybrid Azure AD Join Works
A hybrid joined device has two identities:
AD Computer Account → On-Prem Identity
Azure AD Device Object → Cloud Identity

High-Level Flow
1. Device is joined to AD Domain
2. GPO sets the SCP (Service Connection Point)
3. Device communication → Entra ID via Device Registration Service (DRS)
4. Device registers using Kerberos credentials
5. Entra ID creates a "Device" object
6. Device stores PRT (Primary Refresh Token)
7. Seamless SSO → Cloud Apps

Key Components

























ComponentPurposeSCPTells devices where the Azure DRS isDRS (Device Registration Service)Handles device onboardingPHS/PTA or FederationRequired for user authenticationIntune MDM Auto-enrollment (optional)Automatic device management
Hybrid Join supports:

Windows 10
Windows 11
Windows Server 2016+


🏗️ 4) Requirements for Hybrid Azure AD Join
1. Azure AD Connect (or Cloud Sync)
Hybrid Join requires device writeback or device registration via sync
(not required for Cloud Sync).
2. SCP Configuration
Set via GPO:
Computer Configuration → Policies → Administrative Templates  
→ Windows Components → Device Registration

3. Device OS Support
Windows 10 1607+ or Windows Server 2016+.
4. Network Access to Microsoft endpoints
DRS & login.microsoftonline.com endpoints must be reachable.
5. Entra ID device settings
Enable:
Users may join devices to Azure AD → All / Selected

6. Time Synchronization
Kerberos requires ±5 minutes skew.

🧩 5) Primary Refresh Token (PRT)
The key to seamless SSO
Hybrid joined devices obtain a PRT, which provides:

Token-based authentication
Seamless reauthentication
CA & device info embedded in token
Single sign-on to M365 and cloud apps

PRT contains:

Device ID
MDM status
User identity
Session metadata

PRT issuance requires:

Hybrid Join
User sign-in using AD credentials
Flow validated via Entra ID


🔐 6) Common Security Risks
1. Broken SCP → Device does not join cloud
Device shows as only AD joined → CA breaks.
2. Inconsistent Time Sync → Kerberos failure
Device cannot request registration key.
3. Missing device object
Entra ID does not trust device → CA blocks.
4. Stale or duplicate device objects
Attackers may re-register devices for lateral movement.
5. PRT misuse
If attacker steals PRT → session hijack possibility.

🛡️ 7) Hardening & Best Practices
✔ Use Conditional Access with device filters
Examples:

Require hybrid joined device
Block unmanaged devices
Require compliant devices for admins

✔ Enable Intune auto-enrollment

Ensures device compliance
Provides security signals
Enables MDM policies

✔ Wipe stale devices
Regular cleanup:

Remove devices not active for 180+ days
Block PRT issuance for stale devices

✔ Protect AD Connect
As it impacts device sync and identity.
✔ Use Windows Hello for Business
Best pairing with Hybrid Join for:

Passwordless
Key-based authentication


🛠️ 8) Troubleshooting Hybrid Join
1. Device doesn’t show as “Hybrid Azure AD Joined”
Check:

Event ID 201 (DSREG)
SCP GPO
DRS connectivity
AD Connect sync logs

2. User SSO failure

Check PRT issuance (dsregcmd /status → PRT: Yes)
Check time sync

3. Intune not enrolling

MDM auto-enrollment must be configured
User must have Intune license

CLI Tool
Run:
dsregcmd /status

Key values:

Device state → AzureAdJoined: YES
HybridJoined → YES
PRT → YES
TenantId → matches Entra ID


🧾 9) Summary
Hybrid Azure AD Join bridges traditional AD device identity with cloud-native identity to enable:

Modern authentication
Stronger device-based Conditional Access
Seamless SSO
Compliance posture evaluation
Hybrid → Cloud transition

It is the recommended approach for organizations that still rely on on-prem AD but want to enable Zero Trust with modern device signals.
A secure hybrid device identity ensures that both user and device are verified before access is granted — the essence of Zero Trust.
