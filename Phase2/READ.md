# Phase 2: SIEM Analysis

---

##  Overview

This phase demonstrates security event monitoring using Splunk to:
- Forward SSH authentication logs
- Analyze brute force patterns
- Visualize attack events

---

##  Analysis Methodologies

### 1. Splunk Forwarder Configuration
![image](https://github.com/user-attachments/assets/cdf8d5e3-e954-458c-8b65-de4e11d89488)

#### Setup Commands
```bash
sudo /opt/splunkforwarder/bin/splunk add forward-server 192.168.56.102:9997
sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/auth.log
sudo /opt/splunkforwarder/bin/splunk list forward-server
```

#### Output
```
Active forwards:
192.168.56.102:9997

Configured but inactive forwards:
None
```

---

### 2. Splunk Event Analysis

#### Sample Event
![image](https://github.com/user-attachments/assets/91ada7b9-5df2-4953-b40c-1c8bbfb497e7)



#### Event Fields
- `host`: metasploitable3-ub1404
- `source`: /var/log/auth.log
- `process`: sshd

---

### 3. Attack Pattern Visualization

#### Search Interface
![image](https://github.com/user-attachments/assets/b17e5ab4-38c7-471d-b9ba-0ab048b91a47)

#### Observed Event Patterns
```text
sshd[2363]: Failed password for vagrant
sshd[2363]: Accepted password for vagrant
```
##  Visualization
![visualization](https://github.com/user-attachments/assets/9f3b37f6-2833-4b98-b2d5-9a0943fe883d)
---
This pattern of short, intense bursts of failed logins is exactly what we expect to see when a system is being hit by a brute-force attack. It indicates that an external source was rapidly and repeatedly trying to log in incorrectly during those specific times.
---
---

##  Requirements

- Splunk Enterprise
- Splunk Universal Forwarder v9.4.1
- SSH auth logs from Metasploitable3

---

