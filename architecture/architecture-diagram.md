# Architecture Diagram

## High Level Flow

```text
Kali Linux (192.168.1.16)
        |
        |  Attack traffic
        v
WEB-SERVER - Windows Server 2016 (192.168.1.18)
Services:
- IIS
- FTP
- Windows Firewall Logging
- Splunk Universal Forwarder
        |
        |  Forwarded logs
        v
SIEM-SERVER - Windows Server 2019 (192.168.1.19)
````

Software:
- Splunk Enterprise
- Search
- Alerts
- Triggered Alerts

## Log Flow

- IIS requests are written to IIS log files and forwarded to Splunk
- FTP authentication activity is written to FTP log files and forwarded to Splunk
- Network activity is written to the Windows Firewall log and forwarded to Splunk
- Splunk indexes the data and applies search based detections

## Notes

This architecture separates the attacker, target, and SIEM roles cleanly. The attacker generates traffic, the target records activity, and the SIEM receives and analyzes the logs.