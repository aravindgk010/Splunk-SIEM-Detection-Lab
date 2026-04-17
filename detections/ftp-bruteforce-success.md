# FTP Brute Force Success After Failures

## Objective

Detect a likely brute force success pattern where repeated failed FTP login attempts are followed by a successful login.

## Data Source

- FTP logs
- Splunk source pattern: `*FTPSVC*`

## Splunk Search

```spl
source="*FTPSVC*" ftpuser ("530" OR "230")
| stats count(eval(searchmatch("530"))) as failed count(eval(searchmatch("230"))) as success by c_ip
| where failed>=3 AND success>=1
```
## Validation Method

- Use Hydra with a wordlist containing several wrong passwords followed by the correct password
- Confirm both `530` and `230` appear in Splunk
- Validate the search result
- Confirm the alert triggers

## Expected Indicator

- Same source IP generates multiple failures and at least one success

## Notes

This detection is stronger than failed login detection alone because it reflects a realistic success after guessing behavior.