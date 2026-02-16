# <p align="center">Active Directory Deployment & Domain Configuration
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

## Objective
This lab demonstrates:

- Installing Active Directory Domain Services (AD DS)
- Promoting a Domain Controller
- Creating Organizational Units (OUs)
- Creating Domain Admin accounts
- Joining a client machine to the domain
- Configuring Remote Desktop access
- Bulk user creation with PowerShell
- Verifying domain authentication

---

# Part 1 – Domain Controller Setup

## Install Active Directory Domain Services (AD DS)

Logged into **DC-1** and installed Active Directory Domain Services.

<img src="https://i.postimg.cc/zfXzz1Tg/01-dc1-ad-ds-installed-png.png" width="500">

Promoted DC-1 as a Domain Controller and created a new forest:

**mydomain.com**

Restarted and logged back in as:

**mydomain.com\labuser**

<img src="https://i.postimg.cc/R0VSSzwt/02-domain-login-labuser.png" width="500">

---

## Create Organizational Units (OUs)

In Active Directory Users and Computers (ADUC):

- Created OU: **_EMPLOYEES**
- Created OU: **_ADMINS**

<img src="https://i.postimg.cc/52m9WtQp/03-ad-ou-employees-admins.png" width="500">

---

## Create Domain Admin User

Created:

- Name: **Jane Doe**
- Username: **jane_admin**
- Password: **Cyberlab123!**

<img src="https://i.postimg.cc/g0kzzP3R/04-jane-admin-user-created.png" width="500">

Added **jane_admin** to the **Domain Admins** security group.

<img src="https://i.postimg.cc/vmHYYd57/05-jane-admin-domain-admins-group.png" width="500">

Logged out and back in as:

**mydomain.com\jane_admin**

<img src="https://i.postimg.cc/5tN44M8w/06-domain-login-jane-admin.png" width="500">

From this point forward, **jane_admin** was used as the administrative account.

---

## Join Client-1 to the Domain

Steps:

- Set Client-1 DNS to DC private IP (Azure)
- Restarted Client-1
- Logged in as local admin (labuser)
- Joined domain: **mydomain.com**
- Restarted system

Verified Client-1 appears in ADUC.

<img src="https://i.postimg.cc/R0VSSzwQ/07-client1-joined-domain.png" width="500">

Created OU: **_CLIENTS**

Moved Client-1 into the **_CLIENTS** OU.

<img src="https://i.postimg.cc/258kkfnQ/08-client1-in-clients-ou.png" width="500">

---

# Part 2 – Remote Desktop & Bulk User Creation

## Enable Remote Desktop for Domain Users

Logged into Client-1 as:

**mydomain.com\jane_admin**

Configured:

- System Properties → Remote Desktop
- Allowed **Domain Users** access

This allows non-administrative users to log in via Remote Desktop.

Note: In production environments, this would typically be configured using Group Policy for centralized management.

---

## Bulk User Creation via PowerShell

Logged into DC-1 as **jane_admin**

Steps:

- Opened PowerShell ISE as Administrator
- Created a new script file
- Pasted provided bulk-user script
- Executed script

Observed user accounts being created.

Verified new users appear under:

**_EMPLOYEES OU**

---

## Test Domain Login

Attempted login to Client-1 using:

**mydomain.com\babega.gej**  
Password: **Password1**

Successfully authenticated.

---

# Key Concepts Demonstrated

- AD DS installation and forest creation
- Domain Controller promotion
- Organizational Unit (OU) structure
- Security group management
- Domain join process
- DNS configuration for domain connectivity
- Remote Desktop configuration
- PowerShell automation for bulk user provisioning
- Domain authentication verification
