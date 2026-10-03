# Splunk SOC Log Analysis & Detection Lab

A hands-on Splunk SIEM project documenting a practical SOC Analyst workflow using Windows security logs, SPL, lookup enrichment, reports, dashboards, and alerts.

## Project Overview

**Workflow:** Windows Security Logs → SPL Investigation → Lookup Enrichment → Reports → Dashboard → Alerts

This lab currently contains **one Windows user and one observed failed-login event**. The single failed login is documented as an event to investigate, **not as proof of a brute-force attack**. Threshold detections are included as reusable detection logic for future activity.

## Objectives

- Analyze Windows Security Event IDs in Splunk
- Investigate EventCode 4625 failed logons
- Monitor EventCode 4688 process creation
- Use SPL for filtering, aggregation, classification, and reporting
- Build and use a CSV lookup
- Use `lookup` and `inputlookup`
- Enrich IP information with department, city, country, and threat level
- Build saved reports
- Build a SOC monitoring dashboard
- Create scheduled alerts
- Document evidence, detection logic, and limitations

## Environment

- Splunk
- Windows Security Event Logs
- One Windows user
- One observed failed-login event
- Custom lookup: `pakistan_ip_lookup`

## Repository Structure

```text
Splunk-SOC-Log-Analysis-Lab/
├── README.md
├── LICENSE
├── .gitignore
├── data/
│   └── pakistan_ip_lookup.csv
├── spl/
│   ├── 01_basic_investigation.spl
│   ├── 02_failed_login_detection.spl
│   ├── 03_process_creation_monitoring.spl
│   ├── 04_lookup_enrichment.spl
│   ├── 05_inputlookup_analysis.spl
│   ├── 06_alert_high_risk_ip.spl
│   └── 07_login_activity_analysis.spl
├── reports/
├── dashboard/
├── alerts/
├── docs/
└── screenshots/
```

## Key SPL

### Failed Login Investigation

```spl
index="main" EventCode=4625
| stats count by src_ip
| sort - count
```

### Threshold Detection

```spl
index="main" EventCode=4625
| stats count by src_ip
| where count >= 5
| sort - count
```

### Lookup Enrichment

```spl
index="main"
| lookup pakistan_ip_lookup src_ip OUTPUT department city country threat_level
| table _time user src_ip department city country threat_level EventCode
```

### Inputlookup High-Risk Detection

```spl
| inputlookup pakistan_ip_lookup
| search threat_level="High"
| stats count by ip_address city department country threat_level
| sort - count
```

## Dashboard: SOC Security Monitoring

Current panels:

1. Failed Login Detection
2. IP Address Threat & Location Enrichment
3. EventCode Frequency Analysis
4. Process Creation Monitoring
5. Successful vs Failed Logins

## Alerts

### High Risk IP Detection

Scheduled lookup-based alert using `inputlookup` and `threat_level="High"`.

### Multiple Failed Login Attempts

Reusable detection for 5 or more failed logons from one source IP.

## Investigation Note

A single failed login can have legitimate explanations. This lab therefore distinguishes **observed evidence** from **detection rules** and does not claim that a confirmed attack occurred.

## Skills Demonstrated

Splunk SIEM • SPL • Windows Event Log Analysis • EventCode Analysis • EventCode 4625 • EventCode 4688 • Lookup Enrichment • inputlookup • stats • where • eval • if • case • table • fields • sort • top • rare • timechart • Reporting • Dashboards • Alerts • SOC Investigation Methodology

## Author

**Tariq Ahmad**

Cybersecurity / SOC Analyst Learning Lab
