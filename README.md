# splunk-bruteforce-detection
Brute-force detection in Splunk using simulated Windows failed logon events (Event ID 4625).

# 🕵️ Brute-Force Attack Detection with Splunk (Failed Logons 4625)

## 📄 Project Overview

This project simulates a real-world brute-force detection scenario using Splunk. The goal was to detect multiple failed login attempts that could indicate brute-force activity. Windows Security Event ID `4625` was used to represent failed login attempts. Log data was simulated, uploaded to Splunk, and queried using SPL to identify suspicious patterns.

## 🔧 Tools Used

* Splunk Enterprise (local install)
* Simulated `failed_logons.csv` log file
* Windows Event ID `4625` (Failed Logon)

## ⚖️ Detection Logic (SPL)

```spl
index=main sourcetype=csv EventID=4625
| stats count by Account_Name, IpAddress
| where count > 3
```

## 🔎 Detection Results

| Account Name  | IP Address    | Count |
| ------------- | ------------- | ----- |
| larion.morris | 192.168.1.100 | 6     |
| larion.morris | 192.168.1.101 | 7     |

> These results show repeated failed login attempts for the same user from different IPs, a strong indicator of brute-force behavior.

## 🛡️ SOC Relevance

* Maps to MITRE ATT\&CK technique: **T1110 (Brute Force)**
* Demonstrates log ingestion, correlation, and detection using SPL
* Builds skills in triage, alert logic, and threat hunting foundations

## 🔹 Next Steps

* Expand dataset to include successful logons for correlation
* Set up alert conditions in Splunk (Scheduled Search)
* Integrate with threat intelligence for enrichment (e.g., AbuseIPDB)

---

## 🖼️ Screenshots

- **Splunk Login Page:** Shows initial access to the platform ![image](https://github.com/user-attachments/assets/717516d2-af3f-43cc-8563-c0b086655a68)

- **Splunk Dashboard:** Confirming successful setup ![image](https://github.com/user-attachments/assets/543b5753-de28-4e8b-8789-26071ecdbe49)

- **Query Results:** Detection of brute-force attempts by user `larion.morris` ![image](https://github.com/user-attachments/assets/4471550a-ff5c-4f01-8315-4348da252de5)



*Created by Larion Morris as part of a cybersecurity portfolio to demonstrate hands-on detection capabilities using Splunk.*

