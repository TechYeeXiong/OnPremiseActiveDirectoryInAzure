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
Go to Client1 and Ping DC1 however it doesn't work so you have to go into DC1 and go to wf.msc. Next change the inbound rules by enabling the ICMP Echo Request. Now go back to Client1 and ping DC1; you will notice that now it's able to ping.
</p>
<br />

<p>
<img src="https://i.imgur.com/Mlgh5cY.jpg" height="80%" width="80%" alt="Go to DC1 and click on add roles and features wizard. Activate active directory domain service"/>
<img src="https://i.imgur.com/0AJ3cuO.jpg" height="80%" width="80%" alt="Promote server to Domain Controller"/>
</p>
<p>
Go to DC1 and click on add roles and features wizard. Activate active directory domain service. Notice how there's a warning that something is not finished yet so promote server to Domain Controller.
</p>
<br />

<p>
<img src="https://i.imgur.com/pmMOeSd.jpg" height="80%" width="80%" alt="add a new forest"/>
<img src="https://i.imgur.com/hkBtnBQ.jpg" height="80%" width="80%" alt="Create a password"/>
<img src="https://i.imgur.com/is2uu89.jpg" height="80%" width="80%" alt="Login to DC1"/>
</p>
<p>
First, add a new forest and type a root for the username. Create a password. Exit out of DC1 and then login back using the root and password that you created.
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
