<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create two VMs, one is for domain controller and other one is for client. 
- Set Domain Controller’s NIC Private IP address to be static
- Client’s DNS settings to DC-1’s Private IP address

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/VSKwsdt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We configure Domain Controller's private IP address to be static. By setting the private IP to static, we're making sure the Domain Controller always has the same internal IP, keeping our domain environment stable. We also configure Client-1’s DNS settings to DC-1’s private IP address. This allows Client-1 to find and communicate with the Domain Controller, especially when trying to join the domain or look up domain-related resources.
</p>
<br />

<p>
<img src="https://i.imgur.com/3iIBA82.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We first created a resource group to organize resources, followed by a virtual network and subnet. We then deployed a Windows Server 2022 virtual machine named DC-1. 
</p>
<br />

<p>
<img src="https://i.imgur.com/jayVhRY.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After the VM was created, We set its private IP address to static to ensure consistent network identity. For testing connectivity, We logged into the VM and temporarily disabled the Windows Firewall.
</p>
<br />


<p>
<img src="https://i.imgur.com/OV0v4s4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we created a Windows 10 virtual machine named Client-1 in the same region and virtual network as DC-1. Once Client-1 was deployed, We configured its DNS settings to point to DC-1’s private IP address and restarted the VM through the Azure Portal to apply the changes.
</p>
<br />

<p>
<img src="https://i.imgur.com/VuCqIda.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After logging into Client-1, We verified network connectivity by pinging DC-1’s private IP and confirmed the connection was successfull by opening PowerShell on Client-1, ran ipconfig /all, and verified that the DNS server listed matched DC-1’s private IP address.
</p>
<br />

<p>
<img src="https://i.imgur.com/XlAo19e.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We logged in to DC-1 virtual machine and installed the Active Directory Domain Services. Then, We promoted the server to a Domain Controller
</p>
<br />

<p>
<img src="https://i.imgur.com/rBW88kU.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here, we're configuring account lockout policy by setting it to lock the account after 5 failed login attempts. We then located the locked account by opening  Active Directory Users and Computers and manually unlock it.
</p>
<br />



