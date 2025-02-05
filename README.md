<h1 style="color:blue"> Active Directory Home Lab</h1>


<h3>Resources Used</h3>
<ul type="circle">
 <li>Oracle Virtual Box</li>
 <li>Windows 10 ISO</li>
 <li>Windows server 2019 ISO</li>
 <li>PowerShell Script</li>
</ul>


<h3>Overview</h3>
Create a home lab set up with running active directory utilizing Oracle Virtual Box. Two virtual machines, <b>DC</b> and <b>Client 1</b>, were created with server 19 and Windows 10 installed, respectively.

<h4>DC Virtual Machine</h4>
Acts as the main domain controller and hosts the active directory. Consists of two network interfaces, one connected to the internet and the other as an internal network. The internal network is assigned to IP addressing through the set up. Furthermore, NAT, routing and DHCP are installed in the virtual machine as well for smooth network operation.

<h4>Client 1 Virtual Machine</h4>
Used for experimentation with main active directory as a user. Connected to the virtual machine internal network.

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
