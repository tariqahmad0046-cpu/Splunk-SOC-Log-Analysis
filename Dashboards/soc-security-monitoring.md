# Dashboard: SOC Security Monitoring

## Panels

### 1. Failed Login Detection
```spl
index="main" EventCode=4625
| stats count by src_ip
| sort - count
```

### 2. IP Address Threat & Location Enrichment
```spl
index="main"
| lookup pakistan_ip_lookup src_ip OUTPUT department city country threat_level
| table src_ip department city country threat_level
```

### 3. EventCode Frequency Analysis
```spl
index="main"
| stats count by EventCode
| sort - count
```

### 4. Process Creation Monitoring
```spl
index="main" EventCode=4688
| stats count by host
| sort - count
```

### 5. Successful vs Failed Logins
```spl
index="main" (EventCode=4624 OR EventCode=4625)
| eval login_status=if(EventCode=4624,"Successful Login","Failed Login")
| stats count by login_status
```
