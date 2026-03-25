![Header](https://capsule-render.vercel.app/api?type=waving&color=39ff14&height=200&section=header&text=KACK%20Bayiha%20Cassandra%20|%20Aspiring%20SOC%20Analyst%20L1&fontSize=35&fontColor=ffffff)

![Header](https://capsule-render.vercel.app/api?type=soft&color=00d4ff&height=200&section=header&text=Cassandra%20KACK%20|%20Cybersecurity%20%26%20Blue%20Team%20Operations&fontSize=30&fontColor=ffffff)

![Header](https://capsule-render.vercel.app/api?type=slice&color=1a1a1a&height=200&section=header&text=KACK%20Bayiha%20Cassandra%20-%20SOC%20Analyst%20Portfolio&fontSize=30&fontColor=39ff14)
## About Me

My name is **Kack Bayiha Cassandra**.
I am focused on SOC operations, Blue Team defense, incident detection, and security incident reporting.

This repository showcases hands-on security projects built in a realistic lab environment to develop practical skills in monitoring, detection, and structured incident analysis.

My objective is to grow into a **SOC Analyst / Blue Team** role with strong foundations in:

* SIEM monitoring
* Log analysis (Windows, network, authentication, services)
* Incident investigation methodology
* MITRE ATT&CK mapping
* Professional incident reporting

---

## Objective of This Portfolio

This lab demonstrates:

* Practical experience with SIEM platforms
* Detection of real-world attack scenarios
* Log analysis across Windows and network services
* End-to-end SOC L1 workflow (Detect → Analyze → Report → Lessons Learned)
* Mapping detections to MITRE ATT&CK techniques

Each project represents a complete SOC scenario from attack simulation to documented incident report.

---

# Lab Architecture

**Host OS:** Ubuntu 24.04
**Virtualization:** VirtualBox
**SIEM Platforms:** Wazuh & Splunk
**Endpoints:** Windows 11 (Victim), Kali Linux (Attacker)
**Network:** Isolated internal lab network


---

# Projects Overview

## Wazuh-Based Detection Projects

### 1. Brute Force Detection

* Objective: Detect authentication brute force attempts.
* Tools: Wazuh, Hydra, Windows Event ID 4625
* MITRE ATT&CK: T1110 – Brute Force

---

---

# Splunk Log Analysis Projects

### W. [WINDOWS log analysis](Splunk-Use-Cases/Windows-Security-Logs)

 #### [RDP BRUT-FORCE analysis](Splunk-Use-Cases/Windows-Security-Logs/README.md)
  Objectif is to detect or identify:
  
. Command execution
. User creation
. Privilege escalation
. Lateral movement
. Log clearing

 #### [PHYSHING analysis](Splunk-Use-Cases/Windows-Security-Logs/phishingREADME.md)

 
  Objectif is to detect or identify:
  
- Phishing (malicious document)
- PowerShell execution
- Living Off The Land techniques
- Credential dumping
- Lateral movement
- Command & Control (C2)
- Data exfiltration



---
### [Network & Web Threat Detection](Splunk-Use-Cases/HTTP-DNS-log-analysis/Network-and-Web-Threat-Detection.md) 


> DNS logs
>> HTTP logs

*Objectives*:

Detect suspicious DNS activity (NXDOMAIN flood, DNS tunneling)
Identify web-based attacks (SQL Injection, XSS)
Detect suspicious user behavior (malicious user-agents)
Monitor abnormal outbound traffic (data exfiltration)
Correlate multiple indicators to identify compromised hosts

---

Projet 2 : User Access & Credential Threats**

**Sources de logs :**

* SSH Logs
* FTP Logs

**Objectifs :**

* Détecter les tentatives de brute force SSH
* Identifier les patterns “failed → successful login”
* Surveiller les uploads/downloads FTP suspects ou non autorisés

---

### 8. SMTP Log Analysis

* Detect phishing indicators
* Identify spam campaigns
* Monitor unusual outbound mail traffic

---

### 9. DHCP Log Analysis

* Detect rogue DHCP activity
* Identify unusual IP allocation patterns

---

### 10. Tunnel & Data Exfiltration Detection

* DNS tunneling detection
* ICMP tunneling analysis
* HTTP-based exfiltration patterns

---

# Network Traffic Analysis

## Wireshark Investigations

* PCAP analysis for port scanning
* DNS anomaly inspection
* Suspicious HTTP payload review
* SSH session analysis

---


---

# Security Tools Used

* Wazuh – SIEM & XDR platform
* Splunk Enterprise – Log analysis & correlation
* Sysmon – Advanced Windows logging
* Wireshark – Packet inspection
* Kali Linux – Attack simulation
* MITRE Corporation – ATT&CK Framework

---

# Author

Kack Bayiha Cassandra
Cybersecurity | SOC | Blue Team
