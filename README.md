<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>
<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Windows Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resource Group
- Create Virtual Network and Subnet
- Create and Deploy Virtual Machines
- Setup Windows Remote Desktop for Domain Control/DNS and Client PC
- Configure Networking
- Configure Windows Firewall
- Verify Connectivity

<h2>Deployment and Configuration Steps</h2>

<h3>Setup Resources in Azure</h3>

<p>Begin by setting up an Azure account or login to your existing Azure account. Once logged in navigate to the home screen.<p>
  
<p>
<img src="https://i.imgur.com/2zzd9kI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<h4>Create Resource Group</h4>

<p>
<img src="https://i.imgur.com/nptZ0kD.png"/>
</p>
<p>
Navigate to Resource Groups or use the search bar to type in "Resource Groups.
</p>
<br />

<p>
<img src="https://i.imgur.com/ln4bwrb.png"/>
</p>
<p><ul>
  <li>Click Create to set up a new Resource Group.</li><br>
  <li>Name the Resource Group. I chose <b>Active-Directory-Lab</b>.</li><br>
  <li>Select Region: <b>East US 2</b>. Select Region closest to your location.</li><br>
  </ul>

</p>
<br />

<p>
<img src="https://i.imgur.com/Z9sTJKh.png"/>
</p>
<p>
Click <b>Review + Create</b>, then click <b>Create</b>.
</p>
<p>
  <img src="https://i.imgur.com/K1R4Tk3.png"/>
</p>
<br />

<h4>Create Virtual Network and Subnet</h4>

<p>
<img src="https://i.imgur.com/ODN8cfz.png"/>
</p>
<p>
On the Azure homescreen Navigte to <b>Virtual Network</b> or type it into the search bar.
</p>
<br />

<p>
<img src="https://i.imgur.com/4uvhebg.png"/>
</p>

<br />

<p>
<img src="https://i.imgur.com/r1JmfFi.png"/>
</p>
<p><ul>
  <li>Click <b>Create</b> to set up a new <b>Virtual Network</b>.</li><br>
  <li>Ensure the correct <b>Resource Group</b> is selected that was created in prior steps.</li><br>
  <li>Name the Virtual Network. I chose "<b>Active-Directory-VNet</b>.</li><br>
  <li>Choose same <b>Region</b> you selected for Resource Group. I selected <b>East US 2</b></li>
</ul>
</p>
<br />

<p>
<img src="https://i.imgur.com/gq5LPu0.png"/>
</p>
<p>
<b>Active-Directory-VNet</b> deployed
</p>
<br />


<h4>Create Virtual Machine <em>Windows Server</em></h4>

<p>
<img src="https://i.imgur.com/x4d0ZR5.png"/>
</p>
<p>
On Azure homescreen navigate to <b>Virtual Machine</b> or type in search bar.
</p>
<br />

<p>
<img src="https://i.imgur.com/ZjfWTOP.png"/>
</p>
<p>
  <ul>
  <li>Click <b>Create Azure Virtual Machine</b>. </li><br>
  <li>Ensure the correct <b>Resource Group</b> is selected. The same Resource Group setup in prior steps. <b>Active-Directory-Lab</b></li> <br>
  <li>Name the Virtual Machine. I chose <b>DC-1</b></li> <br>
  <li>Confirm Region: <b>East US 2</b>. Your Region may differ from mine, but be sure it matches the Region you selected through out the project.</li>
  </ul>
  </p>
<br />

<p>
<img src="https://i.imgur.com/Bpnyruf.png"/>
</p>
<p><ul>
  <li>Select <b>Windows Server 2022</b> as the <b>Image</b>.</li>
  <li>Choose a <b>Size</b> with at least <b>2 vcpus</b>.</li>
</ul>
</p>
<br />

<p>
<img src="https://i.imgur.com/kL7t6Dw.png"/>
</p>
<p><ul>
  <li>Create a <b>Username and Password</b>.</li>
  <li>Click Next for <b>Disks</b>.</li>
 </ul> 
</p>
<br />

<p>
<img src="https://i.imgur.com/7T2jGOU.png"/>
</p>
<p>
  <ul>
  <li>Click Next for <b>Networking</b></li>
  <li>Confirm <b>Virtual Network</b> you created in prior steps is selected. <b>Active-Directory-VNet</b></li>
  </ul>
</p>
<br />

<p>
<img src="https://i.imgur.com/LRJPxH0.png"/>
</p>
<p>Click <b>Review + Create</b>, then click <b>Create</b>.</p>
<br />

<p>
<img src="https://i.imgur.com/GQxXBdK.png"/>
</p>
<p>
  Virtual Machine Windows Server Deployed
</p>
<br />

<h4>Create Virtual Machine (Client)</h4>

<p>
<img src="https://i.imgur.com/E1k8zSk.png"/>
</p>
<p><ul>
  <li>On Azure homescreen navigate to <b>Virtual Machine</b> or type in search bar.</li>
  <li>Click <b>Create Azure Virtual Machine</b>.</li>
  <li>Ensure the correct <b>Resource Group</b> is selected. The same Resource Group setup in prior steps. <b>Active-Directory-Lab</b></li>
  <li>Name the Virtual Machine. I chose <b>Client-1</b></li>
  <li>Confirm Region: <b>East US 2</b>. Your Region may differ from mine, but be sure it matches the Region you selected through out the project.</li>
  </ul>
</p>
<br />

<p>
<img src="https://i.imgur.com/cXjzE2y.png"/>
</p>
<p>
  <ul>
    <li>Select <b>Windows 10 Pro, version 22H2</b> as the <b>Image</b></li>
    <li>Choose a <b>Size</b> with at least <b>2 vcpus</b>.</li>
   
  </ul>
</p>

<p>
<img src="https://i.imgur.com/L1HecdU.png"/>
</p>
<p>
  <ul>
    <li>Create a <b>Username and Password</b>.</li>
    <li>Select the <b>Licensing</b> box.</li>
  </ul>
</p>

<p>
<img src="https://i.imgur.com/CC5qJ7n.png"/>
</p>
<p>
  <ul>
  <li>Click Next for <b>Disks</b>and next for <b>networking.</b></li>
  <li>Confirm the Virtual Network you created in prior steps is selected. <b>Active-Directory-VNet</b></li>
  <li>Click <b>Review + Create</b>, and then Click <b>Create.</b></li>
  </ul>
</p>


<p>
<img src="https://i.imgur.com/VXyTmhc.png"/>
</p>
<p>
On the Azure Virtual Machines main tab you can see the Virtual Machines (VMs) created. <b>Client-1 and DC-1</b>
</p>

<h4>Set Domain Controller Network Interface Card (NIC) to Static</h4>
<p>During the project we don't want the Domain Control Server/DNS changing IPs due to the <b>Dynamic</b> setting.</p>This may prevent the Client machine from talking to the Domain Control Server/DNS.

<p>
<img src="https://i.imgur.com/4Csx01e.png"/>
</p>
<p>
  <ul>
    <li>Select the <b>Domain Controller (VM) DC-1</b></li>.
    <li>Expand <b>Networking</b> dropdown menu</li>.
    <li>Select <b>Network settings</b></li>
  </ul>
</p>


<p>
<img src="https://i.imgur.com/RP4PEoI.png"/>
</p>
<p>
Select <b>Network Interface.</b>
</p>


<p>
<img src="https://i.imgur.com/eOPIfxQ.png"/>
</p>
<p>
Select <b>ipconfig1.</b>
</p>


<p>
<img src="https://i.imgur.com/9H2WUX2.png"/>
</p>
<p>
Set <b>Allocation</b> to <b>Static</b> and press save.
</p>


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Fillin.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Fillin.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Fillin.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
