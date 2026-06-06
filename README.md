\# Cloud-Based Log and Intrusion Detection System



!\[Wazuh](https://img.shields.io/badge/Wazuh-4.7.5-blue)

!\[AWS](https://img.shields.io/badge/AWS-EC2-orange)

!\[Ubuntu](https://img.shields.io/badge/Ubuntu-24.04\_LTS-purple)

!\[Windows](https://img.shields.io/badge/Windows-11-cyan)



\*\*B.Tech CSE Project-I (BTCS603-18)\*\*

\*\*I.K. Gujral Punjab Technical University, Kapurthala\*\*

\*\*Student:\*\* Anush Rayat | Roll No: 2323450 | Section A



\---



\## Overview

A cloud-based centralized log analysis and intrusion detection system

built using \*\*Wazuh 4.7.5\*\* deployed on \*\*AWS EC2\*\*, monitoring both

Windows 11 and Linux endpoints in real time without expensive

commercial licensing.



\---



\## System Architecture

Windows 11 Agent ──────┐

(Physical Laptop)      │ TCP 1514

Intel i7 · 16GB RAM    │

▼

Wazuh Server (AWS EC2)

m7i-flex.large · Ubuntu 24.04 LTS

Elastic IP: 35.154.81.157

Manager · Indexer · Dashboard

▲

Linux EC2 Agent ───────┘

(t3.small · Ubuntu 24.04)

172.31.46.155



\---



\## Tech Stack

| Component | Technology |

|---|---|

| Security Platform | Wazuh 4.7.5 (XDR + SIEM) |

| Cloud Infrastructure | AWS EC2 (ap-south-1) |

| Server OS | Ubuntu 24.04 LTS |

| Log Storage | OpenSearch (Wazuh Indexer) |

| Dashboard | Wazuh Dashboard (HTTPS) |

| Threat Framework | MITRE ATT\&CK |

| Windows Endpoint | Windows 11 Home (25H2) |

| Linux Endpoint | Ubuntu 24.04 LTS (EC2) |



\---



\## Features

\- ✅ Real-time log collection from Windows and Linux agents

\- ✅ SSH Brute-Force attack detection with custom rules

\- ✅ File Integrity Monitoring (FIM) on /etc/ directory

\- ✅ Custom detection rules in local\_rules.xml

\- ✅ Automatic MITRE ATT\&CK framework mapping

\- ✅ Centralized Wazuh Dashboard via HTTPS

\- ✅ AWS Security Groups as virtual firewalls



\---



\## Test Results



| Metric | Value |

|---|---|

| Total Alerts Generated | 258 |

| Authentication Failures Detected | 24 |

| FIM Alerts (file create/delete) | Detected successfully |

| Active Agents | 2 (Windows + Linux) |

| Avg Alert Response Time | < 5 seconds |

| Dashboard Load Time | < 3 seconds |

| Level 12+ Critical Alerts | 0 |



\---



\## MITRE ATT\&CK Mapping



| Technique ID | Technique | Detected On |

|---|---|---|

| T1078 | Valid Accounts | Windows Agent |

| T1112 | Modify Registry | Windows Agent |

| T1021 | Remote Services | Linux Agent |

| T1098 | Account Manipulation | Both Agents |

| T1110 | Brute Force | Linux Agent |

| T1565 | Data Manipulation | Linux Agent |



\---



\## Network \& Port Configuration



| Port | Protocol | Purpose |

|---|---|---|

| 22 | TCP | SSH Admin Access |

| 443 | TCP | Wazuh Dashboard (HTTPS) |

| 1514 | TCP | Agent Log Forwarding |

| 1515 | TCP | Agent Registration |

| 55000 | TCP | Wazuh REST API |



\---



\## Infrastructure Specs



\*\*Wazuh Server\*\*

\- Instance: m7i-flex.large

\- OS: Ubuntu 24.04 LTS

\- Storage: 30 GiB EBS

\- Elastic IP: 35.154.81.157



\*\*Linux EC2 Agent\*\*

\- Instance: t3.small

\- OS: Ubuntu 24.04 LTS

\- Storage: 8 GiB EBS



\*\*Windows 11 Agent\*\*

\- Machine: Physical Laptop

\- CPU: Intel Core i7-1255U (12th Gen)

\- RAM: 16 GB



\---



\## Project Report

The complete project report is available in

`CBIDS Final File.pdf` in this repository.



\---



\## Challenges Solved

\- AWS EC2 Public IP binding error → Used Private IP

\- Wazuh OS compatibility check → Used -i bypass flag

\- Agent version mismatch → Specified version explicitly

\- Dynamic IP changes → Assigned static Elastic IP

\- FIM delayed alerts → Waited for baseline scan



\---



\## Future Scope

\- Active response for automatic IP blocking

\- Email/SMS real-time alerting

\- External threat intelligence integration (VirusTotal, OTX)

\- Machine learning based anomaly detection

\- Scale to 100+ agents



\---



\## References

\- \[Wazuh Documentation](https://documentation.wazuh.com)

\- \[AWS EC2 User Guide](https://docs.aws.amazon.com/ec2/)

\- \[MITRE ATT\&CK Framework](https://attack.mitre.org/)

\- \[OpenSearch Documentation](https://opensearch.org/docs/)

