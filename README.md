# ICS344-project

## Contribution:
| Name              | ID        | Contribution     |
|-------------------|-----------|------------------|
| Ali Al-Nassir     | 202155330 | Phase 1, Phase 3 |
| Ali Al-Bugeaey    | 202153970 | Phase 2          |
| Abdullah Al-Jishi | 202183870 | Documentation    |

## Phase Details

### Phase 1: SSH Service Compromise
- **Methods Used**:
  - Metasploit framework (auxiliary/scanner/ssh/ssh_login)
  - Custom Python bruteforce script
- **Proof of Concept**:
  - Successful SSH login with compromised credentials
  - Screenshots of vulnerability scanning and exploitation
- **Details**: [Phase 1 Details](Phase1/READ.md)

### Phase 2: SIEM Analysis
- **Tools Used**: Splunk
- **Key Visualizations**:
  - SSH brute force attack patterns
  - Failed login attempts
  - Source IP analysis
- **Findings**:
  - Identified attack patterns
  - Correlated events from multiple sources
- **Details**: [Phase 2 Details](Phase2/READ.md)

### Phase 3: Defense Strategy (Fail2Ban)
- **Implementation**:
  - Installed and configured Fail2Ban on Metasploitable3
  - Created custom jail for SSH service
  - Set appropriate ban time and retry limits
- **Results**:
  - Before: Unlimited brute force attempts possible
  - After: IP banned after 5 failed attempts (evidence in screenshots)
  - Screenshots show blocked IPs in Fail2Ban log
- **Details**: [Phase 3 Details](Phase3/READ.md)
