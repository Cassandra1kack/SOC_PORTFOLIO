###  Incident Ticket – SOC Escalation (L1 → L2)

**Title:** Suspected Compromise via Phishing leading to Lateral Movement & Data Exfiltration
**Severity:** High
**Status:** Escalated to L2

---

###  Detection Source

SIEM alert triggered in Splunk based on suspicious PowerShell activity and abnormal process chain.

---

###  Affected Assets

* WIN-WS01 (initial compromise)
* WIN-APP01 (post-compromise activity)
* WIN-DB01 (data exfiltration target)

---

###  Timeline of Events

* User *alice* opened `invoice.docm` on **WIN-WS01**
* PowerShell executed with encoded command (`-enc`)
* Use of LoLBins (certutil, wmic, bitsadmin)
* Execution of credential dumping tool (Mimikatz) on **WIN-APP01**
* Lateral movement via PsExec to **WIN-DB01**
* Outbound connection to `185.193.88.10:443`
* Data exfiltration identified (`data.zip`)

---

###  Technical Analysis

* Suspicious parent-child process:
  `winword.exe → powershell.exe`

* Encoded PowerShell execution detected (~150 events)

* Evidence of credential dumping:
  `mimikatz sekurlsa::logonpasswords`

* Lateral movement command observed:
  `psexec \\WIN-DB01 cmd.exe`

* C2 communication:
  PowerShell connecting to external IP over HTTPS

---

###  Impact Assessment

* Administrator credentials likely compromised
* Multiple systems accessed by attacker
* Sensitive data potentially exfiltrated

---

###  Recommended Actions (L2 / IR Team)

1. Isolate affected systems immediately
2. Reset all privileged accounts (especially administrator)
3. Block malicious IP `185.193.88.10` at firewall
4. Investigate lateral movement scope across network
5. Perform full endpoint scan (EDR)
6. Review logs for persistence mechanisms

---

###  Evidence Collected

* Event ID 4688 (PowerShell, cmd execution)
* Event ID 4624 / 4625 (authentication activity)
* Command-line logs (encoded payloads, Mimikatz, PsExec)

---

###  Escalation Reason

Confirmed indicators of compromise including:

* Execution of malicious payload
* Credential dumping activity
* Lateral movement
* Data exfiltration

Incident requires deeper forensic investigation and containment.

---

**Analyst (L1):** SOC Analyst
**Escalated to:** SOC L2 / Incident Response Team
**Date:** [22 march 2026]
