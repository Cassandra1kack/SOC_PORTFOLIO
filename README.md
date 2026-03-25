![Header](https://capsule-render.vercel.app/api?type=slice&color=1a1a1a&height=200&section=header&text=KACK%20Bayiha%20Cassandra%20-%20SOC%20Analyst%20Portfolio&fontSize=30&fontColor=39ff14)
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=700&size=22&pause=1000&color=39FF14&center=true&vCenter=true&width=900&lines=Junior+SOC+Analyst;Incident+investigation+methodology+%7C+Blue+Team;Threat+Detection+%26+Log+Analysis;splunk+%7C+wazuh+%7C+Traffic+Analysis" alt="Typing SVG" />
</p>

## 👤 About Me
My name is **Kack Bayiha Cassandra**, an aspiring SOC Analyst. My expertise focuses on Blue Team operations, intrusion detection, SIEM log analysis, and structured incident reporting.

This repository showcases hands-on security projects built in a realistic lab environment to master the full incident lifecycle: **Detection → Analysis → • → Reporting.**

---
 ##  [Wazuh-Based-Detection-Projects](Wazuh-Based-Detection-Projects)
---
## 🏗️ Lab Architecture

To ensure high-fidelity analysis, I have implemented an isolated enterprise-grade infrastructure:
u
| **Host OS:**| Ubuntu 24.04 LTS (VirtualBox).|
| **SIEM/XDR Platforms:**| Wazuh (Manager & Dashboard) & Splunk Enterprise.|
| **Endpoints:**| Windows 11 (Hardened with **Sysmon**) & Kali Linux (Attacker).|
| **Network:** |Isolated internal virtual network for safe attack simulation.|

---

## 🚀 [Detection & Analysis Projects with wazuh](Wazuh-Based-Detection-Projects) 

###  [RDP/SSH Brute Force Detection](Wazuh-Based-Detection-Projects/README.md)
* **Objective:** Identify and mitigate high-volume authentication attempts.
* **Tools:** Wazuh, Hydra, Windows Event ID **4625**.
* **MITRE Mapping:** [T1110 - Brute Force](https://attack.mitre.org/techniques/T1110/).
* **Outcome:** Configured custom correlation rules and implemented **Active Response** to automatically ban source IPs after 5 failed attempts.
---

##   [SPLUNK Based analytical Projects](Splunk-Use-Cases)

---

###   [Windows log Analysis ](Splunk-Use-Cases/Windows-Security-Logs)

#### 1.Windows Security Event Analysis

🔹 [**RDP Brute Force Analysis**](Splunk-Use-Cases/Windows-Security-Logs/README.md)

Objective: Identify unauthorized access attempts via RDP

> Detection Focus:
>> Multiple failed login attempts
>>> Successful login after brute force
>>>> Suspicious source IP correlation
       

## 2. 🔹 [Phishing & Post-Exploitation log  Analysis on splunk](Splunk-Use-Cases/Windows-Security-Logs/Suspicious-system-activities.md)


 Objective: Detect phishing-related attack activity and post-compromise behavior
 
Detection Focus on:

> Malicious document execution
>> PowerShell activity
>>> Living Off The Land techniques
>>>> Credential dumping
>>>>> Lateral movement
>>>>>> Command & Control (C2)
>>>>>>> Data exfiltration


### [Network & Web Threat Detection](Splunk-Use-Cases/HTTP-DNS-log-analysis)

#### 🔹[DNS & HTTP Log Analysis](Splunk-Use-Cases/HTTP-DNS-log-analysis/Network-and-Web-Threat-Detection.md)

Objective: Detect network-based attacks and suspicious behavior

Detection Focus on :

> NXDOMAIN flood detection
>> DNS tunneling
>>> SQL Injection (SQLi)
>>>> Cross-Site Scripting (XSS)
>>>>> Suspicious user-agents
>>>>>> Abnormal outbound traffic (data exfiltration)
>>>>>>> Correlation of multiple indicators to identify compromised hosts
---

## 🔬 Roadmap & Upcoming Projects

* **Network Threat Detection:** Analyzing DNS logs (Tunneling) and HTTP logs (SQLi, XSS, suspicious User-Agents).
* **Data Exfiltration:** Detecting data leaks via ICMP and web protocol anomalies.
* **Email Security:** Monitoring SMTP traffic and identifying Spam/Phishing indicators.
* **PCAP Analysis:** Wireshark investigations into stealthy port scans and network anomalies.

---

## 🛠️ Technical Stack

| Category | Tools |
| :--- | :--- |
| **SIEM / XDR** | Wazuh, Splunk Enterprise |
| **Host Monitoring** | Sysmon, Windows Event Viewer |
| **Network Analysis** | Wireshark, DNS/HTTP Logs |
| **Attack Simulation** | Kali Linux (Hydra, Metasploit) |
| **Frameworks** | MITRE ATT&CK, NIST Incident Response |

---

## 📂 Repository Structure
* `/Projects`: Detailed folders for each simulation (Logs, Screenshots, Write-ups).
* `/Configs`: Custom configuration files (Wazuh Rules, Sysmon XML).
* `/Reports`: Formal incident reports in PDF format.

---
**linkedin:** [www.linkedin.com/in/cassandra-k-1b323433b] 
