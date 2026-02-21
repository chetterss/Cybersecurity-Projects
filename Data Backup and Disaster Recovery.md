# Data Backup and Disaster Recovery

In this lab I will be walking through the data backup process, creating a system restore point, preforming a backup, and restoring a system with the backup data. This is an essential step for the integrity and availablity for data security.

## Creating a System Image Backup

This Windows service can be used to create a backup image, when paired with the repair your computer function it can be used to restore a system to a working state.

To start I open the control panel and go into backup and restore -> create a system image.

I specify where the image should be saved on the network and enter details.

<img width="774" height="620" alt="image" src="https://github.com/user-attachments/assets/5791907c-f4bb-4bcc-bac8-4b5a6b97c662" />

Once everything is configured I start the backup.

<img width="555" height="285" alt="image" src="https://github.com/user-attachments/assets/79ebab3f-9710-4b01-ad08-113e2b227ce1" />

## Configure System Restore Point

Now I will enable and create a system restore point, and also test rolling back to an earlier state using system restore.

I go into system protection properties and turn on system protection.

<img width="572" height="485" alt="image" src="https://github.com/user-attachments/assets/38563874-427f-4b49-a06e-ffa7eb0b3d7c" />

Next I create the restore point.

<img width="387" height="252" alt="image" src="https://github.com/user-attachments/assets/7b213d4b-6daa-416f-9b6d-10fdc544cd71" />

Now I will test the system restore that was created.

<img width="593" height="461" alt="image" src="https://github.com/user-attachments/assets/528fa081-2d96-48f3-ba41-7a5a1f78f2f3" />

<img width="611" height="497" alt="image" src="https://github.com/user-attachments/assets/7be4a37b-0c95-4ceb-a2ce-f25b0993ee2d" />

After a system restart we see a successful backup!

<img width="421" height="170" alt="image" src="https://github.com/user-attachments/assets/a6ac0ee7-e572-4b78-84d4-387aef737fc7" />

## Enabling Windows Advanced options

Here I will be enabling some advanced startup options to support in the data backup & troubleshooting process(add a few others).

I first go into the boot setting of msconfig.

I set the following configurations:

<img width="624" height="410" alt="image" src="https://github.com/user-attachments/assets/ccf9408b-d92f-40ff-a8ae-53e1203d0ffa" />

## Performing Backup and Restore in Windows

Now I will be performing a full backup in Windows for an admin users download. This would be a great baseline that you could then perform incremental backups on moving forward.

I open Paragon Backup to get started.

For the sake of time we will only be backing up the Admin users downloads.

<img width="868" height="657" alt="image" src="https://github.com/user-attachments/assets/1761aadb-e20a-4ae6-96cf-8472930111ef" />

I create a backup folder on the desktop to save too. Note that in a real rowld scenario you would never save a backup to the same device.

<img width="843" height="638" alt="image" src="https://github.com/user-attachments/assets/4e9ed841-f736-41d8-8dbd-51eca58f6afa" />

I begin the backup...

<img width="659" height="250" alt="image" src="https://github.com/user-attachments/assets/7cc4bb29-4803-49ac-821a-071778c781cb" />

Success! Our data is now backedup.

Now we will test restoring from the backup.

In Paragon I open the backup and select restore.

<img width="639" height="486" alt="image" src="https://github.com/user-attachments/assets/da8326be-b22c-4672-b799-af5ba36722b6" />

<img width="545" height="298" alt="image" src="https://github.com/user-attachments/assets/c725c7d0-2e27-4095-8265-da9d024645bc" />

And boom! Our files have been fully restored.

## Conclusion

In this lab, I successfully created a system image backup, configured and tested a system restore point, enabled advanced startup options, and performed a full backup and restore of user data. This process demonstrated how backups and restore points help protect system integrity and ensure data availability. Overall, this lab reinforced the importance of having reliable backup and recovery procedures in place to prevent data loss and quickly restore systems when issues occur.








