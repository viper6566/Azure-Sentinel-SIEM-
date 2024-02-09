# Azure-Sentinel-SIEM

<h2>Description</h2>
This project is an exposition of my process to establish Azure Sentinel (SIEM) and integrate it with a functional virtual machine serving as a honeypot. Additionally, we shall employ a personalized PowerShell script to retrieve the location details of the attackers and chart it on the Azure Sentinel!
<br />

<h2>Utilities Used</h2>

- <b>Azure</b> 


<h2>Environments Used </h2>

- <b>Azure</b>
- <b>VirtualBox</b>
- <b>Remote Desktop</b>


<h2>Links</h2>

- [Azure](https://portal.azure.com/#home)
- [Powershel script](https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1)
- [IPGeolocation](https://ipgeolocation.io/)

<h2 align="center">Program walk-through</h2>

<p align="center">
<b>The diagram I'll be using for this project.</b> <br/>
<img src="https://i.imgur.com/KFXfRRe.png" height="80%" width="80%" alt="Network Diagram"/>
<br />
<br />
<br />
<p align="center">
<b>I initiated the process by enrolling myself in the Azure portal with a 30-day subscription. Upon its completion, I proceeded to build a Virtual Machine (VM). This process takes the most time.</b> <br/>
<img src="https://i.imgur.com/CxNnwNc.png" height="80%" width="80%" alt="Choose the right option"/>
<br />
<br />
<br />
<b>In the search bar, search for Virtual machine. Press Create > Virtual Machine". </b> <br/>
<img src="https://i.imgur.com/yCgJnlK.png" height="80%" width="80%" alt="Choose the right option"/>
<br />
<br />
<br />
<b>Under Project details > Subscription > Rsource group > Press Create new > Name your Virtual Machine (I chose Beehive - sorry for the typo, I noticed way to late to change it.) For "Instance details" just follow the picture. </b> <br/>
<img src="https://i.imgur.com/whNHLNh.png" height="80%" width="80%" alt="Custom install"/>
<br />
<br />
<br />
<b>Please ensure that you make a note or commit to memory the login credentials, as they will be required subsequently for accessing the virtual machine.</b></br>
<img src="https://i.imgur.com/0R8FzGu.png" height="80%" width="80%" alt="Choose the driver"/>
<br />
<br />
<br />
<p align="center">
<b>Make sure to agree the license. </b> 
<img src="https://i.imgur.com/O2NGFQT.png" height="80%" width="80%" alt="Commands"/>
<br />
<br />
<br />
<p align="center">
<b>Once everything is filled in click “Next: Disk” button, and then “Next: Networking”. Under “Networking” choose “Advanced” for NIC network security group. (This will be like a firewall for your VM). Press “Create a new one” to create your firewall. </b> <br/>
<img src="https://i.imgur.com/hVzyXMk.png" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
<br />
<br />
<br />
 
 <img src="https://i.imgur.com/Tsh6RCn.png" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
<br />
<br />
<br />
 <b>Name your firewall. Remove the the existing inbound rule and create a new one (follow the picture below). When you are done with the inboud rule click "Review and Create" > "Create" </b> 
<img src="https://i.imgur.com/MhK8pJp.png" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
<br />
<br />
<img src="https://i.imgur.com/povS00s.png" height="80%" width="80%" alt="Rename"/>
<br />
<br />
 <img src="https://i.imgur.com/LCkBH0R.png" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
<br />
<br />
<br />
<b>Whilst the virtual machine is being created, we shall establish a log analytics workspace. Ensure that you complete the "instance details" section. Once all fields are populated, click on the "Create and Review" button followed by the "Create" button to proceed..</b> <br/>
 <img src="https://i.imgur.com/nqiGUMk.png" height="80%" width="80%" alt="Rename"/>
<br />
<br />
<img src="https://i.imgur.com/u7mpbHD.png" height="80%" width="80%" alt="IP"/>
<br />
<br />
<b>In the search bar, search Microsoft Defender for cloud > Environment settings > Your subscription (In my case is Azure subscription 1) > law-behive (the speling again :D )</b><br/>
<img src="https://i.imgur.com/kMbHYjH.png" height="80%" width="80%" alt="Renaming the PC"/>
<br />
<br />
<b>You will turn on the server button, and save the changes. From the left panel click "Data collection" option.</b><br/>
<img src="https://i.imgur.com/9NAcyIK.png" height="80%" width="80%" alt="Renaming the PC"/>
<br />
<br />
<img src="https://i.imgur.com/DAymgev.png" height="80%" width="80%" alt="Renaming the PC"/>
<br />
<br />
<b>Under "Data collection" choose "All Events" and save the option.</b> <br/>
<img src="https://i.imgur.com/2VNCIEx.png" height="80%" width="80%" alt="AD installation"/>
<br />
<b>Return to "log analytics workspace" and choose your VM. You can see in the picture the status says "Not connected". Click on the name of your VM and choose "connect"<br/>
<p align="center">
<img src="https://i.imgur.com/MPHCN62.png" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
 <p align="center">
<br />
<br />
 <img src="https://i.imgur.com/Y7BGujP.png" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
 <p align="center">
<br />
<br />
<b>Next, we will create Azure Sentinel. In the search bar, seach for Azure Snetinel.This is our SIEM that we will use to visualize the attack data.</b> <br/>
<p align="center">
 <img src="https://i.imgur.com/VPphyHB.png" height="80%" width="80%" alt="Creating Admin account"/>
<br />
<br />
<p align="center">
<b>Now we will add the Sentinel to a workspace.</b> <br/>
</p>
<p align="center">
<img src="https://i.imgur.com/APLdEo3.png" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
 <b>We shall allow the Sentinel to proceed with its loading task. Following, we shall access the Remote Desk and endeavor to remotely connect to the Virtual Machine. (Need I remind you of the credentials? They shall now prove useful. :) ) Upon returning to the Virtual Machine, we shall copy the IP address.</b>
 <img src="https://i.imgur.com/udldKyK.png" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
   <img src="https://i.imgur.com/dWc5i0d.png" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
   <img src="https://i.imgur.com/PDqgT5u.png" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
<p align="center">
<b>Entering the virtual machine, we shall navigate to the Event Viewer in order to inspect the existing logs. Please take note that the initial launch of the Event Viewer may require an extended period of loading time due to its inherent sluggishness.</b> <br/>
</p>
<p align="center">
 <img src="https://i.imgur.com/2jowSzg.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br />
 <img src="https://i.imgur.com/Zn87cWV.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br />
<p align="center">
<b>Just a peak inside a log. I failed to loggon purposely, just to be able to have a sample to present here.</b> <br/>
</p>
<p align="center">
<img src="https://i.imgur.com/He4SAbs.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
 <b>If you copy the IP you get into the failed log and past it into IPGeolocation (get the link from the link section) you will see the location of the attack.</b>
 <img src="https://i.imgur.com/fRaVnMg.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br />
 <b>We will now utilize Powershell to determine the source location from which the attacker is attempting to gain access.</b>
<p align="center">
<img src="" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br />
<p align="center">
<b>Now the DC and AD are configured. This Finalises the Active Directory Lab. This can be further modified by implementing Group Policies, security features, programs etc.</b>  <br/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in grey
@@ text in purple (and bold)@@
```
--!>
