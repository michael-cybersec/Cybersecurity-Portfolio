# SIEM Log Searches - Splunk SPL Queries

## 📋 Overview
Collection of useful Splunk SPL (Search Processing Language) queries for security monitoring and threat hunting.

---

## 🔍 Basic Log Search Examples

### 1. Authentication Failures
```spl
index=main sourcetype=linux_secure password_change FAILED
| stats count by user, src_ip
| where count > 5
```

### 2. Failed SSH Login Attempts
```spl
index=main sourcetype=linux_secure Failed password
| stats count by src_ip, user
| sort - count
| head 20
```

### 3. Privilege Escalation (sudo)
```spl
index=main sourcetype=linux_secure sudo
| search "user=*" "command=*"
| table _time, user, command, src_ip
```

### 4. Port Scanning Detection
```spl
index=main action=blocked
| stats dc(dest_port) as unique_ports by src_ip
| where unique_ports > 100
```

### 5. Data Exfiltration Detection
```spl
index=main sourcetype=firewall dest_port OUT action=allowed
| search dest_ip!=internal_network
| stats sum(bytes_out) as total_bytes by src_ip, dest_ip
| where total_bytes > 1000000
```

---

## 🎯 Threat Hunting Queries

### 1. Suspicious Process Execution
```spl
index=main sourcetype=WinEventLog:Security EventCode=4688
| search NOT (Image="*\\System32\\*" OR Image="*\\Program Files\\*")
| stats count by Image, user
```

### 2. Lateral Movement Detection
```spl
index=main sourcetype=WinEventLog:Security EventCode=4624
| search LogonType=3
| stats dc(dest_name) as unique_hosts by src_ip, user
| where unique_hosts > 5
```

### 3. Registry Modification (Persistence)
```spl
index=main sourcetype=WinEventLog:Security EventCode=4657
| search ObjectName="*\\Run\\" OR ObjectName="*\\Services\\"
| table _time, Computer, ObjectName, ObjectValueName
```

### 4. Scheduled Task Creation
```spl
index=main sourcetype=WinEventLog:Security EventCode=4698
| search NOT User="NT AUTHORITY\\SYSTEM"
| stats count by User, TaskName, Computer
```

---

## 🛡️ Security Monitoring

### 1. Web Application Attacks
```spl
index=web sourcetype=access_log
| search (url contains "eval" OR url contains "exec" OR url contains "system")
| stats count by src_ip, user_agent, url
| where count > 3
```

### 2. Malware Indicators
```spl
index=main hash=*
| lookup malware_hashes.csv md5 OUTPUT is_malware
| search is_malware=true
| stats count by src_ip, file_name, md5
```

### 3. DNS Tunneling Detection
```spl
index=main sourcetype=dns_query
| stats count by query, src_ip
| where count > 100
| search query="*-*-*-*"
```

---

## 📊 Dashboards & Reports

### Create a Dashboard:
```
| timechart count by severity
| stats avg(response_time) by dest_ip
```

### Create an Alert:
```spl
index=main EventCode=4625
| stats count by src_ip, user
| where count > 10
```

---

**Last Updated:** November 2025  
**Author:** Michael Taylor
