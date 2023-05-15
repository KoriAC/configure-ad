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

- Setup resources in Azure
- Ensure connectivity between the client and domain controller
- Install Active Directory
- Create an administrator and normal user account in active directory
- Join client to domain
- Setup remote desktop for non-administrative users on client computer
- Create additional users and attemot to login into client computer with one of the users

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.gyazo.com/1009c9b8331ebe43afe46fd173d30a17.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This is the Microsoft Azure portal homepage and where the resources will be create to implement an active directory.
</p>
<br />

<p>
<img src="https://i.gyazo.com/f2a3545bb7f7bae3568d35d36cc76614.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here a resource group is being created. A resource group can be thought of as a folder.
</p>
<br />

<p>
<img src="https://i.gyazo.com/e8a2060f89f9a203afc7ca028a29f131.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here is where the resource group is going to be named.
</p>
<br />

<p>
<img src="https://i.gyazo.com/a6d3231623dbe0b508dbc85bcabc1899.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The image above shows that the resource group has been successfully created.
</p>
<br />

<p>
<img src="https://i.gyazo.com/c74a52412f660879a4e5477289a3d0c6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here is where the virtual machines will be created. The "Azure virtual machine" option will be selected.
</p>
<br />

<p>
<img src="https://i.gyazo.com/e60db5e26c3ced397b779fd79f07b7a5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The virtual machine here is named "DC-1" which will act as the domain controller.
</p>
<br />

<p>
<img src="https://i.gyazo.com/140212dd82b1671ae52d860760662465.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The virtual machine here is named "Client-1" which will act as the client.
</p>
<br />

<p>
<img src="https://i.gyazo.com/f5e68525976901b4442e038f0ded8618.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here in the image above, both virtual machines have been successfully created.
<br />

<p>
<img src="https://i.gyazo.com/9b9744e0ee04d149139e15079d6e217d.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here we can see that the IP address of DC-1 is dynamic. Therefore, it's important to switch the IP address from dynamic to static. If the server was assigned a dynamic IP address, it would change occasionally, preventing your router from knowing which computer on the network is the server.
</p>
<br />

<p>
<img src="https://i.gyazo.com/0be761e6db23ccc0bfbab1993746f006.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here the IP address has been switched from dynamic to static.
</p>
<br />

<p>
<img src="https://i.gyazo.com/3fe092a85e3cb52bd321d73a595b8ea2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The IP address of DC-1 is being copied so a remote desktop connection can be made.
</p>
<br />

<p>
<img src="https://i.gyazo.com/60602887a211e9085d0cba5ff24ce197.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The credentials that were made earlier are now being used to access the DC-1 virtual machine.
</p>
<br />

<p>
<img src="https://i.gyazo.com/d0e006e787c9fe535ff134c8db384270.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
Similar to DC-1, the same process will be done for Client-1.
</p>
<br />

<p>
<img src="https://i.gyazo.com/857559b4991dcfab97e208b58ca6b601.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here we are logged into Client-1. To start the process of ensuring connectivity, we are going to continuously ping DC-1's private IP address. To do this, we are going open command prompt and type "ping-t". The "Request Timed Out" means that the pinging is being blocked and that we need to access the firewall to change this.
</p>
<br />

<p>
<img src="https://i.gyazo.com/9e1c71b4cbee27f0f96229eeac896b7f.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here we have opened windows defender firewall with advanced security and will attempt to enable some inbound rules. You'll notice the acronym ICMP which is the Internet Control Messaging Protocol is a network layer protocol. It's mainly used to determine whether or not data is reaching it's intended destination.
</p>
<br />

<p>
<img src="https://i.gyazo.com/615178c700a4ca8cacd687449a618c69.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here we can see that the chosen inbound rules have been enabled.
</p>
<br />

<p>
<img src="https://i.gyazo.com/7c5bd17763507beffe34144b783abf37.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
As you can see, when we switch to CLient-1 and observe the command prompt, we are getting a response from DC-1. We can tell by the private IP address.
</p>
<br />

<p>
<img src="https://i.gyazo.com/98939c5af6247cbc6876fc09ded55b51.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here "CTRL + C" was used to stop the continuous pinging.
</p>
<br />

<p>
<img src="https://i.gyazo.com/b8e566ff414e64959e492a25566a8b03.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here we are switching back to DC-1 so we can start the installation process for Active Directory Domain Services.
</p>
<br />

<p>
<img src="https://i.gyazo.com/4e5356fe17d04fe817b59f5838b5ea53.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This is what we'll see when we begin the installation process. We can simply click next.
</p>
<br />

<p>
<img src="https://i.gyazo.com/1acd8f4547f5b7a59a3bfe49c5ff533d.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here we are going to choose the installation type. The top option will be used.
</p>
<br />

<p>
<img src="https://i.gyazo.com/a257ed3e3b3dfcdf42d6a8dbc825e5c0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The server that will be selected will be the virtual machine that we created earlier.
</p>
<br />

<p>
<img src="https://i.gyazo.com/9c2951569396beb86f1df7df91a45876.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The server role that will be chosen is the Active Directory Domain Services (AD DS) becasue this role in particualr uses domain controllers to give network users access to permitted resources through a simple logon process.
</p>
<br />

<p>
<img src="https://i.gyazo.com/21b105bf0b2c7d85fcff3818479c6414.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here we are simply going to click next.
</p>
<br />

<p>
<img src="https://i.gyazo.com/f459dad73bc9c86e5f24d0621bbed00f.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Just like the previous step, we will simply click next
</p>
<br />

<p>
<img src="https://i.gyazo.com/853a0eef77cf45869c98b189d6dd24fd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here we are going to install all of the roles and features for our server.
</p>
<br />

<p>
<img src="https://i.gyazo.com/43ef50042739e5abeaae46f3d1dc2aed.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
As we can see the installation process was a success.
</p>
<br />

<p>
<img src="https://i.gyazo.com/a636acf9ebf4d38406a8bf3784af99f9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After the installation of the roles and features for the server, the next step is start the configuration. We'll start this by clicking on the flag with the exclamation mark encases in a triangle.
</p>
<br />

<p>
<img src="https://i.gyazo.com/f7e1eb29afacc59889ba3b34a4e397d5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We are going to click "Promote this server to a domain controller. A domain controller is a server that manages network and identity security. This is important for user authentication and authorization into IT resources within the domain.
</p>
<br />

<p>
<img src="https://i.gyazo.com/d43d1b2d5af175d4fa7b9686bca3c97a.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
For the deployment configuration tab, we are going to click "Add new forest" and type in a name. An Active Directory forest is the highest level of organization within Active Directory. Each forest shares a single database. 
</p>
<br />

<p>
<img src="https://i.gyazo.com/f44a3b23da7911491d7f67cd42c19194.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In this image, an DSRM (Directory Services Restore Mode) password will be created.
</p>
<br />

<p>
<img src="https://i.gyazo.com/a637d595ca598d53e25a764e7654141c.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here we are simply going to click next.
</p>
<br />

<p>
<img src="https://i.gyazo.com/0e6067f4c3ee0c78c68a8d55ad73a2cf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The image above shows the NETBIOS domain name. The NETBIOS domain name is a unique identifier for a network that allows computers to communicate with each other.
</p>
<br />

<p>
<img src="https://i.gyazo.com/42a2c57bc6cb6ea24cbd8cc17a170c8a.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here we will simply click next.
</p>
<br />

<p>
<img src="https://i.gyazo.com/3564127a06b956c817e6601c08e5bfd8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After reviewing the options, we will click next.
</p>
<br />

<p>
<img src="https://i.gyazo.com/c157d217701edcef95f4ac0d005be985.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
All prerequisite checks passed successfully and now the installation can begin.
</p>
<br />

<p>
<img src="https://i.gyazo.com/d2c24fc5ad51407d0beca1d275f63f50.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 After the virtual machines restarts, we will login with domain name and original credentials
</p>
<br />

<p>
<img src="https://i.gyazo.com/1382ca9dd8d502fa77a3c13a2d6a70f0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In this image above, we will click on "Tools", scroll down and select "Active Directory Users and Computers".
</p>
<br />

<p>
<img src="https://i.gyazo.com/76fd18dd1cffac52a253d731318c5ae0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We will right click on the domain name, scroll down to "New" and select "Organizational Unit". An organizational unit is like a folder.
</p>
<br />

<p>
<img src="https://i.gyazo.com/7ad8f6c1a825ea82bb104fec20d21e98.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The name of this organizational unit will be "_EMPLOYEES", since this is where we are going to generate random users in this organizational unit. An additional organizational unit will be create and will be named "_ADMINS".
</p>
<br />

<p>
<img src="https://i.gyazo.com/248ea97663adba1e1765571385d6ef44.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
As you can see here, we are creating an administrator in the "_ADMINS" organizational unit.
</p>
<br />

<p>
<img src="https://i.gyazo.com/aae96cd25d8ffbfb05be9f44abfc22e4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The image above demonstrates the administrators information being created.
</p>
<br />

<p>
<img src="https://i.gyazo.com/b9c5fe6d6d935ebccfd92a316373d4b0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
