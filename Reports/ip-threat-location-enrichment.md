# Report: IP Address Threat & Location Enrichment

**Description:** Enriches IP addresses with department, city, country, and threat information.

```spl
index="main"
| lookup pakistan_ip_lookup src_ip OUTPUT department city country threat_level
| table _time user src_ip department city country threat_level EventCode
```
