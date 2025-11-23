# Active Directory Lab
## 🎯Objectives
- Section 1: Set Up an Active Directory (AD) server and a domain with various organisational units and users
- Section 2: Create several Group Policies and test if they have been successfully implemeted
- Section 3: Create a shared network drive for domain users and create settings to enable efficent use of disk space 

## 📝 Resources
For the execution of this project Broadcom's VMware Workstation Pro (17.6.4) was used. It can be downloaded [here](https://knowledge.broadcom.com/external/article?articleNumber=368667).

# Section 1.0: Initial Set Up
In this Section I aim to install a windows server, install Active Directory (AD), create a domain, create oraganisational units (OUs) and finally create user which I can add to these OUs.
## Step 1.1: Setting up the Windows Server
In this project Microsoft's Windows Server 2022 ISO was used.  
Windows Server 2022 ISO [download](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022).

**Image 1: Once downloaded the server file, I created a new machine to be the Windows Server**
<img width="1437" height="750" alt="Képernyőkép 2025-11-09 180526" src="https://github.com/user-attachments/assets/c7b6ad0e-a861-488c-aaea-047898aa4b54" />

**Video 1: Installing the Windows Server on the Virtual Machine**

https://github.com/user-attachments/assets/d3df067d-315e-4eb9-a341-745a44a26ed9

## Step 1.2: Installing AD tools and creating a domain
Once the installation is finished, when logging into the server the Server Manager window automatically comes on. Here is where the AD tool installation can be started.

**Image 2: To start the AD installation process click on "Manage" and then on "Add Roles and Features" which will open a new window**
<img width="1026" height="769" alt="Képernyőkép 2025-11-12 190544" src="https://github.com/user-attachments/assets/1d009ecf-9fde-4754-b170-27bff41ce2aa" />

In the new window different configurations can be selected in various tabs such as installation type, server roles and feautres.  
For Installation type I went with "Role-based or feature-based installation".
  
For Server Roles I chosen:
- Active Directory Domain Services
- File and Storage Services
- DNS Server
- Remote Access
  
Features:
- .NET Framework 4.8 Features
- Group Policy Management

After this I proceeded to the Confirmation tab where I could start the installation.  
***!!! Important, don't close the installation window as this is where you can promote the server to Domain Controller (DC) !!!***

**Video 2: Here are all the tabs after selecting the desired configurations and features before hitting install**

https://github.com/user-attachments/assets/4171fdb3-5ea2-41bf-90fb-3e38084f4e7e

**Image 3: Once the installation is done you can promote the server to DC by clicking the following button**
<img width="1020" height="771" alt="Képernyőkép 2025-11-12 195022" src="https://github.com/user-attachments/assets/9473a724-c860-4143-9a17-123c1be40f9c" />

Promoting the server to DC brings up a new window again, where the domain configurations can be selected. As deployment operation I selected "Add a new forest" and given the name "ad.SZG.com" as the root domain name.

_____________
**📝 Note 1**
*AD forests are root/top level logical containers in an AD environemt. Within it common configurations and directory schemas (defines all object types e.g: users groups etc. and their attributes) and global catalogs (global catalog - an index that contains information about every object within the forest, allowing to quickly search and locate them) are shared. A forest can contain one or multiple domains. These domains within the same forest automatically trust each other enabling secure communications adn resource sharing.*  

*Domain naiming best practice - organisation.local was used in the past frequently as it meant it is not dns resolvable on the public internet. It is however no longer best practice as it can cause issues, one of which is prblem with cloud integration with service providers as they expect publicly routable domain names. As a result using subdomains of actual registered domains is recommended. E.g: ad.organisation.com*
_____________  

**Video 3: All the configurations, domain names and passwords set just before starting the prerequsites checks and clicking on install. Once done with the installation the server restarted to finalise the installation process of the AD Tools.**

https://github.com/user-attachments/assets/3c0fe8e9-aa1d-43e2-a7e7-c70372d61fa4

## Step 1.3: Setting up AD, creating Organisational Units (OUs), Groups and Users
Once the installation is finished, logging back into the server all the AD Tools installed can be access through the Start Menu and under the "Windows Administrative Tools" folder.  
From these tools, now I will be using the "AD Users and Computers" tool.  
  
**Image 4: In the new window I can now create the desired OUs, Groups and Users for my domain. It can be done my right clicking on the domain, selecting new and then selecting OU. The same can be done for new groups and users by clicking on the desired OU or Group to which I want to add them to.**
<img width="1020" height="769" alt="Képernyőkép 2025-11-12 232715" src="https://github.com/user-attachments/assets/bfc90d54-04dc-4f31-bf72-aa6b37adc3ad" />

I made the following 3 OUs for regional departments:
- Americas
- Asia
- Liechtenstein
  
Within each of these OUs I made another set of OUs:
- Computers
- Servers
- Users
  
In the Users OU, I created a set of groups for different business units with 2 groups for each unit, one for security and one for distribution:
- IT & DL-IT
- HR & DL-HR
- Finance & DL-Finance
- Management & DL-Management
- Marketing & DL-Marketing
___________________________________
**📝 Note 2**
*Groups have 2 different options. Group Scope and Group type.  
Group Scope determines to what extent - within or beyond a domain - a group can be accessed. The 3 categories within scope are "Domain Local", "Global" and "Universal".*  
**Image 5: Table Reference of different group scopes. [Source](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-groups)**
<img width="1575" height="697" alt="Képernyőkép 2025-11-12 235712" src="https://github.com/user-attachments/assets/eeac624c-b6f1-405d-9b5d-14d2b42ebf80" />

*Group type on the other hand has 2 categories. "Seucrity" and "Distribution". Security groups are used to assign permissions and user rights to shared resources. Distribution is used to create email distribution lists to send to a group of users.*
___________________

**Image 6: Both for Security and Distribution Groups I have set the scope to Global**
<img width="1021" height="767" alt="Képernyőkép 2025-11-12 234348" src="https://github.com/user-attachments/assets/123662a5-25f5-4510-b91a-4c0fc8741074" />

**Image 7: Once done I created 3 users for each of the departments and added them to both the security and the disribution groups of the respective department. Here is the end result**
<img width="1022" height="765" alt="Képernyőkép 2025-11-13 181232" src="https://github.com/user-attachments/assets/0d2cfc8f-35fd-456d-90ae-14bcc0af6a34" />
  
______________________________________________________  
______________________________________________________
# Section 2.0: Group Policy Management

## Step 2.1: Creating and Setting up Group Policy Objects (GPOs)

Alongside other tools I have already installed the Group Policy Management Tool in Section 1. It can be easily accessed through the Start Menu in the Windows Administrative Tools folder. In the Group Policy Management window the forest and domain can be seen that I created in the previous section. Here several policies and preferencces can be adjusted with the use of User or Computer Configurations.
________________________________________
**📝Note 3** 
*Computer Configuration - configuration that applies only to the local computer and does not change per user  
User Configuration - configuration that applies to users on the local machine and apply to any new users in the future on this local computer  
Under each there are also Policies and Preferences.  
Policies - can't be changed by users. e.g: password or account lockout policies  
Preferences - can be set by admins on default but can changed by users. e.g:mapped network drives, printers, desktop shortcuts.*
________________________________________
The first thing I aimed to do is to set a password policy to ensure strong passwords and for improved security.
  
**Image 8: To create a new GPO/policy right-click on the domain name and choose the first option "Create a GPO in this domain...". Then proceed to name it, for easy navigation it is important to name them clearly to know what they do. Once done it will show up in the list under the chosen domain**
<img width="1017" height="769" alt="Képernyőkép 2025-11-16 170014" src="https://github.com/user-attachments/assets/2330af66-2904-41b9-a639-18ec011b5ccf" />

Now the policy can be edited according to need by right-clicking on it and choosing edit. For this policy I selected to do it via the computer configuration. The reason for this is because it is the computer which is asking for passwords when a user logs in. By applying this policy/rules to the computer I apply it to the computer's local authentication database, something which is shared by all domain users and thus more efficient then doing it by individual users.
  
**Image 9: Next I went under policies as it should not be changable by users. Then under Windows settings > Security Settings > Account policies. Here all the various password settings can be found and edited**
<img width="1022" height="724" alt="Képernyőkép 2025-11-16 171725" src="https://github.com/user-attachments/assets/7aceb183-8189-48b7-8878-607b842507c6" />

The first setting which I defined was the Minimum pasword length. I put this to 15 characters as recommended by the National Institute of Standards and Technology as of April 2025([source](https://www.nist.gov/cybersecurity/how-do-i-create-good-password)). By default it is limited to 14 characters as the max one could put, but it can be increased further if you enable the "Relax minimum password length limits" setting first, which I did.  
Next I set the minimum and maximum password age to 30 and 90. Recoomendations from NIST and other organisations though for there to be no password expiration in case other more secure factors such as multifactor authentication is met.  
I also enforced password history to be remembered up to 12 passwords to prevent reusability within a year.  
Last but not least I enabled Password complexity requirements determined by default Windows requirements to demonstrate it. It has to be noted however that NIST does not recommend complexity, but emphiseses more on length.  

**Image 10: Once I set all the settings here is how it looked like.**
<img width="1011" height="225" alt="Képernyőkép 2025-11-16 180547" src="https://github.com/user-attachments/assets/69dd8f2f-35b0-42a2-8bc9-adf13e27f9f1" />

Next I set up a Drive Mapping GPO. Creating it like how I did with the Password policy and right-click on it to edit. As this is something which is going to be used by the user and also something which is inteded to be changable by users according to their needs and preferences so it will be under User Configuration and Preferences. Then proceeded to Windows Settings and > Drive Maps. Right click it, to create a new mapped drive.
  
**Image 11: In the new window I selected the location where the shared drive is going to be. Starting the path with the server first "WIN-TMIEEA7IFUF" then the folder name "SHARED DRIVE" which is going to function ass the shared network drive. Will get back to this in the next section and set up the actual folder**
<img width="1022" height="725" alt="Képernyőkép 2025-11-23 113417" src="https://github.com/user-attachments/assets/e4bd96ec-89f3-4273-b98b-0a032f3a620b" />

Another GPO I set up was to restrict access to the Control Panel. As it will be applied to users I went with User Configuration > Policies > Administrative Templates > Control Panel.  
There are different options for restrictions. In case access is still desired for users but with limitations it can be limited either with the "Hide Specified Control Panel items" or "Show only specified Control Panel items" options.  

**Image 12: In this instance I opted with prohibiting access instead**
<img width="1022" height="359" alt="Képernyőkép 2025-11-16 184207" src="https://github.com/user-attachments/assets/1126b304-fe22-4332-abaa-89ac566fa243" />

On the next GPO I created a GPO to prevent users from using USB storage devices. As it is applied directly ot the computer I selected Computer Configuration and Policies as it should not be possible to be changed by the user. Then proceeded to Administrative Tools > System > removable Storage Access.  

**Image 13: It is possible to customise this policy based on different types of storage devices. In this instance I went with a blanket measure "All removable Storage classes: Deny all access"**
<img width="1019" height="516" alt="Képernyőkép 2025-11-16 185232" src="https://github.com/user-attachments/assets/3f983deb-0bdf-4ec5-9c7b-03bd453b8302" />

Finally I created a new GPO for Account Lockout Policy. It can be found Under Computer Configuration > Policies > Windows Settings > Security Settings > Account Lockout Policy.  
  
**Image 14: I Set 3 invalid logon attemtps and a 15 minute lockout timer**
<img width="1021" height="309" alt="Képernyőkép 2025-11-16 191031" src="https://github.com/user-attachments/assets/5aa8976f-ab14-4840-887b-520ba7c633f4" />

## Step 2.2: Join a Computer to the Domain to test GPOs with
In order to test the GPOs I have set up in the previous step I have created and installed another VM with a Windows client to join the Domain.
Once installed the computer, I made sure the Windows server has a static IP. To do this on the Server I went into the Network Settings > Change adapter options. Went into Properties and then selected Internet Protocol Version 4 (TCP/IPv4).  

**Image 15: The window where I set the IP address, Sudnetmask, default gateway and preferred DNS. 127.0.0.1 for DNS is a special address known as a loop back address which refers to your own computer/local host. Default gateway is the local network's address through which it will communicate with other networks e.g: the internet. Lastly subnetmask just determines which part of the IP address refers to the host and which one to the network, helping to determine what network is a host part of. Whereever it is the 0 in the sections that section shows the host on the actual IP address**
<img width="1016" height="644" alt="Képernyőkép 2025-11-17 152641" src="https://github.com/user-attachments/assets/0069baeb-753a-4e99-9c3e-9698e47b6fc9" />


Once the IP address has been set I switched back over to the Computer VM to connect it to the domain. Here once again I went into the Network setting > Change adapter options. Then again on properties and and the same option for IP properties how I set the static IP for the Server.  
This time however I left the IP address to be done automatically and I changed only the DNS to use a preferred DNS which was to the the static IP of the Server 192.168.8.128.  

**Image 16: IP properties panel once I set the DNS**
<img width="1020" height="682" alt="Képernyőkép 2025-11-17 154450" src="https://github.com/user-attachments/assets/878d8f02-1f25-46da-9ba6-0837af7df7e8" />
**Image 17: To test if the computer can successfully reach the server/domain controller I used the ping command. To check if the DNS works as intended I also used the nslookup command**
<img width="1002" height="533" alt="Képernyőkép 2025-11-17 155115" src="https://github.com/user-attachments/assets/8d324f89-8541-4134-936f-407716547b9d" />

Now I can connect the PC to the domain. To do this I went to Start Menu > Settings > System > About and in that panel I selected Rename this PC(advanced). In the new window clicked on change where I can set the name of the computer but also the domain it will be a member of. I went with "Workstation01" as name and put in the domain ad.SZG.com that I set up in the early section. 

**Video 4: Connecting the Computer to the domain. Once it is connected a restart will start to fully implement the connection**  

https://github.com/user-attachments/assets/5fecb5e7-cbc7-4030-862f-fa4169866297

**Video 5: After the restart we now can login onto the domain with any of the user we have created. To do this just select Other User and type in the name username and password. Here you can also check which computer you are dealing with by typing .\ into the username field. Once done in this instance it prompted me to change my password as that how I set up each us on their first logon. That's done now I can start to test the GPOs**

https://github.com/user-attachments/assets/bcae1898-f441-44ab-8ef3-4cbe66ffbb3d

## Step 2.3: Implementing and Testing the Group Policy Objects (GPOs)
First things first to implement the GPOs I went back over to the Server client and within the Group Policy Management Tool.

**Image 18: To implement the GPOs to specific OUs I dragged each GPO to the correct OUs. User Policies and Preference GPOs under the User OU and Computer Policies and Preference GPOs under the Computer OU.**
<img width="1019" height="714" alt="Képernyőkép 2025-11-17 170946" src="https://github.com/user-attachments/assets/183b63a6-6e56-4ae8-9c22-d4d44ecccf0f" />

Last step before I could test the GPOs was to open the AD Users and Computers Tool. Here I just needed to add the computer client we added to the domain to one of the Computer OUs I created under a Geographical department OU. In this instance I put it under Americas as it is the main one I am using and it has all the users. It is very easy to do this, just within the general Computers container right-clicked on my computer client "Workstation01" then on Move and selected my desired OU to move it to.
  
Now to test if the GPOs I implemented are working I changed back to the computer client.  
  
**Video 6: Here I tested the GPO to restrict the Control panel completely for users. It did work and came up with the restriction message. Great Success!**

https://github.com/user-attachments/assets/fe226307-ade9-4363-af11-7cee902f67be

**Video 7:Next I tested the Password Policy. Here however I encountered a problem as it wasn't enforcing the minimum 15 character requirement for passwords. After some research there seems to be several hidden AD Group Policy limitations with password policies one of which is that 15+ character password requriements don't work.**

https://github.com/user-attachments/assets/2dc353fe-a01d-4092-ad98-3be51b7950f0

After further research I found a work around for this solution. To not implement it as a Group Policy but to implement it as Fine Grain Password Policy instead through the Active Directory Admin Center.

**Video 8: Setting up the Password Policy through AD Admin Center. Settings I went with: 15 characters and 3 tries before lockout**

https://github.com/user-attachments/assets/fbdec035-5c52-495b-a029-7abba5c4a1cb

**Video 9: After taking out the GPOs for password and account lockout from the domain for them to not to clash with the Fine Grain Password Policy through AD Admin Center I managed to get it to work and successfully test it. In this video I put in a password with only 14 characters and it did tell me that it did not meet requirements**

https://github.com/user-attachments/assets/aad23655-8988-4031-b579-5ce34198b7fb

**Video 10: Here I gave a 15 character password and it did accept it**

https://github.com/user-attachments/assets/32d1e299-ac12-469c-b341-9185317876b8

**Video 11: Here I tested if it would carry out the Account Lockout policy after 3 incorrect attempts. Thankfully this worked as well.**

https://github.com/user-attachments/assets/a35a16e7-2a9a-4484-a1ae-d1c84038a05d

________________________________________
_________________________________________
# Section 3.0: File Services
My aim in this section was to set up a folder on the server which would serve as a shared network drive for domain users as well as set up file services within the AD server.
## Step 3.1: Set up file sharing
To set up file sharing I first created the folder on the server machine's C:Drive named as "SHARED DRIVE". The folder name I gave as the mapped network drive location as part of the Drive Mapping GPO (Please refer to Image 11) By using this GPO I created it enables the folder to be automatically map it as a network drive for users to access.

**Video 12: Next I set the permissions for the folder so that Domain Users will be able to access and read the folder.**

https://github.com/user-attachments/assets/c11005d7-1f09-4de3-b749-360f5f21e0c0

After this I just made sure the policies are updated on the client machines by using the command "gpupdate /force" in the Command Prompt and restarted the machine.

**Image 19: Once booted back up on the client machine the new shared drive could be found and accessed through the file explorer**
<img width="1022" height="724" alt="Képernyőkép 2025-11-23 114526" src="https://github.com/user-attachments/assets/e5b3f1db-e969-46e9-bd06-d5f6edcfdb62" />

## Step 3.2: Set up File Server Resource Manager (FSRM) and configure file quotas and file screening
Storage is not unlimited so to maintain costs and to manage data space effectively quotas can be used. File screening complements this feautre and can be used to make sure that files that would take up lots of space would not fill up the drives very quickyl. FSRM is a tool which can be used to introduce such functions, first one I looked at was quotas.  

**Video 13: As the first step I installed the FSRM tool through the Server Manager. Just like how we installed other AD tools in Section 1.2. After the installation is finished, FSRM can be found in the Windows Administrative Tools folder with the other AD tools. No need to restart the server.**

https://github.com/user-attachments/assets/17cc0dad-eab6-46d1-86c4-5344478b58bd

**Video 14: Within FSRM I created a new quota. Selected the path to the Shared drive folder I wanted to set the quota on. After this it is possible to select given or custom quota properties, where it is possible to determine notification thresholds at which points the server can notify admins or even users that the storage limit is close to be reached. For now I just set it up with the recommended default properties.**

https://github.com/user-attachments/assets/ceb48a4e-08e2-430d-9ed5-62b057ab8c6f

Next up for File Screening the process is almost identical as it was for the quotas.

**Video 15: Similarly to quotas, I selected out the shared drive folder location I wanted to apply it file screening on. Then again there are default screening options. In this instance I went with a custom one to screen out files which are video, audio, images, compressed, executable or web page files.**

https://github.com/user-attachments/assets/ce353b48-65ca-45e5-8810-b2e7610e6cea

_______________________________________
_______________________________________
That's the end of this project for now. Thank you if took your time to look take a peek at it!
