# Project Overview — Splunk SIEM Attack Detection Lab

## Purpose

The purpose of this project was to examine how a security information and event management (SIEM) platform can support an analyst investigating a multi-stage compromise in a controlled environment. The team built an intentionally vulnerable Linux web-server lab, collected security-relevant logs, simulated attacker behaviour and compared the recorded evidence with a baseline captured before the exercise.

Rather than measuring performance against real production networks, the project focused on understanding **what different log sources reveal**, how to connect those observations, and where monitoring controls help identify attempted unauthorised access.

## Objectives

1. **Establish a repeatable lab environment:** Configure two Ubuntu virtual machines in VirtualBox, with one acting as the monitored application server and the other as the SIEM and controlled test workstation.
2. **Prepare realistic monitoring targets:** Run a PHP/MySQL application on Apache and create dummy user files with different access restrictions.
3. **Collect a baseline:** Verify operating-system, web-server and audit events before running the simulated intrusion.
4. **Demonstrate a controlled attack progression:** Examine SQL injection, web-shell activity, host reconnaissance, file access restrictions and privilege escalation caused by a purposely misconfigured SUID binary.
5. **Centralise observations:** Use Splunk Universal Forwarder to send application, authentication and audit logs to Splunk Enterprise.
6. **Develop useful visibility:** Search indexed events and configure alerts corresponding to relevant stages of the scenario.
7. **Evaluate results and limitations:** Determine which activities produced evidence in the SIEM, and identify where controls or external file reputation checking did not yield a positive detection.

## What was implemented

- Two Ubuntu 64-bit VMs on a VirtualBox NAT network.
- An intentionally vulnerable PHP/MySQL web application hosted with Apache.
- Dummy users, directories and controlled file-permission settings.
- `auditd` watches covering selected user-home and web upload directories.
- Splunk Universal Forwarder receiving monitored system and application logs and sending them to Splunk Enterprise.
- A Python-driven VirusTotal file-hash lookup integration described in the report, with results sent to a Splunk-monitored log.
- Named Splunk alerts for SQL injection attempts, web-shell activity, reconnaissance and audited file operations.
- Baseline and post-attack log analysis of the simulated activity.

## Main outcomes

The lab showed that combining server-access and filesystem telemetry gives a clearer investigative trail than examining application events on their own. Splunk provided an indexed interface for following key stages of the simulated attack, while `auditd` was particularly valuable for observing changes in restricted locations.

The VirusTotal integration provided additional context but **did not classify the demonstration web-shell file as malicious** in the documented test. An initial Wazuh implementation was also evaluated and set aside because the team encountered excess log noise and issues with rule matching.

## Scope

This repository documents completed lab work using report evidence, presentation material and VirtualBox setup screenshots. It is not a redeployable infrastructure project: saved SPL queries, VM images, vulnerable application source and original scripts are unavailable in the retained artefacts. No real customer system or production network was assessed.

**Contributors:** Stephen Mc Neill Killeen and Luke O'Sullivan.  
**Institution:** University of Limerick.  
**Year:** 2026.
