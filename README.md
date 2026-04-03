## 📌 Overview
After completing my CompTIA Security+ certification, I built this SOC home lab to gain hands-on experience in security monitoring, detection, and analysis.

This project simulates a Security Operations Center (SOC) environment where brute force and privilege escalation attacks are detected and analyzed using Splunk SIEM.

The goal is to demonstrate hands-on experience in log analysis, threat detection, and incident investigation.

⸻

🎯 Objectives
	•	Detect brute force login attempts
	•	Identify privilege escalation activity
	•	Analyze logs using Splunk
	•	Simulate real-world SOC investigation workflow

⸻

🛠️ Lab Setup
	•	SIEM: Splunk
	•	Environment: VirtualBox
	•	Systems:
	•	Windows (target machine)
	•	Linux (attacker machine)
	•	Log Sources:
	•	Windows Event Logs
	•	Authentication logs

⸻

🚨 Use Case 1: Brute Force Attack

🔍 Description

Multiple failed login attempts followed by a successful login indicate a potential brute force attack.

📊 Detection Logic
	•	High number of failed logins (Event ID 4625)
	•	Followed by successful login (Event ID 4624)

🔎 Splunk Query (SPL)

index=wineventlog EventCode=4625 OR EventCode=4624
| stats count by Account_Name, EventCode

🧠 Analysis
	•	Identified abnormal spike in failed logins
	•	Successful authentication after failures suggests compromised credentials

🧬 MITRE ATT&CK
	•	T1110 – Brute Force

⸻

🚨 Use Case 2: Privilege Escalation

🔍 Description

Detection of a user gaining elevated privileges.

📊 Detection Logic
	•	Event ID 4672 (Special privileges assigned)

🔎 Splunk Query (SPL)

index=wineventlog EventCode=4672

🧠 Analysis
	•	Privileged access assigned unexpectedly
	•	Indicates possible escalation or misuse of admin rights

🧬 MITRE ATT&CK
	•	T1068 – Exploitation for Privilege Escalation

⸻

🧾 Incident Summary

📅 Timeline
	•	Multiple failed logins detected
	•	Successful login observed
	•	Privileged access granted shortly after

⚠️ Impact
	•	Potential account compromise
	•	Unauthorized access to system resources

🛡️ Response Actions
	•	Investigate affected account
	•	Reset credentials
	•	Review access logs
	•	Implement account lockout policies

🚀 Skills Demonstrated
	•	SIEM (Splunk)
	•	Log analysis
	•	Threat detection
	•	Incident investigation
	•	MITRE ATT&CK mapping

	
## 🎣 Phishing Detection (Apache Logs)

This module simulates phishing login attempts against a web server and demonstrates detection using Splunk.

- Detection of POST /login.php requests
- Identification of attacking IP
- Dashboard visualization

📁 Folder: /phishing
	

⸻

📌 Conclusion

This lab demonstrates the ability to detect and analyze common attack techniques in a SOC environment using real logs and SIEM tools.
:::
