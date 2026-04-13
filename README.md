# <p align="center">Active Directory Deployment</p>
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

---

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

---

## Step 1 – Install Active Directory Domain Services

1. Log into **DC-1** using Remote Desktop.  
2. Open **Server Manager**.  
3. Click **Add Roles and Features**.  
4. Select:
   - Role-based or feature-based installation  
   - Choose **DC-1** as the target server  
5. Under Server Roles:
   - Check **Active Directory Domain Services (ADDS)**  
6. Complete the installation.  

<img src="https://i.postimg.cc/zfXzz1Tg/01-dc1-ad-ds-installed-png.png" width="500">

---

### Promote DC-1 to a Domain Controller

7. Click the **notification flag** in Server Manager.  
8. Select **Promote this server to a domain controller**.  
9. Choose:
   - **Add a new forest**  
   - Domain name: `mydomain.com`  
10. Complete the wizard and restart the server.  

---

After the server restarts, log in using your domain credentials:

- **Username:** `mydomain.com\labuser`  
- **Password:** (the password you set when creating the VM)

<img src="https://i.postimg.cc/R0VSSzwt/02-domain-login-labuser.png" width="500">

---

## Step 2 – Create Organizational Units (OUs)

1. Open **Active Directory Users and Computers (ADUC)**.  
2. Right-click your domain (`mydomain.com`).  
3. Select **New → Organizational Unit**.  

Create the following OUs:
- `_EMPLOYEES`  
- `_ADMINS`  

<img src="https://i.postimg.cc/52m9WtQp/03-ad-ou-employees-admins.png" width="500">

---

## Step 3 – Create Domain Admin User

### Create the User

1. Navigate to the `_ADMINS` OU.  
2. Right-click → **New → User**.  
3. Enter:
   - Name: Jane Doe  
   - Username: `jane_admin`  
   - Password: `Cyberlab123!`  

<img src="https://i.postimg.cc/g0kzzP3R/04-jane-admin-user-created.png" width="500">

---

### Add User to Domain Admins Group

4. Open **jane_admin** properties.  
5. Go to the **Member Of** tab.  
6. Click **Add** and enter:
   - `Domain Admins`  

<img src="https://i.postimg.cc/vmHYYd57/05-jane-admin-domain-admins-group.png" width="500">

---

### Log in as Admin

7. Log out and sign back in using:

<img src="https://i.postimg.cc/5tN44M8w/06-domain-login-jane-admin.png" width="500">

From this point forward, **jane_admin** is used as the administrative account.

---

## Step 4 – Join Client-1 to the Domain

### Configure DNS

1. Log into **Client-1**.  
2. Open:
   - Control Panel → Network and Internet → Network Connections  
3. Right-click your network adapter → **Properties**.  
4. Select:
   - Internet Protocol Version 4 (IPv4)  
5. Set Preferred DNS Server to:
   - **DC-1’s private IP address**  

---

### Join the Domain

6. Right-click **This PC** → Properties.  
7. Click:
   - **Rename this PC (Advanced)** → Change  
8. Select:
   - Domain → `mydomain.com`  
9. Enter credentials:
   - `mydomain.com\jane_admin`  
10. Restart the machine.  

<img src="https://i.postimg.cc/R0VSSzwQ/07-client1-joined-domain.png" width="500">

---

## Step 5 – Verify Domain Join

1. On **DC-1**, open **Active Directory Users and Computers (ADUC)**.  
2. Navigate to:
   - Computers  
3. Confirm that **Client-1** appears.  

---

### Organize Client Machine

4. Create a new OU:
   - `_CLIENTS`  
5. Move **Client-1** into `_CLIENTS`.  

<img src="https://i.postimg.cc/258kkfnQ/08-client1-in-clients-ou.png" width="500">
