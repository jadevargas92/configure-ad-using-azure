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

<h2>Operating Systems Used</h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Set up and configure Domain Controller in Azure
- Configure a client VM and join it to the domain
- Install and promote Active Directory Domain Services
- Create domain admins and organize user accounts within OUs
- Enable Remote Desktop for non-administrative users

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Active Directory Configuration Steps"/>
</p>

### 1. Set Up Domain Controller (DC-1) in Azure
   - **Create Resources**: Set up a resource group, virtual network, and subnet in Azure.
   - **Create Domain Controller VM**: Deployed Windows Server 2022 VM named "DC-1".
   - **Configure Networking**: Assigned a static private IP to DC-1 and disabled Windows Firewall for connectivity testing.

### 2. Set Up Client Machine (Client-1) in Azure
   - **Create Client VM**: Created a Windows 10 VM named "Client-1" in the same network and region as DC-1.
   - **DNS Settings**: Configured Client-1's DNS settings to point to DC-1's private IP and confirmed connectivity via ping.

### 3. Install Active Directory Domain Services on DC-1
   - **Active Directory Installation**: Installed and promoted DC-1 to a Domain Controller, setting up a new forest (e.g., `mydomain.com`).
   - **Domain Admin Account**: Created an Organizational Unit (OU) "_ADMINS" and added a new user "Jane Doe" (`jane_admin`) to the "Domain Admins" group.

### 4. Join Client-1 to Domain
   - **Domain Join**: Joined Client-1 to the `mydomain.com` domain and verified its presence in Active Directory Users and Computers (ADUC).
   - **Organizational Structure**: Created a "_CLIENTS" OU and moved Client-1 into this OU for better organization.

### 5. Enable Remote Desktop Access for Domain Users
   - **Remote Desktop Setup**: Allowed "domain users" to access Remote Desktop on Client-1, demonstrating typical access configurations.
   - **Group Policy Note**: Mentioned the potential for automating configurations across multiple systems via Group Policy.

### 6. Bulk User Creation and Domain Login Testing
   - **User Account Creation**: Using PowerShell on DC-1, scripted the creation of multiple user accounts within the "_EMPLOYEES" OU.
   - **Login Verification**: Verified login on Client-1 with one of the newly created user accounts, ensuring account creation and access functionality.

