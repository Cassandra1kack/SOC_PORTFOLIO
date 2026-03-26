#                                   SOC Incident Report – RDP Brute Force Attack



##                                                Incident Summary



A brute-force attack targeting the RDP service was detected from a single external source. The attacker performed multiple failed authentication attempts followed by a successful login, indicating a potential account compromise.

---

##                                                Timeline of Events



>>> **T0:** Multiple failed login attempts detected (Event ID 4625)
>>>>> **T0 + few seconds:** High-frequency authentication failures from IP `192.168.100.20`
>>>>>>>> **T0 + ~2 minutes:** Threshold exceeded → Wazuh alert triggered
>>>>>>>>>>>> **T0 + shortly after:** Successful login detected (Event ID 4624) on account **cassandra**


---


##                                                Detection Details



   >>> **Log Source:** Windows Security Logs

   >>>>> **SIEM:** Wazuh

   >>>>>>> **Detection Rule ID:** 100200

 
 
 **Trigger Condition:**


   > * 5 failed login attempts
   >> * Within 120 seconds
   >>> * Same source IP


 #                                                      **Relevant Events:**

   

   
   >>>>>> * Event ID 4625 → Failed logon
   >>>>>>>>>> * Event ID 4624 → Successful logon

---


##                                                  Indicators of Compromise (IOCs)




* **Source IP:** `192.168.100.20`
* **Target Host:** DESKTOP-OUNOFU4
* **Target Accounts:** Administrateur, cassandra
* **Attack Method:** RDP brute-force

---


##                                                   Impact Assessment




* Unauthorized access achieved via valid credentials
* Potential compromise of user account **cassandra**
* Risk of lateral movement or data access

---



##                                                  Actions Taken




>>>>> * Detection via Wazuh correlation rule
>>>>>>>>> * Automatic blocking of attacker IP (Active Response)
>>>>>>>>>>>>> * Incident contained in real-time

---


##                                                  Recommendations

>>>>>>> Enforce strong password policy

>>>>>>>>>> Enable account lockout after multiple failed attempts

>>>>>>>>>>>>>>> Implement Multi-Factor Authentication (MFA) for RDP access

>>>>>>>>>>>>>>>>>>>> Restrict RDP exposure (VPN / firewall rules)

>>>>>>>>>>>>>>>>>>>>>>>>> Monitor for post-compromise activity

---


## 📊 MITRE ATT&CK Mapping

* **Technique:** T1110 – Brute Force
* **Tactic:** Credential Access

  

---

##  Incident Status

 Contained
 Requires follow-up investigation (post-compromise activity)

---

## 👤 Analyst

Kack B. Cassandra
SOC Analyst (Aspiring)
