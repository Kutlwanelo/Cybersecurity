## Protocol Quick Reference

|**Protocol**|**Port**|**Secure Version**|**Port**|**Layer (OSI)**|
|---|---|---|---|---|
|**HTTP**|80|**HTTPS**|443|7 (Application)|
|**Telnet**|23|**SSH**|22|7 (Application)|
|**SMTP**|25|**SMTPS**|465/587|7 (Application)|
|**POP3**|110|**POP3S**|995|7 (Application)|
|**IMAP**|143|**IMAPS**|993|

## Splunk Investigation Workflow

_Use these queries when triaging web traffic logs (`sourcetype=web_traffic`)._

### 1. Identifying the "Noise" (Reconnaissance)

Attackers often use scripts. To find them, filter out "Known Good" browsers:
index=main sourcetype=web_traffic 
NOT (user_agent="*Mozilla*" OR user_agent="*Chrome*" OR user_agent="*Safari*")| stats count by client_ip, user_agent | sort -count



