![Header](https://capsule-render.vercel.app/api?type=slice&color=1a1a1a&height=200&section=header&text=KACK%20Bayiha%20Cassandra%20-%20SOC%20Analyst%20Portfolio&fontSize=30&fontColor=39ff14)
<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=700&size=22&pause=1000&color=39FF14&center=true&vCenter=true&width=900&lines=Junior+SOC+Analyst;Incident+investigation+methodology+%7C+Blue+Team;Threat+Detection+%26+Log+Analysis;splunk+%7C+wazuh+%7C+Traffic+Analysis" alt="Typing SVG" />
</p>

## 👤 About Me
My name is **Kack Bayiha Cassandra**, an aspiring SOC Analyst. My expertise focuses on Blue Team operations, intrusion detection, SIEM log analysis, and structured incident reporting.

This repository showcases hands-on security projects built in a realistic lab environment to master the full incident lifecycle: **Detection → Analysis → Response → Reporting.**

---

## 🏗️ Lab Architecture
To ensure high-fidelity analysis, I have implemented an isolated enterprise-grade infrastructure:
* **Host OS:** Ubuntu 24.04 LTS (VirtualBox).
* **SIEM/XDR Platforms:** Wazuh (Manager & Dashboard) & Splunk Enterprise.
* **Endpoints:** Windows 11 (Hardened with **Sysmon**) & Kali Linux (Attacker).
* **Network:** Isolated internal virtual network for safe attack simulation.

---

## 🚀 Detection & Analysis Projects (Completed)

### 1️⃣ RDP/SSH Brute Force Detection
* **Objective:** Identify and mitigate high-volume authentication attempts.
* **Tools:** Wazuh, Hydra, Windows Event ID **4625**.
* **MITRE Mapping:** [T1110 - Brute Force](https://attack.mitre.org/techniques/T1110/).
* **Outcome:** Configured custom correlation rules and implemented **Active Response** to automatically ban source IPs after 5 failed attempts.

### 2️⃣ Post-Compromise Forensic Analysis (Splunk)
* **Scenario:** Investigation of a Windows machine following a successful breach.
* **Artifacts Detected:**
    * Suspicious command execution (CMD/PowerShell).
    * Malicious user account creation.
    * Privilege escalation attempts.
    * Security log tampering (**Log Clearing**).

### 3️⃣ Phishing Campaign Investigation
* **Scenario:** Analyzing the execution of a malicious document (macro-based).
* **Analysis Points:**
    * **Living Off The Land (LotL)** techniques via PowerShell.
    * Credential harvesting and C2 (Command & Control) communications.
    * Lateral movement detection across the network.

---

## 🔬 Roadmap & Upcoming Projects
*These modules are currently being implemented in the lab:*

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
| **Network Analysis** | Wireshark, Zeek (DNS/HTTP Logs) |
| **Attack Simulation** | Kali Linux (Hydra, Metasploit) |
| **Frameworks** | MITRE ATT&CK, NIST Incident Response |

---

## 📂 Repository Structure
* `/Projects`: Detailed folders for each simulation (Logs, Screenshots, Write-ups).
* `/Configs`: Custom configuration files (Wazuh Rules, Sysmon XML).
* `/Reports`: Formal incident reports in PDF format.

---
**Contact:** [Your LinkedIn Link] | [Your Email Address]
