<h1 style="color:blue"> Active Directory Home Lab</h1>


<h3>Resources Used</h3>
<ul type="circle">
 <li>Oracle Virtual Box</li>
 <li>Windows 10 ISO</li>
 <li>Windows server 2019 ISO</li>
 <li>PowerShell Script</li>
</ul>


<h3>Overview</h3>
Create a home lab set up with running active directory utilizing Oracle Virtual Box. Two virtual machines, <b>DC</b> and <b>Client 1</b>, were created with Windows server 2019 ISO and Windows 10 installed, respectively.

<h4>DC Virtual Machine</h4>
Acts as the main domain controller and hosts the active directory. Consists of two network interfaces, one connected to the internet and the other as an internal network. The internal network is assigned to IP addressing through the set up. Furthermore, NAT, routing, and DHCP are installed in the virtual machine for smooth network operation.

<h4>Client 1 Virtual Machine</h4>
Used for experimentation with the main active directory as a user. Connected to the virtual machine's internal network.

<h3>VM Setup</h3>
The first VM to be set up is the DC machine with Windows Server 2019 ISO installed. Even though the preferred base memory of the system was set to 2GB (2048MB), due to partition issues in the hard disk, the memory had to be increased to 11450MB.

<br> Furthermore, instead of the default one network adapter connected to the internet, an additional network adapter to accommodate the internal network was set up.

<h3>Network Configuration</h3>
Both machines are automatically connected to the internet through the main network adapter, which will assign IP addresses through the home router DHCP. 

<br> However, for the internal network in the DC machine IP addressing had to be manually assigned using Windows network settings as follows,

<br> <b> IP: 172.16.0.1
<br> <b> Mask: 255.255.255.0
<br> <b> DNS: 172.0.0.1


<h2>Program walk-through:</h2>

<p align="center">
Launch the utility: <br/>
<img src="https://i.imgur.com/62TgaWL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select the disk:  <br/>
<img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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
