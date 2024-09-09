<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure (Create Domain Controller and Client with the use of Virtual Machines)
- Set Domain Controller's NIC Private IP Address to Static
- Set Client's DNS server to Domain Controller's Private IP Address
- Ensure Connectivity between the Client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in Active Directory
- Join Client to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create users and log into Client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

<h3>Part 1: Setup Resources in Azure</h3>

- Create Resource Group and click Review and Create

  ![image](https://github.com/user-attachments/assets/398b7635-93dc-4d5f-b3d9-a490779d8964)

- Create Domain Controller VM w/ Windows Server 2022 and name it "DC-1"

  ![image](https://github.com/user-attachments/assets/ce5f478a-c1d8-4cbe-b172-69a456da3ccd)

- Select at least 2 virtual cpus and 16 GB of RAM for the size
- Create an username and password

  ![image](https://github.com/user-attachments/assets/922fc9d2-52d0-440e-96f0-af5bb6f43d26)

- Take note of the name of the Vnet because it will be used when creating Client-1 VM and then click Create and Review

  ![image](https://github.com/user-attachments/assets/338bc54e-5352-409b-ae9c-f3d8c9f2f023)

- Create Client-1 VM

- Follow the steps about to create another VM but name it Client-1 and select Windows 10 Pro for the image and with the same resource group

  ![image](https://github.com/user-attachments/assets/1cd22175-66fd-45fa-a7ce-2046833b7c3f)

- Create another username and pasword and navigate to the networking tab and make sure to select the same Vnet that was created for DC-1

  ![image](https://github.com/user-attachments/assets/46fb8c84-1411-4b25-8c30-3d41fb1a9ffa)

- Click Review and Create

<h3>Part 2: Set DC-1's NIC Private IP Address to Static</h3>

- Click on DC-1 under Virtual Machines
- Click Network Settings and then click DC-1's Network Interface / IP configuration

  ![image](https://github.com/user-attachments/assets/0b532826-1170-4ff3-9316-ca569af06d15)

- Click on "ipconfig" and then change Private IP address settings from Dynamic to Static and click Save

  ![image](https://github.com/user-attachments/assets/9bcaff70-e755-4865-b0ec-a1a313ab74e3)

<h3>Part 3: Set Client's DNS server to Domain Controller's Private IP Address</h3>

- In Client-1's VM click Network Settings and click Network Interface / IP configuration

- On the left, click DNS Servers

- Under DNS Servers, Select Custom

- Where it says Add DNS Server, paste DC-1's private IP Address and save

  ![image](https://github.com/user-attachments/assets/7189e34a-e349-4c9b-a64f-d2d47d172c40)

<h3>Part 4: Ensure Connectivity between the client and Domain Controller</h3>

- Login to Client-1 with Remote Desktop and ping DC-1's private IP address with "ping -t <IP address>

  ![image](https://github.com/user-attachments/assets/2ecfe550-13f5-475d-87c2-9f4c5add25dd)

- Login into the Domain Controller and enable ICMPv4 in on the local windows Firewall

  ![image](https://github.com/user-attachments/assets/59f215c0-940e-467a-ab9b-f3a1d2a9e428)

- Check back at Client-1 to see the ping succeed
  
  ![image](https://github.com/user-attachments/assets/26580831-56db-4ac3-b751-ea73601bd332)

<h3>Part 5: Install Active Directory</h3>

- Login to DC-1 and Install Active Directory Domain Servies

- Open Server Manage
    - Click Add Roles and Features
      
       ![image](https://github.com/user-attachments/assets/65fa617e-f1a9-4ed7-aa66-c0ed275f5bcd)

    - Click Next
    - Click Next again
    - Under Server Selecton, choose DC-1
    - Under Server Roles, check Active Directory Domain Services, click Add Features
    - Click Next the rest of the way until clicking Install (can optionally check automatically restart server before clicking install)
 
      ![image](https://github.com/user-attachments/assets/f996aeaf-b4ed-4feb-845e-35084f1c35e7)

- Promote as DC: Setup a new forest as mydomain.com (can be anything, this is just what I decided to choose and make sure you don't forget what it is)

- Click the yellow warning flag at the top right and then select Promote this server to a domain controller

  ![image](https://github.com/user-attachments/assets/05542847-80f7-47a2-b240-a028643ae392)

- Select Add a New Forest, create a root domain name, and click next

  ![image](https://github.com/user-attachments/assets/286e35f6-fe47-4aa1-83f7-d1d1cb288071)

-Create a password and click next

- Uncheck create DNS delegation and click next

  ![image](https://github.com/user-attachments/assets/8cabff9d-918f-4165-bebb-7faeecbbaaf3)

- Let it autofill the NETBIOS domain name and click next

- Click next until you get to install and just install

- Restart and then log back into DC-1 as user: mydomain\<username>

<h3>Part 6: Creat an Admin and Normal User Account in AD</h3>

<h3>Part 7: Join Client-1 to your Domain (mydomain.com)</h3>

<h3>Part 8: Setup Remote Desktop for Non-Administrative Users on Client-1</h3>

<h3>Part 9: Create Users and log into Client-1 with one of the users</h3>

