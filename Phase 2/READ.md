# Phase 2: SIEM Analysis  


## 📝 Overview  
This phase demonstrates security event monitoring using Splunk to:
- Forward SSH authentication logs
- Analyze brute force patterns
- Visualize attack events

---

## 🔍 Analysis Methodologies

### 1. Splunk Forwarder Configuration

![image](https://github.com/user-attachments/assets/096a71ac-1cab-414b-b801-445df4d6e58a)

#### Setup Commands
```bash
sudo /opt/splunkforwarder/bin/splunk add forward-server 192.168.56.102:9997
sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/auth.log
sudo /opt/splunkforwarder/bin/splunk list forward-server

Output

Active forwards:
    192.168.56.102:9997
Configured but inactive forwards:
    None

2. Splunk Event Analysis
Sample Event

![image](https://github.com/user-attachments/assets/7e42314a-35b2-449d-baaf-1f1a55501b64)


Event Fields
host:	metasploitable3-ub1404
source:	/var/log/auth.log
process:	sshd

3. Attack Pattern Visualization
Search Interface
![Uploading image.png…]()

Observed Event Patterns
sshd[2363]: Failed password for vagrant
sshd[2363]: Accepted password for vagrant

📋 Requirements
Splunk Enterprise

Splunk Universal Forwarder v9.4.1

SSH auth logs from Metasploitable3
