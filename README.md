<p align="center">
<img src="https://rb.gy/hdy7u" />
</p>

<h1>osTicket - Prerequisites and Installation</h1>
In this tutorial I will outline the prerequisites and installation of the open-source help desk ticketing system osTicket.


<h2>Objectives</h2>

-  More Experience with Azure (I will Create the environment here)
-  Experience as both the administrator AND the user of a ticketing system
-  Gain a better understanding of all parts of ticketing system such as <b>Tickets properties, SLAs, Departments, Permissions</b> and <b>Users</b>.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10 pro

<h2>List of Prerequisites</h2>

- All you need for this lab is the Azure Tenant and Subscription
    
<h2>Installation Steps</h2>

-  Step 1: Create VM1

First thing first, I will create a Research Group (RG-osTicket) in www.portal.azure.com and then create a Virtual Machine(VM1) and Azure automatically assigns me a virtual network and subnet. I chose Windows 10 as OS and 2Vcpu for my VM1 and created a username. Just a reminder that I created VM1 under RG-osTicket.

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/84f84161-9647-4480-b518-ea73ed24b20b)

-  Step 2: Connect to VM1 using RDP

I connected to VM1 via Remote Desktop Connection using VM1's public IP address(20.51.185.57) from the Azure Portal. Then I am prompted to login and now have access to VM1. I use Remote Desktop Connection because my PC runs Windows OS but if you happen to be on a MAC I would recommend to download and Install Microsoft Remote Desktop first.

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/0dc6df39-2748-4f99-bbf5-e431e98f97ca)

-  Step 3: Install and Enable <b>IIS</b> in Windows with CGI and common HTTP features

Internet Information Service(IIS) is essentially a web server that allows our computer to serve up websites because osTicket runs out of a website. Go to control panel -> programs -> Turn windows features on and off. Then chech up this boxes by allowing: World Wide Web Services -> Application Development Features -> CGI -> Common HTTP Features.

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/522227e8-ff10-4ff2-b6f9-1b321fb6af17)

-  Step 4: Confirm IIS is installed

After enabling IIS in Windows WITH CGI, Common HTTP Features and IIS Management Console, I open a web browser in VM1 and type 127.0.0.1 to check if my web server is up and I have a result looking like this 

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/9d293999-5a5a-42be-a028-94fa69de494d)

-  Step 5: Download and Install PHP manager for IIS and other programs

From the <a href="https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6">Installation Files</a>, 1->download and install <b>PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)</b>. 2->Download and install the <b>Rewrite Module (rewrite_amd64_en-US.msi)<b>. Create the directory C:\PHP. 3->Download and install <b>PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip)</b> and unzip the contents into C:\PHP created previously. 4->Download and install <b>VC_redist.x86.exe</b>. 5->download and install <b>MySQL 5.5.62 (mysql-5.5.62-win32.msi).</b> When isntalling MySQL I chose these configurations Typical Setup -> Launch Configuration Wizard (after install) -> Standard Configuration.

-  Step 6: Register PHP from within IIS

First, I open IIS as an admin by typing typing IIS in window search and right click(run as an administrator); then double click on PHP manager -> Register new PHP version. I choose PHP-cgi from browser. After that Reload IIS (Open IIS, Stop and Start the server)

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/d320ba0a-e8ee-410e-8093-c6eeeef7d932)

-  Step 7: Install osTicket v1.15.8

Download osTicket from the <a href="https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6">Installation Files</a>
I extract and copy “upload” folder to c:\inetpub\wwwroot. Within c:\inetpub\wwwroot, Rename “upload” to “osTicket”.
I go back to IIS and reload the server, then Go to sites -> Default -> osTicket.   On the right, click “Browse *:80”.  I have this image displaying which means osTicket is working💪

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/a5f059b0-272a-4e02-a73c-dcbec34d1e26)

<p>
I Note that some extensions are not enabled. Go back to IIS, sites -> Default -> osTicket. Double-click PHP Manager. Click “Enable or disable an extension”...Enable: php_imap.dll, Enable: php_intl.dll, Enable: php_opcache.dll. I refresh the osTicket site in my browse, observe the changes
</p>

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/510b68b5-d825-4dd6-8050-26936cda26d6)

-  Step 8: More Configurations

<b>Rename: ost-config.php</b> From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php to C:\inetpub\wwwroot\osTicket\include\ost-config.php. <b>Assign Permissions: ost-config.php</b> Disable inheritance -> Remove All New Permissions -> Everyone -> All

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/eb1a015a-b647-4ee0-bd5f-144f7591034d)

<p>
Continue Setting up osTicket in the browser (click Continue) Name Helpdesk, Default email (receives email from customers)
</p>

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/141a9e3a-7bea-46f8-8ddc-99e1d5f1940d)

-  Step 9: download and install HeidiSQL

From the <a href="https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6">Installation Files</a>, download and install HeidiSQL. Open Heidi SQL Create a new session, Connect to the session, Create a database called “osTicket”. Basically, Heidi SQL allows me to connect to mySQL server and I will setup a database that the osTicket is going to use.

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/b45aab6c-8e3c-4b1e-bf07-7cefb35026af)

-  Step 10: Continue Setting up osticket in the browser

I set up osTicket in the browser by using the username and password. MySQL Database: osTicket, MySQL Username: root,Click “Install Now!”.                                   CONGRATULATION!!!!!!                     I was able to create osTicket

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/f7753db7-d233-4127-96d0-4931a83f58f7)

-  Step 11: Clean Up and Go Live

I go to my C drive and Delete: C:\inetpub\wwwroot\osTicket\setup. Then Set Permissions to “Read” only: C:\inetpub\wwwroot\osTicket\include\ost-config.php.  Now I can browse to my Helpdesk Login Page

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/8e205001-0013-410a-8459-b327518f3c72)

I can also browse to my End Users osTicket

![image](https://github.com/danielbangm/osticket-prereqs/assets/22795502/cd8a296a-bae0-4c05-8bce-33e3c1174685)
