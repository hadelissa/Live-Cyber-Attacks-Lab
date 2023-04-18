<h1>Azure Sentinel Live RDP Attacks Home Lab Walk Through</h1>


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
**Try to ping the VM IP address on your Computer to check if echo request are allowed.** <br/>
<br />

<h2>PowerShell/ ip geolocation walk-through:</h2> 
The purpose of Creating a PowerShell Script and connecting it to ipegolocation.io is that PowerShell script is going to look through the Security logs and grabs all the events of people who failed to login to the VM. Also, it grabs their IP address and gets the geodata of each Ip address and tehn create a new log file.
**Copy the PowerShell Script for this lab from the Custom_Security_Log_Exporter.ps1 file.** 
  <p align="center">
<br />
<br />
Open Powershell ISE and click New. Next, Paste the PowerShell Script and save it to your desktop: <br/>
<img src="https://i.imgur.com/qeXb3ku.png" height="80%" width="80%" alt=""/>
<br />
<br />
Go to ipgolocation.io, create an account, copy the API_KEY and paste it on the PowerShell script as shown in the screenShot below, Then Run the script.
<br />
<img src="https://i.imgur.com/Njgs68Y.png" height="80%" width="80%" alt=""/>
<img src="https://i.imgur.com/3gLgDup.png" height="80%" width="80%" alt=""/>
<br />
<br /> 
To access the failed logon files go to File Expolorer>Windwos(C:)>ProgramData: <br/>
<img src="https://i.imgur.com/8UqFqfa.png" height="80%" width="80%" alt=""/>
<br />
<br />
<h2>Connecting the failed RDP log file to the Log Analytics workspaces walk-through:</h2>
*Now we're going to create a custom log inside of our log analytics workspace that have created on Azure. This will allow us to bring the log with the Geo-data into the log analytics workspace.*<br/>
<br/>
1-Go to Azure> search for Log analytics workspaces> select the VM that you have created for this lab> Legacy Custome Logs> click on Add a Custom Log: In this case it wants us to add the failed rdp file however this file is on the remote desktop VM.<br />
<br />
2-Here is how to get it, Go to the remote desktop VM go to  File Expolorer>Windwos(C:)>ProgramData> open the file> select all> copy the data in the file.
<br />
3-On your actual Machine add a note file and paste the data then save it on your desktop then add it to the custom log.<br/>

In order for it to collect the logs correctly you need to add the correct  file Path. finish configuring the settings as shown below then click Create: <br/>
<img src="https://i.imgur.com/Vui6hoA.png" height="80%" width="80%" alt=""/>
<br />
<br />
click on Logs and type Name of the custom log that you've created inteh Query then click Run:
*It might Take up to 10 minutes to upload the data!* <br/>
<img src="https://i.imgur.com/2gHs1Z1.png" height="80%" width="80%" alt=""/>
<br />
<br />
 As you can see the RawData it's all included in one line, Now, we're going to extract certain fields from it.<br />
 To extract the Feilds follow these steps:
 click on any of the logs > expand the log> right click next to the expand button> choose Extract Fields from..<br/>
<img src="https://i.imgur.com/vchO4Op.png" height="80%" width="80%" alt=""/>
<br />
<br />
To extract Data to separate fields highlight the data that you want to extract then name it, in the screenshot below i highlighted the data that we wan to extract:<br/>
Select the value of the field data that you want to extract then name the Field Title by the name of the Field Data to have it display as the header of the field value then choose the correct Field Type. Once you're done click Extract then make sure the search results is displaying the correct info then click Save Extraction.<br/>
  <p align="center">
**Repate THE SAME STEPS FOR THE REST TO EXTRACT THE REST OF THE FIELDS**<br/>
<img src="https://i.imgur.com/ipuwNdO.png" height="80%" width="80%" alt=""/>
<img src="https://i.imgur.com/B66k1eT.png" height="80%" width="80%" alt=""/>
<br />
<br />
 
<h2>Creating a MAP to display the Live attacks walk-through:</h2>
  <p align="center">
by creating a Map on Microsoft Sentinel we're going to be able to view the live attacks with the display of teh Geo-Data.
 To create the Map: go to Microsoft Sentinel> choose the workspace that we've created for this lab> Go to Workbook> create New workbook> click on both Edits and select Remove> click on Add> Add Query.
 Here is teh query that you would want to add (FAILED_RDP_WITH_GEO_CL | summarize event_count=count() by sourcehost_CF, latitude_CF, longitude_CF, country_CF, label_CF, destinationhost_CF
| where destinationhost_CF != "samplehost"
| where sourcehost_CF != ""). Next, choose Map from the visualization tab <br/>
<img src="https://i.imgur.com/BINQSdc.png" height="80%" width="80%" alt=""/>
<br />
<br />
 Configure  the Map settings by using the Latitude and longitude as follow then click Apply: <br/>
<img src="https://i.imgur.com/8dcLXal.png" height="80%" width="80%" alt=""/>
<br />
<br />
Click on the save icon to save your map, give it a name, select the source group for this lab, then select the location and Save it.<br />
<br />
<img src="https://i.imgur.com/8yJn7Ev.png" height="80%" width="80%" alt=""/>
<br />
<br />
* I have waited about 2-3 hours to see the final results *
Live RDP Attack Map: <br/>
<img src="" height="80%" width="80%" alt=""/>
<br />
<br />
 : <br/>
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
