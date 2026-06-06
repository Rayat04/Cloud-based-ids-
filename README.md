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