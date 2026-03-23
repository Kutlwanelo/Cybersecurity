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

## My HTTP Mastery Guide

- **Layer:** 7 (Application)
    
- **Default Ports:** 80 (HTTP - Unencrypted) / 443 (HTTPS - Secure)
    
- **Alternative Ports:** 8080, 8443 (Often used for dev/testing servers).
    

#### 🛡️ My Security Checklist:

1. **Information Leakage:** Does the `Server` header reveal a version number I can exploit?
    
2. **Insecure Methods:** Does the server allow `PUT` or `DELETE` to anonymous users?
    
3. **HTTPS Transition:** Does the site force me from port 80 to port 443?
    

#### 💻 My Practical Tools:

- `telnet [IP] [Port]` - To manually "type" HTTP.
    
- `curl -v [URL]` - The modern way to see headers and data at once.

## My Manual HTTP Request (via Telnet)

- **Step 1:** `telnet 10.10.10.10 80`
    
- **Step 2:** Type `GET /index.html HTTP/1.1` (This tells the server _which_ file I want).
    
- **Step 3:** Type `Host: 10.10.10.10` (Modern servers require this to know which website they are serving).
    
- **Step 4:** **Press Enter Twice.**
    

# Obsidian "Web Tools" Note

**Why I do this:** It allows me to see the **Raw Headers** (Server version, Cookies, Date) that a browser usually hides from me.## My `curl` Cheat Sheet

- **The Goal:** To interact with web servers without a browser.
    
- **Basic Command:** `curl [URL]`
    
- **The "Detective" Command:** `curl -v [URL]` (Shows me the headers and the handshake).
    
- **The "Header-Only" Command:** `curl -I [URL]` (Great for quick version checking).

# (File Transfer Protocol THM Room)

I'll make sure to note the "ASCII vs. Binary" trap I saw in the terminal warning.

> ##  FTP (File Transfer Protocol)
> 
> - **My Layer:** 7 (Application)
>     
> - **My Port:** 21 (Control)
>     
> - **My Security Warning:** FTP is **unencrypted**. Anyone sniffing the network with Wireshark can see my password and the files I download.
>     
> 
> ####  My FTP Workflow:
> 
> 1. `ftp [IP]` - Start the connection.
>     
> 2. **Login:** I try `anonymous` first to see if the server is misconfigured.
>     
> 3. **Mode Check:** > * I use `type ascii` for text files (`.txt`, `.html`).
>     
>     - I use `type binary` for images, zip files, or executables.
>         
>     - _Note:_ If I get the "Linefeeds" warning I saw in THM, I probably used the wrong mode!
>         
> 4. **Download:** `get [filename]`
>     
> 
> ####  My Secure Alternative:
> 
> In a real job, I should use **SFTP** (SSH File Transfer Protocol) because it encrypts the entire conversation.

---

## Interview "Pro" Tip

If an interviewer asks: _"What is the risk of using standard FTP?"_ **My Answer:** _"The biggest risk is that it's a clear-text protocol. Using a tool like Wireshark, an attacker can capture the `USER` and `PASS` commands. I would always recommend migrating to SFTP or FTPS to ensure the credentials and data are encrypted in transit."


