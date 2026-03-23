## My WHOIS & OSINT Discoveries

> **Definition:** **WHOIS** (pronounced "Who Is") is the "Title Deed" of the internet. I use it to find out who owns a domain, when it was registered, and how to contact the registrar.

####  My Workflow:

- I run `whois [domain]` in my terminal to pull the registration data.
    
- If a domain is malicious, I look for the **Registrar Abuse Contact Email** to report it.
    
- **Red Flag Check:** I always check the `Creation Date`. If a "Bank" domain was created 2 days ago, I know it is a Phishing attempt.
    

####  Key Data Points I Look For:

1. **Registrar:** The "Landlord" (e.g., GoDaddy, NameCheap).
    
2. **Registrant:** The "Owner." (Often hidden by "Privacy Protection").
    
3. **Name Servers:** The DNS servers that have authority over the domain's records.
    

---

##  My DNS (Domain Name System) Guide

> **My Rule:** DNS is the phonebook. It maps the names I type to the IP addresses the computer needs.

- **My Layer:** 7 (Application).
    
- **My Ports:** 53 (UDP for speed, TCP for large zone transfers).
    

####  The "Big 4" Records I Must Know:

- **A Record:** Maps a name to an **IPv4** address.
    
- **AAAA Record:** Maps a name to an **IPv6** address (Quad-A).
    
- **CNAME Record:** An alias. I use this to point one domain name to another.
    
- **MX Record:** Directs **Mail** to the correct server.
    

####  My Tools:

- I use `nslookup [domain]` to find IP addresses.
    
- I use `nslookup -type=mx [domain]` to find where a company's email is hosted.
    

---

##  My "Battle Scars" & Lab Tips

- **The "User" Trap:** I learned that tutorials use `user@TryHackMe` as a placeholder. On my actual AttackBox, I am `ubuntu`. I don't let the name change trip me up anymore.
    
- **The Identity Switch:** If I am `root` (#) and need to be a normal user ($), I run `su - ubuntu`. Since I am already root, I don't need a password to "drop down."
    
- **Absolute Paths:** I remember that if a script tells me a filename exists, I usually need to add the full path (like `/var/log/`) to open it with `cat`.