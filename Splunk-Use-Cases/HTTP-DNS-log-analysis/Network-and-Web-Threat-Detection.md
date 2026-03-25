# Splunk Project 1 – Network & Web Threat Detection

## >>> Overview

This project simulates a real-world SOC (Security Operations Center) investigation using Splunk.
My objective is to detect, analyze, and correlate multiple network-based and web-based attacks using DNS and HTTP logs.

The dataset includes both normal and malicious activities to replicate realistic enterprise traffic.

---

## >>> My objectives

* Detect suspicious DNS activity (NXDOMAIN flood, DNS tunneling)
* Identify web-based attacks (SQL Injection, XSS)
* Detect suspicious user behavior (malicious user-agents)
* Monitor abnormal outbound traffic (data exfiltration)
* Correlate multiple indicators to identify compromised hosts

---

##  Data Sources

### 1. [DNS Logs](datasets/dns_logs.csv)
### 2. [HTTP Logs](datasets/http_logs.csv)
---
🔔️Unusual Outbound Data Transfer Detected
---
## INVESTIGATION

## >>> Detection Use Cases

### >> 1. NXDOMAIN Flood Detection


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b1f5d3c9-eb27-4c7e-bd59-16ea704dd059" />

 
Which IP generates the most NXDOMAIN?
Is this suspicious?

**Query:**


```spl
index=dns_logs response_code=NXDOMAIN
| stats count by src_ip

```
<img width="1889" height="695" alt="Capture d’écran du 2026-03-24 11-15-38" src="https://github.com/user-attachments/assets/79a9b453-e347-45d7-a7ef-312e31293b52" />

**Finding:**

* Host `192.168.1.20` generated the highest number of NXDOMAIN queries.

**Analysis:**

* The volume is relatively low but may indicate early-stage reconnaissance or misconfigured activity.

---

### >> 2. DNS Tunneling Detection


**Query:**

```spl
index=your_index sourcetype=dns_logs
| eval query_length=len(query)
| stats count by src_ip
| sort - count
```
<img width="1920" height="1080" alt="Capture d’écran du 2026-03-24 11-24-36" src="https://github.com/user-attachments/assets/b1f76147-da60-446a-b14b-43209b15529d" />

Which machine has the longest queries?
Why is that suspicious?

```spl
index=your_index sourcetype=dns_logs
| eval query_length=len(query)
| where query_length > 20
| stats count avg(query_length) by src_ip
| sort - count
```

<img width="1714" height="903" alt="Capture d’écran du 2026-03-24 14-56-32" src="https://github.com/user-attachments/assets/5fe5a330-2210-4119-8105-4d6d1c537531" />


**The finding:**

* Hosts `192.168.1.10` and `192.168.1.15` generated unusually long DNS queries.

**Analysis:**

* Long and random-looking subdomains (e.g., *.exfil.com) strongly indicate DNS tunneling, often used for covert data exfiltration.

---

### >> 3. Suspicious Domain Detection

Which domains appear to be malicious?
  What machine contacts them?

**Query:**

```spl
index=your_index sourcetype=dns_logs
| search query="*.biz" OR query="*.ru"
| stats count by query, src_ip
```
<img width="1918" height="720" alt="image" src="https://github.com/user-attachments/assets/611eef64-3226-4771-882e-1c2a8d087b93" />

**Finding:**

* The domains appear to be malicious:

  * `malicious-domain.ru`
  * `xj3kq2l9.biz`
  * The machines the contacts them: 192.168.1.10	1	192.168.1.20
   
**Analysis:**

* Uncommon TLDs combined with random naming patterns may indicate command-and-control (C2) communication.

---

### >>4. SQL Injection Detection

Which IP address is launching the attack?
What tool is being used?


```spl
index=your_index sourcetype=http_logs
| search url="*OR 1=1*"
| table timestamp src_ip url user_agent
```

<img width="1916" height="1046" alt="Capture d’écran du 2026-03-24 12-10-52" src="https://github.com/user-attachments/assets/9c07b3a2-9694-434d-bc53-f797bf7d7a2f" />


** The finding:**

* Multiple internal hosts attempted SQL Injection:

  * `192.168.1.10`
  * `192.168.1.15`
  * `192.168.1.20`

* The presence of `sqlmap` user-agent confirms automated exploitation attempts.

---

### >>> 5. Cross-Site Scripting (XSS)

What is the payload used?
Is it automated or manual?

**Query:**

```spl
index=your_index sourcetype=http_logs
| search url="*<script>*"
| table timestamp src_ip url
```
<img width="1714" height="938" alt="Capture d’écran du 2026-03-24 12-17-17" src="https://github.com/user-attachments/assets/1e601226-93c5-43fb-94e7-a568fb81de3b" />

**Finding:**

* XSS payload detected:

  * `<script>alert(1)</script>`

**Analysis:**

* This payload is commonly used to test web application vulnerabilities.
* Cannot confirm automation without additional repetition patterns.

---

### >> 6. Suspicious User-Agent Detection

Quels outils sont utilisés ?
Pourquoi c’est suspect ?

**Query:**

```spl
index=your_index sourcetype=http_logs
| stats count by user_agent
| sort - count
```

<img width="1916" height="1046" alt="Capture d’écran du 2026-03-24 12-08-48" src="https://github.com/user-attachments/assets/44a6ef6d-04bd-4ef5-bbbb-7dc92671eae9" />


**Finding:**

* Suspicious tools identified:

  * `sqlmap/1.5`
  * `curl/7.68.0`

**Analysis:**

* `sqlmap` is a well-known SQL injection tool.
* `curl` may indicate scripted or automated activity.

---

### >> 7. Data Exfiltration Detection

**Query (aggregated):**

```spl
index=your_index sourcetype=http_logs
| stats sum(bytes) as total_bytes by src_ip
| sort - total_bytes
```
<img width="1918" height="720" alt="image" src="https://github.com/user-attachments/assets/5f66834d-053e-45c8-8807-d795cb58a851" />

**Query (event-based):**

```spl
index=your_index sourcetype=http_logs
| where bytes > 5000000
| table timestamp src_ip url bytes dest_ip
```
<img width="1918" height="846" alt="image" src="https://github.com/user-attachments/assets/8a1b9061-0a79-454c-b402-f97a91e1f936" />


**Finding:**

* High data transfer observed from:

  * `192.168.1.20` (largest total volume)
  * `192.168.1.15` (single large upload event)

**Analysis:**

* Large outbound transfers may indicate data exfiltration activity.

---

### >>> 8. Correlation: DNS + HTTP

**Query:**

```spl
(index=your_index sourcetype=dns_logs query="*.exfil.com")
OR
(index=your_index sourcetype=http_logs bytes > 5000000)
| stats count by src_ip
| sort - count
```
<img width="1918" height="846" alt="image" src="https://github.com/user-attachments/assets/3afa5001-f535-4f84-a739-331b77c45501" />


**Finding:**

* Multiple hosts involved:

  * `192.168.1.20` (most suspicious)
  * `192.168.1.10`
  * `192.168.1.15`

---

## Analy

The investigation reveals multiple indicators of compromise across several internal hosts:

* SQL Injection attempts using automated tools
* DNS tunneling behavior via suspicious subdomains
* Communication with suspicious external domains
* Large outbound data transfers

---

## ∆ Conclusion

This scenario suggests a **multi-stage attack**:

1. Initial exploitation via web application attacks (SQL Injection)
2. Command and control communication via DNS tunneling
3. Data exfiltration through HTTP

Multiple internal systems appear compromised, indicating a potential coordinated attack within the network.

---

The investigation was triggered by an alert indicating unusually large outbound HTTP data transfers from an internal host.
---

## 🛠 Tools Used

* Splunk
* SPL (Search Processing Language)



## 📌 Author

Cassandra – SOC Analyst Trainee
