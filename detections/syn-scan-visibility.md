# SYN Scan Visibility

## Objective

Identify SYN scan related activity using available Windows Firewall log telemetry.

## Data Source

- Windows Firewall log
- Splunk source: `C:\fwlogs\pfirewall.log`

## Splunk Search

```spl
source="C:\fwlogs\pfirewall.log" "192.168.1.16" "TCP"
```

## Validation Method

- Run a SYN scan from Kali using Nmap
- Confirm TCP based firewall events appear in Splunk
- Correlate source IP, target IP, and ports

## Expected Indicator

- TCP scan related firewall activity from the attacker host

## Notes

The lab did not include deep packet inspection. As a result, SYN scan and TCP connect scan were not perfectly separated at the packet level. Detection was based on firewall log visibility and validation timing.