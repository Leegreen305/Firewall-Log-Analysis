# Firewall-Log-Analysis
Splunk SIEM project analyzing pfSense firewall logs to detect blocked traffic, source IPs, and protocol usage.

This project demonstrates how to use Splunk Cloud to ingest and analyze pfSense-style firewall logs. The goal is to detect suspicious behavior, blocked traffic, and protocol activity using SPL queries and visual dashboards.

---

##  Tools Used
- Splunk Cloud 
- Sample pfSense-style logs (`firewall_log.txt`)
- Search Processing Language (SPL)

---

##  Objectives
- Ingest raw firewall logs into Splunk
- Extract key fields (IP, ports, protocol, action)
- Visualize blocked vs passed traffic
- Identify top source IPs and destination ports

---

##  Key SPL Query

```spl
index=main sourcetype=syslog 
| rex "filterlog:.*,(?<action>pass|block),in,.*,(?<proto>tcp|udp),\d+,(?<src_ip>\d+\.\d+\.\d+\.\d+),(?<dest_ip>\d+\.\d+\.\d+\.\d+),(?<src_port>\d+),(?<dest_port>\d+)"
| stats count by action, proto, src_ip, dest_ip, dest_port
| sort -count
```

---

##  Screenshot

![SIEM Dashboard](dashboard.png)









