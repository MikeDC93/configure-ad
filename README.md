<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1. Setup virtual machines in azure (Domain controller and client 1)
- Step 2. Create connectivity between the domain controller and client 1 
- Step 3. Installing Active Directory 
- Step 4. Creating admin and users in Active Directory
- Step 5. Joinging client 1 to the domain
- Step 6. Allowing non administrators accesess to use remote desktop
- Step 7. Creating users and logging into client 1 with one of them  

<h2>Deployment and Configuration Steps</h2>

Step 1. Setup virtual machines in azure (Domain controller and client 1) (remember user name and password)
  
  -Create VM (Windows Server 2022) named DC-1 
  
  -Create VM (Windows 10 Pro) named Client-1 
<p><img src="https://i.imgur.com/Wdp177A.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>



-Change DC-1 NIC private address from dynamic to static

<p><img src="https://i.imgur.com/68rMBQQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

-Make sure DC-1 and Client-1 are in the same virtual network
<p><img src="https://i.imgur.com/tNG5Lam.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p><img src="https://i.imgur.com/LZPeYfc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
    
Step 2. Create connectivity between the domain controller (DC-1) and client 1
 <p></p> 
 
  
-Log into DC-1 with remote desktop 

-In remote desktop enable ICMPv4 in the windows firewall.

<p><img src="https://i.imgur.com/VW8iKzP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p><img src="https://i.imgur.com/6cuKDRO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

-Log into Client-1 with remote desktop

-While logged into Client-1 ensure connectivity with DC-1 by pinging DC-1 private address
<p><img src="https://i.imgur.com/ZeYNLn3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p><img src="https://i.imgur.com/qeiQTKd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
  
</p>
 
 
 Step 3. Installing Active Directory<p>
   
 
 
  <p>
  -Using DC-1 remote desktop install Active Directory Domain Services using server manager
    <p><img src="https://i.imgur.com/pFckTNa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
    
    
  -Create a new forest www. (can be anything) .com and promte DC-1 into a Domain Controller (remember what you name it)
  <p><img src="https://i.imgur.com/idN2zMp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

  -Restart DC-1
   <p><img src="https://i.imgur.com/z6H8FYp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

  -Log back into DC-1 as user thedomain.com\labuser
  <p><img src="https://i.imgur.com/xJNcPW9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

  Step 4. Creating admin and users in Active Directory

  -In Active Directory Users and Computers create an Organizational Unit called “_EMPLOYEES”<p>

  
  -Create a new organizational unit named "ADMINS"
  <p><img src="https://i.imgur.com/aOXMuRh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><
                                                                                                          
                                                                                                          
  </p>
  -Create a new user named Jane Doe(can be any name)<P>
  <p><img src="https://i.imgur.com/VlKqFwk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><
  <p><img src="https://i.imgur.com/3BoaHnQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><



  -Move or drag Jane Doe to admins orginizational group
  <p><img src="https://i.imgur.com/uMLogdQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>

-Right click Jane Doe and go into Properties and in the members of tab add Jane Doe to Domain Admins
  <p><img src="https://i.imgur.com/5jsClqs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>

  -Log out of DC-1 and log back in as thedomain.com\jane-admin  (use Jane Doe password)<p>



  


  Step 5. Joinging client 1 to the domain

 -In azure go to Client-1 and set the DNS settings to DC-1 private address then restart Client-1
  <p><img src="https://i.imgur.com/8RnXYZl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>

  -Log into Client-1 and join Client-1 to the domain.
  
  -In Client-1 remote desktop go to system and rename this PC Advanced
  <p><img src="https://i.imgur.com/VCxA0NS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>

    -Log into DC-1 (Domain Controller) and verify Client-1 shows up in Active Directory Users and Computers in the computers container
  <p><img src="https://i.imgur.com/zxYvfc6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>


    Step 6. Allowing non administrators accesess to use remote desktop

    -Log into Client-1 as thedomain.com\jane-admin and open system properties.
  <p><img src="https://i.imgur.com/kZoNtbc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>
  <p><img src="https://i.imgur.com/F37C4ak.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>


    
    -Click "Remote Desktop", And under "User Accounts" select users that can remotely accses this computer add "Domain Users" 
  <p><img src="https://i.imgur.com/F37C4ak.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>
  <p><img src="https://i.imgur.com/s45C6L7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>

  -You can now log into Client-1 as a normal, non-administrative user now

  Step 7. Creating users and logging into client 1 with one of them  

  -Log into DC-1 as jane-admin
  
  -Open PowerShell_ise as an administrator

  <p><img src="https://i.imgur.com/gIk3vNk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>

  <p><img src="https://i.imgur.com/RGCGgjT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>

  -Create a new file and paste the provided script file below.
  https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1

  -Run the scripts and watch the new accounts being created

  <p><img src="https://i.imgur.com/tCD91Rr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>


  -While the accounts are being created go into Active Directory and view the new accounts in _EMPLOYEES OU

  <p><img src="https://i.imgur.com/ZKrinbB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>

  -log out of Client-1 and attepmt to log into Client-1 with one ot the new users/accounts

  <p><img src="https://i.imgur.com/GkDazSd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>

  <p><img src="https://i.imgur.com/15bKx5U.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><<p>

 End.



  


    
  









  
