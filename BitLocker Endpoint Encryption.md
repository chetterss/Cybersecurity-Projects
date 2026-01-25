## Data Drive Encryption with BitLocker

This lab focuses on implementing BitLocker Drive Encryption to protect data at rest on a Windows system. It demonstrates secure disk partitioning, configuring Group Policy to enable BitLocker without TPM support, encrypting a fixed data drive, and managing encryption states using command-line tools. The lab emphasizes defending against offline attacks, improper data access, and physical device compromise while reinforcing practical Windows endpoint security and encryption management skills.

### Create a secondary volume

I will first create a secondary disk volume that we will use as a data drive to store user files which are to be encyrpted.

I go into Disk Management and create a new simple volume to get started.

<img width="721" height="595" alt="image" src="https://github.com/user-attachments/assets/314277b0-1b73-4dd6-b037-4de717090047" />

I set the new volume up with ample storage and NTFS.

The new F drive is what we wil be encrypting.

<img width="727" height="262" alt="image" src="https://github.com/user-attachments/assets/dbd79f9a-2b15-4d1d-bb8d-499fb883f758" />


### Enable The Group Policy Setting for BitLocker

Normally, Bitlocker will expect a TPM chip to store the encryption keys. For the purposes of this lab there is no TPM chip, so I will be bypassing this feature through a group policy object.

To do this I make my way to the BitLocker operating system drives in the Local Group Policy Editor. Specifically the portion that requires additional authentication at startup.

I go into this feature and edit it to allow BitLocker without the compatible TPM.

<img width="691" height="638" alt="image" src="https://github.com/user-attachments/assets/65d59b2d-6528-42af-959b-c8353509ed89" />


### Encrypt the Fixed Drive Using Bitlocker

Now we simply need to enhance the security on the drive by enabling and configuring BitLocker.

Firstly, I turn on BitLocker for the new F Drive that we just created. And set a password to get around the TMP requirment.

<img width="738" height="607" alt="image" src="https://github.com/user-attachments/assets/2a700c3c-d13f-495c-998f-d091e86cef76" />

I store the recovery keys to a seperate computer and set the encryption mode.

Finally I hit start encrypting to secure out new drive.

<img width="372" height="189" alt="image" src="https://github.com/user-attachments/assets/3fb51324-c536-4d95-8d19-b73e48845eb5" />

After a quick system restart we can see that the F Drive is now encrypted using BitLocker. Any access to the encrypted drive now requires a password.

<img width="544" height="158" alt="image" src="https://github.com/user-attachments/assets/84dce7af-5bea-4445-85ca-1ac4330fc1e1" />

### Manage A BitLocker - Enabled Drive

Here I will be using the manage-bde tool to view the properties of the new BitLocker protected drive.

A simple 'manage-bde -status' command gives us an overview. Notice the conversation status of the F Drive.

<img width="478" height="287" alt="image" src="https://github.com/user-attachments/assets/80ce8a24-87c1-41d0-9492-09fb56d9d7b5" />

We can use the command 'manage-dbe -lock F:' to lock the drive. Finish our security of the drive.

<img width="540" height="128" alt="image" src="https://github.com/user-attachments/assets/2869d022-47f1-4207-a481-93041a2126f7" />

### Conclusion

This lab provided a simple yet practical introduction to BitLocker Drive Encryption. By creating a secondary data volume, configuring Group Policy to bypass TPM requirements, and encrypting the drive, it demonstrated fundamental techniques for protecting data at rest. Although straightforward, this exercise reinforces important endpoint security skills that are directly applicable to real-world cybersecurity scenarios.



