# TCP Scan Visibility

## Objective

Identify TCP scan related activity from the attacker machine in the Windows Firewall logs.

## Data Source

- Windows Firewall log
- Splunk source: `C:\fwlogs\pfirewall.log`

## Splunk Search

```spl
source="C:\fwlogs\pfirewall.log" "192.168.1.16" "TCP"
```

## Demo Safe Search

```
source="C:\fwlogs\pfirewall.log" "192.168.1.16" "TCP" (" 21 " OR " 80 " OR " 135 " OR " 139 " OR " 445 " OR " 5985 ")
```

## Validation Method

- Run a TCP connect scan from Kali using Nmap
- Confirm matching firewall log entries appear in Splunk
- Review ports and timestamps
- Use a simple alert on the raw query during demo testing

## Expected Indicator

- TCP traffic from `192.168.1.16` to multiple service ports on the target host

## Notes

The firewall logs provided enough visibility to confirm TCP scan related behavior, but they were weaker than dedicated IDS data.