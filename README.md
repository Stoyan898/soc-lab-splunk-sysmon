# 🛡️ SOC Home Lab – Splunk & Sysmon

## 📌 Overview

This project demonstrates a home Security Operations Center (SOC) lab built using VirtualBox, Windows, Linux, Sysmon, and Splunk.

The lab simulates endpoint activity and demonstrates how security analysts detect suspicious behavior using log analysis.

---

## 🧰 Tools & Technologies

* VirtualBox
* Windows 10 VM
* Linux VM
* Sysmon (endpoint logging)
* Splunk (SIEM)
* Splunk Universal Forwarder

---

## 🏗️ Lab Architecture

* Windows VM → generates logs (Sysmon)
* Splunk Forwarder → sends logs
* Splunk Server → collects and analyzes logs

---

## 🔧 Configuration Steps

### 1. Installed Sysmon

* Configured Sysmon with a custom XML configuration
* Enabled logging for:

  * Process creation
  * Network connections
  * File activity

### 2. Installed Splunk Universal Forwarder

* Configured to send logs to Splunk server on port 9997

### 3. Enabled Log Ingestion

* Added Sysmon logs to Splunk using inputs.conf

---

## 🧪 Testing & Validation

### Simulated Activity:

* Executed notepad.exe on Windows endpoint

### Detection in Splunk:

* Queried logs using:

  ```
  index=main notepad.exe
  ```

### Observed:

* EventCode 1 (Process Creation)
* Full process path and user context

---

## 🔍 Key Learnings

* How to collect endpoint telemetry using Sysmon
* How to forward logs to a SIEM
* How to search and analyze logs in Splunk
* Understanding process execution monitoring

---

## 🚀 Future Improvements

* Simulate phishing behavior (PowerShell downloads)
* Detect brute force attacks
* Build Splunk dashboards and alerts
* Create incident response playbooks

---

## 💼 Skills Demonstrated

* SIEM (Splunk)
* Log analysis
* Threat detection
* Windows security monitoring
* SOC fundamentals

-------------------------------------------------------------------------------------------------------------------------------------


## 🔗 Additional Labs

- [Brute Force Detection Lab](brute-force-lab.md)
- [Privilege Escalation Lab](privilege-escalation-lab.md)
