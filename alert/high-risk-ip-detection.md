# Alert: High Risk IP Detection

**Status:** Enabled in the lab

**Type:** Scheduled

**Current schedule:** Hourly, at 0 minutes past the hour

**Trigger:** Number of Results > 0

**SPL**
```spl
| inputlookup pakistan_ip_lookup
| search threat_level="High"
| stats count by ip_address city department country threat_level
| sort - count
```

**Purpose:** Demonstrate scheduled lookup-based detection.

**Important:** This detects entries in the lookup table; it does not prove that those IPs generated malicious activity in the Windows event dataset.
