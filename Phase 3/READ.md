# Phase 3: Fail2Ban Defense Implementation  
![Security](https://img.shields.io/badge/Defense-Fail2Ban-red) 
![Protection](https://img.shields.io/badge/SSH-Hardening-blueviolet)

## 📝 Overview  
This phase demonstrates the implementation of Fail2Ban to:
- Automatically block brute force attempts
- Protect SSH services
- Show before/after attack scenarios

---

## 🛡️ Defense Implementation

### 1. Fail2Ban in Action

#### Event Log
```plaintext
2025-04-25 13:44:26,626 fail2ban.actions: NOTICE [sshd] Ban 192.168.56.102
![image](https://github.com/user-attachments/assets/708c558c-054a-4089-9a57-8df5584605ae)
Showing IP 192.168.56.102 being banned after multiple failed attempts

2. Before/After Comparison
Before Implementation
Apr 25 13:44:22 metasploitable3-ub1404 sshd[2371]: Failed password for invalid user admin from 192.168.56.102
[Repeated multiple times until successful]
After Implementation
2025-04-25 13:44:26 fail2ban: Blocking 192.168.56.102 for 10 minutes

Key Differences
Scenario	Max Attempts	Result
Before Fail2Ban	Unlimited	Successful brute force
After Fail2Ban	3 attempts	IP automatically banned

📋 Requirements

Fail2Ban installed
SSH logs monitored
iptables/firewalld active
