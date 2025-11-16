# SIEM Incident Response Lab

## 📋 Project Overview

This hands-on lab demonstrates **incident response and threat hunting** using SIEM tools. It simulates a real-world security incident, from initial detection through investigation, containment, and remediation.

**Duration:** 4-6 hours  
**Difficulty:** Advanced  
**Tools Used:** Splunk, ELK Stack, YARA, PowerShell, osquery  

---

## 🎯 Objective

To investigate a simulated security breach, identify the attack timeline, determine the scope of compromise, and develop response procedures using SIEM tools and threat hunting techniques.

---

## 🔧 Environment & Setup

### Lab Configuration

| Component | Details |
|-----------|---------|
| **SIEM Platform** | Splunk Enterprise or ELK Stack |
| **Log Sources** | Windows Event Logs, Syslog, Application Logs |
| **Attack Simulation** | Atomic Red Team or custom scripts |
| **Threat Intel** | OSINT, VirusTotal, MITRE ATT&CK |
| **OS** | Windows Server 2019, Ubuntu 20.04 |

### Prerequisites

- SIEM platform deployed and configured
- Log forwarding from endpoints
- Sample data ingested (attacks simulated)
- Threat intelligence feeds configured

---

## 📊 Incident Response Workflow

### Phase 1: Detection & Alerting

**Objective:** Identify suspicious activity through SIEM alerts

**Steps:**
1. **Review Alert Dashboard**
   - Check SIEM alerts and anomalies
   - Identify spike in login failures
   - Flag unusual process executions

2. **Initial Triage**
   ```spl
   # Splunk SPL query to find suspicious login attempts
   index=windows EventCode=4625 
   | stats count by user, src_ip 
   | where count > 10
   ```

3. **Determine Severity**
   - Assess impact (Critical/High/Medium/Low)
   - Estimate affected systems
   - Identify target systems

**Tools Used:** Splunk, Grafana dashboards  
**Duration:** 30 minutes

---

### Phase 2: Investigation & Analysis

**Objective:** Gather evidence and understand the attack

**Steps:**
1. **Timeline Construction**
   ```spl
   # Build attack timeline
   index=* src_ip=192.168.1.100 
   | timechart count by event_type 
   | sort _time
   ```

2. **User Account Analysis**
   - Track user logons and logoffs
   - Identify privilege escalations
   - Review group membership changes
   ```powershell
   # PowerShell script to check account modifications
   Get-EventLog -LogName Security -InstanceId 4728 | Select-Object TimeGenerated, Message
   ```

3. **Process & Execution Analysis**
   ```spl
   # Hunt for suspicious processes
   index=windows EventCode=1 
   | search Image IN (cmd.exe, powershell.exe, psexec.exe)
   | stats count by ComputerName, CommandLine
   ```

4. **Network Connection Analysis**
   ```spl
   # Detect suspicious outbound connections
   index=network dest_port IN (443, 8443, 4444, 5555)
   | stats count by src_ip, dest_ip, dest_port
   | search count > 5
   ```

**Tools Used:** Splunk, ELK Stack, osquery  
**Duration:** 2-3 hours

---

### Phase 3: Containment & Mitigation

**Objective:** Stop the attack and limit damage

**Steps:**
1. **Immediate Actions**
   - Isolate affected systems from network
   - Disable compromised user accounts
   - Reset credentials
   - Block malicious IPs at firewall

2. **Automated Response**
   ```python
   # Python script for automated response
   import requests
   
   def block_ip(malicious_ip):
       firewall_api = "https://firewall.internal/api/block"
       payload = {"ip": malicious_ip, "action": "block"}
       response = requests.post(firewall_api, json=payload)
       return response.status_code
   
   malicious_ips = ["203.0.113.45", "203.0.113.89"]
   for ip in malicious_ips:
       block_ip(ip)
   ```

3. **Threat Hunting with YARA**
   ```yara
   # YARA rule to detect malware signatures
   rule Suspicious_Process_Execution {
       strings:
           $cmd1 = "cmd.exe /c" nocase
           $cmd2 = "powershell.exe -ExecutionPolicy Bypass" nocase
           $cmd3 = "certutil.exe -decode" nocase
       condition:
           any of them
   }
   ```

**Tools Used:** Firewall API, PowerShell, YARA  
**Duration:** 1 hour

---

### Phase 4: Recovery & Remediation

**Objective:** Restore systems and apply long-term fixes

**Steps:**
1. **System Hardening**
   - Apply security patches
   - Update antivirus signatures
   - Review firewall rules

2. **Access Control Review**
   - Audit user permissions
   - Implement principle of least privilege
   - Enable MFA where applicable

3. **Monitoring Enhancements**
   - Create new detection rules
   - Implement additional log sources
   - Tune alert thresholds

**Tools Used:** SIEM, Configuration Management  
**Duration:** 2-3 hours

---

### Phase 5: Post-Incident Analysis

**Objective:** Document lessons learned and improve processes

**Steps:**
1. **Root Cause Analysis**
   - How did the attacker gain access?
   - What vulnerabilities were exploited?
   - Why was it not detected earlier?

2. **Timeline Report**
   - Document all activities chronologically
   - Identify detection gaps
   - Map to MITRE ATT&CK tactics

3. **Recommendations**
   - Specific technical fixes
   - Process improvements
   - Training needs

**Deliverable:** `reports/incident-response-report.md`

---

## 🔍 Key Findings & Tactics

### Attack Timeline

| Time | Event | Severity | Details |
|------|-------|----------|---------|
| 14:32 | Initial Access | High | Phishing email delivered |
| 14:45 | User Clicked Link | High | Malware downloaded |
| 15:02 | Execution | Critical | Process injection detected |
| 15:15 | Privilege Escalation | Critical | UAC bypass attempted |
| 16:30 | Lateral Movement | High | SMB scan on network |
| 17:00 | Data Collection | Critical | Sensitive files accessed |

### MITRE ATT&CK Mapping

| Tactic | Technique | Detection |
|--------|-----------|-----------|
| **Initial Access** | Phishing (T1566) | Email gateway logs |
| **Execution** | Command Line (T1059) | Process creation events |
| **Privilege Escalation** | UAC Bypass (T1548) | Windows event logs |
| **Lateral Movement** | SMB/Windows Admin Shares (T1570) | Network logs |
| **Collection** | Data from Local System (T1005) | File access logs |

---

## 📁 Artifacts & Deliverables

| Artifact | Description | Location |
|----------|-------------|----------|
| SPL Queries | SIEM detection queries | `spl-queries/` |
| YARA Rules | Malware detection rules | `yara-rules/` |
| Investigation Log | Detailed incident timeline | `logs/investigation.md` |
| Incident Report | Executive summary | `reports/incident-response-report.md` |
| Playbook | Automated response procedures | `playbooks/incident-response-playbook.md` |

---

## 🔄 How to Reproduce

### Prerequisites

```bash
# Deploy SIEM environment
docker pull splunk/splunk:latest
docker run -d -p 8000:8000 splunk/splunk:latest

# Or use ELK Stack
docker-compose -f docker-compose-elk.yml up -d
```

### Simulation Steps

1. **Ingest Sample Data**
   ```bash
   # Load attack simulation data
   /opt/splunk/bin/splunk add forward-server 192.168.1.100:9997 \
     -auth admin:password
   ```

2. **Run Attack Simulation** (Atomic Red Team)
   ```powershell
   # On Windows endpoint
   Invoke-AtomicTest T1059.001 -Confirm:$false
   ```

3. **Generate Alerts**
   - Check SIEM dashboard for triggered alerts
   - Verify log collection

4. **Investigate Using SIEM**
   ```spl
   # Start with broad search
   index=* src_ip=192.168.1.100 earliest=-1h
   | timeline
   ```

5. **Execute Response Actions**
   - Follow incident response playbook
   - Document timeline

---

## 📚 SIEM Queries Reference

### User Authentication Analysis
```spl
index=windows EventCode=4624 OR EventCode=4625
| stats count by user, src_ip, EventCode
| search count > 10
```

### Process Execution Monitoring
```spl
index=windows EventCode=1
| search Image IN (cmd.exe, powershell.exe, wmic.exe)
| table _time, ComputerName, Image, CommandLine, User
```

### Network Anomaly Detection
```spl
index=network
| stats count by src_ip, dest_port
| where count > threshold
| search dest_port NOT IN (80, 443, 22, 23)
```

### File Access Tracking
```spl
index=windows EventCode=4663 ObjectName=*sensitive*
| stats count by SubjectUserName, ObjectName
| table _time, SubjectUserName, ObjectName
```

---

## 💡 Key Learnings

✅ **What Worked Well:**
- SIEM detection of attack progression
- Automated response procedures
- Comprehensive logging and correlation
- Clear documentation for stakeholders

⚠️ **Challenges:**
- Alert fatigue from too many rules
- False positives slowing investigation
- Need for better baseline tuning
- Skill gap in threat hunting

🔧 **Improvements:**
- Implement smarter alert correlation
- Use machine learning for anomaly detection
- Expand threat intelligence feeds
- Enhance SIEM query optimization

---

## 🔗 Related Resources

- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [Splunk Documentation](https://docs.splunk.com/)
- [ELK Stack Guide](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)
- [NIST Incident Response](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r3.pdf)
- [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team)

---

## ⚠️ Important Notes

### Authorization

✅ **This lab:**
- Was conducted in isolated lab environment
- Used simulated attack data
- Followed all ethical guidelines
- Documented for educational purposes

### SIEM Best Practices

1. **Baseline First** – Understand normal behavior before detecting anomalies
2. **Alert Tuning** – Continuously refine detection rules
3. **Correlation** – Combine multiple signals for accuracy
4. **Automation** – Use playbooks for faster response

---

## 📞 Questions & Support

For questions about this project:
- Email: michael.taylor@example.com
- GitHub: [michael-cybersec](https://github.com/michael-cybersec)

---

**Project Completed:** November 2025  
**Last Updated:** November 16, 2025  
**Status:** ✅ Complete and Documented
