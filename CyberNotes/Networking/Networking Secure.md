> ## TLS: The Guardian of Integrity
> 
> - **Goal 1: Confidentiality** - No one can _read_ the data (Encryption).
>     
> - **Goal 2: Integrity** - No one can _change_ the data (Hashing).
>     
> - **The evolution:** We moved from SSL (Old/Broken) to TLS 1.2/1.3 (Modern/Strong).
>     
> 
> ####  The "Self-Signed" Red Flag:
> 
> In a lab, we use self-signed certs to save money. In the real world, a self-signed cert is a **Huge Risk** because an attacker could be pretending to be the server (Man-in-the-Middle), and there's no "Official Authority" to prove otherwise.
> 
> ####  Tools to watch:
> 
> - **Let's Encrypt:** The hero of the modern web (Free, automated certificates).


# **The Great Encryption Upgrade**:

| **Naked Protocol** | **Secure Version**     | **What the "S" adds**                              |
| ------------------ | ---------------------- | -------------------------------------------------- |
| **HTTP**           | **HTTPS**              | Web traffic is private.                            |
| **DNS**            | **DoT** (DNS over TLS) | No one can see which websites you visit.           |
| **MQTT**           | **MQTTS**              | IoT devices (like smart home sensors) are secured. |

The secure versions, i.e., over TLS, use the following TCP port numbers by default:

|Protocol|Default Port Number|
|---|---|
|HTTPS|443|
|SMTPS|465 and 587|
|POP3S|995|
|IMAPS|993|

TLS can be added to many other protocols; the reasoning and advantages would be similar.
## HTTPS: The Security Researcher's View

- **The Goal:** To ensure the "Tunnel" is unbreakable.
    
- **Key Vulnerability: SSL Stripping.** An attacker intercepts the initial request and forces the victim to stay on HTTP (Port 80) while the attacker talks to the server on HTTPS (Port 443).
    
- **The Fix:** **HSTS (HTTP Strict Transport Security).** A header that tells the browser: "Only EVER talk to me over HTTPS. If the cert is bad, block the user!"
    

####  What I look for in Wireshark:

- **The SNI (Server Name Indication):** Even in encrypted traffic, the domain name is leaked in the `Client Hello` packet. I use this to map out a target's infrastructure.
    
- **TLS Version:** Anything below **TLS 1.2** is a security risk.
