# Cassandra SOC Lab

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

## [Wazuh-Based Detection Projects](Wazuh-Based-Detection-Projects)

### 1. Brute Force Detection

* Objective: Detect authentication brute force attempts.
* Tools: Wazuh, Hydra, Windows Event ID 4625
* MITRE ATT&CK: T1110 – Brute Force

---

### 2. Endpoint Threat Detection

* Objective: Monitor suspicious processes and malicious scripts.
* Tools: Sysmon, Windows Event Logs, Wazuh custom rules
* MITRE ATT&CK: T1059 – Command and Scripting Interpreter

---

### 3. Lateral Movement & Privilege Abuse

* Objective: Detect SMB abuse and privilege escalation attempts.
* Tools: Wazuh correlation rules, Windows Security logs
* MITRE ATT&CK: T1021 – Remote Services

---

# Splunk Log Analysis Projects
### W. [WINDOWS log analysis](Splunk-Use-Cases/Windows-Security-Logs/README.md)
 #### [RDP BRUT-FORCE analysis](Splunk-Use-Cases/Windows-Security-Logs/README.md)
  Objectif is to detect or identify:
  
. Command execution
. User creation
. Privilege escalation
. Lateral movement
. Log clearing

 #### PHYSHING analysis
  Objectif is to detect or identify:
  
- Phishing (malicious document)
- PowerShell execution
- Living Off The Land techniques
- Credential dumping
- Lateral movement
- Command & Control (C2)
- Data exfiltration


### 4. DNS Log Analysis

* Detect suspicious domains
* Identify DNS tunneling patterns
* Detect NXDOMAIN flood
* MITRE ATT&CK: T1071.004 – Application Layer Protocol (DNS)

---

### 5. HTTP Log Analysis

* Detect SQL Injection patterns
* Identify XSS attempts
* Detect suspicious user-agents
* Monitor large data transfers

---

### 6. SSH Log Analysis

* Detect brute force attempts
* Identify failed → successful login patterns
* Detect suspicious remote access

---

### 7. FTP Log Analysis

* Detect unauthorized file uploads
* Monitor abnormal file transfers
* Identify suspicious authentication attempts

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

# Repository Structure

Cassandra-SOC-Lab/

├── 01-Lab-Architecture/
├── 02-Wazuh-Projects/
│   ├── SOC-BruteForce-Detection/
│   ├── SOC-Endpoint-Threat-Detection/
│   └── SOC-Lateral-Movement/
│
├── 03-Splunk-Projects/
│   ├── DNS-Log-Analysis/
│   ├── HTTP-Log-Analysis/
│   ├── SSH-Log-Analysis/
│   ├── FTP-Log-Analysis/
│   ├── SMTP-Log-Analysis/
│   ├── DHCP-Log-Analysis/
│   └── Tunnel-Detection/
│
├── 04-Wireshark-Analysis/
│
└── README.md

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
