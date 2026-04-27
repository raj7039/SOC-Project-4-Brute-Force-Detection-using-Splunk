# 🔐 Brute Force Detection using Splunk

## 📌 Objective
Detect brute force login attempts in real time by analyzing Windows 
Security Event Logs using Splunk Enterprise.

## 🛠 Tools Used
- Splunk Enterprise
- Splunk Universal Forwarder
- Windows Event Viewer
- Windows Security Logs

## 🎯 MITRE ATT&CK
- Technique: T1110 — Brute Force
- Sub-technique: T1110.001 — Password Guessing

## ⚙️ How It Works

### Step 1 — Environment Setup
- Installed Splunk Enterprise on Windows machine
- Installed and configured Universal Forwarder
- Configured inputs.conf to forward Windows Security logs to Splunk

### Step 2 — Attack Simulation
- Generated multiple failed login attempts using wrong credentials
- Windows logged each failure as Event ID 4625

### Step 3 — Detection Query (SPL)
```spl
index=wineventlog EventCode=4625
| stats count by Account_Name, src_ip
| where count > 5
| sort -count
```

### Step 4 — Alert Created
- Alert name: Brute Force Detection Alert
- Schedule: Runs every 5 minutes
- Trigger condition: count > 5 failed logins from same account
- Action: Add to triggered alerts

### Step 5 — Verified Detection
- Simulated brute force attack
- Alert triggered in real time within 5 minutes
- Dashboard showed failed login count by account and IP

## 📊 Findings
- Detected 100+ failed login attempts from suspicious IPs
- Identified attacker targeting specific user accounts repeatedly
- Confirmed brute force pattern through login frequency analysis

## 🛡️ SOC Response Steps
1. Identify source IP from Splunk results
2. Check if IP is known or suspicious using VirusTotal
3. Block IP at firewall if confirmed malicious
4. Reset targeted account password
5. Escalate to L2 if attack is ongoing
6. Document incident with timeline and findings

## 📸 Screenshots
See /screenshots folder for:
- Splunk query results
- Alert configuration
- Dashboard showing login anomalies
- Alert firing in real time

## 🎓 Skills Demonstrated
- Splunk SIEM — log ingestion, SPL query writing, alert creation
- Windows Event Log analysis — Event ID 4625
- Threat detection and alert triage
- MITRE ATT&CK framework mapping
