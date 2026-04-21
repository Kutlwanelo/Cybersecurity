## What is Phishing?
Phishing is a social engineering attack where an attacker tricks a user into interacting with a malicious email, link, or attachment to achieve goals such as:
- Credential theft
- Malware delivery
- Unauthorized access
- Data exfiltration

---

## How Phishing Attacks Work

1. Attacker crafts a convincing email (spoofed sender or domain)
2. Email contains:
    - Malicious link OR
    - Malicious attachment
3. User interacts with the content
4. Payload executes or credentials are captured
5. Attacker gains access or deploys further attack stages

---

## Key Indicators in Phishing Emails

###  Email-Level Indicators

- Spoofed or lookalike domains (e.g. paypaI.com vs paypal.com)
- Mismatch between sender and reply-to address
- Urgent or threatening language
- Unexpected attachments or links

---

###  URL / Link Indicators

- Suspicious or shortened URLs
- Misspelled domains (typosquatting)
- Use of Unicode characters (Punycode attacks)
- Redirect chains to unknown domains

---

###  Attachment Indicators

- Unusual file types (.exe, .zip, .iso)
- Office documents with macros
- Password-protected attachments
- Files requesting user interaction (Enable Content)

---

##  Attacker Objectives

Phishing is usually the **initial access vector**, leading to:

- Credential harvesting (fake login pages)
- Malware execution (payload delivery)
- Establishing Command & Control (C2)
- Lateral movement inside the network

---

##  Mapping to MITRE ATT&CK

- Initial Access → T1566 (Phishing)
- Execution → T1059 (Command and Scripting Interpreter)
- Credential Access → T1556 / T1110
- Command & Control → T1071

---

## Detection Strategy (SOC Perspective)

###  SIEM Detection

- Suspicious email domains or sender anomalies
- Multiple users receiving identical emails
- Unusual outbound connections after email interaction
- Login attempts from unusual IPs or locations

---

###  EDR Detection

- Office applications spawning PowerShell or cmd.exe
- Execution of files from temporary directories
- Suspicious child processes from email clients
- Script execution with encoded commands

---

###  Network Indicators

- DNS queries to newly registered or unknown domains
- HTTP/HTTPS traffic to suspicious IPs
- Beaconing patterns (regular intervals, small packets)

---

##  Example Attack Flow

1. User receives phishing email with malicious Word document
2. User enables macros
3. Word spawns PowerShell
4. PowerShell downloads malware from external server
5. Malware establishes C2 connection

---

##  Key Takeaways

- Phishing is the most common initial access vector
- Detection should focus on **behavior, not just email content**
- Email → Execution → Network activity must be correlated
- SOC analysts must investigate beyond the email itself

---

##  Analyst Mindset

From a SOC perspective, always ask:

- What happens if the user interacts with this email?
- What logs would show this activity?
- What stage of the attack lifecycle is this?
- How can this be detected or prevented?