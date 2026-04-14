
##  Overview

In this project, I participated in a simulated purple team engagement where malware samples were executed on a workstation. My role as a SOC analyst was to iteratively improve detection capabilities using the Pyramid of Pain framework.

The objective was to move from low-value indicators (easy for attackers to change) to high-value behavioral detections that significantly increase the attacker’s cost of operation.

---

##  Objectives

- Analyze malware behavior across multiple executions
- Apply detection strategies at each level of the Pyramid of Pain
- Improve detection resilience against attacker evasion
- Simulate real-world SOC detection engineering

---

##  Sample 1 – Hash-Based Detection

- File: `sample1.exe`
- Size: 202.50 KB
- Detection: Trojan.Metasploit.A
- Behavior: Suspicious connection to external port
###  Action Taken
- Added SHA-256 hash to blocklist
###  Limitation

- Easily bypassed by recompiling malware

 **Pyramid Level:** Hash (Low Value)

---

##  Sample 2 – IP-Based Detection

- Observed network activity:
    - HTTPS request
    - Multiple TCP/UDP connections
- Suspicious external IP identified

###  Action Taken

- Created firewall rule to block IP

###  Limitation

- Attacker can rotate IP addresses

**Pyramid Level:** IP Address

---

## Sample 3 – Domain-Based Detection

- DNS + HTTPS traffic observed
- Suspicious domain linked to `backdoor.exe`

###  Action Taken

- Blocked malicious domain

### Limitation

- Domains can be easily re-registered

 **Pyramid Level:** Domain

---

## Sample 4 – Host Artifact Detection

- Registry modification detected:
    - Disabled real-time monitoring

### Action Taken

- Created Sigma rule to detect registry changes

###  Insight

- This indicates **defense evasion behavior**

 **Pyramid Level:** Host Artifact (Higher Value)

---

##  Sample 5 – Network Behavior Detection

- Repeated connections to same IP
- Beaconing pattern:
    - Every few minutes
    - Constant packet size (97 bytes)
- Process: `beacon.bat`

###  Action Taken

- Created detection rule for beaconing behavior

###  Insight

- Indicates **Command & Control (C2)** activity

 **Pyramid Level:** Network Artifact

---

## Sample 6 – Exfiltration Detection

- Suspicious file creation:
    - `%temp%\exfiltr8.log`
- Data staging and exfiltration behavior observed

###  Action Taken

- Created detection using Sysmon logs:
    - File path monitoring
    - File name detection

###  Insight

- Maps to **data exfiltration techniques**

 **Pyramid Level:** TTP (High Value)

---

##  Key Progression

|Level|Detection Type|Effectiveness|
|---|---|---|
|Hash|File-based|Weak|
|IP|Network|Weak|
|Domain|Network|Medium|
|Host Artifact|System behavior|Strong|
|Network Artifact|Traffic patterns|Strong|
|TTP|Behavior|Very Strong|

---

## Key Takeaways

- Lower-level indicators are easily bypassed by attackers
- Behavioral detection significantly increases attacker effort
- Detection engineering is an iterative process
- Beaconing and exfiltration patterns are strong indicators
- Combining host + network visibility provides better coverage

---
## Detection Engineering & Purple Team Insights

During this exercise, I developed an understanding of how detection engineering works in a real-world purple team environment.

###  Iterative Detection Development

- Repeatedly reviewed Sigma rules to refine detection logic
- Tuned detections based on observed attacker behavior
- Focused on improving detection resilience rather than one-time alerts

---

###  Network Signature Authoring

- Analyzed network traffic patterns (beaconing, packet size consistency)
- Created detection rules based on behavior rather than static indicators
- Focused on reducing false positives while maintaining detection accuracy

---

###  Multi-Source Investigation

- Correlated data from:
    - Network logs (traffic behavior)
    - Command logs (process execution)
- Used both perspectives to improve detection quality

---

###  Key Insight

Effective detection engineering requires:

- Iteration
- Correlation across multiple data sources
- Focus on behavior over static indicators

This mirrors real-world SOC workflows where analysts continuously refine detections during active threat simulations.
##  Conclusion

This exercise demonstrates how defenders can progressively improve detection capabilities by moving up the Pyramid of Pain. By focusing on behavioral indicators rather than static signatures, organizations can create more resilient defenses against evolving threats.

---

##  Skills Demonstrated

- Detection engineering
- SOC analysis
- Threat behavior analysis
- Sigma rule creation
- Log analysis (Sysmon, network logs)
- Pyramid of Pain application