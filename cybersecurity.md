# 🛡️ Cybersecurity Portfolio

I am building practical cybersecurity skills through hands-on investigation, Windows security, network analysis, and enterprise infrastructure labs.

My projects focus on understanding **what happened, what evidence supports the conclusion, and how a defender could respond.**

---

## 🎯 Current Focus

- Windows security investigation
- Endpoint and log analysis
- Active Directory & identity management
- Network analysis
- Security monitoring and detection
- Enterprise infrastructure fundamentals

---

# 🔎 Featured Projects

## 🖥️ Windows Host Investigation Lab

A controlled Windows investigation lab focused on reconstructing suspicious activity from endpoint telemetry.

### What I investigated

- Process creation using Sysmon
- PowerShell activity and Script Block Logging
- Encoded PowerShell execution
- File creation and concealment
- Registry-based persistence
- Correlation of multiple events into an investigation timeline

### Key technologies

**Windows 11 · Windows Server · Sysmon · PowerShell · Windows Event Logs · MITRE ATT&CK**

🔗 [View Project](https://github.com/mwaithakake/cybersecurity-learning-series/blob/main/projects/Windows_Investigation_Lab/final_report.md)

---
## 🔎 Wazuh SIEM Detection & Investigation

A hands-on blue-team project investigating encoded PowerShell execution on a monitored Windows endpoint using Wazuh and Sysmon.

### What I investigated

- Triaged a Wazuh alert for Base64-encoded PowerShell execution
- Examined Sysmon process-creation telemetry, including process IDs, parent-process information, and account context
- Analyzed local PowerShell Script Block Logging (Event ID 4104) to establish the command's intended behavior
- Verified the resulting marker file and assessed the limits of the available file-creation evidence
- Investigated a related high-severity alert involving a temporary PowerShell script-policy test file
- Reconstructed an event timeline and documented findings, evidence gaps, and recommended response actions

### Key findings

The investigation established that the primary alert corresponded to an intentionally generated, benign lab command. A separate high-severity alert required contextual assessment but could not be classified as malicious from the available evidence.

The project demonstrates how SIEM alerts can be investigated using endpoint telemetry, and why alert severity alone is insufficient to establish malicious activity.

### Key technologies

**Wazuh · Sysmon · Windows 11 · PowerShell · Windows Event Logs · Ubuntu · MITRE ATT&CK**

**MITRE ATT&CK:** T1059.001 — PowerShell

🔗 [View Investigation Report](https://github.com/mwaithakake/cybersecurity-learning-series/blob/main/projects/wazuh_encoded_powershell.md)

--- 

## 🏢 Active Directory Infrastructure & Security Lab

A hands-on Windows Server and Active Directory lab focused on understanding enterprise identity and access management.

### What I worked with

- Domain controller configuration
- Users and security groups
- Organizational Units
- Group Policy
- Password and account policies
- Delegated permissions
- Windows domain administration

### Key technologies

**Windows Server · Active Directory · Group Policy · PowerShell**

🔗 [View Project](https://github.com/mwaithakake/cybersecurity-learning-series/blob/main/projects/active_directory/active_directory_basics.md)

---

# 📚 Cybersecurity Learning Series

My learning series contains guided labs, technical notes, experiments, and other hands-on work documenting my development as I build practical cybersecurity skills.

👉 [Explore the Cybersecurity Learning Series](https://github.com/mwaithakake/cybersecurity-learning-series/tree/main)

---

# 🎓 Certifications

<div>
 <a href="https://www.credly.com/badges/d8de080d-e7aa-4a20-a6f7-a8ef3ff9f656/public_url">
  <img src="https://img.shields.io/badge/-CompTIA_Security%2B-007ACC?&style=for-the-badge&logo=CompTIA&logoColor=white" />
 </a>

 <a href="https://www.credly.com/badges/c52bbe3d-a629-480e-977b-44c1bc923887/public_url">
  <img src="https://img.shields.io/badge/-ISC2_CC-007ACC?&style=for-the-badge&logo=ISC2&logoColor=white" />
 </a>
</div>

---

# 🔧 Technologies & Tools

### Windows & Infrastructure

- Windows Server
- Windows 11
- Active Directory
- Group Policy
- PowerShell
- Windows Event Logs

### Security & Investigation

- Sysmon
- SIEM fundamentals
- Log analysis
- Endpoint investigation
- MITRE ATT&CK

### Networking

- Wireshark
- TCP/IP
- DNS
- ARP

### Operating Systems

- Windows
- Linux

---

_This portfolio documents my progression from guided hands-on labs toward independently investigating and understanding cybersecurity problems._
