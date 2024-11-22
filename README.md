<p align="center">
  <img width="70%" src="https://github.com/user-attachments/assets/ad48c2fb-03f2-4b13-9d20-0c01572069b7" alt="Active Directory Deployment"/>
</p>

<h1 align="center">On-premises Active Directory Deployed in the Cloud (Azure)</h1>

<p align="center">
  In this project, I demonstrate how to set up an on-premises-style Active Directory environment in the cloud using Microsoft Azure. Active Directory (AD) is essential for managing thousands of user accounts, permissions, and devices in one centralized location. This guide walks you through the entire process, from deploying virtual machines to configuring Active Directory and creating users.
</p>

---

<h2>Technologies and Environments Used</h2>
<ul>
  <li><b>Microsoft Azure</b>: Used for creating and managing Virtual Machines (VMs).</li>
  <li><b>Remote Desktop Protocol (RDP)</b>: To remotely access and manage VMs.</li>
  <li><b>Active Directory Domain Services</b>: For managing user accounts, devices, and permissions.</li>
  <li><b>PowerShell</b>: For scripting and automating tasks.</li>
</ul>

<h2>Operating Systems</h2>
<ul>
  <li>Windows Server 2022</li>
  <li>Windows 10 (21H2)</li>
</ul>

---

<h2>Overview of Steps</h2>
<ol>
  <li>Set up the Azure environment by creating Virtual Machines for a Domain Controller and a Client machine.</li>
  <li>Enable communication between the Domain Controller and the Client machine.</li>
  <li>Install and configure Active Directory on the Domain Controller.</li>
  <li>Organize users and security groups in Active Directory.</li>
  <li>Join the Client machine to the domain and verify connectivity.</li>
  <li>Create thousands of users in bulk using a PowerShell script.</li>
  <li>Test the setup by logging into the Client machine as one of the created users.</li>
</ol>

---

<h2>Step-by-Step Implementation</h2>

<h3>1. Setting Up the Azure Environment</h3>
<p>
  I started by creating a <b>Resource Group</b> in Azure to organize the resources I’d need. Within this group, I deployed a Virtual Machine (VM) to act as my <b>Domain Controller (DC-1)</b>. For the operating system, I chose Windows Server 2022.
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/c27d4524-2ee4-418c-af9f-b8cd81c8b789" width="80%" alt="Domain Controller Setup"/>
</p>

<p>
  Next, I created a second VM to act as the <b>Client machine (Client-1)</b>. This machine was set up with Windows 10 and placed in the same virtual network (VNet) as DC-1. I also assigned static private IP addresses to ensure consistent connectivity.
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/4dc201b6-ed39-4972-bdc8-e394ba979c4a" width="80%" alt="Client VM Setup"/>
</p>

---

<h3>2. Verifying Connectivity</h3>
<p>
  To ensure the Client machine could communicate with the Domain Controller, I enabled <b>ICMPv4 (ping)</b> on the Domain Controller's Windows Firewall. This allowed me to test connectivity by sending a continuous ping from Client-1 to DC-1’s private IP address.
</p>
<p>
  Using Remote Desktop Protocol (RDP), I logged into Client-1 and verified the connection by running the <code>ping -t</code> command. After enabling the necessary firewall rule on DC-1, the ping was successful.
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/4956206a-d30f-4ac4-af9f-b8cd81c8b789" width="80%" alt="Ping Test"/>
</p>

---

<h3>3. Installing and Configuring Active Directory</h3>
<p>
  On DC-1, I opened the <b>Add Roles and Features Wizard</b> and installed the <b>Active Directory Domain Services (AD DS)</b> role. I then promoted the server to a Domain Controller and set up a new forest with the domain name <code>mydomain.com</code>. 
</p>
<p>
  After restarting the server, I logged in as a domain administrator to begin configuring Active Directory.
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/4bd7ccb2-623c-4248-b117-3e666c652b6c" width="80%" alt="Active Directory Installation"/>
</p>

---

<h3>4. Organizing Users and Security Groups</h3>
<p>
  Within Active Directory, I created Organizational Units (OUs) to logically group users and devices. These included OUs for employees, admins, and security groups. I added a user named <b>Jane Doe</b> (username: <code>jane_admin</code>) and assigned her to the <i>Domain Admins</i> security group.
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/ceec32e8-2a45-4182-993c-1b85758d0718" width="80%" alt="User and Group Management"/>
</p>

---

<h3>5. Joining the Client Machine to the Domain</h3>
<p>
  Before joining the domain, I updated the Client machine’s DNS settings to use DC-1’s private IP address. This ensured the Client machine could locate the Domain Controller. After this, I went to <b>System → Rename This PC</b> on Client-1 and entered the domain name <code>mydomain.com</code>. The process was completed with a restart.
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/3ccbe7c9-645e-44a2-aaa4-5dfc8722ae1d" width="50%" alt="Join Domain"/>
</p>

---

<h3>6. Creating Users in Bulk</h3>
<p>
  To simulate a real-world scenario, I used a PowerShell script to create thousands of random users. Running this script in <b>PowerShell ISE</b> generated the users and placed them in the <i>_EMPLOYEES</i> Organizational Unit.
</p>
<p align="center">
  <img src="https://i.imgur.com/ez4THWm.png" width="80%" alt="PowerShell Script Execution"/>
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/cd22eb07-2709-41dd-a494-3e742a9f880b" width="80%" alt="Users Created in Active Directory"/>
</p>

---

<h3>7. Testing the Setup</h3>
<p>
  Finally, I logged into Client-1 using one of the newly created user accounts. This verified that the entire setup—from domain configuration to user creation—was successful.
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/3d1f1813-02d4-4218-823b-ea16df7b2434" width="80%" alt="Successful Login"/>
</p>

---

<h2>Summary</h2>
<p>
  This project demonstrated how to deploy and configure an on-premises Active Directory environment in the cloud using Azure. I started by setting up the infrastructure, verified connectivity, installed Active Directory, and created organizational units and users. Finally, I tested the system to ensure everything worked seamlessly.
</p>
<p>
  Through this project, I learned how to leverage cloud technologies to simulate enterprise-level IT environments and gained hands-on experience in Active Directory management, network configuration, and PowerShell automation.
</p>
