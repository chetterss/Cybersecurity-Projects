## Configuring Firewalls on Windows

In this lab I will be configuring inbound and outbound traffic rules on a windows server firewall and monitoring the logs produced by the firewall.

### Install the web server

First I will create a windows web server that we will be creating the firewall for. I will do so via powerShell.
<img width="732" height="190" alt="image" src="https://github.com/user-attachments/assets/c637930d-86f1-40fd-b5f5-b7aeb3427117" />


### Create Sample Website and produce SSL certificate

WIthin the Internet Information Services Manager I will create a new domain certificate for the website.

<img width="640" height="342" alt="image" src="https://github.com/user-attachments/assets/9da786b4-cd59-4436-851e-019d4386360a" />

<img width="795" height="370" alt="image" src="https://github.com/user-attachments/assets/35fb5712-4a76-4a85-a6af-2794d8f7094a" />

<img width="832" height="436" alt="image" src="https://github.com/user-attachments/assets/e506efbb-5183-40e2-be90-d1af4dacac33" />

### Inbound and Outbound Rules

Now we need to ensure proper inbound and outbound rules on the network.

Inbound rules are set by default on windows but I will still verify them brieftly.
<img width="773" height="515" alt="image" src="https://github.com/user-attachments/assets/60d92c2c-3c4b-4bef-b13a-e9dcd5c045b4" />

Next I will test the firewall rules that are set by default to ensure functionality.

I will once again do so through powerShell commands.

I swap to a diffrent computer on the network and use the following powershell command to test if port 80 is open for connections. **Test-NetConnection -ComputerName PLABDC01 -Port 80**

<img width="732" height="250" alt="image" src="https://github.com/user-attachments/assets/6ee18f3f-4569-4ed7-b97c-72c549ac33b0" />

Success. Now to test port 443 for HTTPS. **Test-NetConnection -ComputerName PLABDC01 -Port 443**

<img width="712" height="245" alt="image" src="https://github.com/user-attachments/assets/e24db695-5c47-47b9-8351-6904c04725b0" />

Now that we have tested a few rules the both succeded I will create new rules to customize the network traffic that is allowed.

Within the firewall I disable all access to HTTP as it is not secure. 

<img width="755" height="565" alt="image" src="https://github.com/user-attachments/assets/85293b88-1053-40ad-a68c-0ebce57d4e2c" />

After the configuration I once again test port 80 for HTTP to ensure the new rule is functioning as expected.

<img width="703" height="293" alt="image" src="https://github.com/user-attachments/assets/dfc83cc4-edac-401f-81cb-886732d7ed4f" />

Conenction failed! As expected out new firewall rule is working...

Now it is time for the outbound rules of the firewall.

Within the Windows Defender Firewall I create a new rule for 445. Blocking the traffic.

<img width="841" height="461" alt="image" src="https://github.com/user-attachments/assets/1e42ef1b-afd9-438f-a97e-d1ecfc19c547" />

<img width="801" height="412" alt="image" src="https://github.com/user-attachments/assets/7d3a6442-2d69-48d1-b5af-fab53cf9b644" />

Now to verify the new rule in powerShell. Never assume things are working as expected! Always verify. **Test-NetConnection -ComputerName PLABDC01 -CommonTCPPort SMB**

<img width="791" height="313" alt="image" src="https://github.com/user-attachments/assets/b0055aea-f705-4c1f-92db-aa81ac55663b" />

Connection failed as we wanted.

This rule was created simply to show how an outbound rule would be created and tested. I will disable the rule that is blocking the 445 traffic before we get into logging.

### Firewall Logging

Windows Firewall supports a logging feature that describes how the firewall processes different types of traffic. The collected logs provide important information such as date or time, source or destination IP addresses, port numbers, and protocols.

Firewall logging is useful for verifying that the newly added firewall rule works properly, or to troubleshoot them if the rules do not work as expected. The logs can assist in identifying unusual activity such as repeated failed attempts to access the firewall or an internal computer. Similarly, suspicious and repetitive outbound connections coming from internal servers, like web servers, could be an indication that an intruder is using your system to hack into other corporate networks. Note that the firewall logs are not fully detailed and do not provide conclusive information needed to track down the external source activity.

**In this step of the lab I will install and FTP server and configure an FTP site to have ensure it can be monitored via wireshark**

Install the FTP server using powerShell **Install-WindowsFeature Web-Ftp-Server -IncludeManagementTools**

Create the FTP server in IIS.

<img width="841" height="437" alt="image" src="https://github.com/user-attachments/assets/e722b8c0-d65b-464d-93d5-8c9bf0365f25" />

After putting a test .txt file with some text that we can test the FTP server with I restart the machine and begin testing.

I run the following command in powerShell to begin testing **Test-NetConnection -ComputerName PLABDC01 -Port 21**

<img width="712" height="252" alt="image" src="https://github.com/user-attachments/assets/c3aa1a4e-0947-422b-a911-d84157d30488" />

Connection success! Which confirms that a diffrent machine can connect to the FTP server we created.

Now we need to configure the firewall logging.

I open the Windows Firewall Propeties to get started.

I enable inbound connections and go deeper into the logging settings.

<img width="593" height="482" alt="image" src="https://github.com/user-attachments/assets/7ac2fa6a-077a-4f0d-95bb-d5e268da023a" />

I enable the logging of dropped packets and sucessful connections.

<img width="378" height="248" alt="image" src="https://github.com/user-attachments/assets/365fc6f5-fead-45a3-b0a8-42a9ad8ad5f5" />

**I repeat these steps for the Domain, Private, and Public profile of the firewall.**

On a seperate machine I connect to the FTP server and open files to simulate traffic that will be logged.

<img width="708" height="501" alt="image" src="https://github.com/user-attachments/assets/220cb559-1bfc-4d91-b7cc-3b4271744c76" />

On the machine hosting the FTP server I open wireshark and review the FTP traffic to ensure logging is happening correctly.

We can see the the traffic is porperly being collected.

<img width="918" height="458" alt="image" src="https://github.com/user-attachments/assets/f1facddc-2d4f-4ae9-bf6b-b344cec85bda" />

As a side note we can also see the password that I input shown in cleartext due to the FTP protocol 

<img width="792" height="32" alt="image" src="https://github.com/user-attachments/assets/a0143b9f-05c0-4323-a832-2e2a04476d03" />


### Interpreting Logs

I now go into the log files saved by windows and review and interpret their meaning.

<img width="947" height="562" alt="image" src="https://github.com/user-attachments/assets/52cc2c37-c9ec-4892-9cf1-133110960689" />





































