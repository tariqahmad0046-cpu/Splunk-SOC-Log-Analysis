# Detection: Multiple Failed Login Attempts

**SPL**
```spl
index="main" EventCode=4625
| stats count by src_ip
| where count >= 5
| sort - count
```

**Suggested configuration:** Scheduled every 5 minutes; trigger when number of results > 0.

**Current lab status:** One observed failed-login event, so this is detection logic rather than a confirmed brute-force incident.
