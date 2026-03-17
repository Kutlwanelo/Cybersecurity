### The Coffee Shop Connection: Core Protocols

|Protocol|Role|Analogy|Key Detail|
|---|---|---|---|
|DHCP|Configuration|The Concierge|Uses DORA (Discover, Offer, Request, ACK). Ports 67/68.|
|DNS|Translation|The Phonebook|Maps Names -> IPs (e.g., A, AAAA, MX records). Port 53.|
|ARP|Resolution|The Office Shouter|Maps IP -> MAC address. Operates at Layer 2.|



## Protocol Deep Dives

#### 1. DHCP (DORA Process)

- **Discover:** Client shouts for a server (`0.0.0.0` -> `255.255.255.255`).
    
- **Offer:** Server offers an available IP.
    
- **Request:** Client accepts the specific IP.
    
- **Acknowledge:** Server confirms the lease.
    

#### 2. DNS Record Types (SOC Analyst Cheat Sheet)

- **A:** IPv4 address.
    
- **AAAA:** IPv6 address.
    
- **CNAME:** Alias (points to another domain).
    
- **MX:** Mail servers.
    
- **TXT:** Verification/Security info.
    

#### 3. ARP (Address Resolution Protocol)

- **The Problem:** IP packets need a MAC address to travel over Ethernet/WiFi.
    
- **The Solution:** Broadcast an "ARP Request" -> Receive a Unicast "ARP Reply."
    
- **Security Risk:** **ARP Spoofing** (Attacker pretends to be the Gateway to intercept traffic).
    

---

## 💡 Professor's Tip :

> If you're ever troubleshooting a network connection:
> 
> 1. Can't get an IP? Check **DHCP**.
>     
> 2. Can't reach `google.com` but can reach `8.8.8.8`? Check **DNS**.
>     
> 3. Can't talk to the laptop sitting right next to you? Check **ARP**
>

### The OSI Model Cheat Sheet

| Layer | Name         | Data Unit | Protocols/Hardware         |
| ----- | ------------ | --------- | -------------------------- |
| 7     | Application  | Data      | HTTP, DNS, DHCP, FTP       |
| 6     | Presentation | Data      | SSL/TLS, JPEG, GIF         |
| 5     | Session      | Data      | NetBIOS, RPC               |
| 4     | Transport    | Segments  | TCP, UDP                   |
| 3     | Network      | Packets   | IP, ICMP, Routers          |
| 2     | Data Link    | Frames    | Ethernet, ARP, Switches    |
| 1     | Physical     | Bits      | Cables, Hubs, WiFi signals |
|       |              |           |                            |

### The Troubleshooting Flow

- ​**Is the cable plugged in?** (Layer 1)
- ​**Can I see the MAC address of my gateway?** (Layer 2 - ARP)
- ​**Can I ping the target IP?** (Layer 3 - ICMP/IP)
- ​**Is the service port open?** (Layer 4 - TCP/UDP)
- ​**Is the website loading?** (Layer 7 - HTTP/Application)

