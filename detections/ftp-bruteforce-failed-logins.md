# FTP Brute Force Failed Logins

## Objective

Detect repeated failed FTP login attempts against the target FTP service.

## Data Source

- FTP logs
- Splunk source pattern: `*FTPSVC*`

## Splunk Search

```spl
source="*FTPSVC*" "530"
```

Stronger Detection Version

```text
source="*FTPSVC*" "530"
| stats count earliest(_time) as first_attempt latest(_time) as last_attempt by c_ip host
| where count >= 5
```

## Validation Method

- Create repeated failed FTP login attempts manually or using Hydra
- Confirm `530` appears in Splunk
- Validate that the search returns events
- Confirm the alert triggers when configured

## Expected Indicator

- Multiple `530` status events from the same source IP

## Notes

This was the most reliable detection in the lab because FTP authentication logs were very clear and easy to validate.