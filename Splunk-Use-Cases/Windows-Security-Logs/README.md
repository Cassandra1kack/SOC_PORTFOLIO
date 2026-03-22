# SOC Investigation Project: RDP Brute Force & Lateral Movement

##  Overview

This project demonstrates a real-world SOC investigation scenario using Windows logs analyzed in Splunk.

The objective was to detect, analyze, and understand a security incident involving:

* RDP brute force attack
* Successful unauthorized access
* Post-compromise activity
* Lateral movement
* Evidence tampering

---

##  Tools Used

* Splunk
* Windows Event Logs [here](Splunk-Use-Cases/Windows-Security-Logs/dataset/windows__logs.csv)
  

---

##  Objectives

* Identify suspicious authentication activity
* Detect brute force patterns
* Trace attacker behavior after compromise
* Reconstruct the attack timeline
* Identify indicators of compromise (IoCs)

---




##  Scenario Summary

The attack originated from IP 45.77.22.91 targeting the administrator account via RDP.
Post-compromise activity included:

* Command execution
* User creation
* Privilege escalation
* Lateral movement
* Log clearing

---

##   Investigation Areas

### 1. Brute Force Detection
I begin by identifying the user/IP with the highest number of failed login attempts.
```splunk
index = windows  EventCode=4625 | top src_ip
```
<img width="1917" height="877" alt="Capture d’écran du 2026-03-21 22-06-14" src="https://github.com/user-attachments/assets/bb720c08-252d-4fca-905c-7450b92e2b7d" />
Detect FAILED authentication (Event ID 4625) after failures
45.77.22.91 who generates the most 4625

### 2. Successful Login Correlation
Now I want to know which IP address successfully connected after the failed attempts.
```splunk
index=windows (EventCode=4625 OR EventCode=4624) src_ip!=10.*
| stats count by _time, user ,src_ip,EventCode
```

<img width="1912" height="1031" alt="Image collée" src="https://github.com/user-attachments/assets/ee0b0fda-9dd0-4da3-8bcc-22a7124c8320" />


I detected a successful authentication (event ID 4624) after failures with the user administrator..
Classic signature of successful brute force.

### 3.Activity after login
What does the attacker do after logging in?
```splunk
index=windows src_ip="45.77.22.91"
| stats count by _time command_line , user
```
<img width="1917" height="979" alt="image" src="https://github.com/user-attachments/assets/abb70136-0889-4dcd-b39b-cf721ce46cb4" />

### 4. Persistence Mechanisms And  Privilege Escalation

Is the attacker adding or creating new users?
```splunk
index=windows (EventCode=4720 OR EventCode=4732)
| table _time , user, command_line, process
```
<img width="1917" height="902" alt="image" src="https://github.com/user-attachments/assets/16852fe6-5dda-49b4-a591-bfd93874bae6" />
user  backupadmin added(Event ID 4720)
> net user backupadmin Password123 /add

user  backupadmin added to privileged groups (Event ID 4732) 
> net localgroup administrators backupadmin /add	


### 6. Defense Evasion
```splunk
index=windows EventCode=1102
```
<img width="1917" height="669" alt="Capture d’écran du 2026-03-21 21-15-46" src="https://github.com/user-attachments/assets/5b4960b9-8302-487f-bd99-cb0bdf9fbc87" />
This is one of the most critical indicators.
This indicates the attacker is attempting to evade detection and hinder investigation.

### 7. Lateral Movement
 I observe remote execution using tools like PsExec.
```splunk
source="windows__logs.csv" host="cassandra-HP-EliteBook-850-G6" 45.77.22.91
| stats count by _time , user ,command_line ,extracted_host
```
<img width="1917" height="889" alt="image" src="https://github.com/user-attachments/assets/bde68bcc-75ce-4bbb-8131-3b096d1e67db" />

Observe remote execution using tools like PsExec.
The attacker  moved laterally to WIN-WS02 using PsExec

---
##  Incident Summary

The investigation identified a successful RDP brute force attack originating from IP 45.77.22.91 targeting the administrator account.

Following initial access on WIN-APP01, the attacker executed commands, created a new privileged user (backupadmin), and established persistence.

The attacker then moved laterally to WIN-WS02 using PsExec and cleared system logs (Event ID 1102) to evade detection.

This indicates a full system compromise with privilege escalation and defense evasion.

---

##  Dataset

The dataset used for this investigation is located in:

```
dataset/windows_soc_training_logs.csv
```

---

##  Detailed Report

A full incident report with detailed analysis, timeline, and conclusions is available :

 [here](Splunk-Use-Cases/Windows-Security-Logs/README%20(Copie).md)

---

##  Skills Demonstrated

* Log analysis
* Threat detection
* Incident investigation
* Splunk query building
* Understanding of Windows Event Logs
* Attack pattern recognition

---

---

## 📌 Author

SOC Analyst (Junior) – Focused on Threat Detection 
