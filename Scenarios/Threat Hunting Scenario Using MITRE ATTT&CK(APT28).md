
##  Overview

In this scenario, I acted as a SOC analyst responding to intelligence about potential activity from an APT group targeting the organization. Using the MITRE ATT&CK framework, I identified tactics, techniques, and procedures (TTPs) associated with the threat group and mapped them across the attack lifecycle.

---

##  Objective

- Identify potential attacker behavior using threat intelligence
- Map techniques to MITRE ATT&CK
- Determine detection opportunities across the attack chain

---

##  Attack Progression (MITRE Mapping)

### Initial Access & Reconnaissance

- Technique: Spearphishing Link
- Target: Email accounts

---

### Execution

- Techniques:
    - Malicious File
    - Malicious Link
- Indicators:
    - PowerShell execution
    - Windows Command Shell usage

---

### Persistence

- Registry Run Keys modified

---

### Defense Evasion

- Use of `rundll32` for proxy execution
- Obfuscated scripts

---

### Discovery

- Network sniffing using tools like `tcpdump`

---

### Lateral Movement

- Exploitation of remote services:
    - SMB / Windows Admin Shares

---

### Collection & Exfiltration

- Target: SharePoint repositories
- Exfiltration Methods:
    - External Proxy
    - Multi-hop Proxy

---

##  Key Takeaways

- APT groups follow predictable behavioral patterns
- MITRE ATT&CK helps map attacks end-to-end
- Detection should focus on:
    - PowerShell usage
    - Registry persistence
    - Network sniffing tools
    - Lateral movement via SMB

---

##  Conclusion

This exercise demonstrates how SOC analysts can use MITRE ATT&CK to proactively hunt for attacker behavior and identify potential compromises before significant damage occurs.

---

##  Skills Demonstrated

- Threat hunting
- MITRE ATT&CK mapping
- Attack lifecycle analysis
- Detection awareness