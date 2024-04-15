<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS) and CGI

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Item 1:
  Have an active account and subscription to Microsoft Azure (Free subscriptions are valid)
- Item 2:
  Create a Resource Group
- Item 3:
  Create a Virtual Network
- Item 4:
  Create a Subnet
- Item 5:
  Create a Virtual Machines (VMs)
  
<h2>Installation Steps</h2>

<p>

![Azure Portal](https://github.com/Onstarva/osticket-prereqs/assets/166679644/78a53463-24df-4809-86c3-547a889d4d7d)

</p>
<p>
First you need to have an account and active subscription on Microsoft Azure. Once you've made an account and subscription with Microsoft Azure. You will want to go to https://portal.azure.com/#home. You should see at the top a few selection choices. Click Vitual Machine tab and hit "create Virtual Machine". 
</p>
<br />

<p>
  
![VM Setup](https://github.com/Onstarva/osticket-prereqs/assets/166679644/ccc232c7-e768-48d5-ab8a-ff9d091afe2e)

</p>
<p>
In Virtual Machine setup. You will first pick your active subscription. Under that create a Resource Group name. Create a Vitual Machine name, pick a region of your choice, Zone of your choose and Image to Windows 10 or 11. For Size, this effects the speed and preformance of your VM so pick accordingly. Create a Username and Password, important to remember these. Then click Review + Create. If all go well everything should be validated and hit Create. You may need to adjust Regions if all Region options are greyed out. At this point, you've created an Resource Group, Virtual Network, subnet and as they're created with the VM. It's important to note that the Size of your VM should be at least 2 vcpu if your running more than one VM at a time.
<br />

<p>

![VM Logged in](https://github.com/Onstarva/osticket-prereqs/assets/166679644/b7acbc60-d695-46d8-99e1-232a007836c2)

</p>
<p>
Go to the VM tab when both VMs are running. Click one VM and copy the Public IP Address. Next go to windows, accessories, Remote Desktop Connection and click it. Paste the copied IP Address and login to your VM with the Username and Password you've created. Hit yes to connect. A windows startup screen will appear similar to starting your original PC. Wait for everything to set it's self up. You should now be on default windows pc screen.
</p>
<br />

</p>

![IIS with CGI](https://github.com/Onstarva/osticket-prereqs/assets/166679644/ac2904af-9ad8-41dc-85e1-b3c249fe1304)

Now we need to setup the IIS (Internet Information Services) to run TicketOs. In your VM you logged into. Go to Windows, Settings, Apps, Programs, Turn Windows Features on or off. When the menu is open, click the box Internet Information Services, expand World Wide Web Services, expand Application Development Features, Checkmark CGI. Next go to Common HTTP Features, Checkmark all of the folder boxes from Default Documents to WebDAV Publishing. Hit OK and it will begin installing IIS with CGI.

</p>

![Folder Installation](https://github.com/Onstarva/osticket-prereqs/assets/166679644/cd03cdfe-29f4-467d-925b-b32ab9098518)

Next you will be installing the file for OsTicket from this directory, https://drive.google.com/drive/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6. First download and install PHP Manager for IIS and Rewrite Module. Create a folder in C drive named PHP. Continue to download and install PHP-7.3.8 zip, VC_redist and MySql from the installation folder. For Mysql hit Typical Setup, launch config (after setup), standard config and password of your choosing. Extract PHP zip into the C/PHP folder you created.

</p>

![IIS config](https://github.com/Onstarva/osticket-prereqs/assets/166679644/b137587e-dc1e-4f32-82c4-b6b1ff34c318)

In the bottom search window type IIS and open IIS as Admin. Now register PHP from within IIS by going to PHP Manager, Register New PHP version, find your C:\PHP and clicking PHP-cgi.exe. Close and reopen IIS as Admin. Now download and install osTicket from the file directory. Extract the files into c:\inetput\wwwroot. Within c:\inetpub\wwwroot, rename "upload" to osTicket. Restart IIS again. Go to PHP Manager, click "Enable or disable an extension". Enable php_imap, php_intl.dll, and php_opcache.dll. From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php, rename "ost-sampleconfig.php" to ost-config.php.
Right click ost-config-> properties-> security-> advanced-> disable inheritance and remove all inheritance. Click apply and okay. Click advanced and Add new Select principals. Type "Everyone" in text space and hit ok. Now check Full control and hit ok. Apply and ok.
</p>

![osTicket installed](https://github.com/Onstarva/osticket-prereqs/assets/166679644/ab55d6b3-c639-4790-89de-e21a601dc2b7)

In PHP Manager left-hand tab, left click osTicket. Go to the right-hand side of PHP Manager and open "Browser *80(http)" and hit continue. Now fill out the Help Desk name, email and passwords of your choosing. Next download and install HeidiSQL from your file installation directory from before. Open HeidiSQL and in the left tab. Hit new session, enter a username and password. Hit open, right click "unnamed"->create new-> Database-> name the database and hit ok. Now go back to the web browser you were in and enter the username, password and database you created in HeidiSQL and hit install now. Now you can click the URLs to login as an Administrator or an End user.
