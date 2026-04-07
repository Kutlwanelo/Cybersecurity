EDR solutions extend beyond traditional antivirus by continuously monitoring endpoint activity and detecting suspicious behavior, not just known malware signatures. For example, if a Word document executes a macro that spawns PowerShell, which then downloads a payload, EDR can detect this unusual parent-child process relationship and flag it as suspicious, even if the initial file was not recognized as malicious.

### EDR Scenario
### Step 1: Initial Access

- User opens phishing email
- Downloads Word document

 Nothing obviously malicious yet

###  Step 2: Execution
- Macro runs
Suspicious:
- Office apps executing macros is a common attack vector

###  Step 3: Process Spawn
- `winword.exe` → `powershell.exe`
 BIG RED FLAG
Why?
- Word should NOT normally spawn PowerShell

###  Step 4: Command Execution
- Obfuscated PowerShell runs
 Another red flag:
- Obfuscation = attacker trying to hide intent
###  Step 5: Network Activity
- PowerShell downloads payload
 Now we’re in confirmed malicious territory
#  What EDR Is REALLY Doing Here
It’s not just “logging everything”
 It’s building a **story of behavior over time**
 EDR is like:
> “I don’t just see one action—I see a chain of suspicious actions”

### Process of investigating EDR Telemetry
### Step 1: Confirm the Activity
- PowerShell downloaded a file
### Step 2: Check the Source
- What IP/domain?
- Is it known malicious?
- Is it internal or external?
### Step 3: Add Context (This Is What You’re Missing Slightly)
Ask:
- Has this IP been seen before in the environment?
- Did other machines connect to it?
- Is it flagged in threat intel?
### Step 4: THEN Map to MITRE
- “This aligns with **Command and Control** or **Ingress Tool Transfer**”
 MITRE is for **classification**, not first investigation step

### Examples of IOCs
### Network IOCs
- Malicious IP address
- Suspicious domain
- Unusual outbound traffic
Example:
> PowerShell connects to `185.x.x.x`

### File IOCs
- File hash (MD5, SHA256)
- Suspicious file names
- Unexpected file locations
 Example:
> `invoice.exe` in Downloads
### Host / Endpoint IOCs
- Strange processes
- Unusual parent-child relationships
- Registry changes
Example:
> `winword.exe → powershell.exe`
### User Behavior IOCs
- Multiple failed logins
- Login from unusual location
- Access at odd hours
 Example:
> User logs in from SA, then Russia 5 mins later
