# SOC Investigation Project: Phishing → LoLBins → RDP → Data Exfiltration

## 📌 Overview

This project simulates a real-world SOC investigation using Windows logs analyzed in Splunk.

The objective is to detect and analyze a full attack chain including:

- Phishing (malicious document)
- PowerShell execution
- Living Off The Land techniques
- Credential dumping
- Lateral movement
- Command & Control (C2)
- Data exfiltration

---

## 🛠️ Tools

- Splunk
- Windows Event Logs
- Sysmon (simulated logs)

---

## ⚠️ Attack Scenario

1. User opens a phishing document (`invoice.docm`)
2. PowerShell payload is executed
3. Attacker uses LoLBins:
   - certutil
   - bitsadmin
   - wmic
4. Credentials are dumped using Mimikatz
5. Lateral movement via PsExec
6. C2 communication to external IP
7. Data exfiltration (`data.zip`)

---

## 🔍 Key Findings

- Suspicious process chain:
  winword.exe → powershell.exe

- Encoded PowerShell detected:
  powershell -enc

- Credential dumping:
  mimikatz sekurlsa::logonpasswords

- Lateral movement:
  psexec \\WIN-DB01

---

## 📊 Splunk Queries

### Detect PowerShell encoded
