# Active-Directory
This repository showcases my hands-on experience with Active Directory, including installation, user and group management, Group Policy implementation, and security best practices. This project demonstrates my understanding of enterprise directory services and domain management.

## Overview  
This project showcases my hands-on experience with Active Directory (AD). It includes setting up and configuring an AD environment, managing users and groups, implementing Group Policy, and troubleshooting common issues.  

## Key Features  
✅ **Active Directory Setup** – Installed and configured AD on a Windows Server  
✅ **User & Group Management** – Created and managed users, groups, and organizational units  
✅ **Group Policy Implementation** – Configured GPOs to enforce security and user settings  
✅ **DNS & DHCP Configuration** – Set up and managed domain name resolution and IP assignment  
✅ **Security Best Practices** – Implemented access controls, permissions, and auditing  

## Technologies Used  
- Windows Server  
- Active Directory Domain Services (ADDS)  
- Group Policy Management  
- DNS & DHCP  
- PowerShell  

## What I Learned  
- How to install and configure an AD environment from scratch  
- The importance of organizational units and group policies  
- How to manage and automate tasks using PowerShell  
- Security best practices for an enterprise environment  

## Step 1: Setting Up the Domain Controller in Azure

### 1. Create a Resource Group
In the Azure Portal, navigate to Resource Groups and create a new one.

### 2. Create a Virtual Network and Subnet
Create a Virtual Network (VNet) and assign a Subnet for communication between VMs.

### 3. Create the Domain Controller VM (Windows Server 2022)
Create a new Windows Server 2022 VM named DC-1.
- **Username**: labuser
- **Password**: Cyberlab123!
Attach the VM to the previously created Virtual Network.
Set DC-1’s NIC Private IP address to static.
After VM creation, disable Windows Firewall for testing connectivity.

## Step 2: Setting Up the Client Machine in Azure

### 1. Create the Client VM (Windows 10)
Create a new Windows 10 VM named Client-1.
- **Username**: labuser
- **Password**: Cyberlab123!
Attach Client-1 to the same Virtual Network as DC-1.
Set Client-1’s DNS settings to DC-1’s Private IP.
Restart Client-1 via the Azure Portal.

### 2. Verify Network Connectivity
Log in to Client-1.
Open Command Prompt and ping DC-1’s private IP address.
Open PowerShell and run `ipconfig /all` to confirm DNS settings show DC-1’s Private IP.

## Step 3: Installing Active Directory

### 1. Install Active Directory Domain Services (AD DS)
Log into DC-1 and open Server Manager.
Select **Manage** → **Add Roles and Features**.
Choose Active Directory Domain Services (AD DS) and install.
Promote the server to a Domain Controller, setting up a new forest as `mydomain.com`.
Restart DC-1 and log back in as `mydomain.com\labuser`.

## Step 4: Creating Users and Groups

### 1. Create Organizational Units (OUs)
Open Active Directory Users and Computers (ADUC).
Create the following OUs:
- _EMPLOYEES
- _ADMINS

### 2. Create a Domain Admin User
In _ADMINS, create a new user:
- **Name**: Jane Doe
- **Username**: jane_admin
- **Password**: Cyberlab123!
Add `jane_admin` to the Domain Admins Security Group.
Log out and back in as `mydomain.com\jane_admin`.

## Step 5: Joining Client-1 to the Domain

### 1. Configure Client-1 for Domain Join
Log into Client-1 as `labuser`.
Open **System Properties** → **Change settings**.
Enter the domain name `mydomain.com` and authenticate with `jane_admin`.
Restart Client-1.
Verify in ADUC that Client-1 appears under Computers.
Move Client-1 into the _CLIENTS OU.

## Step 6: Configuring Remote Desktop for Users
Log into Client-1 as `mydomain.com\jane_admin`.
Open **System Properties** → **Remote Desktop**.
Allow Domain Users access to Remote Desktop.

## Step 7: Creating Bulk Users and Testing Authentication

### 1. Create Multiple Users via PowerShell
Log into DC-1 as `jane_admin`.
Open PowerShell ISE as Administrator.
Run a script to generate multiple user accounts in _EMPLOYEES.
Verify in ADUC that the accounts were created.
Attempt to log into Client-1 with one of the new users.

## Step 8: Configuring and Testing Account Lockout Policy

### 1. Implement Account Lockout Policy
Configure Group Policy to lock an account after 5 failed login attempts.
Attempt to log in 6 times with an incorrect password.
Observe that the account is locked.

### 2. Unlock and Reset a User Account
Log into DC-1.
Open ADUC and unlock the locked user account.
Reset the password and attempt to log in again.

### 3. Enabling and Disabling Accounts
Disable a user account in ADUC.
Attempt to log in and observe the error message.
Re-enable the account and test login again.

## Step 9: Observing Logs
Open Event Viewer on DC-1 and Client-1 to observe security logs.
Review authentication attempts, account lockouts, and login failures.

## Conclusion
This walkthrough provides a step-by-step guide to deploying and managing an Active Directory environment in Azure. The lab reinforced essential skills, including domain controller setup, user and group management, Group Policy enforcement, and troubleshooting domain connectivity.
