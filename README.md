<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
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
For a detailed explanation of creating Virtual Machines, please visit the project [Creating Virtual Machines in Azure Portal](https://github.com/tylergehm/vm)
