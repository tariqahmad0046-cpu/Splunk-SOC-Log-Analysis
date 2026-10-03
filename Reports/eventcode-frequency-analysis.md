# Report: EventCode Frequency Analysis

**Description:** Shows the frequency of Windows EventCodes observed in the Splunk index.

```spl
index="main"
| stats count by EventCode
| sort - count
```

**Visualization:** Bar Chart
