---
icon: elementor
---

# Sunbird - Infra Access

#### VPN Access <a href="#vpn-access" id="vpn-access"></a>

Steps to provide vpn access.

* login to vpn using admin credentials [https://vpn.sunbirded.org/admin/](https://vpn.sunbirded.org/admin/)
* Click on user permission under User Managenet
* Add new username and password
* click on save settings
* click on update running server

Steps to connect to vpn:

* Enter the VPN URL: [https://vpn.sunbirded.org/](https://vpn.sunbirded.org/)
* Enter the Details in the form: USERNAME and PASSWORD and click on GO&#x20;
* At the bottom of the New screen, there will be an option to enable MFA (MULTI FACTOR AUTHENTICATION)&#x20;
* Install authenticator app from playstore if using android, or install a chrome extension for authenticator \[This will help you to store the MFA in your personal device]&#x20;
* After MFA is scanned, click on I’ve scanned the MFA, this will redirect you to login part and then reenter the credentials with MFA.
* download the Yourself (user-locked profile) , this is your vpn client key.
* Install vpn client on your local machine
* Connect to VPN using command : sudo openvpn --config client.ovpn

#### Jenkins access <a href="#jenkins-access" id="jenkins-access"></a>

* Share the jenkins url and ask the user to sign up and share username or directly create the user in jenkins. go to manage jenkins → manage users → create user with password.
* Add permission to users: go to **Manage and Assign Roles → Assign Roles →** Add new user in the user/group list and select roles

#### SSH Access <a href="#ssh-access" id="ssh-access"></a>

Use jenkins jobs to provide ssh access to dev and staging servers.

jenkins job path : OpsAdministration/dev/Core/CreateUser

Add hostname, username, encrypted password and public key as parameter

Open Screenshot from 2023-02-02 15-13-20.png![](blob:https://project-sunbird.atlassian.net/87b54f54-4522-4d9d-ab8a-2c902d899005#media-blob-url=true\&id=09c88d8b-2379-48df-af12-418c8ee4176d\&collection=contentId-3278438471\&contextId=3278438471\&mimeType=image%2Fpng\&name=Screenshot%20from%202023-02-02%2015-13-20.png\&size=107611\&width=1506\&height=790\&alt=)

<figure><img src="../../../../../../.gitbook/assets/Screenshot from 2023-02-02 15-13-20.png" alt=""><figcaption></figcaption></figure>

#### Rancher Access <a href="#rancher-access" id="rancher-access"></a>

* login to rancher with admin credentials
* Go to Users → add users → Add username, password and display name
* select standard user in permission section
* click on create user
* To provide access to specific cluster or namespace
* go to Global → select project → namespace
* click on Memeber → Add Member → select user from drop down list
* select project permission → Read Only
* click on create
