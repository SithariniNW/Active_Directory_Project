<h1 style="color:blue;"> Active Directory Home Lab</h1>


<h3 Resources Used </h3>
<ul type="circle">
 <li>Oracle Virtual Box</li>
 <li>Windows 10 ISO</li>
 <li>Windows server 2019 ISO</li>
 <li>PowerShell Script</li>
</ul>


<h3>Overview</h3>
Create a home lab set up with running active directory utilizing Oracle Virtual Box. Two virtual machines, <b>DC</b> and <b>Client 1</b>, were created with Windows server 2019 ISO and Windows 10 installed, respectively.

<br> <img src="Images/Active Directory.drawio (3).png" height="60%" width="60%" alt="Directory creation" align="center"/>

<h4>DC Virtual Machine</h4>
Acts as the main domain controller and hosts the active directory. Consists of two network interfaces, one connected to the internet and the other as an internal network. The internal network is assigned to IP addressing through the set up. Furthermore, NAT, routing, and DHCP are installed in the virtual machine for smooth network operation.

<h4>Client 1 Virtual Machine</h4>
Used for experimentation with the main active directory as a user. Connected to the virtual machine's internal network.

<h3>VM Setup</h3>
The first VM to be set up is the DC machine with Windows Server 2019 ISO installed. Even though the preferred base memory of the system was set to 2GB (2048MB), due to partition issues in the hard disk, the memory had to be increased to 11450MB.

<br> Furthermore, instead of the default one network adapter connected to the internet, an additional network adapter to accommodate the internal network was set up.

<br> The second VM, CLIENT1 is created after the network configuration and installation of active directory in DC.

<br> The second VM contains Windows 10 ISO with 4 processor cores, 2GB base memory and one network interface that connects to the internal VM network.

<h3>Network Configuration</h3>
Both machines are automatically connected to the internet through the main network adapter, which will assign IP addresses through the home router DHCP. 

<br> However, for the internal network in the DC machine IP addressing had to be manually assigned using Windows network settings as follows,

<br> <b> IP: 172.16.0.1 </b>
<br> <b> Mask: 255.255.255.0 </b>
<br> <b> DNS: 172.0.0.1 </b>

<h3>Active Directory Installation</h3>

Using the server manager dashboard of the DC Virtual Machine, an active directory named DC was created as follows,

<br> <img src="Images/Screenshot 2025-02-07 215156.png" height="50%" width="50%" alt="Directory creation"/>

After the creation, the post-deployment configuration is done by adding a forest name <b> mydomain.com </b>. 

<br> <img src="Images/Screenshot 2025-02-07 215304.png" height="50%" width="50%" alt="Directory creation"/>

Afterwards, a dedicated domain admin account named <b> a-SWewalwala </b> is created under the organizational unit <b> /ADMIN </b>

<br> <img src="Images/Screenshot 2025-02-08 160845.png" height="50%" width="50%" alt="Directory creation"/>

<h3>NAT and DHCP installation</h3>

Remote Access and NAT should be configured to allow internal clients such as the Client machine to access the internet through a common public IP address. This could be done using the server manager wizard on the DC machine.

<br> <img src="Images/Screenshot 2025-02-08 165115.png" height="50%" width="50%" alt="Directory creation"/>

DHCP allows client machines to access a range of IP addresses to access the internet instead of using their private IP address. The IP address range of <b> 172.16.0.100 to 172.16.0.200 </b> is considered as the range of addresses that the DHCP server can distribute to the clients. There are no excluded IP addresses within the range and they are valid for 8 days of use.

<br> <img src="Images/Screenshot 2025-02-08 165857.png" height="50%" width="50%" alt="Directory creation"/>

The IP address of the internal network of the DC machine <b> 172.16.0.1 </b> is used as the gateway address for the DHCP server.

<br> <img src="Images/Screenshot 2025-02-08 170235.png" height="50%" width="50%" alt="Directory creation"/>

<h3>Generation of users</h3>

To visualize the functionality of the domain controller and active directory, 1k users are generated and created within the active directory. This is achieved with the use of the following power shell script,

```
$PASSWORD_FOR_USERS   = "Password123"
$USER_FIRST_LAST_LIST = Get-Content .\names.txt

$password = ConvertTo-SecureString $PASSWORD_FOR_USERS -AsPlainText -Force
New-ADOrganizationalUnit -Name _USERS -ProtectedFromAccidentalDeletion $false

foreach ($n in $USER_FIRST_LAST_LIST) {
    $first = $n.Split(" ")[0].ToLower()
    $last = $n.Split(" ")[1].ToLower()
    $username = "$($first.Substring(0,1))$($last)".ToLower()
    Write-Host "Creating user: $($username)" -BackgroundColor Black -ForegroundColor Cyan
    
    New-AdUser -AccountPassword $password `
               -GivenName $first `
               -Surname $last `
               -DisplayName $username `
               -Name $username `
               -EmployeeID $username `
               -PasswordNeverExpires $true `
               -Path "ou=_USERS,$(([ADSI]`"").distinguishedName)" `
               -Enabled $true
}

```
<br> <img src="Images/Screenshot 2025-02-08 174631.png" height="50%" width="50%" alt="Directory creation"/>

<br> <img src="Images/Screenshot 2025-02-08 175854.png" height="50%" width="50%" alt="Directory creation"/>

<h3>Testing CLIENT1 connectivity</h3>

Client VM was configured with one network adapter connected to the internal VM network that connects it to the main Domain Controller.

<br> If connected properly, the default gateway of the Client 1 machine should be the IP address of DC as it accesses the internet through DC. This could be verified by using the <b> ipconfig </b> command on the command prompt of the client machine. 

<br> The client is also able to reach the internet through the internal network as the ping to <b> www.google.com </b> is successful.

<br> <img src="Images/Screenshot 2025-02-09 164142.png" height="50%" width="50%" alt="Directory creation"/>

<br> The final alteration that is done to the client machine is to make it a member of mydomain.com active directory.

<br> <img src="Images/Screenshot 2025-02-09 164445.png" height="50%" width="50%" alt="Directory creation"/>

<h3>Conclusion</h3>

This active directory home lab successfully demonstrated the setup and configuration of a domain controller using <b> Oracle VirtualBox, Windows Server 2019, and Windows 10 </b>. By integrating Active Directory, NAT, and DHCP, a functional internal network was created, allowing the Client 1 VM to communicate with the domain controller and access the internet.

<br> Additionally, the deployment of 1,000 users using a PowerShell script highlights automation capabilities within Active Directory, showcasing its scalability for enterprise environments. The final validation of network connectivity and domain membership confirms that the setup is fully operational.

<h3>Reflection</h3>

This lab served as a foundational exercise for me to understand the active directory infrastructure, network configuration and enterprise-level user management of Windows-based computers. 

<h5> Skills obtained </h5>
<ul type="circle">
 <li>Active Directory Configuaration</li>
 <li>Network configuration of DHCP, routing and NAT</li>
 <li>Power shell scripting </li>
</ul>

<h5> References </h5>
https://www.microsoft.com/en-au/software-download/windows10
<br> https://www.youtube.com/watch?v=MHsI8hJmggI&t=1829s


