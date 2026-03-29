# 🚨 Privilege Escalation Lab (Windows + Splunk)

## 📌 Overview

As part of building my SOC home lab after completing my CompTIA Security+ certification, I simulated and detected privilege escalation activity using Windows Security logs and Splunk.

---

## 🧪 Scenario

Simulated a user gaining administrative privileges on a Windows system.

---

## 🏗️ Steps Performed

### 1. Created a new user

```bash
net user socuser Password123! /add
```

---

### 2. Added user to Administrators group

```bash
net localgroup administrators socuser /add
```

---

### 3. Generated security events

This action triggered Windows Security logs for privilege escalation.

screenshot event viewer4732

---

## 🔍 Detection in Splunk

### Basic Query

```spl
index=main EventCode=4732
```

screenshot event4732


---

### Focused Detection

```spl
index=main EventCode=4732
| search Group_Name="Administrators"
```

screenshot event search 4732

---

### Advanced Query

```spl
index=main EventCode=4732
| stats count by Member_Name, Group_Name, ComputerName
```
alert created 

screenshot alert created

---

## 🎯 Key Events

| EventCode | Description                               |
| --------- | ----------------------------------------- |
| 4732      | User added to local group                 |
| 4672      | Special privileges assigned (admin login) |

---

## 🧪 Results

* Successfully detected user added to Administrators group
* Identified privilege escalation activity
* Observed admin-level access behavior in logs

---

## ⚠️ Challenges Faced

### Logs not appearing initially

* Issue with log ingestion configuration

### Fix

* Used Splunk “Add Data” to ingest Windows Security logs directly

---

## 🧠 Key Learnings

* Privilege escalation detection using Windows logs
* Monitoring group membership changes
* Writing detection queries in Splunk
* Understanding admin-level activity

---

## 🚀 Future Improvements

* Detect privilege escalation via PowerShell
* Correlate with suspicious processes
* Build alerting rules

---

## 💼 Skills Demonstrated

* SIEM (Splunk)
* Threat detection
* Windows security monitoring
* Log analysis
