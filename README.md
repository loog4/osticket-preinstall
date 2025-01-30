<p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>Implementing a Help Desk Ticketing System (osTicket) using Azure Virtual Machines</h1>
This tutorial outlines the prerequisites and installation of the open-source helpdesk ticketing system osTicket within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

<ul>
<li>Microsoft Azure</li>
<li>Virtual Machine</li>
<li>osTicket Installation Files</li>
</ul>



<h2>Intial Install</h2>
<h3>Create the Azure Virtual Machine</h3>
<p>Create the Azure VM with the following requirements below:</p>

- Windows 10, 4 vCPUs
- Name: osticket-vm
- Username: labuser
- Password: osTicketPassword1!

![1](img/1.jpg)

<h3>Log into the Virtual Machine via Remote Desktop</h3>

![2](img/2.jpg)

<h3>Download the osTicket-Installation-Files.zip and unzip it onto your desktop.</h3>

[osTicket-Installation-Files.zip](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD)
<p>We will use the files in this folder to install osTicket and some of the dependencies.</p>
<p> The folder should be called “osTicket-Installation-Files”>

![3](img/3.jpg)

<h3>Install and Enable IIS with CGI
<p>Navigate to Control Panel --> Programs --> Programs and Features</p>
<p>Make sure to the following boxes are checked</p>

![4](img/4.jpg)

<h4>You can test to see if this feature is working by going to your browser and typing 127.0.0.1</p>

![5](img/5.jpg)

<h3>Install PHP Manager for IIS</h3>
<p>From the “osTicket-Installation-Files” folder, install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)</p>

![6](img/6.jpg)

<h3>Install the Rewrite Module</h3>
<p>From the “osTicket-Installation-Files” folder install the Rewrite Module (rewrite_amd64_en-US.msi)</p>

![7](img/7.jpg)

<h3>Create the PHP directory</h3>
<p>Navigate to the system's C: drive and create a directory named "PHP"</p>

![8](img/8.jpg)

<h3>Unzip PHP files into the folder</h3>
<p>From the “osTicket-Installation-Files” folder, unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into the “C:\PHP” folder</p>

![9](img/9.jpg)

<h3>Install VC Redist Dependency</h3>
<p>From the “osTicket-Installation-Files” folder, install VC_redist.x86.exe.</p>

![10](img/10.jpg)

<h3>Install MySQL</h3>
<p>From the “osTicket-Installation-Files” folder, install MySQL 5.5.62 (mysql-5.5.62-win32.msi)</p>

- Typical Setup ->
- Launch Configuration Wizard (after install) ->
- Standard Configuration ->
- Username: root
- Password: root

![11](img/11.jpg)
![12](img/12.jpg)

![13](img/13.jpg)
![14](img/14.jpg)


<h3>Open IIS as an Admin</h3>
<p>Type IIS Manager into the Search bar and open it as Administrator</p>

![15](img/15.jpg)

<h3>Register PHP from within IIS</h3>
<p>Click on PHP Manager and Register PHP (PHP Manager -> C:\PHP\php-cgi.exe)</p>

![16](img/16.jpg)

<h3>Reload IIS (Open IIS, Stop and Start the server)</h3>

![17](img/17.jpg)

<h3>Install osTicket</h3>

- From the “osTicket-Installation-Files” folder, unzip “osTicket-v1.15.8.zip” 
- copy the “upload” folder into “c:\inetpub\wwwroot”
- Within “c:\inetpub\wwwroot”, Rename “upload” to “osTicket”

![18](img/18.jpg)

<h3>Reload IIS (Open IIS, Stop and Start the server)</h3>

![17](img/17.jpg)

<h3>Navigate to osTicket in IIS</h3>
<p>Go to sites -> Default -> osTicket.  On the right, click “Browse *:80”</p>

![19](img/19.jpg)
![20](img/20.jpg)


<h3>Enable required extensions for osTicket</h3>\
<p>osTicket still requires some extensions that we need to enable in IIS</p>

![21](img/21.jpg)

- Go back to IIS, sites -> Default -> osTicket
- Double-click PHP Manager
- Click “Enable or disable an extension”

![22](img/22.jpg)

  - Enable: php_imap.dll
  - Enable: php_intl.dll
  - Enable: php_opcache.dll

![23](img/23.jpg)

- Refresh the osTicket site in your browser, observe the changes

![24](img/24.jpg)

<h3>Finishing Touch</h3>
<p>Rename: ost-config.php

- From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
- To: C:\inetpub\wwwroot\osTicket\include\ost-config.php

![25](img/25.jpg)
![26](img/26.jpg)

<p>Assign Permissions: ost-config.php</p>

- Disable inheritance -> Remove All
- New Permissions -> Everyone -> All

![27](img/27.jpg)
![28](img/28.jpg)

<h2>Intial osTicket Install</h2>
<h3>Continue Setting up osTicket in the browser</h3>

- Name Helpdesk
- Default email (receives email from customers)

<p>Choose any name and email you want.</p>

![29](img/29.jpg)

<h3>Install HeidiSQL</h3>
<p>From the “osTicket-Installation-Files” folder, install HeidiSQL.</p>

![30](img/30.jpg)

- Open Heidi SQL
- Create a new session, root/root
- Connect to the session

![31](img/31.jpg)

- Create a database called “osTicket”

![32](img/32.jpg)

<h3>Continue osTicket Setup</h3>
<p>Continue Setting up osTicket in the browser</p>

- MySQL Database: osTicket
- MySQL Username: root
- MySQL Password: root
- Click “Install Now!”

![33](img/33.jpg)

<h2> osTicket is now Installed</h2>
<h3>Congratulations, osTicket has now installed with (hopefully) no errors</h3>

![34](img/34.jpg)
![35](img/35.jpg)

- Login Page: http://localhost/osTicket/scp/login.php 
- End User Login Page: http://localhost/osTicket/ 

<h3>Clean Up</h3>

- Delete: C:\inetpub\wwwroot\osTicket\setup
- Set Permissions to “Read” only: C:\inetpub\wwwroot\osTicket\include\ost-config.php

![36](img/36.jpg)
