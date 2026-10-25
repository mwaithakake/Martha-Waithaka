# Cybersecurity Portfolio

[← Back to home](./README.md)

I investigate suspicious activity on Windows systems and build and test the monitoring that detects it. Each project below is documented with its evidence, findings, and the limits of what the evidence can prove.

**Certifications:** CompTIA Security+ · ISC2 CC

---

## Projects at a glance

| Project | What it shows | Tools | Report |
|---|---|---|---|
| Windows Host Investigation | Reconstructing a multi-stage attack simulation from endpoint telemetry | Sysmon, PowerShell Script Block Logging | [Read report](https://github.com/mwaithakake/cybersecurity-learning-series/blob/main/projects/Windows_Investigation_Lab/final_report.md) |
| Wazuh Alert Investigation | Triaging SIEM alerts and judging what the evidence supports | Wazuh, Sysmon | [Read report](https://github.com/mwaithakake/cybersecurity-learning-series/blob/main/projects/wazuh_encoded_powershell.md) |
| Network Detection Lab | Building and validating a network detection pipeline | Snort, Wazuh, Wireshark, Nmap | [Read report](https://github.com/mwaithakake/cybersecurity-learning-series/blob/main/projects/YOUR-FILE-NAME.md) |

---

## Windows Host Investigation Lab

I investigated a controlled multi-stage attack simulation on a domain-joined Windows 11 workstation, reconstructing each stage from Sysmon and PowerShell telemetry and correlating them into one timeline.

**Key findings:** Identified three stages of activity: encoded PowerShell execution, file staging and concealment, and registry-based persistence. No single log source showed the full picture. Correlating process, file, registry, and PowerShell events did. Because this was a lab simulation, the findings show simulated attacker behavior, not an actual compromise.

**Timeline (EAT):**

| Time | Activity | Evidence |
|---|---|---|
| 10:33:50 | Encoded PowerShell execution | Sysmon Event 1, PowerShell Event 4104 |
| 10:51:45 | File staged, then hidden with `attrib.exe` | Sysmon Event 11, Sysmon Event 1 |
| 10:52:52 | Registry Run key persistence added | Sysmon Event 1, Sysmon Event 13 |

**Tools:** Windows 11 · Active Directory domain · Sysmon · PowerShell Script Block Logging · Windows Event Viewer · MITRE ATT&CK (T1547.001)

[Read the full report →](https://github.com/mwaithakake/cybersecurity-learning-series/blob/main/projects/Windows_Investigation_Lab/final_report.md)

<details markdown="1">
<summary>What I investigated</summary>

- Captured a baseline of local accounts and running processes before the simulation
- Identified `-EncodedCommand` PowerShell execution in Sysmon and recovered the underlying command from Event ID 4104
- Traced a staged file and the `attrib.exe` command used to hide it
- Found a Registry Run key added for persistence and noted that Sysmon labels it with the outdated T1060, while the current technique is T1547.001
- Documented defensive recommendations: script block logging, Run key monitoring, file concealment monitoring, and event correlation

</details>

---

## Wazuh SIEM Detection & Investigation

I triaged a Wazuh alert for Base64-encoded PowerShell execution on a monitored Windows endpoint, using Sysmon and PowerShell logs to work out what actually happened.

**Key findings:** The primary alert was an intentionally generated, benign lab command. A separate high-severity alert could not be classified as malicious from the available evidence. Alert severity alone is not enough to establish malicious activity.

**Timeline (EAT):**

| Time | Evidence | Interpretation |
|---|---|---|
| 07:45:06 | Sysmon Event 1, Wazuh rule 92057 | Encoded PowerShell execution recorded |
| 07:45:06-09 | PowerShell Event 4104 | Command decoded: writes a benign marker file |
| 07:45:08 | Sysmon Event 11, Wazuh rule 92213 | Temporary script-policy test file flagged |
| 07:45:09 | Filesystem check | Marker file present, timestamps consistent |

**Tools:** Wazuh · Sysmon · Windows 11 · PowerShell · Ubuntu · MITRE ATT&CK (T1059.001, PowerShell)

[Read the investigation report →](https://github.com/mwaithakake/cybersecurity-learning-series/blob/main/projects/wazuh_encoded_powershell.md)

<details markdown="1">
<summary>Full investigation steps</summary>

- Triaged a Wazuh alert for Base64-encoded PowerShell execution
- Examined Sysmon process-creation telemetry, including process IDs, parent-process information, and account context
- Analyzed PowerShell Script Block Logging (Event ID 4104) to establish the command's intended behavior
- Verified the resulting marker file and assessed the limits of the available file-creation evidence
- Investigated a related high-severity alert involving a temporary PowerShell script-policy test file
- Reconstructed an event timeline and documented findings, evidence gaps, and recommended response actions

</details>

---

## Network Detection Lab: Snort + Wazuh

I built an isolated attack-and-defend lab where Kali Linux generated Nmap SYN scan traffic, a custom Snort rule detected it, and the Wazuh agent forwarded the alerts to a central dashboard.

**Pipeline:** Kali (Nmap) → Snort on Ubuntu → Wazuh agent → Wazuh dashboard

**Key findings:** Validated the whole path from packet to dashboard. Wireshark confirmed the SYN probes, the custom rule (SID 1000001) fired on them, and Wazuh parsed the alerts (rule 20101) with source and destination IPs. I also documented the rule's limits: it flags any SYN packet from that source, can't tell the scan came from Nmap, and says nothing about whether a connection succeeded.

**Tools:** VirtualBox · Kali Linux · Ubuntu 24.04 · Nmap · Snort · Wireshark · Wazuh (Docker)

[Read the full report →](https://github.com/mwaithakake/cybersecurity-learning-series/blob/main/projects/snort-wazuh-siem-integration.md)

<details markdown="1">
<summary>What I built and tested</summary>

- Generated TCP SYN scan traffic with Nmap and inspected the packets in Wireshark
- Wrote a custom Snort rule and confirmed it produced alerts in Snort's fast-alert log
- Configured the Wazuh agent to collect Snort alerts and confirmed they were parsed and displayed in the dashboard
- Identified improvements: distinguishing single connections from port sweeps, custom Wazuh rules, and automated active response

</details>

---

## Also built

**Active Directory lab:** a Windows Server domain with users, security groups, OUs, Group Policy, and password policies. [View lab](https://github.com/mwaithakake/cybersecurity-learning-series/blob/main/projects/active_directory/active_directory_basics.md)

**Cybersecurity Learning Series:** guided labs, notes, and experiments documenting how I got here. [Explore the series](https://github.com/mwaithakake/cybersecurity-learning-series/tree/main)

---

## Currently working on

Network traffic investigation with Wireshark and packet captures (in progress).

---

_This portfolio documents my progression from guided hands-on labs toward independently investigating cybersecurity problems._
