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


|**Action**|**Linux (Bash)**|**Windows (CMD)**|
|---|---|---|
|**Read a File**|`cat`|`type`|
|**Clear the Screen**|`clear`|`cls`|
|**List Directory**|`ls`|`dir`|
|**Find Where You Are**|`pwd`|`cd` (by itself)|
|**Search for Text**|`grep`|`findstr`|
|**Change Password**|`passwd`|`net user`|
|**Help Manual**|`man [command]`|`[command] /?`|
