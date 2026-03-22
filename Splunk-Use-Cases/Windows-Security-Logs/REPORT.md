## Attack Summary

The investigation reveals a successful compromise of **WIN-APP01** following a brute force attack on an administrator account. After gaining access, the attacker executed commands, established persistence, escalated privileges, moved laterally, and attempted to erase evidence.

---

## Attack Timeline

**08:22:00** — Initial command execution

* `whoami`
  > Attacker verifies access and privileges.

**08:23:00** — Suspicious PowerShell execution

* `powershell -enc SQBFAFgA`
  > Encoded command indicates potential malicious script execution.

**08:24:00** — Persistence established

* `net user backupadmin Password123 /add`
  > New user created for long-term access.

**08:25:00** — Privilege escalation

* `net localgroup administrators backupadmin /add`
  > User added to Administrators group.

**08:26:00** — Malicious service installed
>Indicates persistence or malware deployment.

**08:27:00** — Defense evasion

* `audit log cleared`
  > Attacker deletes logs to hide activity.

**08:30:00 – 08:30:15** — Lateral movement

* `psexec \\WIN-DB01 cmd.exe` (from WIN-WS02)
   Attacker moves to another system using PsExec.

---

## Impact Assessment

* Unauthorized administrative access
* Persistence established via new admin account
* Potential malware/service deployment
* Lateral movement across systems
* Evidence tampering (log deletion)

---

## Recommendations

###  Access Control

* Disable direct RDP exposure to the internet
* Enforce **strong password policies**
* Enable **Multi-Factor Authentication (MFA)**

### Monitoring & Detection

* Monitor critical Event IDs:

  * 4624 (login success)
  * 4625 (login failed)
  * 4720 (user creation)
  * 4732 (privilege escalation)
  * 1102 (log clearing)
* Alert on:

  * Multiple failed logins followed by success
  * PowerShell with encoded commands

###  Endpoint Security

* Deploy an EDR solution
* Monitor use of tools like PsExec

### Incident Response

* Reset compromised accounts immediately
* Remove unauthorized users (e.g., backupadmin)
* Investigate all affected hosts (WIN-APP01, WIN-WS02, WIN-DB01)

---

## Conclusion

This attack follows a classic pattern:

**Brute Force → Initial Access → Persistence → Privilege Escalation → Lateral Movement → Defense Evasion**

