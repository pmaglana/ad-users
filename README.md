<p align="center">
<img width="2544" height="416" alt="_adbanner" src="https://github.com/user-attachments/assets/9ec096fb-3475-4826-b381-e6226792e685" />
</p>

<h1>Creating Users with PowerShell, Group Policies, & Managing Accounts</h1>

<h2>About this Project</h2>

In this project we are going to create users which we will use to attempt to log into client-1. Hers, we will learn how to deal with Account Lockouts, Enabling and Disabling Accounts, and we will also observe logs via the Domain Controller and on a Client Machine.

<h2>Environment & Technology Used</h2>

- Microsoft Azure Virtual Machine 
- Microsoft Windows Server
- Microsoft Windows 10
- Remote Desktop
- Active Directory
- Powershell

<h2>Prerequisites</h2>

1. Setup Domain Controller(VM) in Azure
    - Create the Domain Controller VM (Windows Server 2022) named “DC-1”.
    - Set Domain Controller’s NIC Private IP address to static.
2. Setup Client(VM) in Azure
    - Create the Client VM (Windows 10) named “Client-1”.
    - Attach it to the same Region and Virtual Network as DC-1.
    - Set Client-1’s DNS settings to DC-1’s Private IP address.
3. Credentials:
    - Username: labuser
    - Password: Cyberlab123!
      
<h2>Getting Started</h2>

<h3>Creating multiple users using PowerShell</h3>

1. Login to DC-1 as jane_admin. Open PowerShell_ise as an administrator.
2. Create a new File and paste the contents of this [script](https://github.com/pmaglana/ad-users/blob/main/generate-users) into it, and save it in your desktop.
        <details><summary>See screenshots</summary>
        <img width="896" height="808" alt="actdir20" src="https://github.com/user-attachments/assets/9e6a4d0d-744a-4945-978c-abd06d37b1df"/>
        </details>

3. Run the script and observe the accounts being created.
        <details><summary>See screenshots</summary>
        <img width="967" height="1024" alt="actdir21" src="https://github.com/user-attachments/assets/db7026a3-eca1-41e8-8a69-04c308b0b906" />
        </details>

4. When finished, open ADUC and observe the accounts in the appropriate OU　(_EMPLOYEES).
        <details><summary>See screenshots</summary>
        <img width="1466" height="659" alt="actdir22" src="https://github.com/user-attachments/assets/2e4885ea-8e41-480f-a67a-cf449903b03b" />
        </details>
        
5. Attempt to log into Client-1 with one of the accounts (take note of the password in the script).

   
<h3>Dealing with Account Lockouts</h3>

1. Log-in to dc-1 and pick a random user account you created previously, then attempt to log in with it 10 times with a bad password.


<h3>Enabling and Disabling Accounts</h3>

1.

<h3>Observing Logs</h3>

1.

<h2>Finishing Up</h2>

<h3>Congratulations...</h3>


<sub>*Having issues and trouble with this Lab Project? Please reach out to easy.patch3668@fastmail.com*</sub>

