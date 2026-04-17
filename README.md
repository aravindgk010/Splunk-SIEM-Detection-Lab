# Splunk SIEM Detection Lab

## Overview

This project is a small SOC style detection lab built in an isolated virtual environment using Splunk Enterprise. The purpose of the lab was to simulate attacker activity against a Windows based web server and detect that activity using centralized log collection, search queries, and alerts.

The lab was designed around four required detection scenarios:

- FTP brute force
- SYN scan
- TCP scan
- UDP scan

The environment included a Kali Linux attacker machine, a Windows Server 2016 web server hosting IIS and FTP services, and a Windows Server 2019 SIEM server running Splunk Enterprise.

## Objectives

- Build an isolated virtual lab for attack simulation and detection
- Configure IIS and FTP on the target server
- Forward IIS, FTP, and Windows Firewall logs into Splunk
- Simulate brute force and scan activity from Kali Linux
- Build Splunk searches and alerts for the observed attack patterns
- Document the setup, detections, and response workflow

## Lab Architecture

### Systems

- **Kali Linux**
  Role: Attacker
  IP: `192.168.1.16`

- **Windows Server 2016**
  Role: Web Server
  Services: IIS, FTP, Windows Firewall logging, Splunk Universal Forwarder
  IP: `192.168.1.18`

- **Windows Server 2019**
  Role: SIEM Server
  Software: Splunk Enterprise
  IP: `192.168.1.19`

## Tools Used

- Splunk Enterprise
- Splunk Universal Forwarder
- IIS
- FTP Service
- Windows Firewall Logging
- Kali Linux
- Nmap
- Hydra
- curl

## Data Sources

The following telemetry sources were ingested into Splunk:

- IIS web logs
- FTP service logs
- Windows Firewall log file

## Attack Scenarios

### 1. FTP Brute Force
The FTP service on the Windows Server 2016 host was used as the brute force target. Manual failed login attempts and Hydra based password attempts were used to generate repeated authentication failures and eventual success events.

### 2. SYN Scan
A SYN scan was executed from Kali using Nmap against selected ports on the target server. Scan related activity was observed through Windows Firewall logs.

### 3. TCP Scan
A TCP connect scan was launched using Nmap and correlated with firewall log entries in Splunk.

### 4. UDP Scan
A UDP scan against selected ports was executed from Kali and reviewed through Windows Firewall log activity.

## Key Detections

- FTP brute force failed logins
- FTP brute force success after repeated failures
- TCP scan visibility
- SYN scan visibility
- UDP scan visibility

## Validation Summary

The strongest and most reliable detections in this lab were the FTP related detections because the FTP logs clearly showed failed and successful authentication events.

The scan scenarios were validated through firewall log visibility and Splunk searches. Scan alerting was less stable than the FTP detection workflow due to lab limitations such as VM time drift and the weaker nature of Windows Firewall telemetry compared to dedicated IDS tooling.

## Main Lessons Learned

- Telemetry quality matters more than fancy detection logic
- Clear log validation must happen before alerting can be trusted
- FTP logs provided strong evidence for brute force detection
- Windows Firewall logs were sufficient for scan visibility, but not ideal for deep packet level distinction
- VM time drift can directly affect alert reliability

## Limitations

- No dedicated IDS such as Suricata or Snort was deployed
- Scan detections relied on Windows Firewall logs rather than packet level network telemetry
- Alert triggering became unstable after VM restarts due to clock drift and timing mismatch between systems

## Repository Structure

- `architecture/` contains environment design and IP layout
- `detections/` contains detection notes and Splunk queries
- `attack-simulation/` contains Kali attack commands and validation notes
- `runbooks/` contains the incident response runbook
- `report/` contains the final report draft
- `screenshots/` contains evidence used for validation and documentation

## Future Improvements

- Add dedicated IDS telemetry for stronger scan detection
- Add SQL injection and XSS detection using IIS logs
- Improve alert stability through better time synchronization
- Add Sysmon or richer Windows telemetry for broader detection coverage