## The Networking Toolkit (Windows & Linux)

_Focus: Connectivity, Routing, and DNS._

|**Command**|**What it does (The "Dev" View)**|**Security Purpose (The "SOC" View)**|
|---|---|---|
|`ping [IP/Domain]`|Checks if a host is "alive."|**ICMP Scanning:** If a host doesn't ping, it might be "hidden" or behind a firewall.|
|`tracert` (Win) / `traceroute` (Lin)|Shows every "hop" (router) between you and the target.|**Path Analysis:** If your traffic is going through a weird country it shouldn't, you might be a victim of **BGP Hijacking**.|
|`nslookup [Domain]`|Queries the DNS server for an IP.|**DNS Spoofing:** Checks if a domain is pointing to the _real_ IP or a fake malicious one.|
|`ipconfig /flushdns`|Clears your local DNS cache.|**Remediation:** If you accidentally visited a malicious site, you flush this to "forget" the bad IP.|
|`arp -a`|Shows the mapping of IP addresses to Physical MAC addresses.|**ARP Poisoning:** If two different IPs have the same MAC address, someone is likely "sniffing" your network!|

# **Netcat (`nc`)** 

- **Linux/Windows Command:** `nc -zv [IP] [Port]`
    
- **What it does:** It tells you if a specific port is open without the overhead of a full browser or app.
    
- **Security Use:** Checking if a web server is listening on Port 443 before you try to fix the HTTPS settings.

# **Administration**

|**Action**|**Linux (Bash)**|**Windows (CMD)**|
|---|---|---|
|**Read a File**|`cat`|`type`|
|**Clear the Screen**|`clear`|`cls`|
|**List Directory**|`ls`|`dir`|
|**Find Where You Are**|`pwd`|`cd` (by itself)|
|**Search for Text**|`grep`|`findstr`|
|**Change Password**|`passwd`|`net user`|
|**Help Manual**|`man [command]`|`[command] /?`|

# **Process Management**
| **Syntax Word (Mandatory)** | **What it represents**    | **Example**            |
| --------------------------- | ------------------------- | ---------------------- |
| **`IMAGENAME`**             | The .exe file name        | `imagename eq cmd.exe` |
| **`PID`**                   | The Process ID number     | `pid eq 1432`          |
| **`MEMUSAGE`**              | RAM usage in KB           | `memusage gt 5000`     |
| **`SERVICES`**              | The name of the service   | `services eq eventlog` |
| **`STATUS`**                | Running or Not Responding | `status eq running`    |


# **Malware Analysis** 
Hash Comparison Table

|**Algorithm**|**Length (Chars)**|**Security Level**|**Use Case**|
|---|---|---|---|
|**MD5**|32|Low|Quick file verification.|
|**SHA1**|40|Medium|Legacy systems.|
|**SHA256**|64|High|**Standard** for modern security.|
|**SHA512**|128|Ultra|High-sensitivity data.|

## Incident Response Snippets

- **Check Connections:** `Get-NetTCPConnection | Where-Object State -eq "Established"`
    
- **Find Hidden Streams (ADS):** `Get-Item -Path "C:\Path\To\File.txt" -Stream *`
    
- **Verify Integrity:** `Get-FileHash -Path "file.exe" -Algorithm SHA256`
    
- **Filter Running Services:** `Get-Service | Where-Object Status -eq "Running"`


## Linux Essentials (Bash)

- **Navigation:** `pwd` (Where am I?), `ls -a` (Show everything, including hidden).
    
- **The "Bloodhound":** `find /path -name "file" 2>/dev/null` (Finds files while hiding errors).
    
- **The "Sieve":** `grep "text" file` (Filter for specific strings).
    
- **Permissions:** `chmod +x script.sh` (Unlocks the "Run" button).
    
- **Root Power:** `sudo su` (Become the boss).
    

## 🪟 Windows Essentials (PowerShell)

- **Navigation:** `Get-ChildItem -Force` (The `ls -a` equivalent).
    
- **Integrity:** `Get-FileHash -Algorithm SHA256` (Check for file tampering).
    
- **Processes:** `Get-NetTCPConnection` (See who is talking to your machine).
    
- **Formatting:** `| Format-List` (See the full data without the `...` cuts).
    

## 🛠️ The "Scripting" Logic

- **Shebang:** `#!/bin/bash` (Always at the very top).
    
- **Variables:** `name="Value"` (To set), `$name` (To use).
    
- **Redirection:** `>` (Overwrite/Kill), `>>` (Append/Safe).
-

# Struggles & Solutions

|**The Struggle**|**The "Aha!" Moment**|
|---|---|
|**The "File Not Found" Loop**|Just because a script says a name doesn't mean it's in your current folder. **Always use the Absolute Path** (e.g., `/var/log/file.log`).|
|**The "Nano" Trap**|You can't use a mouse in the terminal! **Use Arrow Keys** and `CTRL+O` / `CTRL+X` to escape.|
|**The "Space" Bug**|In Bash, `directory = "/var/log"` fails. **Remove spaces** around the `=` sign!|
|**The "Relative" Confusion**|`./` means "Starting right here." If you are in `/home/user`, then `./var` doesn't exist because `var` is at the **Root** (`/`).|
|**VM Lag vs. Typing**|When the VM is slow, use **Tab Completion**. It prevents typos and confirms the file actually exists before you hit Enter.|