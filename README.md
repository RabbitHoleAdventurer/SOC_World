<h2>SOC World </h2>

<h4> This repository includes random nuggets of information to help guide you through SOC Investigations </h4>

<br />

<h2> 📝 What is a SOC?  📝 </h2>
<h5>
A Security Operations Center (SOC) is a team within an organization that is responsible for monitoring and managing security-related issues. The primary goal of a SOC is to detect, analyze, respond, and mitigate cybersecurity threats in real-time. SOC teams use a combination of tools to triage alerts and make informed decisions. 
</h5>

<br /><br />

<h2> 📝What are SID's and why are they important 📝</h2>
A security identifier is a unique alphanumeric identifier for a security principal or security group.
A security principal can be anything from a user account, a computer account, or a thread or process that runs in the security context of a user/computer account.

Every user, group, or task on a computer gets a special ID, called a SID. This SID is generated by an authority system such as a Domain Controller.
The computer keeps a list of these IDs to make sure everything is safe and secure.

Each time a user signs in, the system creates an access token for that user. The access token contains the user's SID, user rights, and the SIDs for any groups the user belongs to.

There are some SID's that identify generic groups and users. A few examples are the Everyone group and the SYSTEM user.

Everyone Group: S-1-1-0

SYSTEM: S-1-5-18

<br /><br />
The components of a SID are easier to visualize when SIDs are converted from a binary to a string format by using standard notation:

***S-R-X-Y1-Y2-Yn-1-Yn***
<br /><br />

Example: S-1-5-21-1574559362-3190734025-665073282-100269

SID Breakdown:

A revision level (1)

An identifier authority (5, NT Authority)

A domain identifier (21-1574559362-3190734025-665073282, Domain)

A relative identifier (100269)

<br /><br />
For more info: https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-identifiers


<br /><br />


<h2> 📝 Processes and Process Trees 📝</h2>
Processes on a computer show us what programs and binaries are running which helps us understand if there are nefarious things happening in our systems. 
<br /><br />
Process trees allow us to further add context into the commands that we observe running on the systems we analyze.
<br /><br />
With the relationship context, this allow us to make better informed decisions on what action to take during our investigations.
<br /><br />
There are times when a command looks suspicious but understanding the parent or grandparent relationship helps us know if this command should be running on our system or if it needs to be stopped and investigated.
<br /><br />
It is also much easier to find malicious activity by using process trees as when malicious activity is identified, we can look at the parent process and see what else spawned from that same parent. Allowing us to find other malicious activity quickly.
<br /><br />
<br /><br />


<h3> 📝 Linux Process Analysis 📝</h3>
Everything in Linux is a file, this allow us to investigate things running in memory
<br /><br />
Processes in memory can be queried from /etc/proc

<br /><br />
Another way of triaging processes running in memory is through the use of the lsof command
<br /><br />
This binary allows us to list open files. There are a few flags here to quickly triage suspicious or malicious activity on a Linux host
<br /><br />
Listing processes that have open internet connections can be done with the -i flag
```Shell
lsof -i 
```


List process information, this can be done with the -P flag (this flag allows us to skip the port number)
<br /><br />
We now have 
```Shell
lsof -i -P
```
 

<br /><br />
Equipped with the process ID, we can now run 
```Shell
lsof -p [PID OF INTEREST] 
```
where more information can be obtained about the process including:
<br /><br />
cwd: Current Working Directory
<br /><br />
txt: Usually used to figure out what binary is running
<br /><br />
mem: Libraries associated with the binary
<br /><br />


<h2> 📝 Common Areas of Persistence 📝</h2>


<h3>Windows</h3>

<h4>Services</h4>
<h4>Scheduled Tasks</h4>
<h4>Registry Keys</h4>
<h4>Startup Items</h4>





<br /><br />
<h3>Linux</h3>
<h4>Cron Jobs</h4>
<h4>Systemd Units</h4>
<h4>Startup Items</h4>
<h4>SSH Keys</h4>

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
The Domain Name System (DNS) serves as the Internet's contact list. When individuals browse the web, they use domain names such as google.com or amazon.com. However, web browsers communicate using Internet Protocol (IP) addresses. Yes, browsers use the IP protocol, the set of numbers that humans would never care to remember (x.x.x.x). DNS bridges this gap by translating domain names into IP addresses, enabling browsers to access online resources. Beyond facilitating web browsing, DNS is crucial for various network software, including malware, as it resolves domains to IP addresses before establishing connections over protocols like HTTP(S) and SMTP, among other protocols. As a result, DNS logging provides a comprehensive record of domain accessed by endpoints in the network environment, extending beyond just HTTP(S) traffic. This makes DNS logs a valuable resource for defenders seeking insights into network activity.
<br /><br />

Key things to look for on DNS logs:
<br /><br />
Top Level Domains not widely used in the organization
<br /><br />
Inbound and Outbound requests for top level domains for countries outside of where an organization does business
<br /><br />
Domains with short TTLs as these domains may be being used by attackers that are associating multiple IP addresses with one domain (DNS fast flux)
<br /><br />
Newly registered domains

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
> [!NOTE]
> -Algorithm
> > Specifies the cryptographic hash function to use for computing the hash value of the contents of the specified file or stream. The acceptable values for this parameter are: SHA1, SHA256, SHA384, SHA512, MD5

<br /><br />

<h4>Linux</h4>

```Shell
LINUX COMMAND
```

<br />

<h4>MacOS</h4>

```zsh
shasum -a 256 [FILE]
```

> [!NOTE]
> Algorithms available to be used with the shasum command: 1 (default), 224, 256, 384, 512



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
<h2>📝 Tools 📝</h2>
Splunk - Platform used for searching, monitoring, and analyzing logs and events and used to provide operational intelligence
<br /><br />
Volatility - Open-source memory forensics framework which helps obtain running processes, open network sockets, injected code and more from memory images
<br /><br />
Cyberchef - Provides a set of tools for analyzing and decoding data. It's commonly used for tasks like converting data formats, encryption/decryption, compression/decompression, and more
<br /><br />
VirusTotal - A service that analyzes suspicious files and URLs to detect malware and provide insights into potential threats by scanning them with multiple antivirus engines
<br /><br />
AbuseIPDB - A database that collects and shares information about IP addresses that have been reported for malicious activity, such as hacking attempts, spamming, and other cyber threats. Provides a confidence of abuse score for each IP provided.
<br /><br />
ANY.RUN - Interactive malware analysis tool that allows users to execute malware samples in a controlled environment and observe their behavior
<br /><br />
Urlscan.io - A service that analyzes and scans websites for malicious content, phishing attempts, and other suspicious activities by examining their structure, behavior, and reputation. Also provides a view of the site without having to visit it yourself and any redirects that site may make.
<br /><br />
Osquery - Open-source operating system instrumentation framework for Windows, OS X (macOS), and Linux. It exposes an operating system as a high-performance relational database. This allows an analyst to write SQL queries to explore operating system data and query things such as running processes, loaded kernel modules, open network connections, browser plugins, hardware events or file hashes.
<br /><br />
Velociraptor - An endpoint visibility and digital forensics tool designed for incident response, threat hunting, and monitoring. It enables querying and monitoring endpoints at scale.
<br /><br />
DB Browser for SQLite - A visual tool for creating, designing, and managing SQLite databases. It allows users to execute SQL queries, browse data, and manage database files. Can be used to analyze Browser History for most main browsers. 
<br /><br />
MITRE ATT&CK Framework - A knowledge base maintained by MITRE Corporation that describes adversary tactics, techniques, and procedures (TTPs) based on real-world observations. It's widely used in cybersecurity for threat intelligence, detection, and mitigation strategies.
<br /><br />
Atomic Red Team - A framework for testing detection capabilities and validating security controls by emulating adversary behaviors. These tests are mapped to the MITRE ATT&CK Framework.

<br /><br />
<br /><br />
