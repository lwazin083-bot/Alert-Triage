<h2>Description</h2>
A walk through on how to classify and triage alerts, write comments and reports on the alerts, close false positives and escalate real threats.

<br />
<br />

<p align="center">
Potential Data Exfiltrationt</b>: <br/>
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
<b>2. Attackers use Social Engineering</b> <br/>
The cats2025.mp4.exe case shows us how crafty attackers can be in trying to break defences. They can disguise malware as something as harmless as cat videos. They can use double extensions to hide the executable. They might target high-value, but non-technical staff who may be less security-aware, which highlights the importance of employee security education. <br/>
<b>3. External tools can are important</b> <br/>
VirusTotal turned a <b>suspected</b> True Positive into a <b>confirmed</b> one.

<br />
<br />
<p align="center">
Creating Backdoor Accounts:  <br/>
<img src="https://i.imgur.com/2HqNoCb.png" height="80%" width="80%"/>
<br />
<br />
Role Assignments:  <br/>
<img src="https://i.imgur.com/qVrjYtn.png" height="80%" width="80%"/>
<br />
<br />
Adding Alternate MFA Methods:  <br/>
<img src="https://i.imgur.com/6Ld2S6G.png" height="80%" width="80%"/>
<br />
A soon as our attacker, IP 149.120.234.27, bypassed the MFA control, they created an account-"rafael.michael@finegalo.thm". This classic backdoor creation. They want to ensure that they can survive a password reset on "igor.bicalho@finegal.thm". The newly created account was then escalated to the roles of "Global Administrator" and "Tenant Admin". 5 minutes later, "rafael.michael@finegalo.thm" performs MFA seeding, registering their own MFA. This was a tenant compromise: Credential theft --> MFA bypass --> Backdoor account creation --> Global Admin privilege --> MFA seeding --> Persistent access. 
Recommendations: disable both accounts at the centre of the compromise. Revoke all active sessions tenant-wide. Audit all role assignments made after 2026-03-04. Block the new MFA registration. Investigate possible data exiltration.

<br />
<br />

</p>

