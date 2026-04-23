### Objective

Analyze a suspicious phishing email and extract actionable indicators for SOC triage and containment.

---
### Tools Used
- ANY.RUN
- CyberChef
- Message Header Analyzer

---

###  Investigation Steps
#### 1. Email Header Analysis
- Identified recipient domain via `X-Apparently-To`
- Detected spoofed sender domain (typosquatting)

---

#### 2. Sandbox Analysis
- Uploaded sample to ANY.RUN
- Navigated to:
    - **Processes**
    - **Connections**

**Extracted IOCs:**

- SHA256 hash
- Malicious IP address
- Suspicious process behavior

---

#### 3. URL Analysis (Safe Handling)
- Extracted phishing URL without clicking
- Preserved for:
    - enrichment
    - sandbox detonation

---

###  Findings
- Email used **social engineering + obfuscation**
- Malware exhibited **C2 communication behavior**
- Indicators suitable for:
    - SIEM alerts
    - firewall blocking
    - threat intel enrichment

---

###  Recommendations
- Block malicious IP at firewall
- Add hash to EDR blocklist
- Monitor for similar phishing patterns
- Implement user awareness training

---
