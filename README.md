# Cloud-Based Log and Intrusion Detection System

![Wazuh](https://img.shields.io/badge/Wazuh-4.7.5-blue)
![AWS](https://img.shields.io/badge/AWS-EC2-orange)
![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04_LTS-purple)
![Windows](https://img.shields.io/badge/Windows-11-blue)

## About This Project

This is my 6th semester B.Tech project where I built a cloud-based
intrusion detection system that monitors security logs from multiple
machines in real time. Instead of using expensive commercial security
tools, I used Wazuh which is open source and deployed it on AWS EC2.

The idea was simple — modern systems generate thousands of log entries
every hour and manually checking them is impossible. So I set up an
automated system that watches for threats and raises alerts the moment
something suspicious happens.

## What I Built

I set up a central Wazuh security server on an AWS EC2 instance and
connected two machines to it as agents — my own Windows 11 laptop and
a Linux EC2 instance. The server collects logs from both machines,
analyzes them using detection rules, and shows everything on a live
dashboard.

I also wrote custom detection rules to catch SSH brute-force attacks
and configured File Integrity Monitoring to detect any unauthorized
changes to files in the /etc/ directory on the Linux machine.

## How It Works

The Wazuh agents installed on both machines continuously collect logs
and forward them to the central server over TCP port 1514. The Wazuh
Manager then checks these logs against thousands of built-in rules plus
my own custom rules. When a rule matches, an alert is generated and
appears on the dashboard instantly.

All detected threats are automatically mapped to the MITRE ATT&CK
framework which is an internationally recognized standard for
classifying cyber threats.

## Tech Stack

| Component | Details |
|---|---|
| Security Platform | Wazuh 4.7.5 |
| Cloud Provider | AWS EC2 (Mumbai Region) |
| Server OS | Ubuntu 24.04 LTS |
| Log Storage | OpenSearch |
| Windows Agent | Windows 11 Home |
| Linux Agent | Ubuntu 24.04 LTS |
| Threat Framework | MITRE ATT&CK |

## Testing and Results

To test the system I simulated real attacks:

For brute-force detection, I ran repeated SSH login attempts using a
fake username against the Linux machine. The system detected all 24
failed attempts and raised alerts in under 5 seconds each time.

For file integrity monitoring, I created and deleted a file inside
/etc/ on the Linux machine. Wazuh detected both the creation and
deletion immediately and raised syscheck alerts on the dashboard.

| Metric | Result |
|---|---|
| Total Alerts Generated | 258 |
| Authentication Failures Detected | 24 |
| Average Alert Response Time | Under 5 seconds |
| Active Agents Monitored | 2 |
| Critical Alerts (Level 12+) | 0 |

## Challenges I Faced

The biggest challenge was that the Wazuh installer rejected Ubuntu
24.04 as unsupported so I had to use a bypass flag to get past the
compatibility check. I also ran into an issue where the Wazuh Indexer
refused to bind to the public IP of the EC2 instance because AWS uses
NAT internally, so I had to use the private IP instead.

Another issue was that apt installed a newer version of the Wazuh agent
than the server was running, which caused registration to fail. I fixed
this by specifying the exact version during installation.

## Infrastructure

**Wazuh Server**
- AWS EC2 m7i-flex.large
- Ubuntu 24.04 LTS
- 30 GiB storage
- Static Elastic IP assigned

**Linux Agent**
- AWS EC2 t3.small
- Ubuntu 24.04 LTS
- 8 GiB storage

**Windows Agent**
- My personal laptop
- Intel Core i7-1255U, 16GB RAM
- Windows 11 Home

## MITRE ATT&CK Mapping

| Technique ID | Technique | Detected On |
|---|---|---|
| T1078 | Valid Accounts | Windows Agent |
| T1112 | Modify Registry | Windows Agent |
| T1021 | Remote Services | Linux Agent |
| T1098 | Account Manipulation | Both Agents |
| T1110 | Brute Force | Linux Agent |
| T1565 | Data Manipulation | Linux Agent |

## Network Configuration

| Port | Purpose |
|---|---|
| 22 | SSH Admin Access |
| 443 | Wazuh Dashboard (HTTPS) |
| 1514 | Agent Log Forwarding |
| 1515 | Agent Registration |
| 55000 | Wazuh REST API |

## Future Improvements

There are a few things I want to add to this project in the future.
Right now the system only detects threats but does not block them
automatically. I want to configure Wazuh active response so it
automatically blocks attacking IP addresses during a brute-force attack.

I also want to add email and SMS alerts so I get notified instantly
when a high severity event is detected without having to check the
dashboard manually. Integrating external threat intelligence feeds like
VirusTotal would also help identify known malicious IP addresses
automatically.

## Project Report

The full project report with all implementation details, screenshots
and security analysis is available in the PDF file in this repository.

---

**Anush Rayat | Roll No: 2323450 | B.Tech CSE | IKGPTU Kapurthala**