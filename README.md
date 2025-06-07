<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation Using Microsoft Azure Virtual Machies</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket using Windows 11 and Microsoft Azure Virtual Machines. Feel free to try it for yourself at no cost since <a href="https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account">Microsoft Azure</a> can be used with a free subscription for 30 days and/or $200 worth of credits. Lets do it!<br />

<h2>💻 Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)
- MySQL
- osTicket

<h2>👨‍💻 Operating Systems Used </h2>

- Windows 11 Pro
- Windows 10</b> (21H2)

<h2>⚠️ Prerequisites</h2>

- Resource group with a virtual machine.
- osTicket requirements such as PHP Manager, IIS Manager, MySQL, HeidiSQL etc..
- Installation of osTicket.

<h2>🧰 Installation Steps</h2>

<p>
*Assuming you have a Microsoft Azure account already setup, the first thing we need to do is create a resource group in Microsfot Azure and create a virtual machine within that resource group. We will use Windows 10, 2 vCPUs with 8GB of RAM. I'll call it osTicketVM with a simple Username: osticket and Password: Password1234.
</p>
<br />

- Once logged into Microsoft Azure, type "resource group" in the search bar located at the top of the screen and click on "Resource groups" to be taken to a screen where you can create a new resource group. I'll call the resource group "osTicketVM" as well, but you can name it anything you would like.

![image](https://github.com/user-attachments/assets/81bd76f6-58d7-47a1-9001-bf2bfa04ea1f)

- Click on Create.

![image](https://github.com/user-attachments/assets/34282295-4737-47e7-87b7-6830debb0a38)

- I'll call this VM "osTicketVM". 

![image](https://github.com/user-attachments/assets/c88441ea-c88a-446b-8443-b1e546ebcde2)

- Once you click on "Review and Create" on the bottom left side of the screen, it will take you to the next screen for review where you will click "Create".
- You will then see a notification letting you know the Resource has been created successfully.

![image](https://github.com/user-attachments/assets/5d6ae4b0-2347-4579-a30a-bcb72c28574d)

![image](https://github.com/user-attachments/assets/ac5549f2-d70f-4ac6-b96a-e3dc8255eb20)

- From here, you can type "vm" into the search box up top and click on "Virtual machines".
- On the next screen you will click the "create" drop down in either the top left under "Virtual Machines" or the blue "create" drop down towards bottom middle -> "Azure Virtual Machine".

![image](https://github.com/user-attachments/assets/238085eb-8019-4765-a9d6-f9a56f1a48ca)

![image](https://github.com/user-attachments/assets/69e536b9-01c3-44dc-9ff2-28e7f98c0747)

- Next, click on the "Resource group" drop down and select the resource group you created. I'll also name the VM "osTicketVM" and keep it in the same region as the resource group. 

  ![image](https://github.com/user-attachments/assets/af3f14d4-d365-4dde-a1d8-41b6648eeb61)

- Don't worry about anything else other than the *Image and *Size.
- For the "Image" drop down, we will select "Windows 10 Pro, version 22H2 - x64 Gen2 (free services eligible)". ***(If you do not see this option immediately available, scroll all the way down within the drop down for "Image" and click on "See all images". The next screen will show you all available operating systems available and you can search or find "Windows 10", click the drop down and select "Windows 10 Pro, version 22H2 - x64 Gen2 (free services eligible)".***
- For "Size", select Standard_D2s_v3 - 2 vcpus, 8 GiB memory".

  ![image](https://github.com/user-attachments/assets/6eb32307-4ebd-463e-9c8f-3b30fb03cec8)

- I'll use the username: osticket and password: Password1234 for this VM. Make sure you check the "Licensing" box.
- For this lab, we do not need to worry about the "Disks", "Networking" or any of the "Next" options for creating a VM so we can just click on "Review + create", and then "Create" on the following screen.

  ![image](https://github.com/user-attachments/assets/aafbb3ba-3825-4333-a5fb-1d910e954b3b)

  ![image](https://github.com/user-attachments/assets/4c5ba525-a619-474f-92bc-8781946bc7c3)

- It will take a bit for the VM to be created so you can relax for a moment until the notification shows you that the VM has been deployed.

![image](https://github.com/user-attachments/assets/90ef2ecb-ea83-40cf-9fe5-8d614ce3cedf)

<p>
*Once the VM (virtual machine) is created, we will log into it remotely using Remote Desktop Connection which can be pulled up from the start menu or searching it in the taskbar. You will need to copy and paste the public IP address into the text box and log in using the credentials you set for the VM when it was created. Once logged into the VM, we will begin installing the required software/programs for osTicket.
</p>
<br />

- After deployment of the VM shows to be done, click on "Home" in the top left of the screen.
- Here you will see shortcuts under "Azure services" and you can just click on Virtual machines to be taken to the VM you just made.
- You will see the public IP Address on the far right side of the listed VM and you can go ahead and highlight and copy it to the clipboard. 

![image](https://github.com/user-attachments/assets/2b534731-5d77-496e-9ebf-91d90e2355ca)

![image](https://github.com/user-attachments/assets/4e81bde1-9981-418c-a9ac-3212e3211bd2)

![image](https://github.com/user-attachments/assets/517172de-1637-44ff-aefe-b8d3ac959f2f)

- Next, type "Remote Desktop Connection" (RDC) in the search box located in the taskbar of your computer.
- Open RDC and paste the publick IP address of the osTicketVM in the text box and click on "Connect".
- Then log in with your admin credentials. For me it will be "osticket" for username and "Password1234" for the password. ***(You may need to click on "more choices" -> "use a different account" towards the bottom if it has a username prepopulated in the text box to sign in with.)***
- Wait for the VM to load.

  ![image](https://github.com/user-attachments/assets/06fe365e-aaba-49b1-bd89-c7873013b876)

![image](https://github.com/user-attachments/assets/9806a474-074e-44e8-881e-c3ca55b27c06)

*When confronted with all the options for Windows 10 after logging into the VM and/or pulling up the Microsoft Edge web browser, you can decline/say no to everything. If you already clicked through with any of the options selected it is not a big deal.

- Copy and paste the <a href="https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account">osTicket-Installation-Files.zip</a> link inside our osTicketVM in a web browser to download the required files for osTicket.
- Click "download anyway".

![image](https://github.com/user-attachments/assets/42e6b105-d41e-4faa-bed3-5e7a5c2c6737)

- It may help to move the osTicket-Installation-Files.zip to the Desktop by opening file explorer -> downloads and then clicking and dragging it once downloaded. Either way go ahead and unzip it onto your desktop.

![image](https://github.com/user-attachments/assets/d88d566c-c85f-40c6-bc5c-73a8b9868e3c)

![image](https://github.com/user-attachments/assets/44c81560-17b1-40b1-9661-bc695908e7f9)

*We will first need to enable IIS (Internet Information Services) ***With CGI***.
- Pull up the control panel by searching for it in the task bar.
- Click on "Uninstall a program" under "Programs".
- On the left side, click on "Turn windows features on or off".

![image](https://github.com/user-attachments/assets/2c8661e2-a4db-4464-9c93-1fb15cd8faac)

![image](https://github.com/user-attachments/assets/7db9c2ef-ec1e-4a25-92f5-6592030d1a8d)

- Scroll down a bit and check the box next to "Internet Information Services" and hit the "+" in front of it.
- Then, click the "+" in front of "World Wide Web Services".
- Click on "+" in front of "Application Devopment Features".
- Check the box next to CGI.
- Click "OK" and wait while it installs.

![image](https://github.com/user-attachments/assets/f4360b61-0ea3-477e-b0f0-8e30ca3207c9)

![image](https://github.com/user-attachments/assets/6078737e-716a-4b8e-9957-dab1dbf9825a)

- Once completed, go back to or open up the osTicket-Installation-Files folder and install PHP Manager (PHPManagerForIIS_V1.5.0.msi).
- Hit next and agree to the terms.

  ![image](https://github.com/user-attachments/assets/9ed5803c-0109-4184-9094-bd0ac54e4bdb)

  - Back in the osTicket-Installation-Files folder, install the Rewrite Module (rewrite_amd64_en-US.msi).
  - Accept the terms and hit "install".
 
    ![image](https://github.com/user-attachments/assets/59777b47-6e06-48f6-a3ab-8f8a190e9d41)

  - Next, we'll create a directory/folder named "PHP" in the C: drive.
  - In File Explorer, navigate to C:
  - Create a new folder and name it PHP
  - Then, unzip the PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) folder from the osTicket-Installation-Files folder into the C:\PHP folder we just created by right clicking on it and clicking "extract all", and then navigating to the C:\PHP folder by clicking browse -> Extract.

  ![image](https://github.com/user-attachments/assets/ad4d25c9-83a7-4dfe-b9ac-ed1adfa985ec)

  ![image](https://github.com/user-attachments/assets/e1354a4d-b78c-4fec-8a23-2e144fdb85f4)

- Back in the osTicket-Installation-Files folder, install VC_redist.x86.exe
- Agree to terms and install.

![image](https://github.com/user-attachments/assets/ed7354e2-e28c-4fc6-8a5b-1168cc0f4aa5)

***This next step is important that you pay attention to detail.***
- Back in the osTicket-Installation-Files folder, install MySQL 5.5.62 (mysql-5.5.62-win.32.msi)
- Choose "Typical Setup" when presented with the option.
- Leave "Launch Configuration Wizard (after install)" checked.
- Choose "Standard Configuration" and to make it easy and simple use username: root and password: root. So the word "root" for both username and password.

  ![image](https://github.com/user-attachments/assets/3f5e3ec3-6465-4452-9778-0a009a0f417f)

![image](https://github.com/user-attachments/assets/b6841b05-d21e-4cc9-ad2d-7a275bf852dc)

![image](https://github.com/user-attachments/assets/e9c7d75a-bfaa-4bfc-8581-83daad71eb7a)

![image](https://github.com/user-attachments/assets/f42a8858-edd7-4869-a2a3-1f7525486694)

![image](https://github.com/user-attachments/assets/d9583162-eb15-4aa5-a736-f42aecff6509)

![image](https://github.com/user-attachments/assets/6853065f-feda-4744-bf14-17f26342d728)

- Click "Execute"

![image](https://github.com/user-attachments/assets/21189413-62a5-42b3-ae3e-7e38f125d7c5)

- Once installation of MYSQL is completed, Open IIS Manager as an Admin by typing "IIS" in the search box on the task bar
- Right click on it and click "Run as Administrator"
- Double click on "PHP Manager" in IIS Manager
- Click on "Register new PHP version"


  ![image](https://github.com/user-attachments/assets/e0199b8d-22a9-4e16-a548-ca5c86802cb4)

![image](https://github.com/user-attachments/assets/03c86d0f-436b-4a64-9fa7-989f4d5b0a95)

- Click the three dots next to the text box to browse to the C:\PHP folder we created earlier.
- Open up the folder to select the php-cgi file by double clicking it or selecting it and clicking "open".

  ![image](https://github.com/user-attachments/assets/300a97e1-b77b-418f-98bd-333cca893fd3)

![image](https://github.com/user-attachments/assets/f278051e-76fa-4232-ab68-19bc6c23df56)

![image](https://github.com/user-attachments/assets/24c18254-5d98-44ab-8d59-9ddb070e2121)

- After that, click on "osTicketVM" in the top left in IIS Manager
- Then click "Restart" on the right side.

![image](https://github.com/user-attachments/assets/711a5f1f-8f8e-47e5-a959-910cbf74eb08)

-  Back in the osTicket-Installation-Files folder, unzip the "osTicket-v1.15.8.zip" by right clicking -> extract all -> Extract (bottom right).
-  Wait for the files to extract.
-  Copy the "upload" folder into C:\inetpub\wwwroot.
-  Then, rename upload to "***osTicket***" inside of C:\inetpub\wwwroot by right clicking on upload once its moved and clicking "rename".

  ![image](https://github.com/user-attachments/assets/1f3a2ace-8fd3-4887-9d94-db11dbde8e92)

![image](https://github.com/user-attachments/assets/168923f2-7e54-4716-ac25-4a9dbd65c607)

![image](https://github.com/user-attachments/assets/01eac87e-36c3-4f0f-9c58-43bbc56c7237)

![image](https://github.com/user-attachments/assets/25b72bef-8201-4178-937f-24c4b04e107e)

![image](https://github.com/user-attachments/assets/2a05bde1-5e8b-4960-b3a7-06ae60341f28)

- Go back to IIS Manager and restart it by clicking on "Restart" on the right side.
- Click the drop down in front of "Sites".
- Click the drop down in front of "Defaults".
- Click on "osTicket", then click "Browse *.80" on the right side lower than where the "Restart" button is located.

  ![image](https://github.com/user-attachments/assets/6fece7ad-badf-49d3-932c-5b1671286b38)

![image](https://github.com/user-attachments/assets/b6eb5228-58b7-4240-887a-cd6658d24287)

*As long as all previous steps were done correctly, we should now see osTicket Installer pull up like magic!

![image](https://github.com/user-attachments/assets/d63769be-64f6-4381-9276-0b15b3765a0a)

*You'll see towards the bottom half that some of the extensions are disabled. We are going to enable those. 

- Back in IIS Manager, make sure you still have "osTicket" highlighted on the left side and click on PHP Manager.
- Click on "Enable or disable an extension" towards the bottom of the screen.
- Enable: php_imap.dll , php_intl.dll , and php_opcache.dll by right clicking them and hitting "enable". You'll see them go form the bottom grayed out disabled half to the top enabled half.
- Refresh the osTicket site\installer that pulled up in your browser to see the changes reflected (extensions enabled).

![image](https://github.com/user-attachments/assets/d074f420-339a-488f-b91d-b97f68e5a07f)

![image](https://github.com/user-attachments/assets/a64e2d25-b6fb-422e-94ba-97fa7e33a9a3)

![image](https://github.com/user-attachments/assets/e62db9dd-cb93-424d-93f8-0f791ccd24d6)

![image](https://github.com/user-attachments/assets/0642f42e-404a-47f9-ba8c-b0bf61a0fa8f)

***Accuracy of the following steps are important!***

- In the C:\inetpub\wwwroot\osTicket\include folder, scroll down to find "ost-sampleconfig.php".
- Rename it to ost-config.php by right clicking it and hitting rename.

![image](https://github.com/user-attachments/assets/f0450f97-4006-407d-95f0-9d42e96b1488)

![image](https://github.com/user-attachments/assets/28a89af3-6899-49b9-bc59-c63719d6c647)

- After renaming, right click it and go to properties.
- Click on the "Security" tab.
- Click on "Advanced" on the bottom right.
- In the Advanced Security Settings screen, click "Disable inheritance" on the bottom left.
- Click Remove all in the "are you sure?" pop up.
- Then, click "Add" right above the inheritance button.

![image](https://github.com/user-attachments/assets/66bcf416-ba3d-4a34-8767-8657acb0ad70)

![image](https://github.com/user-attachments/assets/224f9ae4-3af2-43c0-baef-8fdc9b225c15)

![image](https://github.com/user-attachments/assets/2b933687-9a71-4146-98d8-ab499cd986c0)

- Click "Select a principal" towards the top of the screen.
- Type Everyone and hit "Check Names" -> click Ok.
- Check the box next to "Full control" -> click Ok -> click "Apply" on bottom right.

![image](https://github.com/user-attachments/assets/3b768ede-f05b-46be-88f3-9db78aab832e)

![image](https://github.com/user-attachments/assets/f0ca2843-e2c8-49d3-b404-06ab47053b29)

![image](https://github.com/user-attachments/assets/8c965296-8901-484e-9bda-6331e804fb9b)

![image](https://github.com/user-attachments/assets/07676b78-636a-4037-b5fd-9b0e94d0e7aa)

- Now we can go back to the osTicket Installer in our browser window and click "Continue" on the bottom of the screen.

  ![image](https://github.com/user-attachments/assets/1da56536-bbc7-47ac-8893-43d0581f8aef)

- I'll just name the osTicket account "Helpdesk" with a fake email for the purpose of this tutorial.
- Just fill out the blanks for your admin account. For my admin account I'll keep it simple and use the username: admin119 and password: Password1. (***I tried to use "admin" but I got an error later on so I updated it to "admin119" for the username to be able to complete installation.***)

![image](https://github.com/user-attachments/assets/916a7c9a-556f-4bca-8f0c-6b1cd9c1eee1)

- Next, we will need to install HeidiSQL in the osTicket-Installation-Files folder.
- Agree to the terms and keep hitting next until you can hit "Install".
- Make sure the box is checked that says "Launch HeidiSQL".
- Skip the Donate screen.

![image](https://github.com/user-attachments/assets/8260d473-31de-4b3d-b869-13d5c8419437)

![image](https://github.com/user-attachments/assets/faa1dc49-569a-4898-bec5-6506d8ca905a)

- Click on "New" on bottom left.
- User and Password should both be: root

![image](https://github.com/user-attachments/assets/f2715e3f-ddda-4875-bd04-08ac7ac896f4)

![image](https://github.com/user-attachments/assets/a4be7da2-15f2-44e8-b9e1-4b8254e99788)

- Right click on "Unamed" next to the dolphin symbol towards top left.
- Go to "Create new" -> click "Database"
- Name the database: osTicket

![image](https://github.com/user-attachments/assets/16cc8267-726d-4fbd-a278-5608d73a4408)

![image](https://github.com/user-attachments/assets/5156fff3-423c-4dc6-b1d3-279051824a31)

- Back in the osTicket Installer browser, fill out the information for the MySQL Database we just created.

![image](https://github.com/user-attachments/assets/2c97538d-d1e3-475e-89d8-e4402fc3944b)

- Click Install on the bottom to be congratulated. The two underlined links are the ones you will be using the most. The first one is for the end users who would be submitting the ticket. The second link is for the admin and IT Helpdesk employees who work the tickets to log in and work their magic. ***I would copy and paste each one it's own tab.***

![image](https://github.com/user-attachments/assets/e97260ea-d0e6-4371-9ff3-992edab38b5a)

*End user log in/ticket opener.

![image](https://github.com/user-attachments/assets/3a963817-d73d-4e5a-800a-831be1c5438c)

*Admin/Helpdesk log in/ticket closer.

![image](https://github.com/user-attachments/assets/b72c19a5-25bb-423c-9cb0-b6ab43b40baf)

*Once logged in you can see the "Agent Panel" which shows any open tickets specific to your department/team or all of them if your the Admin with full control/access. 
From here you can open a ticket by clicking on "New Ticket" if you need to create one yourself, look at and work open tickets or assigned tickets, view closed tickets if you have access, view the detail and work/route a ticket. Note that it shows you the ticket number, last updated date, subject, department/team it came from, ahe SLA (Service Level Agreement) which is essentially the priority or importance level, and to whom/where it is assigned.

![image](https://github.com/user-attachments/assets/492d08f6-8ff7-4ca0-b38a-ee216dc43220)

- In the top right of the screen you can click on "Admin Panel".
*On the next screen is where you can see all the different categories of controls by hovering over them and choose what you would like to customize and configure for the helpdesk. You can create users, agents, departments, teams, and configure what they can and cannot have access too. Under "Manage" you can create and configure help topics such as general inquiry or system outage, and also create/configure SLAs. 

![image](https://github.com/user-attachments/assets/7434417e-9ffc-4ec4-a665-17b7c337de0a)

***Be sure to DELETE the RESOURCE GROUP in Microsoft Azure when you are completely done so you don't rack up charges to your subscription!***

![image](https://github.com/user-attachments/assets/98bb5442-9462-489a-a3c7-024e81b42560)

- Back on the Resource group page in Azure, clcik on your resource group.
- Click Delete resource group.
- Copy and paste the name of your resource group in the text box at the bottom and hit delete.
- Wait and verify the resource group was deleted completely.
- Repeat these steps for the NetworkwatcherRG resource group as well.

![image](https://github.com/user-attachments/assets/feaf1d16-2025-4363-8932-1ebbdc25d2e8)

![image](https://github.com/user-attachments/assets/7c0237a3-386f-42c1-a723-6fe0f9b93e64)




<p>
  *Feel free to practice and play around in the osTicketing system to become a pro! 
  You can start by creating an agent who can open tickets by logging into the end user interface, and then create a couple of agents in different departments or teams who can work the tickets. Make sure to set up the SLAs. ChatGPT is a great tool for creating scenarios for you to practice and also to assist you in configuring your helpdesk business if you need it!! I thank you for using this tutorial for you osTicket installation and wish you the best! : )
</p>
<br />
