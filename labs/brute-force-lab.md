# 🛡️ SOC Home Lab – Splunk & Windows Security Logs

## 📌 Overview

After completing my CompTIA Security+ certification with no prior hands-on SOC experience, I built a home lab to simulate real-world security monitoring and detection.

This lab focuses on detecting brute force login attempts using Windows Security logs and Splunk SIEM.

---

## 🧰 Tools & Technologies

* VirtualBox
* Windows VM
* Sysmon
* Splunk Enterprise

---

## 🏗️ Lab Setup

### Step 1 – Install Splunk

* Installed Splunk Enterprise on Windows VM
* Accessed web interface via:

  ```
  http://localhost:8000
  ```

---

### Step 2 – Configure Log Ingestion

* Used Splunk “Add Data” feature
* Selected:

  * Local Event Logs
  * Security logs

---

### Step 3 – Generate Security Events

* Locked system using:

  ```
  Windows + L
  ```
* Entered incorrect password multiple times
* Generated:

screenshot event_viewer

  * EventCode 4625 (failed login)

---

### Step 4 – Verify Logs in Splunk

Search used:

```
index=main EventCode=4625
```
screenshot event_code_4625
---

## 🚨 Brute Force Detection

### Detection Query

```
index=main EventCode=4625
| stats count by Account_Name, Source_Network_Address
| where count > 5
```
screenshot stats_count
---

### Advanced Detection

```
index=main EventCode=4625
| bin _time span=5m
| stats count by _time, Account_Name
| where count > 5
```
screenshot bin_time
---

## 🧪 Results

* Successfully detected multiple failed login attempts
* Identified potential brute force behavior
* Observed login patterns in real time

---

## ⚠️ Challenges & Troubleshooting

### Issue 1 – No logs in Splunk

* Forwarder was installed but not collecting logs
* Missing configuration file (inputs.conf)

### Fix:

* Created inputs.conf manually
* Added Windows Security logs configuration

---

### Issue 2 – Splunk Forwarder service not responding

Error:

```
service is not responding to control function (NET HELPMSG 2186)
```

### Fix:

* Terminated splunkd.exe process manually
* Restarted forwarder using command line
* Eventually switched approach to direct ingestion

---

### Issue 3 – Access denied when starting Splunk

Error:

```
Splunkd: Unable to start the service: Access is denied
```

### Fix:

* Ran Command Prompt as Administrator
* Verified correct installation path

---

### Issue 4 – Splunk command not recognized

Error:

```
'splunk' is not recognized as an internal or external command
```

### Fix:

* Navigated to correct directory:

  ```
  C:\Program Files\Splunk\bin
  ```
* Ran Splunk from installation folder

---

### Issue 5 – No EventCode 4625 in Splunk

* Logs existed in Event Viewer but not in Splunk

### Root Cause:

* Forwarding configuration issues

### Final Fix:

* Switched to direct log ingestion using Splunk “Add Data”
* Selected Windows Security logs directly

---

## 🧠 Key Learnings

* Windows Security Event logging (EventCode 4625)
* SIEM log ingestion and troubleshooting
* Splunk search and detection queries
* Brute force attack detection techniques
* Real-world troubleshooting of logging pipelines

---

## 🚀 Future Improvements

* Simulate phishing attacks
* Detect PowerShell-based threats
* Implement privilege escalation scenarios
* Build dashboards and alerts
## 📸 Screenshots

![Brute Force Detection](../screenshots/brute-force/event_code_4625.png)
---

## 💼 Skills Demonstrated

* SIEM (Splunk)
* Log analysis
* Threat detection
* Troubleshooting
* SOC fundamentals

* ## 🔑 Key Event Explained

**EventCode 4625 – Failed Logon**
- Generated when a login attempt fails
- Common indicator of brute force attacks
- Contains username, source IP, and logon type
