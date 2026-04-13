<p align="center">
<img width="2544" height="416" alt="_adbanner" src="https://github.com/user-attachments/assets/9ec096fb-3475-4826-b381-e6226792e685" />
</p>

<h1>Creating Users with PowerShell, Group Policies, & Managing Accounts</h1>

<h2>About this Project</h2>

In this project we are going to create Users using PowerShell which we will use to attempt to log into client-1. Here, we will learn how to deal with Account Lockouts, Enabling and Disabling Accounts, and we will also observe logs via the Domain Controller and on a Client Machine.

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
    - Username: mydomain.com\jane_admin
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
        <img width="967" height="1024" alt="actdir21" src="https://github.com/user-attachments/assets/db7026a3-eca1-41e8-8a69-04c308b0b906"/>
        </details>

4. When finished, open ADUC and observe the accounts in the appropriate OU　(_EMPLOYEES).
        <details><summary>See screenshots</summary>
        <img width="1466" height="659" alt="actdir22" src="https://github.com/user-attachments/assets/2e4885ea-8e41-480f-a67a-cf449903b03b"/>
        </details>
        
5. Attempt to log into Client-1 with one of the accounts (take note of the password in the script).

   
<h3>Managing Group Policy and Dealing with Account Lockouts</h3>

1. Log-in to dc-1 and click Start, and type gpmc.msc in the search box, then press Enter. This opens the Group Policy Management Console.
2. In the GPMC, navigate to Default Domain Policy, right-click and select Edit to modify it.
        <details><summary>See screenshots</summary>
        <img width="751" height="529" alt="actdir25" src="https://github.com/user-attachments/assets/ef7c9921-cb81-4c84-b3ff-def6582e0773"/>
        </details>
        
3. In the Group Policy Management Editor, expand the following:

      Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.
      <details><summary>See screenshots</summary>
      <img width="703" height="514" alt="actdir26" src="https://github.com/user-attachments/assets/923db3f7-b2cc-4e1c-8944-a1381c9ed484" />
      </details>
        
4. By double-clicking on each policy, configure the Account Lockout Policy to the following settings: *(Some settings will be autopopulated after setting Account lockout duration)*
    - Account lockout duration:                30 minutes
    - Account lockout threshold:               5 invalid logon attempts                
    - Allow Administrator account lockout:     Enabled   
    - Reset account lockout counter after:     10 minutes

6. To update the group policy, log-on to a client machine and open Command Prompt then type *gpupdate /force*, then press Enter.
        <details><summary>See screenshots</summary>
        <img width="655" height="396" alt="actdir27" src="https://github.com/user-attachments/assets/7fdd4aa3-0771-43b7-bed0-67138fa354d8" />
        </details>

7. Log-in to dc-1 and pick a random user account you created previously.
   Start > Search Active Directory Users and Computers > expand mydomain.com > expand _EMPLOYEES > select one random User.
        <details><summary>See screenshots</summary>
        <img width="777" height="786" alt="actdir23" src="https://github.com/user-attachments/assets/4b5fe25a-ab07-42a2-b255-a8bafa82a5d1"/>
        <img width="557" height="492" alt="actdir24" src="https://github.com/user-attachments/assets/98902649-765c-423c-8c2c-afe7896f4b9d"/>
        </details>
  
8. Do the following Account lockout steps/exercises. 
    - Using the "random user" you've created previously, attempt to login at client-1 6 times with a bad password.
        <details><summary>See screenshots</summary>
        <img width="555" height="145" alt="actdir28" src="https://github.com/user-attachments/assets/ff3124c7-fad6-4ef1-a230-f86155c5506a" />
        </details>
        
    - Observe that the account has been locked out within Active Directory.
    - Unlock the account at dc-1, open Active Directory Users and Computers, double-click on the User, select Account tab and check/tick "Unlock account". Click Apply and OK.
        <details><summary>See screenshots</summary>
        <img width="1004" height="548" alt="actdir29" src="https://github.com/user-attachments/assets/a1ab19b1-5327-4189-b9e1-4c4bfd1ac655" />
        </details>

    - Reset the password by right clicking on the User, select and Reset Password, check/tick Unlock the user's account, click OK, and attempt to log-back in.
        <details><summary>See screenshots</summary>
        <img width="577" height="536" alt="actdir30a" src="https://github.com/user-attachments/assets/66de568d-7831-40b5-8eb5-eb359eb27ae8" />
        <img width="379" height="258" alt="actdir30" src="https://github.com/user-attachments/assets/37161711-35cf-4e21-947f-75527b8dffdb" />
        </details>
      

<h3>Enabling and Disabling Accounts</h3>

1. Disable the same account in Active Directory. Open ADUC, right-click on the user you want to disable, and click Disable Account.
        <details><summary>See screenshots</summary>
        <img width="576" height="536" alt="actdir31" src="https://github.com/user-attachments/assets/b2c9e379-1264-4fc1-9d8a-eaed67d0c334" />
        </details>
        
2. Attempt to login with it, observe the error message.
        <details><summary>See screenshots</summary>
        <img width="565" height="141" alt="actdir32" src="https://github.com/user-attachments/assets/0ca9fce2-9af9-44b3-b57e-b3da5d2fba03" />
        </details>
        
3. Re-enable the account by oppening ADUC, right-click on the user you want to enable, and click Enable Account. Attempt to log back in. 
        <details><summary>See screenshots</summary>
        <img width="575" height="536" alt="actdir33" src="https://github.com/user-attachments/assets/bd99ab30-2e02-4869-96df-1a65940df132" />
        </details>

<h3>Observing Logs</h3>

1.

<h2>Finishing Up</h2>

<h3>Congratulations...</h3>


<sub>*Having issues and trouble with this Lab Project? Please reach out to easy.patch3668@fastmail.com*</sub>

