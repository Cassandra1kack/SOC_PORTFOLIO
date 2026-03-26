# Brute Force Detection – SOC Use Case (Wazuh SIEM)

```
Objective:

Detect and respond to high-volume authentication attempts targeting remote access services (RDP).

```
---
## Lab Architecture

![sortie](https://github.com/user-attachments/assets/7b0308a9-1a7c-4c64-b4ef-25e88cb1c7b0)

Attacker: Kali Linux `192.168.100.20`
Victim: Windows 11 `192.168.100.30`
SIEM: Wazuh Manager – Ubuntu Server `192.168.100.10`

---

##  Internal isolated network simulating real SOC environment.

## Attack Simulation
![lR1Aa](https://github.com/user-attachments/assets/d272acab-90e3-4c2b-af43-01fd869a4a72)


>>> Tool used: Hydra
>>>>> Attack type: RDP brute-force
>>>>>>> Target: Windows 11 machine
>>>>>>>>> Generated logs: Multiple failed logins → Windows Event ID 4625

---
## Attack simulation with kali 

Network reconnaissance to identify active hosts

<img width="909" height="1054" alt="Capture d’écran du 2026-03-26 02-30-45" src="https://github.com/user-attachments/assets/2cad8b51-29cd-402b-92d2-7aa837c22bfc" />

>> Execution of brute-force attack using Hydra
>>>>Generation of repeated authentication failures

<img width="911" height="1000" alt="Capture d’écran du 2026-03-26 01-30-56" src="https://github.com/user-attachments/assets/1786829d-dca1-4422-9dc8-ffb6241f7925" />


---

## Investigation 


---

### Event viewer analysis

<img width="1151" height="1000" alt="Capture d’écran du 2026-03-26 01-39-42" src="https://github.com/user-attachments/assets/1abbeb37-4d1c-4cd6-9be6-3e1154a4623b" />



<img width="1916" height="1048" alt="Capture d’écran du 2026-03-26 01-41-03" src="https://github.com/user-attachments/assets/8d3420c3-d388-4b23-a255-c0b07f620c08" />



<img width="1916" height="1048" alt="Capture d’écran du 2026-03-26 01-41-22" src="https://github.com/user-attachments/assets/b1ffb3c0-e782-4b1b-beb2-f114305f97df" />



<img width="1916" height="1048" alt="Capture d’écran du 2026-03-26 01-41-56" src="https://github.com/user-attachments/assets/f620fbc2-90d3-413b-9100-5b157583ff7a" />

**observations:**
In the event viewer log, we see the attacker's machine Kali and its IP address` 192.168.100.20` (event ID: 4625). 
After repeated failures → Successful login detected on account: cassandra • Host: DESKTOP-OUNOFU4

This pattern clearly indicates a brute-force attack followed by account compromise.

>> Same source IP
>>>> Repeated failures
>>>>>> Multiple credential attempts
>>>>>>>> Successful login 

## WAZUH log analysis : use case

We are continuing our investigation in the  wazuh SIEM
Query :
```
data.win.system.eventID:4625 AND data.win.eventdata.ipAddress:192.168.100.20

```

<img width="1916" height="1048" alt="Capture d’écran du 2026-03-26 01-50-32" src="https://github.com/user-attachments/assets/6bc29faf-6722-4ada-ac35-51fec1555fd8" />



<img width="1916" height="1054" alt="Capture d’écran du 2026-03-26 02-18-46" src="https://github.com/user-attachments/assets/b55d7f62-29e1-42ee-b484-b85f3eb31c8b" />





# Behavior observed:

>> High frequency login attempts Event ID: 4625 (Failed Logon)
>>>> Same source IP :`192.168.100.20`
>>>>> Multiple username/password combinations
>>>>>>>> Eventual successful authentication after multiple failures


 This sequence is a classic indicator of a successful brute-force attack.

 
 ## Detection Logic (Wazuh)

Custom rule created to detect brute force behavior:

<img width="1047" height="997" alt="Capture d’écran du 2026-01-11 14-31-59" src="https://github.com/user-attachments/assets/3a5988cc-0a1f-46f2-8971-a01e6148346c" />

Condition:

```XML

<group name="windows,authentication,bruteforce">
  <rule id="100200" level="10" frequency="5" timeframe="120">
    <if_matched_sid>60122</if_matched_sid>
    <same_source_ip />
    <description>
      windows brute force attack detected: multiple failed london attempts
    </description>
    <mitre>T1110</mitre>
  </rule>
  <group>authentication_failed,bruteforce,windows</group>
</group>
```

```
It is configured to activate after 5 failed attempts within 120 seconds, and refers to the MITRE ID T1110 (Credential Stuffing)
```
## MITRE ATT&CK Mapping
 
Technique: T1110 – Brute Force

**Alerting & Response**
 
**Detection**

>> Wazuh triggered alert based on correlation rule
>>> Response (Active Response)
>>>>> Automatic blocking of attacker IP after threshold reached
  Result
>> Attack successfully detected and contained
>>>> Source IP banned in real-time

---

## Key SOC Skills Demonstrated
>>> Log analysis (Windows Security Events)
>>>>>SIEM correlation rule creation
>>>>>>>Threat detection (Brute Force)
>>>>>>>>>MITRE ATT&CK mapping
>>>>>>>>>>>Incident triage
>>>>>>>>>>>>>>Active Response automation

---

##  Key Takeaways


>>Brute force attacks are easily detectable via log patterns

>>>>Correlation rules are critical for reducing noise

>>>>>>Automated response significantly reduces reaction time

>>>>>>>>SIEM visibility is essential for early detection

---

**Author**
Kack B. Cassandra
SOC Analyst (in progress) | Blue Team | Threat Detection
