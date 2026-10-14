<h2>Description</h2>
A walk through on how to classify and triage alerts, write comments and reports on the alerts, close false positives and escalate real threats.

<br />
<br />

<p align="center">
Potential Data Exfiltration</b>: <br/>
<img src="https://i.imgur.com/QH8bGWT.png" height="80%" width="80%"/>
<br />
<br />
Verdict: False positive <br/>
<img src="https://i.imgur.com/ni63Sep.png" height="80%" width="80%"/>
<br />
<br />
Double-Extension File Creation:  <br/>
<img src="https://i.imgur.com/HGG2Qxm.png" height="80%" width="80%"/>
<br />
<br />
Run the file hash against VirusTotal: <br/>
<img src="https://i.imgur.com/sDfyOjQ.png" height="80%" width="80%"/>
<br />
<br />
Verdict True positive:  <br/>
<img src="https://i.imgur.com/4ZEf8fA.png" height="80%" width="80%"/>
<br />
Escalate -- This needs immediate action: Isolate host LPT-HR-009 from the network. Determine if S.Conway executed the file or just downloaded it. Check for any lateral movement from host LPT-HR-009. Check for C2 callbacks. 
MD5:14d8486f3f63875ef93cfd240c5dc10b <br/>
Host: LPT-HR-009 / User: S.Conway.

Suspicious Double-extension executable disguised an mp4 file downloaded via Chrome from suspicious ".monster" domain. Isolation and IR should follow.
<br />
<br />
<p align="center">
Download from Github Repository:  <br/>
<img src="https://i.imgur.com/XYsFbS7.png" height="80%" width="80%"/>
<br />
Verdict: False Positive: https://github.com/facebook/react is the official <b>React Javascript library</b> -- maintained by <b>Meta</b>. It is one of the most widely used open-source frameworks in the world. legitimate developer activity.
<br />
<br />
<br />

<h3>What we have learned so far.</h3>
<b>1. Context is everything</b> <br/>
The same "large data transfer" alert was <b>Critical</b>, but in the end it was a <b>False Positive</b>. This tells us that alert <b>severity</b> has no bearing on the <b>verdict</b>. This is to say that we are more concerned about the impact <b>if</b> the <b>critical</b> alert be real than being wrong that it is not. Severity dictates how urgently to investigate, not the outcome. The cost of being <b>wrong</b> and <b>late</b> is what compels us. Severity drives investigation, evidence drives the verdict. <br />
<br />
<b>2. Attackers use Social Engineering</b> <br/>
The cats2025.mp4.exe case shows us how crafty attackers can be in trying to break defences. They can disguise malware as something as harmless as cat videos. They can use double extensions to hide the executable. They might target high-value, but non-technical staff who may be less security-aware, which highlights the importance of employee security education. <br/>
<br />
<b>3. External tools can are important</b> <br/>
VirusTotal turned a <b>suspected</b> True Positive into a <b>confirmed</b> one.

<br />
<br />
<p align="center">
Email marked as phishing after delivery:  <br/>
<img src="https://i.imgur.com/Qt4DQbi.png" height="80%" width="80%"/>
<br />
<br />
Phishing email alert report:  <br/>
<img src="https://i.imgur.com/LeZRnOS.png" height="80%" width="80%"/>
<br />

<b>WHO?</b> <br />
<ul>
  <li><b>Sender:</b> Claims to be <b>Microsoft support</b> <support@microsoft.com>, but this is clearly spoofed </li>
  <li><b> Recipient:</b> Eddie Huffman, IT Manager, a high-value target with elevated privileges</li>
</ul>
<b>WHAT?</b> <br />
<ul>
  <li>A spoofed email with a <b>REPORT.rar</b> attachment</li> 
  <li>Body uses classic urgency tactic: <i>"600% price increase, urgent notice , download report"</i></li>
  <li>.rar files can contain malicious executables, similar to .exe files</li>
</ul>
<b>WHEN?</b> <br />
<ul>
  <li>March 27 2025 at 19:25 -- Outside business hours, a common period attackers exploit when oversight is lower. </li>
</ul>
<b>WHERE?</b> <br />
<ul>
  <li> Delivered directly to e.huffman@tryhackme.thm inbox before being flagged</li>
</ul>
<b>WHY?</b> <br/>
<ul>
  <li><b>Spear Phishing:</b> targeting IT manager to gain privileged access</li>
  <li>Urgency manufactured around fake Microsoft Teams enormous price hike to pressure a quick and unconsidered response </li>
</ul>

<br />
<br />
<p align="center">
Spike of domain descovery commands:  <br/>
<img src="https://i.imgur.com/XA8TZkX.png" height="80%" width="80%"/>
<br />
<br />
Alert report: <br/>
<img src="https://i.imgur.com/GZzhBRX.png" height="80%" width="80%"/>
<br />

<b>WHO?</b> <br/>
<ul>
  <li><b>User:</b> NT AUTHORITY\SYSTEM -- the highest privilege account on Windows, meaning the attacker likely already has full control of this machine</li>
  <li><b>Host:</b> DMZ-MSEXCHANGE-20213 -- a small mail server sitting in the DMZ, extremely high value target</li>
</ul>
<b>WHAT?</b> <br />
<ul>
  <li>Commands run: "dir", "hostname", "whomai / priv", "net group 'Domain Admins'", "nltest" /dclist:tryhackme.twhm"</li>
  <li>Parent Process: C:\Users\Public\revshell.exe -- this is a reverse shell, the attacker gains remote access </li>
  <li>Grandparent Process: w3wp.exe -- IIS web worker process suggesting the mail server was cpmpromised via a web exploit</li>
</ul>
<b>WHEN?</b> <br />
<ul>
  <li>March 27, 2025 at 19:56 -- 31 minutes after the phishing email alert (19:25)</li>
</ul>
<b>WHERE?</b> <br />
<ul>
  <li>DMZ-MSEXHANGE-2013 -- a DMZ mail server running <b>Windows Server 2012 R2 </b>(outdated and unpatched OS)</li>
</ul>
<b>WHY?</b> <br />
<ul>
  <li>Attacker is performing domain discovery to find Domain Admins and DCs -- <b>pre-lateral movement reconnaissance</b></li>
  </ul>
  
<br />
<br />
<h3>What we have learned:</h3>
<b>1. Alerts don't exist in isolation</b> <br />
The phishing email (19:25) and domain discovery commands (19:56) 31 minutes apart on the same day. <br />
<br/>
<b>2. High value targets get targeted differently</b> <br />
<ul>
  <li>The phishing email went to the IT Manager (privileged access)</li>
  <li>The compromised host was a DMZ mail server (internet-facing and high value)</li>
  Attackers deliberately target assets that give them the most leverage.
</ul>

<b>3. Legacy systems are vulnerable to attacks </b> <br />
Outdated systems are basically open doors for attackers. <br />
<br />
<b>4. Email Authentication failures are hard evidence</b> <br />
SPF/Fail + DKIM/Fail is not just suspicious, it is proof that the email could not be from Microsoft. <br />




</p>

