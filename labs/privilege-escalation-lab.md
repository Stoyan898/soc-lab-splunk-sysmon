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
## 🧠 Detection Logic

This query identifies when a user is added to the Administrators group.

Adding a user to this group grants elevated privileges, which may indicate privilege escalation.

Monitoring these events helps detect unauthorized access and potential security breaches.

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
* ## 📸 Screenshots

![Privilege Escalation](../screenshots/privilege-escalation/event4732.png)

## 🛡️ SOC Analyst Response

If this activity was detected in a real environment, I would:

- Verify if the user addition to the Administrators group was authorized
- Identify who performed the action and from which system
- Check for related suspicious activity (logins, processes, commands)
- Review recent changes to user accounts and permissions
- Investigate whether this is part of a larger attack
- Escalate immediately if unauthorized privilege escalation is detected
## 🔑 Key Event Explained

**EventCode 4732 – User Added to Local Group**
- Triggered when a user is added to a group (e.g. Administrators)
- Indicates potential privilege escalation
- Important for detecting unauthorized admin access
