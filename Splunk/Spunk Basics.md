## Protocol Quick Reference

|**Protocol**|**Port**|**Secure Version**|**Port**|**Layer (OSI)**|
|---|---|---|---|---|
|**HTTP**|80|**HTTPS**|443|7 (Application)|
|**Telnet**|23|**SSH**|22|7 (Application)|
|**SMTP**|25|**SMTPS**|465/587|7 (Application)|
|**POP3**|110|**POP3S**|995|7 (Application)|
|**IMAP**|143|**IMAPS**|993|

## Splunk Investigation Workflow

_Use these queries when triaging web traffic logs (`sourcetype=web_traffic`)._

### 1. Identifying the "Noise" (Reconnaissance)

Attackers often use scripts. To find them, filter out "Known Good" browsers:
index=main sourcetype=web_traffic 
NOT (user_agent="*Mozilla*" OR user_agent="*Chrome*" OR user_agent="*Safari*")| stats count by client_ip, user_agent | sort -count

### 2.Detecting Path Traversal

Looking for attempts to escape the web directory (e.g., `../../etc/passwd`):
index=main sourcetype=web_traffic path="*../*" | table _time, client_ip, path, status

### 3. SQL Injection (SQLi) "Smoking Guns"

Look for time-delay functions. A **504 Gateway Timeout** following a `SLEEP` command usually indicates a successful exploit.
index=main sourcetype=web_traffic (path="*sleep*" OR path="*benchmark*") | table _time, client_ip, path, status

### TryHackMe Splunk Basics Did You SIEM(Advent of Cyber 2025 room)
## The Attack Lifecycle (Cyber Kill Chain)

Based on the **King Malhare** investigation:

1. **Recon:** Scanned for `.env`, `phpinfo`, and `.git` files (Status: 404/403).
    
2. **Exploitation:** Used `sqlmap` to find vulnerabilities (Status: 504/200).
    
3. **Action on Objectives:** Uploaded `shell.php` and executed `bunnylock.bin` (RCE).
    
4. **Exfiltration:** Large outbound data transfer to C2 (Command & Control) server

Note:
- **Log Ingestion:** Ensuring `user_agent` and `client_ip` are correctly parsed in Splunk.
    
- **Egress Filtering:** Blocking outbound traffic from web servers to unauthorized external IPs/Ports (Stopping the C2 contact you found).
    
- **Protocol Hardening:** Enforcing TLS 1.3 and disabling legacy cleartext protocols (Telnet/FTP).

```mermaid
graph LR
    subgraph Layer 7 - Application
    A[Web Server] -->|Log| B[Splunk: web_traffic]
    B -->|Filter| C{Suspicious UA?}
    C -->|Yes| D[Identify SQLi/RCE]
    end

    subgraph Layer 4 - Network
    D -->|Pivot| E[Splunk: firewall_logs]
    E -->|Check Port 25/143/4444| F{Outbound Connection?}
    F -->|Yes| G[**C2 EXFILTRATION**]
    end
    
    style G fill:#f96,stroke:#333,stroke-width:4px `