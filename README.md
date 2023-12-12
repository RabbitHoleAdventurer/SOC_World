<h2>SOC World </h2>

<h4> This repository includes random nuggets of information to help guide you through SOC Investigations </h4>

<br />

<h2> 📝 What is a SOC?  📝 </h2>
<h5>
A Security Operations Center (SOC) is a team within an organization that is responsible for monitoring and managing security-related issues. The primary goal of a SOC is to detect, analyze, respond, and mitigate cybersecurity threats in real-time. SOC teams use a combination of tools to triage alerts and make informed decisions. 
</h5>

<br /><br />

<h2> 📝What are SID's and why are they important 📝</h2>


<br /><br />


<h2> 📝 Processes and Process Trees 📝</h2>

<br /><br />


<h3> 📝 Linux Process Analysis 📝</h3>

LSOF Commands

<br /><br />


<h2> 📝 Common Areas of Persistence 📝</h2>


<h3>Windows</h3>

<h4>Services</h4>
<h4>Scheduled Tasks</h4>
<h4>Registry Keys</h4>
<h4>Startup Items</h4>





<br /><br />
<h3>Linux</h3>

<br /><br />
<h3>MacOS</h3>

<h4>Launch Daemon and Launch Agents</h4>



Launch Agents/Daemons are often installed to perform updates to programs, launch user specified programs at login, or to conduct other developer tasks.

Launch Agents/Daemons behavior is stored in a plist file used to interact with Launchd (the service management framework) used by macOS.

Launch Daemons require elevated privileges to install, are executed for every user on a system prior to login and run in the background without the need for user interaction.



 <br />

<h4>Required Launch Daemons parameters include</h4>


  Label to identify the task

  Path to the executable

  RunAtLoad to specify when the task is run (set to true to run at Startup)

 
<br />


Biggest difference between launch daemons and launch agents are that:
Daemons execute tasks at the system-level

Agents execute tasks within the context of the user’s interactive session


<br /><br />








<h2> 📝 DNS Logs 📝</h2>

<br /><br />



<h2>📝 MacOS 📝</h2>
<h3>MacOS Best Practices</h3>

Enabling Gatekeeper, Configuring System Integrity Protection (SIP), Enabling Auto Update, Disabling Screen Sharing


<br />
<h4>Enabling Gatekeeper</h4>


This feature protects the machine from launching unknowingly malicious applications.

This is done by enforcing code signing and limiting the sources that applications can be downloaded from.


<br /><br />


<h4>Configuring System Integrity Protection (SIP)</h4>


This feature provides:

Protection to the entire system by preventing the execution of unauthorized code. 

For example, protection for system files and directories, code injection protection, runtime attachments protection, protection against unsigned kernel extensions.

Reduces the chance of a Mac being subject to malicious runtime attachments.



<br /><br />

<h4> What is a Plist file? Why are they important? </h4>


Plist stands for property list 

Used to store application preferences, in essence this is the configuration information for an application.

The behavior of a daemon/agent is specified in this property file usually written in XML



<br /><br />





<h2>📝 Rapid Fire Commands 📝</h2>

<h3>Hashes For Files</h3>
<h4>Windows</h4>


```PowerShell
Get-FileHash [FILE] -Algorithm [ALGORITHM] | Format-List
```
-Algorithm

Specifies the cryptographic hash function to use for computing the hash value of the contents of the specified file or stream. The acceptable values for this parameter are:

SHA1

SHA256

SHA384

SHA512

MD5

<br /><br />

<h4>Linux</h4>

```
LINUX COMMAND
```

<br />

<h4>MacOS</h4>

```
shasum -a 256 [FILE]
```

Algorithms available to be used with the shasum command

1 (default)

224

256

384

512


<br />
<h3>Displaying User Info</h3>

<h4>Command Line</h4>

```Batch
net user [USER] /domain
```

<h4>PowerShell</h4>

```PowerShell
Get-ADUser -Identity [USER]
```

```PowerShell
Get-ADUser -Identity [USER] -Properties *
```


<br /><br />
<h3>Disabling Domain User</h3>

<h4>Command Line</h4>

```Batch
net user [USER] /domain /active:no
```

<h4>PowerShell</h4>

```PowerShell
Disable-ADAccount -Identity [USER | Distinguished Name]
```

<br /><br />

<h3>Disabling Local User</h3>

<h4>Command Line</h4>

```Batch
net user [USER] /active:no
```

<br /><br />
<br /><br />
