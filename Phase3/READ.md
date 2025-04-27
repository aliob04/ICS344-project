

# Phase 3: Fail2Ban Defense Implementation  

## Overview  
This phase demonstrates the implementation of Fail2Ban to:
- Automatically block brute force attempts
- Protect SSH services
- Show before/after attack scenarios

---

## Defense Implementation  

### 1. Fail2Ban in Action  

#### Event Log  

```
2025-04-25 13:44:26,626 fail2ban.actions: NOTICE [sshd] Ban 192.168.56.102
```

> **Output Description**:  
> The IP `192.168.56.102` is banned after multiple failed login attempts.

---

### 2. Before/After Comparison  

#### Before Implementation  

```plaintext
Apr 25 13:44:22 metasploitable3-ub1404 sshd[2371]: Failed password for invalid user admin from 192.168.56.102
[Repeated multiple times until successful]
```

#### After Implementation  

```plaintext
2025-04-25 13:44:26 fail2ban: Blocking 192.168.56.102 for 10 minutes
```

---

### Key Differences  

| Scenario           | Max Attempts | Result                     |
|---------------------|--------------|----------------------------|
| Before Fail2Ban     | Unlimited    | Successful brute force     |
| After Fail2Ban      | 3 attempts   | IP automatically banned    |

---

### Requirements  

- Fail2Ban installed
- SSH logs monitored
- iptables/firewalld active

---


