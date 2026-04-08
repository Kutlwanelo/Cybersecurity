## Scenario

In this investigation, I analyzed web traffic logs using Splunk to identify malicious activity across different stages of an attack lifecycle. The objective was to detect reconnaissance, exploitation attempts, and potential data exfiltration.

---

## 🛠️ Tools Used

- Splunk (SIEM)
- Web traffic logs (`sourcetype=web_traffic`)

---

## 🧠 Investigation Approach

The investigation followed a structured approach based on attacker behavior, moving from initial reconnaissance to final actions on objectives.

---

## 🔍 Detection & Analysis

### 1. Reconnaissance (Noise Filtering)

Attackers often use automated tools instead of standard browsers. To identify suspicious activity, I filtered out known browser user agents.

```
index=main sourcetype=web_traffic 
NOT (user_agent="*Mozilla*" OR user_agent="*Chrome*" OR user_agent="*Safari*")
| stats count by client_ip, user_agent 
| sort -count
```

**Insight:**

- Non-browser user agents (e.g., `curl`, `sqlmap`) indicate automated scanning.

---

### 2. Path Traversal Detection

To identify attempts to access restricted files, I searched for directory traversal patterns.

```
index=main sourcetype=web_traffic path="*../*" 
| table _time, client_ip, path, status
```

**Insight:**

- Patterns like `../` indicate attempts to escape the web root directory.

---

### 3. SQL Injection Detection

To detect SQL injection attempts, I searched for time-based payloads.

```
index=main sourcetype=web_traffic (path="*sleep*" OR path="*benchmark*") 
| table _time, client_ip, path, status
```

**Insight:**

- Use of `SLEEP` or `BENCHMARK` functions suggests SQL injection attempts.
- A `504 Gateway Timeout` response may indicate a successful time-based SQL injection.

---

## 🔗 Attack Lifecycle (Kill Chain Mapping)

The investigation revealed the following attack progression:

1. **Reconnaissance**
    - Scanning for sensitive files (`.env`, `.git`, `phpinfo`)
    - HTTP status: 403 / 404
2. **Exploitation**
    - SQL injection attempts using automated tools (e.g., `sqlmap`)
    - HTTP status: 200 / 504
3. **Post-Exploitation**
    - Upload of malicious file (`shell.php`)
    - Execution of payload (`bunnylock.bin`)
4. **Exfiltration**
    - Large outbound traffic to external Command & Control (C2) server

---

## 🚨 Findings

- Identified suspicious client IP performing automated scanning
- Detected use of SQL injection techniques
- Confirmed successful exploitation based on response behavior
- Observed potential data exfiltration to external server

---

## 🛡️ Mitigation Recommendations

- **Egress Filtering:** Restrict outbound connections from web servers to unknown external IPs
- **Log Ingestion Improvements:** Ensure fields like `user_agent` and `client_ip` are properly parsed
- **Protocol Hardening:** Enforce TLS (e.g., TLS 1.3) and disable insecure protocols (e.g., Telnet, FTP)
- **Input Validation:** Strengthen defenses against injection attacks

---

## 🧠 Key Insights

- Filtering known-good traffic is essential to reduce noise
- Individual logs may appear benign, but correlation reveals the full attack chain
- HTTP status codes can provide strong indicators of successful exploitation
- Understanding attacker behavior is critical for effective detection

---

## 🎯 Conclusion

This investigation demonstrates how Splunk can be used to detect and analyze multi-stage web attacks. By correlating different log patterns, it is possible to move from isolated events to a complete attack narrative, improving both detection and response capabilities.

---

## 📎 Skills Demonstrated

- SIEM (Splunk) usage
- Log analysis and filtering
- Detection of web-based attacks (SQLi, path traversal)
- Attack lifecycle analysis (Kill Chain)
- Investigative and analytical thinking