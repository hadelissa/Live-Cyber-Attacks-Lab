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

<h2>Creating a Virtual Machine on Azure walk-through:</h2>
***To start this Lab you need to create Azure subscription(It's free, you get $200 worth of free credits by signing up OR use your student account)***

<p align="center">
Create a VM: this VM is going to play the role of a Honeypot that will be exposed to the internet to see the process of attackers trying to gain access to the VM as we disable the firewall to make it vulnerable and discoverable on the internet. <br/>
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
Remove the existing firewall by clicking on the three dots then click remove. Click on the + Add an inbound rule and configure it as follow then Click Add (by doing this step it's going to allow attackers to try to gain access to the VM): Once you configure the following settings click OK. <br/>
<img src="https://i.imgur.com/eRvMwtq.png" height="80%" width="80%" alt=""/>
<br />
<br />
 Click Review + Create: Once you review your configuration Click Create. <br/>
<img src="https://i.imgur.com/95DofSd.png" height="80%" width="80%" alt=""/>
<br />
<br />
 
 <h2>Creating Log Analytics workspace walk-through:</h2>
 
 <p align="center">
Now, Let's Create a Log Analytics Workspace: By doing this step we'll be able to create custom log that contains geographic information to discover where the attackers are coming from. <br/>
<img src="https://i.imgur.com/w3GVvTj.png" height="80%" width="80%" alt=""/>
<br />
<br />
Click on Create Log Analytics Workspaces: <br/>
<img src="https://i.imgur.com/FWCKVF7.png" height="80%" width="80%" alt=""/>
<br />
<br />
Configure the setting as follow: Choose the Group source that we have created previously, then Name your workspace. Once you're done click on Review + Create: <br/>
<img src="https://i.imgur.com/rdDMgyn.png" height="80%" width="80%" alt=""/>
<br />
<br />
Review your configuration then click Create: <br/>
<img src="https://i.imgur.com/6bLO9kL.png" height="80%" width="80%" alt=""/>
<br />
<br />
 
 <h2>Microsoft  Defender for  Cloud walk-through:</h2>
 
  <p align="center">
Search Microsoft Defender for the Cloud: To enable the ability to gather logs from the VM into the Log analytics workspace <br/>
<img src="https://i.imgur.com/TzxwwlW.png" height="80%" width="80%" alt=""/>
<br />
<br />
Go to Environment Settings, then choose the workspace that we've created previously: <br/>
<img src="https://i.imgur.com/hz9m1bU.png" height="80%" width="80%" alt=""/>
<br />
<br />
configure the settings as follow: Then click Save. <br/>
<img src="https://i.imgur.com/hm6FZ9p.png" height="80%" width="80%" alt=""/>
<br />
<br />
Click on Data collection and select All Events Then click Save: <br/>
<img src="https://i.imgur.com/Brjfczf.png" height="80%" width="80%" alt=""/>
 
 <h2>Connecting workspace to the VM walk-through:</h2>
  <p align="center">
Go to Logs Analytics Workspaces: <br/>
<img src="https://i.imgur.com/AGNakgg.png" height="80%" width="80%" alt=""/>
<br />
<br />
Click on Virtual Machines select the VM that we have created: <br/>
<img src="https://i.imgur.com/FDAWy61.png" height="80%" width="80%" alt=""/>
<br />
<br />
Click on Connect: <br/>
<img src="https://i.imgur.com/fKHWoe0.png" height="80%" width="80%" alt=""/>

  <h2>Connecting Microsfot Sentinel (SIEM) walk-through:</h2>
 *This is where we're going to use to visualize the attack data*
  <p align="center">
Go to Microsoft Sentinel: <br/>
<img src="https://i.imgur.com/HaGg6BJ.png" height="80%" width="80%" alt=""/>
<br />
<br />
select the VM that we've created previously for this lab: <br/>
<img src="https://i.imgur.com/mYLJIpM.png" height="80%" width="80%" alt=""/>
<br />
<br />
 
<h2>Connecting VM to The Remote Desktop walk-through:</h2> 

  <p align="center">
Go to Virtual Machine then copy the Public IP address:<br />
<img src="https://i.imgur.com/RXEs5ZX.png" height="80%" width="80%" alt=""/> 
<br />
<br />
On your Computer, search for Remote Desktop Connection then paste your Ip address the click connect: <br/>
<img src="https://i.imgur.com/vFZ1y8y.png" height="80%" width="80%" alt=""/>
<br />
<br />
Go to Wf.msc, click on Windows Defender Firewall Properties: <br/>
<img src="https://i.imgur.com/G0DciTe.png" height="80%" width="80%" alt=""/>
<br />
<br />
 on the Domain Profile tab turn off the Firewall State, Click Apply then OK: <br/>
<img src="https://i.imgur.com/7gc3gTp.png" height="80%" width="80%" alt=""/>
<br />
<br />
Try to ping the VM IP address on your Computer to check if echo request are allowed. <br/>
<br />
<br />
Copy the PowerShell Script for this lab from the file 
<img src="" height="80%" width="80%" alt=""/>
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
