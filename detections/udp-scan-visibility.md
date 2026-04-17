
# UDP Scan Visibility

## Objective

Identify UDP scan related activity using Windows Firewall logs.

## Data Source

- Windows Firewall log
- Splunk source: `C:\fwlogs\pfirewall.log`

## Splunk Search

```spl
source="C:\fwlogs\pfirewall.log" "192.168.1.16" "UDP"
```
## Validation Method

- Run a UDP scan from Kali using Nmap
- Confirm UDP entries appear in Splunk
- Correlate timestamps and attacker IP

## Expected Indicator

- UDP traffic from `192.168.1.16` targeting the web server

## Notes

UDP scan visibility was dependent on the selected ports and Windows Firewall logging behavior. It was weaker than FTP based detections but still useful for scan evidence.