# Validation Notes

## IIS Validation
- Confirmed the default IIS page was reachable from Kali
- Confirmed HTTP requests appeared in Splunk under IIS logs

## FTP Validation
- Confirmed FTP site was created and reachable from Kali
- Confirmed valid login worked
- Confirmed failed logins generated `530`
- Confirmed successful logins generated `230`

## Firewall Validation
- Enabled Windows Firewall logging
- Confirmed the firewall log file was forwarded to Splunk
- Confirmed traffic from `192.168.1.16` appeared in Splunk searches

## Alert Validation
- FTP brute force failed login alert triggered successfully
- FTP success after failures search was validated
- Scan log visibility was confirmed through firewall log searches
- Scan alert reliability was affected by VM time drift after restart

## Lab Limitation
The biggest operational issue in the environment was VM clock drift after restart. This affected alert timing and made scan alerts less reliable than the raw search validation.