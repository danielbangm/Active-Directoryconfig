<p align="center">
<img src="https://rb.gy/hdy7u" />
</p>

<h1>Active Directory - Prerequisites and Installation</h1>

In this tutorial I will implement Active directory in Azure cloud by creating 2 Virtual Machines(one acting like a server and the other one like the client) and then use use Active Directory to set up a bunch of users.

<h2>Objectives</h2>

-  More Experience with Azure (I will Create the environment here)
-  Understanding of the Domain Controler and DNS
-  Gain a better understanding of all parts of Active Directory such resetting passwords and setting up users.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Virtual Machine(DC-1)
- Virtual Machine(client-1)
- Remote Desktop

<h2>Operating Systems Used</h2>

-  Windows Server 2022
-  Windows 10 pro

<h2>List of Prerequisites</h2>

-  All you need for this lab is the free Azure Tenant and Subscription

<h2>Installation steps</h2>

-  Step 1: Setup Ressources in Azure

I am going to wwww.portal.azure.com and create a Domain Controller Virtual Machine(DC-1) with windows server 2022 installed in it and another Virtual Machine(client-1) with windows 10 pro installed in it. I put both VM in the same ressource group(RG-AD). Automatically, azure assigns my VMs virtual private network and subnet. I ensure that both DC-1 and client-1 are in the same domain
![image](https://github.com/danielbangm/configure-ad/assets/22795502/64f6212d-f0bc-4de5-8299-431f36d936bf)
![image](https://github.com/danielbangm/configure-ad/assets/22795502/c907f100-b8a3-4b64-970b-b2c55c2b0b0b)

-  Step 2: Set Domain Controller's NIC Private IP address to be static

Because I don't want my Domain Controller IP address to be changing automatically, I am going to set it up to be static. I click on DC-1 -> Networking -> Network Interface -> IP configurations -> choose static on private IP address. I just set up my Domain Controller private IP address to be static from now on.
![image](https://github.com/danielbangm/configure-ad/assets/22795502/2459439d-9850-4d35-acb5-5905ecbc3482)

-  Step 3: Ensure Connectivity between the client and Domain Controller

I connect to client-1 Virtual Machine through Remote Desk Connection and I will try to ping DC-1's address with a perpetual(-t) ping to see if there is a connection established. I see that the ping -t 10.0.0.4 is timeout probably because DC-1 Firewall is blocking ICMPv4 traffic
![image](https://github.com/danielbangm/configure-ad/assets/22795502/ed15f1ee-52a4-4fa3-9252-61e6c882e090)

To solve this issue, I am going to log into DC-1 through Remote Desktop Connection using DC-1 Public IP address and enable ICMPv4 in the local Windows Firewall. Go to Windows Defender Firewall with advanced security -> Inbound Rules -> Protocol -> ICMPv4 -> Enable Rules.
![image](https://github.com/danielbangm/configure-ad/assets/22795502/676ced27-4310-4f7b-b5f4-edbe460c3034)

Now I going back to client-1 and notice that the ping -t 10.0.0.4 starts working after I enabled the firewall rules in DC-1
![image](https://github.com/danielbangm/configure-ad/assets/22795502/039b13a5-9efa-4dbc-b5d5-d5923128c1ed)

-  Step 4: Install Active Directory

I log in to DC-1 and install Active Directory. Go to Server Manager -> Add Roles and Features -> Active Directory Domain Services -> Install
![image](https://github.com/danielbangm/configure-ad/assets/22795502/cd87f549-b47c-43cb-9f26-df57d6c3fe81)

Now I am going to promote this server as a Domain Controller and Setup a new forest as daniel.com. To do so I just click on the upper right conner of the previous snippet on that yellow triangle. When everything is done it automatically logs me out. Because DC-1 is now a Domain Controller, in order to log in I have to use a different username which is <b>daniel.com\labuser</b>

