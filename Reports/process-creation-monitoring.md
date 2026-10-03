# Report: Process Creation Monitoring

**Description:** Monitors Windows process creation activity using EventCode 4688.

```spl
index="main" EventCode=4688
| stats count by host
| sort - count
```

**Visualization:** Bar Chart
