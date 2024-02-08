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
<b>Now I’ve configured the Internal network adapter and assigned it an IP address based on the diagram above (172.16.0.1) and I do not need to give it a default gateway as the DC is the gateway. As for the DNS server, I assigned an IP based on the diagram because when we install Active Directory it will install DNS. I set it as a loopback address so it pings itself.</b> <br/>
<img src="https://imgur.com/xMM9gt2.jpg" height="80%" width="80%" alt="IP"/>
<br />
<br />
<b>Now that the NICs are differentiated, I renamed the VM as Practise. This forces a restart</b> <br/>
<img src="https://imgur.com/tKcm0DH.jpg" height="80%" width="80%" alt="Renaming the PC"/>
<br />
<br />
<b>After restarting, I installed Active Directory Domain Services through Server Manager and set up the server as the domain immediately. When the server is promoted to a domain, it forces a restart.</b> <br/>

<img src="https://imgur.com/t0DUH6T.jpg" height="80%" width="80%" alt="AD installation"/>
<br />
<p align="center">
 <img src="https://imgur.com/7ug890z.jpg" height="80%" width="80%" alt="Configuring the Network Adapter for the Domain Controller Virtual Machine"/>
 <p align="center">
<br />
<br />
<p align="center">
<b>Using the built-in Admin account, I will create a dedicated domain Admin account, granting it Domain Admin permissions on AD. </b> <br/>
</p>
<p align="center">
 <img src="https://imgur.com/HG50Cdg.jpg" height="80%" width="80%" alt="Creating Admin account"/>
<br />
<br />
<p align="center">
<b>Now I need to install RAS/NAT (incl Routing) for my Windows 10 client to gain access to the internet through the internal network via the DC.</b> <br/>
</p>
<p align="center">
 <img src="https://imgur.com/CKYDBRh.jpg" height="80%" width="80%" alt="Installing RAS"/>
<br />
<br />
<p align="center">
<b>Now that the role is installed, I need to configure the Routing and Remote Access under tools in Server Manager. Click Tools in Server Manager and Right click ‘Practice’ and configure and enable routing and remote access. Under configuration, select NAT and the external NIC (the internet).</b> <br/>
</p>
<p align="center">
<img src="https://imgur.com/9sdMtQs.jpg" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
   <img src="https://imgur.com/xBwrlKz.jpg" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
   <img src="https://imgur.com/6ArB8q6.jpg" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
   <img src="https://imgur.com/cWGOFtd.jpg" height="80%" width="80%" alt="Config Remote Access"/>
<br />
<br />
<p align="center">
<b>After Remote Access has been configured, install the DHCP Server. This will allow our Windows 10 clients to be assigned an IP address and gain access to the internet..</b> <br/>
</p>
<p align="center">
 <img src="https://imgur.com/VpQuR04.jpg" height="80%" width="80%" alt="Install DCHP"/>
<br />
<br />
<p align="center">
<b>The purpose of the DHCP server is to allow machines on the network to automatically be assigned an IP address. The scope created will assign IP addresses in a range, that being 172.16.0.100-200 so the DHCP will effectively be able to give out 100 IP addresses (you can also configure the lease time of the IP addresses for the client machines so that the IP cannot be used by other devices).</b> <br/>
</p>
<p align="center">
<img src="https://imgur.com/JTjhG5n.jpg" height="80%" width="80%" alt="Install DCHP"/>
<br />
<p align="center">
<img src="https://imgur.com/4MNAjEQ.jpg" height="80%" width="80%" alt="Install DCHP"/>
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
