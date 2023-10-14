# act_dir
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This section outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>Steps to Setup Active Directory</h2>

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain
- Setup Remote Desktop for non-administrative users on Client-1

<h2>Deployment and Configuration Steps</h2>

<p >
  <h3>Setup Resources in Azure</h3> <br />
  Create the Domain Controller VM (Windows Server 2022) <em>Ex: DC-1</em>. <br />
  Set Domain Controller’s NIC Private IP address to be static. <br />
  Create the Client VM (Windows 10) <em>Ex: Client-1</em> and use the same Resource Group and Vnet that was created before. <br />
  Ensure that both VMs are in the same Vnet. <br />
</p>
<p>
  <h3>Ensure Connectivity between the client and Domain Controller</h3> <br />
  Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping. <br />
  Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall. <br />
  Check back at Client-1 to see the ping succeed. <br />
</p>
<p>
  <h3>Install Active Directory</h3> <br />
  Login to DC-1 and install Active Directory Domain Services. <br/>
  Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is). <br />
  Restart and then log back into DC-1 as your domain name \ username for the domain controller VM. <em>Ex: mydomain.com\user1</em>
</p>
<p>
  <h3>Create an Admin and Normal User Account in AD</h3> <br />
  In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES” and another one called "_ADMINS". <br />

  ![image](https://github.com/steffan-h/act_dir/assets/146549173/d3e442df-d1dc-4480-9e4e-4b1a21d9022c) <br />
  Create a new employee with a name, username, and password. Add this employee to the "Domain Admins" Security Group. <br />

  ![image](https://github.com/steffan-h/act_dir/assets/146549173/38535445-075c-4c21-9d79-412aec638700) <br />
  Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\user”. <br /> <br />
  <em>Ex: mydomain.com\firstlast</em>

  ![image](https://github.com/steffan-h/act_dir/assets/146549173/6dfd6393-5eaa-4952-ba3f-9f726bbd29c0) <br />
  Use this account as your admin account from now on. <br />
</p>
<p>
  <h3>Join Client-1 to your domain (mydomain.com)</h3> <br />
  From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address. <br /> <br />
  <em>Ex: 10.0.0.4 is DC's Private IP</em>

  ![image](https://github.com/steffan-h/act_dir/assets/146549173/53e13921-b7dd-49c6-be14-da5ad7bf8ef4) <br />
  From the Azure Portal, restart Client-1. <br />
  Login to Client-1 (Remote Desktop) as the original local admin and join it to the domain. <br /> <br />
  <em>Ex: Connecting "VM2" to "mydomain.com" with "firstlast" user</em>

  ![image](https://github.com/steffan-h/act_dir/assets/146549173/3e1b4ad0-53b3-4d35-b053-93b63534d066) <br />
  Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain. <br />

  ![image](https://github.com/steffan-h/act_dir/assets/146549173/ef7afdd2-b555-4b11-85df-d0ac67498bb1) <br />
</p>
<p>
  <h3>Setup Remote Desktop for non-administrative users on Client-1</h3> <br />
  Log into Client-1 as mydomain.com\user1 and open system properties and click "Remote Desktop". Allow "Domain Users access to remote desktop. <br />

  ![image](https://github.com/steffan-h/act_dir/assets/146549173/cedce6c5-7d54-404f-8e8b-da950806b402) <br />
  You can now log into Client-1 as a normal, non-administrative user. Create a new user account to test it out.
</p>
