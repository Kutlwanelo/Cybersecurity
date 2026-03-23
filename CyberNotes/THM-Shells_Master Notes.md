
#  Shells & System Analysis: Master Notes

## 1.  PowerShell File Navigation

- **The "Path Not Found" Fix:** If a file exists but the CLI can't find it, use quotes or check the extension.
    
    - `Get-Content "big-treasure.txt"` (Always use quotes for spaces/special chars).
        
    - `Get-ChildItem -Force` (To see hidden pirate files).
        
- **The "Search Party" Command:** If you know a file exists but don't know where:
    
    - `Get-ChildItem -Path C:\ -Filter "filename.txt" -Recurse -ErrorAction SilentlyContinue`
        

## 2.  Real-Time System Analysis (Blue Team)

|**Command**|**Purpose**|**Security Insight**|
|---|---|---|
|`Get-Process`|Lists running programs.|Look for high CPU or weird names like `nc.exe`.|
|`Get-Service`|Lists background services.|Check for `Stopped` vs `Running` critical services.|
|`Get-NetTCPConnection`|Shows network activity.|Identify `Established` connections to unknown IPs.|
|`Get-FileHash`|Generates a digital fingerprint.|Use `-Algorithm SHA256` to verify file integrity.|

- **Pro-Tip:** Use `| Format-List` (or `| fl`) to see the **Full Hash** if it gets cut off in the table view.
    
- **The Link:** The `OwningProcess` property in `Get-NetTCPConnection` tells you which PID started the network connection.
    

## 3.  Remote Management (`Invoke-Command`)

- **Usage:** Running commands on remote servers without leaving your desk.
    
- **Syntax:** `Invoke-Command -ComputerName "Server01" -ScriptBlock { Get-Service }`
    
- **Why it matters:** Essential for **Incident Response** to scan 100+ machines for a threat simultaneously.
    

## 4.  Linux Shell Fundamentals (Bash)

- **The "Big Four" vs PowerShell:**
    
    - `pwd` = `Get-Location` (Where am I?)
        
    - `ls` = `Get-ChildItem` (What's here?)
        
    - `cat` = `Get-Content` (Read this.)
        
    - `grep` = `Select-String` (Find this text pattern.)
        
- **Piping:** `ls | grep "flag"` (Taking the output of one and filtering it with the next).
    

## Shell Comparison Table

|**Feature**|**Bash (Linux)**|**PowerShell (Windows)**|
|---|---|---|
|**Data Type**|Plain Text (Thin/Fast)|**Objects** (Heavy/Data-Rich)|
|**Piping**|Passes Text strings|Passes Data Objects|
|**Default**|Standard on 90% of Linux|Standard on modern Windows|

## Restricted Shells (`rbash`)

- **The "r" stands for Restricted.**
    
- Limits the user: No `cd`, no changing `$PATH`, no redirection.
    
- **Security Context:** Used to "handcuff" users to a specific area. Attackers look for "Shell Escapes" via allowed binaries like `python` or `vim`.
## Remote Execution (Invoke-Command)

- **Run a single command remotely:** `Invoke-Command -ComputerName "TargetPC" -ScriptBlock { Get-Service | Where-Object Status -eq "Stopped" }`
    
- **Run a local script on a remote PC:** `Invoke-Command -ComputerName "TargetPC" -FilePath "C:\MyScripts\SecurityAudit.ps1"`
    
- **Pro-Tip:** You can provide a list of names `("PC1", "PC2", "PC3")` to run the command on all of them at once!

# Bash Scripting Essentials

- **Extension:** `.sh`
    
- **Header:** `#!/bin/bash`
    
- **Make Executable:** `chmod +x filename.sh`
    
- **Run:** `./filename.sh`
    
- **Variables:** Use `$` to call them (e.g., `$USER`).
    
- **Logic Ends:** `if` ends with `fi`, `do` ends with `done`.