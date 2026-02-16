# <p align="center">Active Directory Deployment
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>


## Project Summary

This project demonstrates the deployment and configuration of Active Directory Domain Services within a Microsoft Azure environment. The lab includes domain controller promotion, Organizational Unit (OU) creation, administrative account provisioning, and domain joining of client machines.

### Languages Used
- PowerShell (basic administrative tasks)

### Environments Used
- Microsoft Azure
- Windows Server (Domain Controller)
- Windows 10 (Client Machine)

### Technologies / Services Used
- Active Directory Domain Services (ADDS)
- Azure Virtual Machines
- Azure Networking
- Remote Desktop Protocol (RDP)


---
# Demonstration
## Step 1 – Install Active Directory Domain Services

Logged into **DC-1** and installed **Active Directory Domain Services (ADDS)**.

<img src="https://i.postimg.cc/zfXzz1Tg/01-dc1-ad-ds-installed-png.png" width="500">

Promoted DC-1 as a Domain Controller and created a new forest:

**mydomain.com**

Restarted the server and logged back in as:

**mydomain.com\labuser**

<img src="https://i.postimg.cc/R0VSSzwt/02-domain-login-labuser.png" width="500">

---

## Step 2 – Create Organizational Units (OUs)

Opened **Active Directory Users and Computers (ADUC)** and created:

- OU: **_EMPLOYEES**
- OU: **_ADMINS**

<img src="https://i.postimg.cc/52m9WtQp/03-ad-ou-employees-admins.png" width="500">

---

## Step 3 – Create Domain Admin User

Created new user:

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

## Step 4 – Join Client-1 to the Domain

- Set Client-1 DNS to DC-1’s private IP address (Azure)
- Restarted Client-1
- Logged in as local admin (**labuser**)
- Joined domain: **mydomain.com**
- System restarted

<img src="https://i.postimg.cc/R0VSSzwQ/07-client1-joined-domain.png" width="500">

---

## Step 5 – Verify Domain Join

- Verified **Client-1** appears in ADUC
- Created OU: **_CLIENTS**
- Moved Client-1 into **_CLIENTS** OU

<img src="https://i.postimg.cc/258kkfnQ/08-client1-in-clients-ou.png" width="500">

---

## Result

- Active Directory successfully installed
- Domain Controller configured
- Domain Admin account created
- Client machine successfully joined to domain
- Organizational Unit structure established

