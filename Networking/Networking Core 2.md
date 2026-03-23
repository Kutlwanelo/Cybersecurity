
## My SMTP Command Glossary

I'm adding these to my notes so I can "speak" Mail Server:

| **Command**           | **What it means in "Human"**     | **My Action**          |
| --------------------- | -------------------------------- | ---------------------- |
| **HELO / EHLO**       | "Hi, I'm a client."              | Start the session.     |
| **MAIL FROM**         | "This is who is sending it."     | Specify the sender.    |
| **RCPT TO**           | "This is who should get it."     | Specify the recipient. |
| **DATA**              | "Here comes the actual message." | Start typing the body. |
| **.** (on a new line) | "I'm done writing."              | Sends the email.       |
| **QUIT**              | "Goodbye."                       | Closes the connection. |

## My SMTP Protocol Guide

- **Layer:** 7 (Application)
    
- **Default Port:** 25 (Standard/Unencrypted)
    
- **Submission Ports:** 465 or 587 (Modern/Secure versions).
    

#### 🛡️ My Discovery:

I can use `telnet [IP] 25` to manually send an email. This is a great way to test if a Mail Server is "Open," meaning it lets anyone send mail through it. (Bad for spam!)

#### ⚠️ My Security Warning:

Standard SMTP is "Clear-Text." If I use Wireshark on port 25, I can read the entire body of the email as it flies across the network.

- **My Alternative:** I should look for **SMTPS** or **STARTTLS** to make sure the "Envelope" is encrypted.

> # **My SMTP Practical Lessons** 
> 
> - **The Sequence:** `HELO` -> `MAIL FROM` -> `RCPT TO` -> `DATA` -> `.` -> `QUIT`.
>     
> - **My "Invisible" Header:** I noticed that if I don't type `Subject: My Subject` inside the `DATA` section, the email arrives with no subject line. The protocol doesn't "force" me to have one, but a real inbox would flag it as spam.
>     
> - **The Port 25 Reality:** I am using Port 25 because this is a lab. In my future career, I’ll likely see **Port 587** for modern, encrypted mail submission.
>     

---

## 🇿🇦 Fun Fact for my Interview

If I ever have to explain **Email Spoofing**, I can now say:

> _"I’ve manually sent emails via Telnet on Port 25. I saw firsthand that the protocol trusts whatever I type in the `MAIL FROM` field. This is why we need security layers like **SPF, DKIM, and DMARC** to verify that the sender is actually who they claim to be."

