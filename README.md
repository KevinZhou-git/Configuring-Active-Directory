![image](https://github.com/user-attachments/assets/20a01d72-348c-49f9-bdda-680121d559ba)

# Configuring Active Directory
This tutorial will guide you through Active Directory Domain Services and how to setup an admin account, organizational units, and creating new users with a script to simulate the onboarding on employees and production workstations.

## Environments and Technologies
- Microsoft Azure
- Remote Desktop
- Active Directory Domain Services
- PowerShell

## Operating Systems
- Windows Server 2022
- Windows 10

## Creating Organizational Units
- Connect to the domain controller that was created in the last tutorial through Remote Desktop.
- Open Active Directory Users and Computers -> New -> Organizational Unit.
- Create an organization unit for employees and admins. 
![image](https://github.com/user-attachments/assets/3daa3a3b-7e4a-4ca4-85a4-0ae5911281c2)
![image](https://github.com/user-attachments/assets/4f6174c5-1cf0-4466-a21c-cfb1cc1efd87)

## Creating an Admin User Account
- Right click on our admins organizational unit -> New -> User -> Fill out the information and assign a password
  - Uncheck "User must change password at next logon"
  - Check "Password never expires"
![image](https://github.com/user-attachments/assets/2cf2139b-c7ea-4b6a-8367-a43865bb6439)
![image](https://github.com/user-attachments/assets/12dcc8a0-f0d7-4244-81a8-fa9e531f55a9)

## Assigning the New Admin to the Admins Security Group
- Right click on our new admin user -> New -> Properties
- Click Member Of -> Add -> Type Domain -> Check Names -> Domain Admins and select Ok
![image](https://github.com/user-attachments/assets/99dd2910-85c7-4a64-afc5-6eaf81db15b4)
![image](https://github.com/user-attachments/assets/cc0934d1-b24a-4c85-9e0c-59c7dc07b69e)
![image](https://github.com/user-attachments/assets/4d2311ca-99a5-46d1-922b-5067b1cd1dc5)
![image](https://github.com/user-attachments/assets/eeeee95b-4d46-49ea-8be2-c16a4798b02e)
- Signout and login with our new admin user credentials
- You should now be signed into the admin user account
![image](https://github.com/user-attachments/assets/6143e917-d340-4cfc-8ac8-12e9c197d6b2)

## Joining the Client to the Domain Controller
- Connect to our client virtual machine.
- Right click on Start -> System -> Rename this PC (advanced).
- Click Change -> Domain -> Type in mydomain.com -> Ok.
- Enter the client virtual machine credentials.

![image](https://github.com/user-attachments/assets/6b4c2dd5-1930-433f-82c6-90f058fd9edb)
![image](https://github.com/user-attachments/assets/6312b3f9-d2a5-4e60-890b-3add6f288443)
![image](https://github.com/user-attachments/assets/19cf4c47-a609-432f-b67c-bacd3775eb91)
![image](https://github.com/user-attachments/assets/a4444c4e-9f86-4d5c-9ee3-6ba79ac6674b)

- To verify that the client has been joined to the domain, open Active Directory Users and Computers -> Computers -> Your client should be here.
  
![image](https://github.com/user-attachments/assets/fe04e15f-ec76-4f92-a40a-b4fc99fb505d)

## Setting up Remote Desktop for Users/Non-admin Users
- On the client virtual machine, right click System -> Properties -> Remote Desktop -> select users that can remotely access this PC.
- Click Add -> Type Domain Users -> Check Names -> Enter credentials -> Ok.
![image](https://github.com/user-attachments/assets/b0f5747e-deaa-457b-aeb2-33583c356c28)
![image](https://github.com/user-attachments/assets/5544169f-65d2-4164-9658-b512b282818d)

Now all domain users can access the client.

## Creating users with PowerShell
- To create a large number of users, we will use a script provided [here](https://github.com/AsiaPonder001/BunchofUsers/blob/main/README.md?plain=1)
- Click RAW at the top right and copy the text.
![image](https://github.com/user-attachments/assets/cbfb33d2-9a43-49cd-9409-0ba7b509db79)
- Open PowerShell ISE and run as an administrator on the domain controller virtual machine.
- Click New Script -> paste the script -> Run Script
![image](https://github.com/user-attachments/assets/f1d45ff9-208e-467c-b97b-295f2512745d)
![image](https://github.com/user-attachments/assets/9fc3b097-27f9-4851-afc1-23ccd4de4962)

We have now created a number of new users and they can be found in the _EMPLOYEES organization unit.
![image](https://github.com/user-attachments/assets/127402d8-83c3-4b06-935f-16ec8520b197)

## Testing the Login Credentials of a Newly Created User
- Simply sign in using one of the names of a newly created user. The password is **Password1** as specified in the script.

## BONUS: Setting Group Policies and Password
- If you would like to perform various tasks such as adding a user to a new group, resetting a password, disable the user, you can simply right click the user and select the appropriate option.
![image](https://github.com/user-attachments/assets/b853adac-6c47-44ad-8cc7-5ba734888c51)

- You can also set group policies such as password policy, account lockout policy, Kerberos policy, and more.
- Open Group Policy Management -> Forest: mydomain.com -> Domains -> mydomain.com -> Group Policy Objects -> Default Domain Policy -> settings.
- Alternatively open Group Policy Management Editor by right clicking a policy and clicking edit.
![image](https://github.com/user-attachments/assets/d35a3389-3569-40d7-96fa-86df66f93ad0)
![image](https://github.com/user-attachments/assets/f1356c98-4e1e-402e-9d58-b6cd63216f3c)
