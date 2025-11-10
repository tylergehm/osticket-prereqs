<p align="center">
  <img src="https://raw.githubusercontent.com/tylergehm/post-install-config/main/osticketlogo.jpg" alt="GitHub banner" style="max-width:100%;height:auto;" />
</p>

<h1>osTicket - Building  osTicket Support Ticketing System from scratch</h1>
osTicket is a widely-used open-source support ticketing system that streamlines customer service by routing inquiries from email, web forms, and phone calls into a simple, multi-user web-based platform, enabling agents to efficiently track, prioritize, and resolve issues while automating workflows like ticket assignment and notifications. 
</p>
Ticketing systems, in general, are essential software tools for help desks and IT support teams, functioning as centralized repositories to log user requests, categorize problems, assign tasks to responders, monitor progress, and maintain detailed audit trails—ultimately improving response times, reducing email clutter, and enhancing overall service quality in enterprise environments. 
</p>
This Azure project focuses on deploying and configuring osTicket on a virtual machine, involving the setup of IIS with CGI support, PHP, MySQL database, and necessary extensions like IMAP and internationalization. After extracting installation files, renaming configuration templates, adjusting file permissions, and creating a dedicated database via tools like HeidiSQL, a web-based installer is used to launch a functional helpdesk portal. 

<h2>Video Demonstration</h2>

- ### [YouTube: osTicket - Building osTicket Support Ticketing System from scratch](https://youtu.be/3rf6qRmcQwg)

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
- Step 5 - Install IIS URL Rewrite Module
- Step 6 - Place PHP files into the “C:\PHP” folder
- Step 7 - Install Microsoft Visual Studio C++ Redistributable
- Step 8 - Install MySQL
- Step 9 - Register PHP from within IIS
- Step 10 - Install osTicket
- Step 11 - Enable extensions
- Step 12 - Rename ost-config.php
- Step 13 - Assign permissions
- Step 14 - Set up osTicket in web browser
- Step 15 - Install HeidiSQL
- Step 16 - Complete installation

<h2>Step 1 - Create a Virtual Machine </h2>
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/16e18249-cb5b-4444-b89f-41280792bc93" /> </p>

This project begins by creating a Windows 11 Pro virtual machine inside Microsoft Azure. </p>


For a detailed explanation of creating Virtual Machines, please visit the project [Creating Virtual Machines in Azure Portal](https://github.com/tylergehm/vm)

<img width="1487" height="538" alt="image" src="https://github.com/user-attachments/assets/e6fe8c8c-0536-4ad1-a573-b9b150f88322" /> </p>
<img width="542" height="303" alt="image" src="https://github.com/user-attachments/assets/d0fdebd6-ccbb-4733-9bd2-6889ea126e1b" /> </p>

After the VM has been created, the Public IP address will be used to log into the VM using Remote Desktop Connection </p>

Step 2 - Download Os Ticket installation files

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/67f016c5-fa53-4338-a29c-2ad76eae61d7" /> </p>

Once inside the Windows 11 VM, a zipfile containing all the installation files was extracted. </p>

Here are the links to download all files contained in the installation folder shown on VM screenshot: </p>

  - [osTicket](https://osticket.com/download/) - The actual help-desk application files (PHP code, templates, and installer) you upload to your web server.
  - [HeidiSQL](https://www.heidisql.com/download.php) - A lightweight GUI tool to connect to MySQL, create the osTicket database, and manage its schema.
  - [MySQL](https://www.mysql.com/downloads/) - The database server that stores all tickets, users, settings, and attachments.
  - [PHP](https://www.php.net/releases/index.php) - The scripting language interpreter that runs osTicket’s backend logic on the server.
  - [PHP Manager for IIS](https://www.iis.net/downloads/community/2018/05/php-manager-150-for-iis-10) - A simple IIS plugin to register PHP, switch versions, and enable required extensions like mysqli and gd.
  - [IIS URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) - An IIS module that translates clean URLs (e.g., /open) into the actual PHP scripts
  - [Visual Studio C++ Redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#latest-supported-redistributable-version) - System-level runtime libraries required for PHP and MySQL to execute properly on Windows. </p>

osTicket is a PHP help-desk application that needs a web server, PHP runtime, and MySQL database to function. On Windows with IIS, the listed downloads provide every required component to build a complete, working environment from scratch. </p>

<h2>Step 3 - Enable IIS in Windows with CGI</h2>

IIS (Internet Information Services) is Microsoft’s built-in web server for Windows. IIS is enabled with CGI because osTicket runs on PHP, and IIS needs CGI to execute PHP scripts. Without it, the osTicket site will show only code or errors. </p>

CGI (Common Gateway Interface) lets a web server like IIS run external programs (like PHP) to generate dynamic pages. PHP is the scripting language osTicket is written in—CGI tells IIS how to execute PHP files and return HTML to the browser. </p>

<img width="1914" height="1072" alt="image" src="https://github.com/user-attachments/assets/896ed728-9834-4f51-b09e-1ba7410eb462" /> </p>

The process begins by typing "Windows Features" in the search box next to the Windows icon. Click on "Turn Windows features on or off". </p>

<img width="543" height="485" alt="image" src="https://github.com/user-attachments/assets/e1ea871b-879d-463e-8440-a130c32453e9" /> </p>

Inside Windows Features, the first step is to check the box next to "Internet Information Services" to turn IIS on. </p>

<img width="549" height="493" alt="image" src="https://github.com/user-attachments/assets/18c384fa-4b87-4e05-8c7f-c8d6c786c323" /> </p>

Next, click the + sign next to "Internet Information Services" to expand the folder. Then expand the "World Wide Web Services" folder and expand "Application Development Features" folder. Check the box next to "CGI", then click "OK" to begin the IIS with CGI installation. </p>

<img width="758" height="628" alt="image" src="https://github.com/user-attachments/assets/1bb7ae98-5c3c-4eeb-a6b1-5e91e374e1b7" /> </p>

With IIS and CGI enabled, the computer can now serve web pages and run PHP scripts. It listens on port 80 (HTTP), accepts browser requests, and executes dynamic code via CGI, making it a functional web server ready for osTicket. </p>

<h2>Step 4 - Install PHP Manager for IIS</h2>

<img width="611" height="501" alt="image" src="https://github.com/user-attachments/assets/440c7b97-ec76-4f89-958b-92e23c8cdef2" />

For the next step, the installation for PHP Manager will begin. PHP Manager for IIS is a GUI tool inside IIS that lets you easily register PHP, switch versions, and enable extensions (like mysqli for MySQL) without editing config files. It is essential for osTicket to run properly. </p>

<img width="611" height="502" alt="image" src="https://github.com/user-attachments/assets/0f263b7b-6449-4005-bfd0-9cf13b24eca2" /> </p>

PHP Manager for IIS has been successfully installed. </p>

<h2>Step 5 - Install IIS URL Rewrite Module</h2>

<img width="605" height="475" alt="image" src="https://github.com/user-attachments/assets/fbb7dcb5-db1f-4189-8a68-7da1a99511fe" /> </p>

Now, the IIS URL Rewrite Module installation begins. The IIS URL Rewrite Module enables clean, user-friendly URLs in osTicket by routing requests to the correct PHP scripts. This is required for the ticketing site to function and navigate properly. </p>

<img width="602" height="472" alt="image" src="https://github.com/user-attachments/assets/44eff92c-e9b4-471c-8da8-fd6da6c234ee" /> </p>

The IIS URL Rewrite Module has been succesfully installed. </p>

<h2>Step 6 - Place PHP files into the “C:\PHP” folder</h2>

<img width="1399" height="731" alt="image" src="https://github.com/user-attachments/assets/50dade12-d988-4ba8-9860-fcda513c1fe3" /> </p>
The first step in this next installation will be to create a new folding on the C:\ drive called "PHP". </p>

<img width="1239" height="720" alt="image" src="https://github.com/user-attachments/assets/b975ccca-22c6-4d7a-863e-0dcd74b21abd" /> </p>

Since the PHP files are in a zip folder, the files will be extracted into the C:\PHP folder. This is done by right-clicking on the zip file and clicking on "Extract All..." </p>

<img width="697" height="577" alt="image" src="https://github.com/user-attachments/assets/46a6749d-8f86-46af-aa57-7296f2d6894c" /> </p>

The destination for the extraction will be "C:\PHP". </p>

<img width="1401" height="713" alt="image" src="https://github.com/user-attachments/assets/7e3902da-77b4-49d2-b03b-2a73657cdfe9" /> </p>

The files were successfully extracted to the C:\PHP folder. </p>
Extracting PHP files to C:\PHP creates a dedicated folder for the PHP runtime. This keeps all PHP binaries organized and ready for IIS (via PHP Manager) to register and run osTicket scripts. </p>

<h2>Step 7 - Install Microsoft Visual Studio C++ Redistributable</h2>

<img width="592" height="362" alt="image" src="https://github.com/user-attachments/assets/13d3f701-b91c-4f4b-9cb0-b21fb4153c94" /> </p>

The next installation will be for the Microsoft Visual Studio C++ Redistributable. The Visual C++ Redistributable supplies runtime libraries that PHP and MySQL binaries need to run on Windows - without it, PHP crashes or fails to start. </p>

<img width="596" height="365" alt="image" src="https://github.com/user-attachments/assets/7c54bac1-0e69-449c-b283-7447eb6865ea" /> </p>

Installation was successful. </p>

<h2>Step 8 - Install MySQL</h2>

<img width="609" height="479" alt="image" src="https://github.com/user-attachments/assets/d22db185-c580-45d5-a82e-6bdc64080ade" />

This process will begin by installing MySQL Server. MySQL Server is the database engine that stores all osTicket data—tickets, users, settings, and attachments. Without it, osTicket has nowhere to save information and won’t work.

<img width="606" height="473" alt="image" src="https://github.com/user-attachments/assets/62a194e0-d198-4e0d-88d9-df3d22d7ac7a" /> </p>

Once the installation has finished, check the box to launch the MySQL instance configuration wizard. The MySQL Instance Configuration Wizard sets up the database service, root password, and port—required so osTicket can securely connect and create its database tables. </p>

<img width="617" height="466" alt="image" src="https://github.com/user-attachments/assets/5e3a4f49-2538-4521-b6e1-c562ac603299" /> </p>

<img width="613" height="475" alt="image" src="https://github.com/user-attachments/assets/61f14b23-567a-4986-8f2b-5d44e77cae9c" /> </p>

Select standard configuration. </p>

<img width="621" height="467" alt="image" src="https://github.com/user-attachments/assets/654cedd8-b024-4b91-8e43-0eba4239b85b" /> </p>

Configuration wizard has completed and MySQL has been succesfull installed. </p>

<h2>Step 9 - Register PHP from within IIS</h2>

<img width="962" height="904" alt="image" src="https://github.com/user-attachments/assets/7a07aec0-45bc-4ad1-9faa-b672b4f5b8f1" />

Registering PHP in IIS tells the web server where php-cgi.exe is and how to run PHP files—without this, IIS can’t process osTicket’s code and will show errors or blank pages. Essentially, this is telling the web server where PHP is on the computer. </p>

To begin, type "IIS" in the Windows search box and right-click on it to "Run as administrator". </p>

<img width="1414" height="726" alt="image" src="https://github.com/user-attachments/assets/50309692-0f9e-4d45-a92a-693d81dd8c80" /> </p>

Inside the IIS Manager, open "PHP Manager". </p>

<img width="1407" height="719" alt="image" src="https://github.com/user-attachments/assets/50fc4e3a-fc6d-4f24-95b8-abb7065734da" /> </p>

Click the link "Register new PHP version". </p>

<img width="635" height="274" alt="image" src="https://github.com/user-attachments/assets/59f6168d-01cc-43e6-b341-84090596d0a7" /> </p>

<img width="1421" height="856" alt="image" src="https://github.com/user-attachments/assets/02b86a0f-f0d0-4446-9cb8-3b056738df93" /> </p>

In the Register New PHP Version box, click the "..." to search for "php-cgi". This executable file is located in the C:\PHP folder. </p>

<img width="1422" height="730" alt="image" src="https://github.com/user-attachments/assets/1e2692de-833d-4287-bfc4-dddc0698ed15" /> </p>

The PHP-cgi file is now linked. </p>

<img width="1417" height="725" alt="image" src="https://github.com/user-attachments/assets/730f921e-e1a6-4d8d-95c4-a02a8425f05a" /> </p>

Next, click on "osticket-vmd (osticket-vmd\)" inside the PHP Manager. Under actions, on the right side, click on "Stop" under Manage Server. Once IIS has stopped, click "Start". </p>

Stopping and restarting IIS applies the new PHP registration, reloads php-cgi.exe, and ensures IIS uses the correct PHP version. </p>

<h2>Step 10 - Install osTicket</h2>

<img width="1410" height="733" alt="image" src="https://github.com/user-attachments/assets/bfe3034b-ae1f-40d7-a3fc-332a9718f577" />

Now osTicket will be installed. To begin, extract the osTicket folder from it's zip file. </p>

<img width="1919" height="1078" alt="image" src="https://github.com/user-attachments/assets/3cb4d771-0834-4032-8c5e-f0b3ad602ead" /> </p>

Once extracted, the "upload" folder is going to be moved into C:\inetpub\wwwroot folder. </p>

<img width="1394" height="736" alt="image" src="https://github.com/user-attachments/assets/4ff9d7e4-232a-4784-a77b-785d04e6ff11" /> </p>

Once the "upload" folder has been moved, it is renamed "osTicket" inside the C:\inetpub\wwwroot folder. </p>
This is placing osTicket's web files (the upload folder) into IIS's default web root (C:\inetpub\wwwroot\osTicket) so the server can access them via http://localhost/osTicket. </p>

<img width="1417" height="725" alt="image" src="https://github.com/user-attachments/assets/730f921e-e1a6-4d8d-95c4-a02a8425f05a" /> </p>

Return to IIS Manager and Stop then Start the IIS Server again. Restarting IIS ensures the site loads fresh and is ready for the browser-based setup.</p>

<img width="1418" height="727" alt="image" src="https://github.com/user-attachments/assets/b9b3ebfa-951f-4177-b447-535fe9c9e929" />

Click the drop-down arrow next to "osticket-vmd" then continue to expand the folders Sites > Default Website > then click on osTicket. On the right side, click "Browse*:80 (http)" under Manage Folder. </p>

*Browse :80 (http) opens your default browser to http://localhost/osTicket (port 80) so you can start the web-based osTicket installer. It tests that IIS is serving the site correctly. </p>

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/486fdc83-39f5-4e73-af70-767909357028" /> </p>

The osTicket installer has correctly loaded. Notice the red Xs that indicate multiple extensions are not open. The next step will correct this and enable the extensions required for this project. </p>

<img width="1414" height="728" alt="image" src="https://github.com/user-attachments/assets/0183250a-c9d5-4459-99cd-ce2ee43ba822" /> </p>

Return to the IIS Manager and open PHP Manager in the osTicket folder. </p>

<img width="1414" height="729" alt="image" src="https://github.com/user-attachments/assets/a4e370c7-0dc0-4659-a324-895867bdd45f" /> </p>

Click on the link "Enable or disable an extension". </p>

<img width="1415" height="727" alt="image" src="https://github.com/user-attachments/assets/023b5f85-dc15-4c3b-8a03-e9c2d62b76a8" />


Enable the extensions "php_imap.dll", "php_inti.dll", "php_opcache.dll". This is done by clicking on each extension, the clicking "Enable" on the right side of the PHP Manager. </p>

  - php_imap.dll: Lets osTicket fetch emails from mail servers to auto-create tickets.
  - php_intl.dll: Handles language formatting, time zones, and translations.
  - php_opcache.dll: Speeds up PHP by caching compiled scripts in memory. </p>

<img width="1005" height="883" alt="image" src="https://github.com/user-attachments/assets/8b1430ed-6c22-4c57-a8fb-a0e7537cb528" /> </p>

Refreshing the osTicket Installer web page displays that "PHP IMAP Extension" and "Intl Extension" have been enabled. </p>

<h2>Step 12 - Rename ost-config.php</h2>

In this step, a file on the harddrive that osTicket uses to make configurations will be renamed. </p>

<img width="1406" height="740" alt="image" src="https://github.com/user-attachments/assets/a7a906b6-60d7-4c93-97ee-9ff439a19a3a" /> </p>

Return to the C:\inetpub\wwwroot folder and open osTicket folder. </p>

<img width="1394" height="736" alt="image" src="https://github.com/user-attachments/assets/bf030c80-d15c-40ed-adfc-d921020d704f" /> <p>

Inside the osTicket folder, open the folder "include" and find the file "ost-sampleconfig.php". </p>

<img width="778" height="58" alt="image" src="https://github.com/user-attachments/assets/3d4f5224-761a-480c-957b-6b8df21dbdef" /> </p>

Rename the file "ost-config.php" </p>

<h2>Step 13 - Assign permissions</h2>

<img width="1398" height="736" alt="image" src="https://github.com/user-attachments/assets/3966b08a-e384-4957-8a98-39f60a020b5b" />


After renaming the file, right-click on it and click on "Properties". Once inside Properties, click on the "Security" tab. Next, click "Advanced". </p>

<img width="1005" height="640" alt="image" src="https://github.com/user-attachments/assets/9e92bf5e-046f-442c-a329-29a86672ed51" /> </p>

Inside Advanced Security settings for ost-config.php, click on "Disable inheritance" then click "Remove all inherited permissions from this object". This will remove all permissions on this file. </p>

<img width="1554" height="933" alt="image" src="https://github.com/user-attachments/assets/56db6967-aa5e-428d-9b94-86465e9be18a" /> </p>

After the permissions have been removed, click "Add". Inside Permission Entry for osg-config.php box, click the link "Select a principal". A principal is the user or service account that runs PHP under IIS. </p>

<img width="608" height="309" alt="image" src="https://github.com/user-attachments/assets/39fed80f-8610-4f80-b9c2-fa54800d9e2a" /> </p>

In the Select User or Group box, type "Everyone" then click "OK". </p>

<img width="1207" height="717" alt="image" src="https://github.com/user-attachments/assets/58acb2fb-3f60-44cb-a4ac-2e9845792bea" /> </p>

Next, check the box next to "Full Control" then click "OK". This will give everyone full access; this is not good to do in a real-life scenario for security reasons, but for the lab this makes sure everything is working fluidly. </p>

<img width="1022" height="640" alt="image" src="https://github.com/user-attachments/assets/0c2fcae7-88ce-413a-92fd-162abbb6b05c" /> </p>

Everyone now has full control. Click "Apply" then "OK". </p>

<h2>Step 14 - Set up osTicket in web browser</h2>

<img width="730" height="885" alt="image" src="https://github.com/user-attachments/assets/b7dfff47-aa14-4e16-a74b-17972fbaed41" /> </p>

Return to the osTicket Installer and select "Continue". </p>

<img width="675" height="887" alt="image" src="https://github.com/user-attachments/assets/a84a2251-5b57-47ad-85f8-f6980f7c251b" /> </p>

Now the form for osTicket Installation is filled out. This is where the Helpdesk name and e-mail address is configured. This is also where the admin is configured. </p>

Now the Database Settings must be configured. Before the details are entered, the database must be installed and set up. </p>

<h2>Step 15 - Install HeidiSQL</h2>

<img width="691" height="565" alt="image" src="https://github.com/user-attachments/assets/26ca53f3-c3ae-4ec2-8d56-bc6e6bb59b6d" /> </p>

To begin, HeidiSQL must be installed. HeidiSQL is a GUI tool that lets you connect to MySQL, create the osTicket database, set up a user/password, and verify it’s ready before entering those details in the installer.</p>

<img width="851" height="596" alt="image" src="https://github.com/user-attachments/assets/00a77831-2a06-40c9-8663-80d10b21ec30" /> </p>

After installing HeidiSQL, click "New" and enter in the username and password that was established while installing MySQL. </p>

<img width="1159" height="738" alt="image" src="https://github.com/user-attachments/assets/07f6f5c1-36a1-4b80-87bb-08c72027bae0" /> </p>

Once the connection to the database has been established, right-click on "Unnamed". Then go to "Create new" and click on "Database". </p>

<img width="394" height="317" alt="image" src="https://github.com/user-attachments/assets/fc1eee7f-3070-4e04-bfb8-1cd946f74553" /> </p>

Name the database and click "OK". </p>

<h2>Step 16 - Complete Installation</h2>

<img width="605" height="461" alt="image" src="https://github.com/user-attachments/assets/f1ffd350-a1a6-41e5-ad88-95711d24d4b7" /> </p>

Return to osTicket installer and fill out the database information forms. Then click "Install Now". </p>

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/bef536a5-905e-40e6-ba04-8bd247c7a75c" /> </p>

<img width="1913" height="1013" alt="image" src="https://github.com/user-attachments/assets/92f055fb-cb55-422b-a5fb-6183ef7f5b57" /> </p>


osTicket has been succesfully installed! </p>

<h2>Conclusion</h2>
This Azure-based project successfully deployed a fully functional osTicket help desk system on a Windows 11 VM by configuring IIS with CGI, installing PHP and MySQL, enabling required extensions, and securing configuration files—transforming a basic virtual machine into a professional ticketing platform that centralizes support requests, automates workflows, and improves response efficiency for IT and customer service teams. 




















































