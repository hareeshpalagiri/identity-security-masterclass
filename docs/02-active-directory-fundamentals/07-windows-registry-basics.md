Chapter 06A — Windows Registry Basics for AD & Identity Engineers
(Simple, practical, medium-depth, exactly what was requested)

This chapter teaches only what Identity / AD / IAM engineers truly need, without turning it into a full OS internals course.


🔹 1. What is the Windows Registry? (Simple Explanation)
The Windows Registry is a hierarchical database that stores:

OS configuration
Application settings
Authentication & identity parameters
Network and DNS client settings
Kerberos & NTLM behavior
Group Policy results
Service configurations

The registry is the brain of Windows configuration.

🔹 2. Why Identity Engineers Must Know the Registry
Even though GPO manages configuration at scale, the Registry is critical for:

Troubleshooting Kerberos failures
Fixing DNS client misconfigurations
Understanding GPO applications
Hardening authentication protocols
Controlling LSA, NTLM, LDAP, SMB settings
Understanding site-aware DC locator behavior

These settings are stored under registry keys such as:
HKLM\SYSTEM\CurrentControlSet\Services\Netlogon  
HKLM\SYSTEM\CurrentControlSet\Services\KDC  
HKLM\SYSTEM\CurrentControlSet\Services\Dnscache  
HKLM\SYSTEM\CurrentControlSet\Control\Lsa  


🔹 3. Registry Structure (Practical Basics)





























HivePurposeHKLMMachine-level settings (AD, DNS, Kerberos)HKCUUser profile & login settingsHKCRFile associations, COM componentsHKUProfiles of all user accountsHKCCHardware profile
Think of each hive like departments inside a kingdom —
each silo handles different responsibilities.

🔹 4. How to Open & Navigate the Registry
Open Registry Editor
Win + R → regedit → Enter

Navigation Basics
Left pane = folders (keys)
Right pane = configuration items (values)

🔹 5. Registry Data Types (Easy to Remember)





























TypeMeaningREG_SZTextREG_DWORD32‑bit number (most security settings)REG_BINARYRaw binary dataREG_MULTI_SZList of stringsREG_EXPAND_SZVariables allowed
Most AD-related hardening (Kerberos, NTLM, SMB) uses REG_DWORD.

🔹 6. AD / Identity-Related Registry Keys (Very Important)
✔ Kerberos
HKLM\System\CurrentControlSet\Control\Lsa\Kerberos

✔ NTLM Hardening
HKLM\System\CurrentControlSet\Control\Lsa

✔ DNS Client Behavior
HKLM\System\CurrentControlSet\Services\Dnscache\Parameters

✔ LDAP Signing
HKLM\System\CurrentControlSet\Services\LDAP\Parameters

✔ Netlogon (DC Locator)
HKLM\System\CurrentControlSet\Services\Netlogon\Parameters

✔ GPO applied settings
(GPO writes registry settings automatically)
HKLM\Software\Policies\Microsoft


🔹 7. Safe Ways to Edit the Registry
Never edit blindly. Apply these rules:
✔ Always Export Before Editing
Right‑click key → Export
✔ Prefer GPO Instead of Manual Editing
GPO writes to the registry anyway.
✔ Do NOT modify:

Kerberos
LSA
DNS client
Cryptography keys
unless you understand the impact.

✔ Create system restore points on workstations

🔹 8. Useful Registry Commands
✔ Query value
PowerShellreg query HKLM\SYSTEM\CurrentControlSet\Services\KDCShow more lines
✔ Add value
Mermaidreg add HKLM\Software\Test /v DemoValue /t REG_DWORD /d 1 /fShow more lines
✔ PowerShell Registry Provider
PowerShellGet-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Services\NetlogonShow more lines

🔹 9. When Registry Knowledge Helps the Most

Kerberos failing → Check LogLevel, SupportedEncryptionTypes
DNS issues → Check Dnscache parameters
NTLM disabled → LSA policies reflect it
LDAP signing → LDAP Parameters registry key
GPO not applying → Check applied registry under Policies path
Domain join issues → Netlogon parameters

For AD engineers, registry insight = faster troubleshooting.

🔹 10. Summary (Short & Clear)
This chapter covered:

What the registry is
Why IAM/AD engineers need it
Structure of hives
Important keys for identity
Safe editing
Commands
How registry + GPO are related

This is a foundation chapter for later topics such as:

AD hardening
Authentication protocols
Kerberos/NTLM tuning
GPO troubleshooting
DC Locator behavior

