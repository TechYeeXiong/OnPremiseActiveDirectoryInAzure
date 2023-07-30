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
<img src="https://i.imgur.com/TTuCJQ1.jpg" height="80%" width="80%" alt="Creating Jane Doe as an admin user"/>
<img src="https://i.imgur.com/Lrvixmd.jpg" height="80%" width="80%" alt="login as Jane Doe"/>
</p>
<p>
First, create Jane Doe as an admin user and create the username as "jane_admin". Next, add Jane Doe into the Domain Admins group. Now log into Jane Doe's account as admin by typing "mydomain.com\jane_admin" as the username and your password.
</p>
<br />

<p>
<img src="https://i.imgur.com/x5XpP71.jpg" height="80%" width="80%" alt="Change client1"/>
<img src="https://i.imgur.com/OyZuXwB.jpg" height="80%" width="80%" alt="Change the dns server of client1"/>
<img src="https://i.imgur.com/Q7V4epV.jpg" height="80%" width="80%" alt="restart client1"/>
</p>
<p>
Go into Client1 and go into the about page. Click on rename this page(advanced) then click "change...". Type in "mydomain.com", however there's an error because Client1's DNS Server is not connected to DC1. Go into DC1 and change the DNS Server into DC1's private address which is "10.0.0.4" then restart Client1.
</p>
<br />

<p>
<img src="https://i.imgur.com/Yum6wDk.jpg" height="80%" width="80%" alt="Change the Client1 Domain"/>
</p>
<p>
Join Client1 into DC1 server's domain. 
</p>
<br />

<p>
<img src="https://i.imgur.com/O1EUspE.jpg" height="80%" width="80%" alt="Login to Client1"/>
</p>
<p>
Login to Client1 with the username of DC1 server's domain which is "mydomain.com\jane_admin"
</p>
<br />

<p>
<img src="https://i.imgur.com/yy1c8qM.png" height="80%" width="80%" alt="Allow remote desktop"/>
</p>
<p>
Allow remote desktop connection for all domain users on Client1.
</p>
<br />

<p>
<img src="https://i.imgur.com/ow1lUwa.jpg" height="80%" width="80%" alt="Check the Users"/>
</p>
<p>
Check the users member and you notice that we have added Jane Doe as an admin and labuser as the domain users. This means that anyone can login to Client1 machine using their username and password.
</p>
<br />
