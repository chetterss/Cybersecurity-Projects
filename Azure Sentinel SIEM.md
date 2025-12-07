## Introduction
The purpose of this project was to design, deploy, and monitor a fully vulnerable honeypot environment in Microsoft Azure in order to observe real-world cyberattacks in action. By intentionally exposing a virtual machine to the public internet with minimal security controls, I was able to collect authentic attack data, analyze adversary behavior, and visualize global threat activity using Azure’s security tools. This hands-on lab demonstrates end-to-end configuration of a cloud-based honeypot, integration with Microsoft Sentinel, real-time log ingestion, and geographic mapping of malicious activity. The goal was not defense, but visibility—building a controlled environment to study attacker techniques and better understand how threat actors discover and target exposed cloud resources.

## Project Details

Firstly I created a VM in microsoft azure to be turned into a honey pot so that I could review attacks.

Once created I needed to entice attackers so that I could monitor activity. I disabled the default inbound security features of the resource group and replaced them with a fully vulnerable ruleset of allow all.
<img width="1640" height="152" alt="image" src="https://github.com/user-attachments/assets/bc38fff4-6d15-4555-8031-824d22e3feb6" />

After I had updated the rules of the resource group I now needed to disable any security features with the windows operating system on the VM itself. I simply went into the windows defender fire wall properties and turned everything off.
<img width="382" height="445" alt="image" src="https://github.com/user-attachments/assets/a541ae91-cec8-452c-8ba6-8712c14aa763" />

Now that I created an vulnerable enviroment I needed to ensure that it could be reached. A simple ping in powershell will confirm... and boom we are able to reach the VM.
<img width="440" height="171" alt="image" src="https://github.com/user-attachments/assets/bb402d2b-f326-4d20-95cc-4a7148989c5a" />

We have successfully created a vulnerable VM, now I will link Azure to the miscrosoft event viewer to keep track of any and all activity on the machine.

Next I created a log analytics workspace and connected it to a Microsoft Sentinel SIEM within Azure. Finally I install / configure the azure monitoring agent security event connector to connect our VM to the log analytics workspace.
<img width="1848" height="286" alt="image" src="https://github.com/user-attachments/assets/59e56d2f-f511-4207-9086-1f615b6a8202" />

Now I can view all of the logs from our virtual machine directly in our Log Analytics Workspace. A simple SecurityEvent query will confirm this.
<img width="1506" height="523" alt="image" src="https://github.com/user-attachments/assets/3994a5df-fc46-49ed-b7b8-b93124dd7f18" />

### We already are getting attacked???
I opened the VM to the internet about 10 minutes ago and their is already a wide range of login attemps and brute force tools attacking us. Non of the attempted login below are from me.
<img width="1520" height="824" alt="image" src="https://github.com/user-attachments/assets/10f414f7-19db-44c5-876c-7b94949f572c" />

A quick lookup of their IP address and we can see that we are currently being attacked from Tijuana, Mexico.

I will now map all of the IPs with geolocation to see where the attacks are coming from. Let create a new sentinel watchlist to do so. I will put the source of the watchlist to an excel file that has locational IP data and create. After it is created we can query the log analytics workspace with out new watchlist to see the attacker geolocations.

We can also create a map within sentinel to better visualize the analyitics of our SIEM. We will create a new workbook to do so. Within the last 5 minutes we can see the below activity for the americas.

<img width="740" height="398" alt="image" src="https://github.com/user-attachments/assets/910ced6e-90c5-45e5-b065-10c10f95db4a" />

If we really wanted to finalize out SOC here we could set up alerts and incedents within sentinel. However this lab was simply to assess the webtraffic, we dont really have a need for that functionality. 
