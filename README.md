# Active Directory Lab
## 🎯Objectives
- 1 Install Windows Server
- 2 Install Active Directory (AD) tools on the Windows Server and creating a domain
- 3 Create organisational units (OU) for different business departments (e.g.: IT, HR, Finance etc)
- 4 Create user accounts and groups within the different OUs

## 📝 Resources
For the execution of this project Broadcom's VMware Workstation Pro (17.6.4) was used. It can be downloaded [here](https://knowledge.broadcom.com/external/article?articleNumber=368667).

## Step 1: Setting up the Windows Server
In this project Microsoft's Windows Server 2022 ISO was used.  
Windows Server 2022 ISO [download](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022).

##### Image 1: Once downloaded the server file, I created a new machine to be the Windows Server
<img width="1437" height="750" alt="Képernyőkép 2025-11-09 180526" src="https://github.com/user-attachments/assets/c7b6ad0e-a861-488c-aaea-047898aa4b54" />

##### Video 1: Installing the Windows Server on the Virtual Machine
https://github.com/user-attachments/assets/d3df067d-315e-4eb9-a341-745a44a26ed9

## Step 2: Installing AD tools and creating a domain
Once the installation is finished, when logging into the server the Server Manager window automatically comes on. Here is where the AD tool installation can be started.

##### Image 2: To start the AD installation process click on "Manage" and then on "Add Roles and Features" which will open a new window
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
### !!! Important, don't close the installation window as this is where you can promote the server to Domain Controller (DC) !!!

##### Video 2: Here are all the tabs after selecting the desired configurations and features before hitting install
https://github.com/user-attachments/assets/4171fdb3-5ea2-41bf-90fb-3e38084f4e7e

##### Image 3: Once the installation is done you can promote the server to DC by clicking the following button
<img width="1020" height="771" alt="Képernyőkép 2025-11-12 195022" src="https://github.com/user-attachments/assets/9473a724-c860-4143-9a17-123c1be40f9c" />

Promoting the server to DC brings up a new window again, where the domain configurations can be selected. As deployment operation I selected "Add a new forest" and given the name "ad.SZG.com" as the root domain name.

_____________
### 📝 Note 1
*AD forests are root/top level logical containers in an AD environemt. Within it common configurations and directory schemas (defines all object types e.g: users groups etc. and their attributes) and global catalogs (global catalog - an index that contains information about every object within the forest, allowing to quickly search and locate them) are shared. A forest can contain one or multiple domains. These domains within the same forest automatically trust each other enabling secure communications adn resource sharing.*  

*Domain naiming best practice - organisation.local was used in the past frequently as it meant it is not dns resolvable on the public internet. It is however no longer best practice as it can cause issues, one of which is prblem with cloud integration with service providers as they expect publicly routable domain names. As a result using subdomains of actual registered domains is recommended. E.g: ad.organisation.com*
_____________  

##### Video 3: All the configurations, domain names and passwords set just before starting the prerequsites checks and clicking on install. Once done with the installation the server restarted to finalise the installation process of the AD Tools.
https://github.com/user-attachments/assets/27eb6027-cbe9-4527-b2cd-9b8615e40bea

## Step 3: Setting up AD, creating Organisational Units (OUs), Groups and Users
Once the installation is finished, logging back into the server all the AD Tools installed can be access through the Start Menu and under the "Windows Administrative Tools" folder.  
From these tools, now I will be using the "AD Users and Computers" tool.  
##### Image 4: In the new window I can now create the desired OUs, Groups and Users for my domain. It can be done my right clicking on the domain, selecting new and then selecting OU. The same can be done for new groups and users by clicking on the desired OU or Group to which I want to add them to.
<img width="1020" height="769" alt="Képernyőkép 2025-11-12 232715" src="https://github.com/user-attachments/assets/bfc90d54-04dc-4f31-bf72-aa6b37adc3ad" />

  



