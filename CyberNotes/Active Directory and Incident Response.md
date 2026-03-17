
## 1. Active Directory Architecture (Scaling the Network)

|**Term**|**Definition**|**Key Characteristic**|
|---|---|---|
|**Domain**|A logical group of users, computers, and resources.|Managed by a **Domain Controller (DC)**.|
|**Tree**|A collection of domains that share a **contiguous namespace**.|Example: `thm.local` -> `uk.thm.local`.|
|**Forest**|The highest level of AD grouping; a collection of Trees.|Can have different namespaces (e.g., `thm.local` & `mht.local`).|

## 🔑 Key Security Groups

- **Domain Admins:** Full control over a **single domain**. The "prize" for a local breach.
    
- **Enterprise Admins:** Full control over the **entire Forest**. The "ultimate prize" for an attacker.
    

## 🌉 Trust Relationships

- **Direction Rule:** Trust direction is **opposite** to the access direction.
    
    - If A trusts B, users in B can access resources in A.
        
- **Transitive Trust:** By default, joining a Tree or Forest creates a **Two-Way Transitive Trust** (everyone can talk to everyone).
    
- **Authorization:** A trust only opens the "door"; an admin must still grant specific permissions to files/folders.
    

---

## 2. Incident Response Frameworks (The Playbook)

## SANS Framework: **PICERL**

1. **Preparation:** Building the team, tools (SIEM/EDR), and training _before_ an attack.
    
2. **Identification:** Detecting abnormal behavior (e.g., `.locked` extensions, high CPU, suspicious logins).
    
3. **Containment:** "Stopping the bleeding." Using **Network Segmentation** or isolation to prevent lateral movement.
    
4. **Eradication:** Removing the root cause. Deleting malware binaries/backdoors (but **not** the encrypted data if backups are missing!).
    
5. **Recovery:** Restoring from clean backups, patching the original hole, and returning to "Business as Usual."
    
6. **Lessons Learned:** Post-incident report. Identifying gaps in defense to improve the next **Preparation** phase.
    

## NIST Framework (4 Phases)

- **Preparation**
    
- **Detection & Analysis** (Combines SANS Identification)
    
- **Containment, Eradication, & Recovery** (Lumped together)
    
- **Post-Incident Activity** (Lessons Learned)
    

---

## 📝 The Incident Response Plan (IRP)

A formal document approved by management that defines:

- **Roles:** Who does what?
    
- **Communication:** Who do we call (Internal vs. External/Legal)?
    
- **Escalation:** When do we involve senior leadership?