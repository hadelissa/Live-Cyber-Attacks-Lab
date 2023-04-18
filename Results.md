<h1>Failed RDP to IP Geolocation Information</h1>


<h2>Description</h2>
<b>The PowerShell script found in this repository is designed to extract data related to unsuccessful Remote Desktop Protocol (RDP) attempts from the Windows Event Log, and then employ a third-party API to retrieve geographic details concerning the location of the attackers.

</b>
<br />
<br />
In this lab, the script is utilized to configure Azure Sentinel (SIEM) and link it to a functioning virtual machine functioning as a honeypot. The demo involves monitoring ongoing RDP brute force attacks originating from various locations worldwide, and leveraging a customized PowerShell script to retrieve the geolocation data of the attackers and depict it on an Azure Sentinel map.


<br />
<br />

<p align="center">
<img src="https://i.imgur.com/039UO0r.png" height="85%" width="85%" alt="RDP event fail logs to iP Geographic information"/>
</p>
<h2>Languages Used</h2>

- <b>PowerShell:</b> Extract RDP failed logon logs from Windows Event Viewer 

<h2>Utilities Used</h2>

- <b>ipgeolocation.io:</b> IP Address to Geolocation API

<h2>Attacks from severL countries coming in; Custom logs being output with geodata</h2>

<p align="center">
<img src="https://i.imgur.com/DIJkfEx.png" height="85%" width="85%" alt="Image Analysis Dataflow"/>
</p>

<h2>World map of incoming attacks after 24 hours (built custom logs including geodata)</h2>

<p align="center">
 Scan Live attacks</p>
<img src="https://i.imgur.com/tkPtz8b.png" height="85%" width="85%" alt="Image Analysis Dataflow"/>
</p>


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
