<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Building  osTicket Support Ticketing System from scratch</h1>
osTicket is a widely-used open-source support ticketing system that streamlines customer service by routing inquiries from email, web forms, and phone calls into a simple, multi-user web-based platform, enabling agents to efficiently track, prioritize, and resolve issues while automating workflows like ticket assignment and notifications. 
</p>
Ticketing systems, in general, are essential software tools for help desks and IT support teams, functioning as centralized repositories to log user requests, categorize problems, assign tasks to responders, monitor progress, and maintain detailed audit trails—ultimately improving response times, reducing email clutter, and enhancing overall service quality in enterprise environments. 
</p>
This Azure project focuses on deploying and configuring osTicket on a virtual machine, involving the setup of IIS with CGI support, PHP, MySQL database, and necessary extensions like IMAP and internationalization. After extracting installation files, renaming configuration templates, adjusting file permissions, and creating a dedicated database via tools like HeidiSQL, a web-based installer is used to launch a functional helpdesk portal. 

<h2>Video Demonstration</h2>

- ### [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 11 Pro (21H2)
- Windows 11 Home (host machine)

<h2>Installation Steps</h2>

- Step 1 - Create a Virtual Machine
- Step 2 - Download Os Ticket installation files
- Step 3 - Enable IIS in Windows with CGI
- Step 4 - Install PHP Manager for IIS
- Step 5 - Install Rewrite Module
- Step 6 - Install VC_redist.x86
- Step 7 - Install MySQL
- Step 8 - Register PHP from within IIS
- Step 9 - Install OsTicket
- Step 10 - Enable extensions
- Step 11 - Assign permissions
- Step 12 - Set up OsTicket in web browser
- Step 13 - Install HeidiSQL
- Step 14 - Complete installation

<h2>Step 1 - Create a Virtual Machine </h2>
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/16e18249-cb5b-4444-b89f-41280792bc93" /> </p>

This project begins by creating a Windows 11 Pro virtual machine inside Microsoft Azure. </p>


For a detailed explanation of creating Virtual Machines, please visit the project [Creating Virtual Machines in Azure Portal](https://github.com/tylergehm/vm)

<img width="1487" height="538" alt="image" src="https://github.com/user-attachments/assets/e6fe8c8c-0536-4ad1-a573-b9b150f88322" /> </p>
<img width="542" height="303" alt="image" src="https://github.com/user-attachments/assets/d0fdebd6-ccbb-4733-9bd2-6889ea126e1b" /> </p>

After the VM has been created, the Public IP address will be used to log into the VM using Remote Desktop Connection </p>

Step 2 - Download Os Ticket installation files

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/67f016c5-fa53-4338-a29c-2ad76eae61d7" /> </p>

Once inside the Windows 11 VM, a zipfile containing all the installation files was opened. </p>

Here are the links to download all files used for the osTicket installation process: </p>

  - [osTicket](https://osticket.com/download/) - The actual help-desk application files (PHP code, templates, and installer) you upload to your web server.
  - [HeidiSQL](https://www.heidisql.com/download.php) - A lightweight GUI tool to connect to MySQL, create the osTicket database, and manage its schema.
  - [MySQL](https://www.mysql.com/downloads/) - The database server that stores all tickets, users, settings, and attachments.
  - [PHP](https://www.php.net/releases/index.php) - The scripting language interpreter that runs osTicket’s backend logic on the server.
  - [PHP Manager for IIS](https://www.iis.net/downloads/community/2018/05/php-manager-150-for-iis-10) - A simple IIS plugin to register PHP, switch versions, and enable required extensions like mysqli and gd.
  - [IIS URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) - An IIS module that translates clean URLs (e.g., /open) into the actual PHP scripts
  - [Visual Studio C++ Redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#latest-supported-redistributable-version) - System-level runtime libraries required for PHP and MySQL to execute properly on Windows. </p>

osTicket is a PHP help-desk application that needs a web server, PHP runtime, and MySQL database to function. On Windows with IIS, the listed downloads provide every required component to build a complete, working environment from scratch. </p>

<h2>Step 3 - Enable IIS in Windows with CGI</h2>


