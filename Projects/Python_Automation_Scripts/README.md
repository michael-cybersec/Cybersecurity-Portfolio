# Python Security Automation Scripts

## 📋 Project Overview
Custom Python scripts for automated security monitoring, log analysis, and vulnerability scanning.

## 🎯 Objectives
- Automate routine security tasks
- Improve efficiency and consistency
- Reduce manual error
- Enable scalable security operations

## 🛠️ Technologies & Libraries
- **Python 3.9+**
- **Requests** - HTTP requests
- **BeautifulSoup** - Web scraping
- **Paramiko** - SSH automation
- **PyYAML** - Configuration files
- **Elasticsearch** - Log querying
- **Splunk SDK** - SIEM integration

## 📁 Project Structure
```
Python_Automation_Scripts/
├── README.md                   # This file
├── requirements.txt            # Dependencies
├── config/                     # Configuration files
├── scripts/
│   ├── log_analyzer.py        # Log analysis
│   ├── vulnerability_scanner.py
│   ├── threat_hunter.py       # Threat hunting
│   └── siem_integrator.py     # SIEM integration
├── utils/                      # Utility modules
└── tests/                      # Unit tests
```

## 🔧 Available Scripts

### 1. Log Analyzer (`log_analyzer.py`)
Parses and analyzes security logs for anomalies.

```bash
python log_analyzer.py --file logs.txt --filter error
```

### 2. Vulnerability Scanner (`vulnerability_scanner.py`)
Scans systems for common vulnerabilities.

```bash
python vulnerability_scanner.py --target 192.168.1.0/24
```

### 3. Threat Hunter (`threat_hunter.py`)
Executes threat hunting queries against SIEM.

```bash
python threat_hunter.py --query config.yaml
```

### 4. SIEM Integrator (`siem_integrator.py`)
Pushes custom alerts to SIEM platform.

```bash
python siem_integrator.py --alert alert.json
```

## 📦 Installation

```bash
# Clone repository
git clone https://github.com/michael-cybersec/Cybersecurity-Portfolio.git

# Install dependencies
pip install -r requirements.txt

# Run scripts
python scripts/log_analyzer.py
```

## 📝 Configuration
Create a `config.yaml` file:

```yaml
siem:
  type: splunk
  host: 192.168.1.10
  port: 8089
  username: admin
  password: ${SIEM_PASSWORD}

logging:
  level: INFO
  file: logs/automation.log
```

## ✅ Features Implemented
- [ ] Log Analysis
- [ ] Vulnerability Scanning
- [ ] Threat Hunting Queries
- [ ] SIEM Integration
- [ ] Alert Generation
- [ ] Report Generation
- [ ] Scheduling/Cron Integration

## 🧪 Testing
```bash
python -m pytest tests/
```

## 📊 Performance Metrics
- Average scan time: X minutes
- Detection accuracy: X%
- False positive rate: X%

---

**Last Updated:** November 2025  
**Version:** 1.0.0  
**Author:** Michael Taylor
