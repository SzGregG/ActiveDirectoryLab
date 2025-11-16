# Active Directory Lab
## 🎯Objectives
- 1 Install Windows Server
- 2 Install Active Directory (AD) tools on the Windows Server and creating a domain
- 3 Create organisational units (OU) for different business departments (e.g.: IT, HR, Finance etc)
- 4 Create user accounts and groups within the different OUs

## 📝 Resources
For the execution of this project Broadcom's VMware Workstation Pro (17.6.4) was used. It can be downloaded [here](https://knowledge.broadcom.com/external/article?articleNumber=368667).

# Section 1.0: Initial Set Up

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
**Image 11: In the new window I selected the Location and the drive to be used then hit Apply.**
<img width="1019" height="728" alt="Képernyőkép 2025-11-16 182517" src="https://github.com/user-attachments/assets/2b8fe62c-d6da-4ef7-b66c-d39b0f94e16f" />

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

