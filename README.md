<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory deployed in the Cloud (Azure)</h1>
This guide outlines the implementaiton of Active Directory within Azure Virtual Machines.<br/>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create a Resource group
- Create a Virtual Network
- Create the Domain Controller and Client Virtual Machines
- Set the Domain Controllers private IP address to static
- Set the Client VM's DNS settings to the DC's private IP
- Use Remote Desktop to access our DC and install Active Directory Domain Services
- Promote the server to a domain controller
- Create a domain admin user inside an organizational unit
- Join the client VM to the domain
- Allow non-admin users to login to client VM

<h2>Deployment and Configuration Steps</h2>
Search for Resource Groups or use the portal menu to navigate to Resource Groups.
<img width="518" height="301" alt="image" src="https://github.com/user-attachments/assets/fa17ed58-33f4-4db1-8e52-ec46f7437d50" /> <br/>

Once you are in Resource Groups, click on create. Then give a name to the Resource Group and select the region you would like to use. (Note: Use the same region for the other parts of the demonstration, as using a different one will prevent the virtual machines from communicating properly. This is more important for the future steps.) <br/>
<img width="749" height="373" alt="image" src="https://github.com/user-attachments/assets/c227d747-5e02-42c9-b325-d2b8c971ee23" /> <br/>

Finally, click Review and Create. Press the create button on the bottom. (Note: May take Azure a few to deploy it.)<br/>
Confirm the Resource Group is deployed. 
<img width="2487" height="136" alt="image" src="https://github.com/user-attachments/assets/2c816940-8008-4d4e-9548-769a50e80c07" /> <br/>

Search for Virtual Networks or use the portal menu to navigate to Virtual Networks. Then click create. <br/>
In the basics tab, select the Resource Group from the previous step. Give your Virtual Network a name and keep the region the same as the last step. Then click Review and create, and press the create button to make the virtual network. (Note: This will take some time for Azure to make.) <br/>
<img width="849" height="707" alt="image" src="https://github.com/user-attachments/assets/23cfca5e-d330-4db7-a3e5-656831982ead" /> <br/>

Search for Virtual Machines or use the portal menu to navigate to Virtual Machines. Then click create, and select virtual machine. <br/>
<img width="707" height="662" alt="image" src="https://github.com/user-attachments/assets/a7dff7f2-bd61-4a45-9c77-d0d7fe4ed881" /> <br/>

To create our Domain Controller virtual machine, in the basics tab, select the resource group that was made earlier. Give a name to the VM. Select the same region as the virtual network. Under the Image option, select Windows Server 2022. Select a size that suits your needs (Note: The choice you make can be determined by the level of processing power you want and your budget.) Then create a username and password for the VM.
<img width="942" height="1143" alt="image" src="https://github.com/user-attachments/assets/4518fc68-367c-4dfd-aaa6-0634eaa6d8ee" />

In the networking tab, select the Virtual Network that was made previously.
<img width="773" height="218" alt="image" src="https://github.com/user-attachments/assets/40f41d50-e9bc-483a-9d8c-3b5852900eef" /> <br/>

Then Review and create your virtual machine. <br/>
For the client VM, follow the same steps as the other virtual machine, except under the image option, select Windows 10 Pro version 22H2, and check the licensing box at the bottom. Then create the virtual machine. <br/>

To set the Domain controller's IP address to static, we select our virtual machine. Then select Networking, followed by Network settings, and then click on the Network interface/IP configuration to access the virtual NIC settings.
<img width="801" height="576" alt="image" src="https://github.com/user-attachments/assets/40ac3a8a-1a09-48b8-9229-cfffd47c6d4b" />

Click on ipconfig 1. Then, under allocation, select Static and save the settings. <br/>
<img width="1599" height="489" alt="image" src="https://github.com/user-attachments/assets/37d93018-22d4-4f08-8c55-e245a2b78e70" /> <br/>

To set the Client VM's DNS settings to the DC's private IP, we select our virtual machine. Then select Networking, followed by Network settings, and then click on the Network interface/IP configuration to access the virtual NIC settings. Then, under settings, select DNS servers, select Custom. Then, enter the private IP address of the Domain Controller under DNS server and click save. <br/>
<img width="587" height="414" alt="image" src="https://github.com/user-attachments/assets/d3ca1f19-84cb-48ce-a709-2d3bed842270" /> <br/>

We will use Remote Desktop to access our Domain Controller VM. Open Remote Desktop. Enter the public IP Address of the Domain Controller VM. Click Connect, then enter the username and password used for the VM.
<img width="1468" height="711" alt="image" src="https://github.com/user-attachments/assets/690d018f-b0ed-40bc-8582-29677268e36e" /> <br/>

Once the connection to the virtual machine is made, open the server manager and select Add Roles and Features.
<img width="951" height="418" alt="image" src="https://github.com/user-attachments/assets/086f04af-ab1d-4be2-8bea-21bcca84b9d0" /> <br/>

Proceed through the steps by clicking next when we reach server selection, make sure to select the correct server. (Note: There is only one in the example. This applies if you have more than one available server.) Click next. <br/>
<img width="779" height="549" alt="image" src="https://github.com/user-attachments/assets/ed604821-af2c-4628-b671-5b527ee2d573" /> <br/>

Under Server Roles, check the "Active Directory Domain Services" box. Add the feature and click next until you reach the confirmation page. <br/>
<img width="785" height="552" alt="image" src="https://github.com/user-attachments/assets/e212a8f7-2e8e-4f86-9a30-f3f25ab17186" />

Once you reach the confirmation page, check the top box and click install to add the features.
<img width="777" height="552" alt="image" src="https://github.com/user-attachments/assets/4ca3e0e9-22b9-4506-a603-78ade884effb" /> <br/>

Once the installation is complete, click on the flag and select "promote this server to a domain controller." <br/>
<img width="2417" height="383" alt="image" src="https://github.com/user-attachments/assets/555d6b10-22f1-425c-93a0-e9de499f65e0" /> <br/>

Select, Add a new forest. Enter a name in the Root domain name. Then click "next" for the remaining steps until you reach the Prerequisites Check tab. <br/>
<img width="753" height="551" alt="image" src="https://github.com/user-attachments/assets/a1f1a088-fa3f-4297-afee-4abfebb372ff" /> <br/>

Once the check is complete, click install. (Note: This will restart the VM so the connection wtih remote desktop will end) <br/>
<img width="753" height="555" alt="image" src="https://github.com/user-attachments/assets/cd6bc295-90ac-4934-9b59-8eafb84f3e65" />

Reconnect to the Domain Controller VM. The username will (domain\username) i.e "mydomain.com\labuser" in this instance. <br/>

Upon successful login, open "Active Directory Users and Computers". Right-click on the domain to create a new Organizational Unit. <br/>
<img width="637" height="528" alt="image" src="https://github.com/user-attachments/assets/d8242f84-1dd7-4183-a158-c729c5ddea12" /> <br/>

Right-click on the organizational unit from the previous step to create a user. Fill in the information for the user. (name, username, etc.) <br/>
<img width="434" height="371" alt="image" src="https://github.com/user-attachments/assets/4aa5245f-592c-44c3-86b7-21084a1bd08c" /> <br/>

Right-click on the user. Select "properties", followed by "Member Of", and click "Add". Then enter Domain admins (click check names to make sure the built-in group is selected). Then apply the settings.
<img width="866" height="598" alt="image" src="https://github.com/user-attachments/assets/30c490a0-6889-46a0-bebe-d261bc176c9a" /> <br/>

Now log in to the client VM using the local admin. Navigate to Windows settings. Go to the about page and click on "Rename this PC (advanced)". Under the "Computer Name" tab, click "Change". Under "Member of", select "Domain" then enter the domain name. Then, enter the admin user credentials. <br/>
<img width="1237" height="1006" alt="image" src="https://github.com/user-attachments/assets/34f50b48-5fa9-452a-81ab-817ae1410b9d" /> <br/>

This pop-up should appear if successful. Then restart the machine.<br/>
<img width="350" height="185" alt="image" src="https://github.com/user-attachments/assets/d0d1785a-7bb6-46b3-9e03-1cf46017e266" /> <br/>

To confirm the client is joined to the domain, log in to the domain controller under the admin account. Open "Active Directory Users and Computers". Click on "computer" to check if the client machine is joined. <br/>
<img width="790" height="551" alt="image" src="https://github.com/user-attachments/assets/828a6cdf-1164-4dc6-8a61-2a4ba43b9dad" />

Now we will configure the settings to allow other users access to the client VM. Log in to the client VM with the admin credentials. Go to the Windows settings under Remote Desktop. Click on the line under "User Accounts". Click "Add". Then enter "domain users" and click "Check Names". And confirm it. This will allow all users in the domain to use the client VM remotely. <br/>
<img width="919" height="1017" alt="image" src="https://github.com/user-attachments/assets/84a7b11f-555d-406a-990f-191bfcaa50e1" />
