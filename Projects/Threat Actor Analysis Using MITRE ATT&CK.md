
##  Overview

In this project, I used the MITRE ATT&CK framework to analyze real-world threat groups and understand how their tactics, techniques, and tools can impact an organization. The goal was to simulate how a SOC analyst would use threat intelligence to improve detection and defensive strategies.

---

## Objectives

- Identify threat actors targeting specific industries
- Map attacker behavior using MITRE ATT&CK
- Understand associated tools and techniques
- Identify detection and mitigation opportunities

---

## Threat Group 1: Mustang Panda

###  Background

- Origin: China
- Targets: Government entities, NGOs, non-profits

---

###  Observed Behavior (MITRE Mapping)

- **Initial Access** → Phishing
- **Persistence** → Scheduled Tasks
- **Defense Evasion** → File Obfuscation
- **Command & Control** → Ingress Tool Transfer

---

###  Key Insight

Mustang Panda relies heavily on:

- Social engineering (phishing)
- Persistence mechanisms
- Obfuscation techniques to evade detection

---

##  Threat Group 2: APT33

###  Background

- Active since: 2013
- Sector: Aviation

---

###  Key Technique

- **Sub-technique:** Cloud Accounts
- Target: Cloud environments (e.g., Office 365)

---

###  Associated Tool

- Tool: Ruler

 Used for:

- Abusing cloud accounts
- Maintaining access

---

##  Detection Strategy

- **Detection ID:** DET0546

Focus:

- Detect compromised or abused cloud accounts

---

### Detection Opportunities

- Monitor abnormal login behavior
- Detect unusual cloud activity
- Identify privilege misuse

---

##  Mitigation Strategy

- **User Account Management**

Actions:

- Remove inactive accounts
- Enforce least privilege
- Monitor account usage

---

## CAR Analytics Insight

- **Tactic:** Defense Evasion
- **Analytic Type:** Situational Awareness

 Highlights the importance of:

- Monitoring changes in access permissions
- Detecting stealthy attacker behavior

---

##  Emerging Frameworks Awareness

###  AADAPT

- Focus: Digital assets (blockchain, wallets)
- Example Technique: ADT3025

---

###  ATLAS

- Focus: AI/ML threats
- Example Tactic: Defense Evasion (LLM Prompt Obfuscation)

---

##  Key Takeaways

- MITRE ATT&CK helps map real-world attacker behavior
- Threat groups reuse techniques across campaigns
- Detection should focus on behavior, not just indicators
- Cloud environments introduce new attack surfaces
- Frameworks like ATLAS show how threats are evolving into AI systems

---

##  Conclusion

This exercise demonstrates how MITRE ATT&CK can be used by SOC analysts to analyze threat actors, understand attack patterns, and improve detection strategies. By mapping techniques and identifying gaps, organizations can better prepare against targeted attacks.

---

##  Skills Demonstrated

- Threat intelligence analysis
- MITRE ATT&CK framework usage
- Detection strategy thinking
- Cloud security awareness
- Analytical reasoning