<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>
<p style="text-indent: 2em;">This text is indented.</p><h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
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
<p>
  * Click Create to set up a new Resource Group.<br>
  * Name the Resource Group. I chose <b>Active-Directory-Lab</b>.<br>
  * Select Region: <b>East US 2</b>. Select Region closest to your location.<br>
  

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
<p>
  * Click <b>Create</b> to set up a new <b>Virtual Network</b>.<br>
  * Ensure the correct <b>Resource Group</b> is selected that was created in prior steps.<br>
  * Name the Virtual Network. I chose "<b>Active-Directory-VNet</b>.<br>
  * Choose same <b>Region</b> you selected for Resource Group. I selected <b>East US 2</b>

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
  * Click <b>Create Azure Virtual Machine</b>. <br>
  * Ensure the correct <b>Resource Group</b> is selected. The same Resource Group setup in prior steps. In my case the Resource Group is <b>Active-    
    Directory-Lab</b> <br>
  * Name the Virtual Machine. I chose <b>DC-1</b> <br>
  * Confirm Region: <b>East US 2</b>. Your Region may differ from mine, but be sure it matches the Region you selected through out the project.
</p>
<br />

<p>
<img src="https://i.imgur.com/Bpnyruf.png"/>
</p>
<p>
  * Select <b>Windows Server 2022</b> as the <b>Image</b>. <br>
  * Choose a <b>Size</b> with at least <b>2 vcpus</b>. <br>

</p>
<br />

<p>
<img src="https://i.imgur.com/kL7t6Dw.png"/>
</p>
<p>
  * Create a <b>Username and Password</b>. <br>
  * Click Next for <b>Disks</b>. <br>
  
</p>
<br />

<p>
<img src="https://i.imgur.com/7T2jGOU.png"/>
</p>
<p>
  * Click Next for <b>Networking</b> <br>
  * Confirm <b>Virtual Network</b> you created in prior steps is selected. <b>Active-Directory-VNet</b> <br>
  
</p>
<br />

<p>
<img src="https://i.imgur.com/LRJPxH0.png"/>
</p>
<p>* Click <b>Review + Create</b>, then click <b>Create</b>.</p>
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
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  * On Azure homescreen navigate to <b>Virtual Machine</b> or type in search bar. <br>
  * Click <b>Create Azure Virtual Machine</b>. <br>
  * Ensure the correct <b>Resource Group</b> is selected. The same Resource Group setup in prior steps. In my case the Resource Group is <b>Active-    
    Directory-Lab</b> <br>
  * Name the Virtual Machine. I chose <b>Client-1</b> <br>
  * Confirm Region: <b>East US 2</b>. Your Region may differ from mine, but be sure it matches the Region you selected through out the project.
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
