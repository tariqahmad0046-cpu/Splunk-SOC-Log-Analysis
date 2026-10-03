# Report: Failed Login Detection

**Description:** Shows failed Windows login attempts grouped by source IP.

```spl
index="main" EventCode=4625
| stats count by src_ip
| sort - count
```

**Current evidence:** One observed failed-login event.

**Interpretation:** A single failed login is not sufficient to conclude brute-force activity.
