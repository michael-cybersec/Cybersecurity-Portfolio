# Linux Security Commands Cheat Sheet

## 📋 Overview
Essential Linux commands for security operations, system hardening, and threat hunting.

---

## 🔍 User & Permission Management

### View Current User
```bash
whoami
id
groups
```

### Add/Remove Users
```bash
# Add user
sudo useradd -m -s /bin/bash newuser
sudo usermod -aG sudo newuser

# Remove user
sudo userdel -r newuser
```

### Set File Permissions
```bash
chmod 644 file.txt      # rw-r--r--
chmod 755 script.sh     # rwxr-xr-x
chmod 600 private.key   # rw-------

# Recursive
chmod -R 755 /var/www/html
```

### Check File Ownership
```bash
ls -la /var/www/
chown user:group file.txt
chown -R user:group /directory/
```

---

## 🔐 SSH Security

### Generate SSH Keys
```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -N ""
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519
```

### SSH Key Permissions
```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
chmod 644 ~/.ssh/authorized_keys
```

### Secure SSH Config
```bash
# Edit /etc/ssh/sshd_config
Port 2222
PermitRootLogin no
PubkeyAuthentication yes
PasswordAuthentication no
AllowUsers user1 user2
```

### Restart SSH Service
```bash
sudo systemctl restart sshd
sudo service ssh restart
```

---

## 📋 Log Analysis

### View System Logs
```bash
# System logs
tail -f /var/log/syslog
tail -f /var/log/messages

# Authentication logs
tail -f /var/log/auth.log
grep "Failed password" /var/log/auth.log

# SSH logs
grep sshd /var/log/auth.log
grep "Failed password" /var/log/auth.log | wc -l

# Web server logs
tail -f /var/log/apache2/access.log
tail -f /var/log/nginx/access.log
```

### Filter Logs
```bash
# Failed SSH attempts
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c

# Port scans
grep "UFW" /var/log/syslog | grep "BLOCK"

# File access
audit logs: /var/log/audit/audit.log
```

---

## 🛡️ Firewall & Network Security

### UFW (Ubuntu Firewall)
```bash
# Enable/Disable
sudo ufw enable
sudo ufw disable

# Allow/Deny ports
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw deny 23/tcp

# View status
sudo ufw status
sudo ufw status verbose

# Reset
sudo ufw reset
```

### iptables Rules
```bash
# View current rules
sudo iptables -L -n -v

# Add rule
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Block IP
sudo iptables -A INPUT -s 192.168.1.100 -j DROP

# Save rules
sudo iptables-save > /etc/iptables/rules.v4
```

---

## 📊 System Monitoring

### Process Management
```bash
# List processes
ps aux
ps aux | grep user

# Monitor processes
top
htop

# Kill process
kill PID
kill -9 PID
killall process_name
```

### Network Monitoring
```bash
# Network connections
netstat -tulpn
netstat -an | grep LISTEN
netstat -an | grep ESTABLISHED

# Modern alternative
ss -tulpn
ss -an | grep LISTEN

# DNS lookups
nslookup example.com
dig example.com
```

### Open Files
```bash
# List open files
lsof -i :8080        # Port 8080
lsof -u username     # By user
lsof /var/log/syslog # By file
```

---

## 🔎 Threat Hunting

### Find Recently Modified Files
```bash
find / -type f -mtime -1        # Modified in last 24 hours
find / -type f -mmin -30        # Modified in last 30 minutes
find / -type f -newermt "2025-01-01"
```

### Find SUID/SGID Binaries
```bash
find / -perm -4000  # SUID
find / -perm -2000  # SGID
```

### Search for Backdoors
```bash
# Find suspicious startup scripts
ls -la /etc/rc.local
ls -la /etc/init.d/
ls -la ~/.bashrc
ls -la ~/.bash_profile

# Check cron jobs
crontab -l
cat /etc/crontab
```

### Check for Rootkits
```bash
# Download rootkit hunter
sudo apt-get install rkhunter
sudo rkhunter --check --skip-keypress

# Alternative: chkrootkit
sudo apt-get install chkrootkit
sudo chkrootkit
```

---

## 🔐 Hardening Commands

### Password Policy
```bash
# Edit password aging
sudo chage -l username
sudo chage -M 90 username  # Max 90 days
sudo chage -m 1 username   # Min 1 day between changes
```

### Sudo Configuration
```bash
# View sudoers
sudo visudo

# Add user to sudoers
sudo usermod -aG sudo username
```

### Disable Services
```bash
# Stop service
sudo systemctl stop service_name
sudo systemctl disable service_name

# List services
sudo systemctl list-unit-files | grep enabled
```

---

**Last Updated:** November 2025
