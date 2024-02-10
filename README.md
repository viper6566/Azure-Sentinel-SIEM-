# Azure-Sentinel-SIEM

<h2>Description</h2>
This project is an exposition of my process to establish Azure Sentinel (SIEM) and integrate it with a functional virtual machine serving as a honeypot. Additionally, I shall employ a personalized PowerShell script to retrieve the location details of the attackers and chart it on the Azure Sentinel!
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
<br /></p>
<p align="center">
<b>In the search bar, search for Virtual machine. Press Create > Virtual Machine. </b> <br/>
<img src="https://i.imgur.com/yCgJnlK.png" height="80%" width="80%" alt="Choose the right option"/>
<br />
<br />
<br /></p>
<p align="center">
<b>Under Project details > Subscription > Resource group > Press Create new > Name your Virtual Machine (I chose Beehive - sorry for the typo, I noticed way to late to change it.) For "Instance details" just follow the picture. </b> <br/>
<img src="https://i.imgur.com/whNHLNh.png" height="80%" width="80%" alt="Custom install"/>
<br />
<br />
<br /></p>
<p align="center">
<b>Please ensure that you make a note or commit to memory the login credentials, as they will be required subsequently for accessing the virtual machine.</b></br>
<img src="https://i.imgur.com/0R8FzGu.png" height="80%" width="80%" alt="Choose the driver"/>
<br />
<br />
<br /></p>
<p align="center">
<b>Make sure to agree the license. </b> 
<img src="https://i.imgur.com/O2NGFQT.png" height="80%" width="80%" alt="Commands"/>
<br />
<br />
<br /></p>
<p align="center">
<b>Once everything is filled in click “Next: Disk” button, and then “Next: Networking”. </b> <br/>
<img src="https://i.imgur.com/hVzyXMk.png" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
<br />
<br />
<br /></p>
<p align="center">
<b>Under “Network interface” choose “Advanced” for NIC network security group. (This will be like a firewall for your VM). Press “Create a new one” to create your firewall (Ignore the highlighted button).</b>
<img src="https://i.imgur.com/Tsh6RCn.png" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
<br />
<br />
<br /></p>
<p align="center">
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
<br /></p>
<p align="center">
<b>Whilst the virtual machine is being created, we shall establish a log analytics workspace. Ensure that you complete the "instance details" section. Once all fields are populated, click on the "Create and Review" button followed by the "Create" button to proceed..</b> <br/>
<img src="https://i.imgur.com/nqiGUMk.png" height="80%" width="80%" alt="Rename"/>
<br />
<br />
<img src="https://i.imgur.com/u7mpbHD.png" height="80%" width="80%" alt="IP"/>
<br />
<br /></p>
<p align="center">
<b>In the search bar, search Microsoft Defender for cloud > Environment settings > Your subscription (In my case is Azure subscription 1) > law-behive (the speling again :D )</b><br/>
<img src="https://i.imgur.com/kMbHYjH.png" height="80%" width="80%" alt="Renaming the PC"/>
<br />
<br /></p>
<p align="center">
<b>You will turn on the server button, and save the changes. From the left panel click "Data collection" option.</b><br/>
<img src="https://i.imgur.com/9NAcyIK.png" height="80%" width="80%" alt="Renaming the PC"/>
<br />
<br />
<img src="https://i.imgur.com/DAymgev.png" height="80%" width="80%" alt="Renaming the PC"/>
<br />
<br /></p>
<p align="center">
<b>Under "Data collection" choose "All Events" and save the option.</b> <br/>
<img src="https://i.imgur.com/2VNCIEx.png" height="80%" width="80%" alt="AD installation"/>
<br /></p>
<p align="center">
<b>Return to "log analytics workspace" and choose your VM. You can see in the picture the status says "Not connected". Click on the name of your VM and choose "connect"<br/>
<img src="https://i.imgur.com/MPHCN62.png" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
<br />
<br />
<img src="https://i.imgur.com/Y7BGujP.png" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
<p align="center">
<br />
<br /></p>
 <p align="center">
<b>Next, we will create Azure Sentinel. In the search bar, seach for Azure Snetinel. This is our SIEM that we will use to visualize the attack data.</b> <br/>
<img src="https://i.imgur.com/VPphyHB.png" height="80%" width="80%" alt="Creating Admin account"/>
<br />
<br /></p>
<p align="center">
<b>Now we will add the Sentinel to a workspace.</b> <br/>
</p>
<p align="center">
<img src="https://i.imgur.com/APLdEo3.png" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br /></p>
<p align="center">
<b>We shall allow the Sentinel to proceed with its loading task. Following, we shall access the Remote Desk and endeavor to remotely connect to the Virtual Machine. (Need I remind you of the credentials? They shall now prove useful. :) ) Upon returning to the Virtual Machine, we shall copy the IP address.</b></p>
<p align="center"> 
<img src="https://i.imgur.com/udldKyK.png" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
<img src="https://i.imgur.com/dWc5i0d.png" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
<img src="https://i.imgur.com/PDqgT5u.png" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br /></p>
<p align="center">
<b>Entering the virtual machine, we shall navigate to the Event Viewer in order to inspect the existing logs. Please take note that the initial launch of the Event Viewer may require an extended period of loading time due to its inherent sluggishness.</b> <br/>
</p>
<p align="center">
<img src="https://i.imgur.com/2jowSzg.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br />
<img src="https://i.imgur.com/Zn87cWV.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>
<p align="center">
<b>Just a peak inside a log. I failed to loggon purposely, just to be able to have a sample to present here.</b> <br/>
</p>
<p align="center">
<img src="https://i.imgur.com/He4SAbs.png" height="80%" width="80%" alt="Install DCHP"/>
<br /></p>
<p align="center">
<b>If you copy the IP you get into the failed log and paste it into IPGeolocation (get the link from the link section) you will see the location of the attack.</b></p>
<p align="center">
<img src="https://i.imgur.com/fRaVnMg.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>
 <p align="center">
<b>First, we will need to turn off the firewall. In your computer, NOT the VM, open Command Prompt and ping the VM. Command line: Ping (your VM's IP) -t, you will see the ping command times out.</b></p>
<p align="center">
<img src="https://i.imgur.com/tSVbye8.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>p
<p align="center">
<b>In the VM, press Start button and open the firewall by typing wf.msc.</b>
<img src="https://i.imgur.com/1oN1xPk.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>
<p align="center">
<b>Click Windows Defender Firewall </b><br/>
<img src="https://i.imgur.com/XcAHg8Z.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>
<p align="center">
<b>Turn off the firewall (see the pictures). Don't forget to press the "Apply" button once you turn off everything.</b>
<img src="https://i.imgur.com/tdynIPB.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br />
<img src="https://i.imgur.com/KBEat2h.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br />
<img src="https://i.imgur.com/JsXE2RU.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>
<p align="center">
<b>When all options are off, minimize the VM and ping the it again.This time you will see that is responding.</b>
<img src="https://i.imgur.com/IpcYdsT.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>
 <p align="center">
<b>Remaining in the VM  we will download the Powershell script (find the link in the link section).</b>
<b> I just copy and paste the script into Notepad and save it to Desktop.</b>
<b>You will need to have an IPGeolocation account to get the API key, otherwise the script will not work.</b> 
<img src="https://i.imgur.com/xnRS62g.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br />
<img src="https://i.imgur.com/vUTfMG5.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>
<p align="center">
<b>Run the scrip. Allow about half an hour to see new entries (attacks)</b>
<img src="https://i.imgur.com/2D3uA5p.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>
<p align="center">
<b>After initiating the PowerShell script, we shall navigate back to the Azure portal, where we can proceed to generate a custom log. In the search bar, seach for log analitics workspace > Choose your log (mine is law-beehive) > Custom log > Add custom log > At this step you will have to go back into your VM and copy the contents of you log file from the VM (You can find the log at the following path C:\Windows >ProgramData > failed log (if you cannot see the file in View section tick the "View hidden" box). Once you copy and saved the content on your compter return to Azure portal and add the file into the Sample log.</b></p>
<p align="center">
<b>In the "collection paths" make sure to choose the "type" (In my case is Windows). Under path type C:\ProgramData\failed_rdp.log (Please bear in mind that the name of your log may differ from mine. My log file is titled "failed_rdp.log", but regardless of the name, the path will remain the same.).</b></p>
<p align="center">
<img src="https://i.imgur.com/QfActY2.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>
<p align="center">
<b>In the "Custom log details" chose the name of your custom log. See the picture below. Have you noticed that under the name in the right corner you have a "CL"? That is attached authomatically and stands for "Custom log".</b></p>
<p align="center">
<b>Note: Please be mindful that the log will be generated automatically, however, it may require some time to populate. I advise that you allow enough time for the attackers to detect your virtual machine on the network.</b>
<img src="https://i.imgur.com/83mxpMj.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>
<p align="center">
<b>To see an overview of the results go to Sentinel > Overview and you will see a chart (like the one below) with your results.</b></p>
<p align="center">
<b></b>I have attached some screen shots with my results.</b></p>
<p align="center">
<b>The first 12 hours.</b></p>
<p align="center">
<img src="https://i.imgur.com/bcOU42T.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>
<p align="center">
<b>After 24 hours<br/>
<img src="https://i.imgur.com/sgl9eej.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>
<p align="center">
<b>After 7 days</br>
<img src="https://i.imgur.com/iRNKh4u.png" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br /></p>

<p align="center">
<b>If you followed along "Congratulations!" Now you have your first (or second, or third:D) honeypot VM.</br></p>
<p align="center">
<b>Thank you for reading, and don't forget to leave a review, comment or connect with me via LinkedIn.</br>  
<img src="https://i.imgur.com/COLQyQB.jpeg" height="80%" width="80%" alt="Thank you!"/>
<br />
<br /></p>
 
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in grey
@@ text in purple (and bold)@@
```
--!>
