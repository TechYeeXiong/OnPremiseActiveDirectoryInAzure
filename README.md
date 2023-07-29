<h1>Creating On Premise Active Directory in Azure</h1>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Command Line Interface (CLI)

<h2>Operating Systems Used </h2>

- Windows 10
- Windows Server 2022</b>

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/pBIdWFa.png" height="80%" width="80%" alt="Create 1 RG and 2 VM"/>
</p>
<p>
Diagram of entire process
</p>
<br />

<p>
<img src="https://i.imgur.com/x8c7j0L.png" height="80%" width="80%" alt="Make the DC1 into a static ip address"/>
<img src="https://i.imgur.com/D1BYtb3.png" height="80%" width="80%" alt="Make the DC1 into a static ip address"/>
</p>
<p>
Create 2 virtual machine inside the Resource Group; one is Windows Server 2022 and the other is Windows 10.
</p>
<br />

<p>
<img src="https://i.imgur.com/CRxUTPJ.jpg" height="80%" width="80%" alt="Ping DC1 but it don't work so use wf.msc on DC1"/>
<img src="https://i.imgur.com/KaLgZFR.png" height="80%" width="80%" alt="change the inbound rules"/>
<img src="https://i.imgur.com/Yo882X3.jpg" height="80%" width="80%" alt="Ping now works"/>
</p>
<p>
Ping DC1 however it doesn't work so you have to go into DC1 and go to wf.msc. Next change the inbound rules by enabling the ICMP Echo Request.
</p>
<br />

<p>
<img src="https://i.imgur.com/OHQ1B65.jpg" height="80%" width="80%" alt="Go to DC1 and click on add roles and features wizard. Activate active directory domain service"/>
</p>
<p>
Download Wireshark inside the virtual machine
</p>
<br />

<p>
<img src="https://i.imgur.com/gjlwxEo.jpg" height="80%" width="80%" alt="Use Ping"/>
<img src="https://i.imgur.com/mdfsOYp.png" height="80%" width="80%" alt="Use Ping"/>
<img src="https://i.imgur.com/W094nVH.jpg" height="80%" width="80%" alt="Use Ping"/>
</p>
<p>
Use the ICMP protocol as the filter to observe the traffic. Open Windows Powershell then use "ping 10.0.0.5" and "ping www.google.com". Next go to VM2's network security group and create an inbound security rule to deny ICMP traffic. These commands will show how much data is being sent and received.
</p>
<br />

<p>
<img src="https://i.imgur.com/CyRmSTz.jpg" height="80%" width="80%" alt="After installing AD, promote it into a domain controller. Add a new forest and create the root name. Create a password."/>
</p>
<p>
Use SSH to filter the traffic. In Powershell, use SSH to remotely connect to VM2 by typing "ssh labuser@10.0.0.5". Next type "pwd", "id", and "ls -lasth". Observe the traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/JF6RkKG.jpg" height="80%" width="80%" alt="DHCP"/>
</p>
<p>
Use DHCP to filter the traffic. In Powershell, type "ipconfig /renew" then observe the traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/lFkECUi.jpg" height="80%" width="80%" alt="Go onto whatismyipaddress.com"/>
</p>
<p>
The IP Address is now located in Tokyo.
</p>
<br />

<p>
<img src="https://i.imgur.com/f06KkBn.jpg" height="80%" width="80%" alt="DNS"/>
</p>
<p>
Use DNS to filter the traffic. In Powershell, type "nslookup www.google.com" and "nslookup www.disney.com" to find the IP Address for both website and observe the traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/KqAPmcB.jpg" height="80%" width="80%" alt="RDP"/>
</p>
<p>
In order to use RDP in the filter; you type in "tcp.port == 3389". Since RDP was selected as the protocol for VM1 when it was created; the rdp filter will spam nonstop. Every movement or words being typed inside the virtual machine will cause traffic to be sent.
</p>
<br />
