# ICS344-project

## Phase Details

### Phase 1: SSH Service Compromise
- **Methods Used**:
  - Metasploit framework (auxiliary/scanner/ssh/ssh_login)
  - Custom Python bruteforce script
- **Proof of Concept**:
  - Successful SSH login with compromised credentials
  - Screenshots of vulnerability scanning and exploitation

### Phase 2: SIEM Analysis
- **Tools Used**: Splunk
- **Key Visualizations**:
  - SSH brute force attack patterns
  - Failed login attempts
  - Source IP analysis
- **Findings**:
  - Identified attack patterns
  - Correlated events from multiple sources

### Phase 3: Defense Strategy (Fail2Ban)
- **Implementation**:
  - Installed and configured Fail2Ban on Metasploitable3
  - Created custom jail for SSH service
  - Set appropriate ban time and retry limits
- **Results**:
  - Before: Unlimited brute force attempts possible
  - After: IP banned after 5 failed attempts (evidence in screenshots)
  - Screenshots show blocked IPs in Fail2Ban log
