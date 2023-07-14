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

I am going to create a Domain Controller Virtual Machine(DC-1) with windows server 2022 installed in it and another Virtual Machine(client-1) with windows 10 pro installed in it. I put both VM in the same ressource group(RG-AD). Automatically, azure assigns my VMs virtual private network and subnet. I ensure that both DC-1 and client-1 are in the same domain
![image](https://github.com/danielbangm/configure-ad/assets/22795502/64f6212d-f0bc-4de5-8299-431f36d936bf)
![image](https://github.com/danielbangm/configure-ad/assets/22795502/5f9b214b-6e64-40b8-8f06-b375687b01db)

-  Step 2: Set Domain Controller's NIC Private IP address to be static

Because I don't want my Domain Controller IP address to be changing automatically, I am going to set it up to be static. I click on DC-1 -> Networking -> Network Interface -> IP configurations -> choose static on private IP address. I just set up my Domain Controller private IP address to be static from now on.
![image](https://github.com/danielbangm/configure-ad/assets/22795502/2459439d-9850-4d35-acb5-5905ecbc3482)

