<h1>Azure Sentinel Live Cyber Attacks Home Lab</h1>


<h2>Description</h2>
In this lab I configured Azure Sentinel SIEM and linked it to a running virtual machine that was set up as a honey pot. By doing so, I was able to monitor RDP Brute Force attacks from various locations worldwide. Additionally, I have used a customized PowerShell script that retrieves geolocation details of the attackers and displays them on the Azure Sentinel Map.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell: Extract RDP failed logon logs from Windows Event Viewer</b> 
- <b>ipgeolocation.io: IP Address to Geolocation API</b> 


<h2>Environments Used </h2>

- <b>Windows 10</b>
- <b>Azure</b>
- <b>Remote Desktop Connection</b>

<h2>Program walk-through:</h2>
***To start this Lab you need to create Azure subscription(It's free, you get $200 worth of free credits by signing up OR use your student account)***

<p align="center">
Create a VM: this VM is going to play the role of a Honeypot that will be exposed to the internet to see the process of attackers trying to gain access to the VM <br/>
<img src="https://i.imgur.com/tnZFnRF.png" height="80%" width="80%" alt=""/>
<br />
<br />
Click on the Create button: <br/>
<img src="https://i.imgur.com/tnZFnRF.png" height="80%" width="80%" alt=""/>
<br />
<br />
Create a New Resource Group: To have everything we're going to use for this lab in the same lifespan: <br/>
<img src="https://i.imgur.com/ynBscZY.png" height="80%" width="80%" alt=""/>
<br />
<br />
Configure your settings as follow: Create your Adminstrator account with something that you can remember! we'll be using it to login to the VM later. Then, click Next:Disks> Next>Networking  <br/>
<img src="https://i.imgur.com/CAqCmXi.png" height="80%" width="80%" alt=""/>
<br />
<br />
On the NIC network security group, click on Advanced. Next, on the Configure Network group click Create New: <br/>
<img src="https://i.imgur.com/h7NKkVC.png" height="80%" width="80%" alt=""/>
<br />
<br />
Remove the existing firewall by clicking on the three dots then click remove. Click on the + Add an inbound rule and configure it as follow then Click Add (by doing this step it's going to allow attackers to try to gain access to the VM): <br/>
<img src="https://i.imgur.com/N9B5cU4.png" height="80%" width="80%" alt="description"/>
<br />
<br />
tittle: <br/>
<img src="image source" height="80%" width="80%" alt="description"/>
<br />
<br />
tittle: <br/>
<img src="image source" height="80%" width="80%" alt="description"/>
<br />
<br />
tittle: <br/>
<img src="image source" height="80%" width="80%" alt="description"/>
<br />
<br />
tittle: <br/>
<img src="image source" height="80%" width="80%" alt="description"/>
<br />
<br />tittle: <br/>
<img src="image source" height="80%" width="80%" alt="description"/>
<br />
<br />
tittle: <br/>
<img src="image source" height="80%" width="80%" alt="description"/>
<br />
<br />

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
