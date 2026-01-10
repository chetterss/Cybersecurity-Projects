# Default Credential Policy Enforcement

Default crendtials on user and guests accounts pose a major security threat to organizations. They are widely know by threat actors and predictable. Default credentials present one of the easiest targets imaginable for an attacker and should be changed as soon as possible.
Guest accounts for contractors & clients may use default passwords, or in some cases no password at all. For attackers these kinds of accounts become easily expoilted attack vectors.

Within this lab an orginizational with a written security policy that forbids the use of default credentials for any account. We will be discovering and updating accounts with default credentials to enforcing this policy.

## Discover The Guest Accounts

First we need to discover the account(s) with default credenials so we can update them and ensure we are adhereing to organizational controls.

I will attempt to login into the asocciated guest accounts and see if there is a default password. I enter 'Guest' for the usename and no password.

<img width="487" height="443" alt="image" src="https://github.com/user-attachments/assets/4fd22b54-513e-4440-bfad-a0e104245cf6" />

To my suprise it actually works... the guest account does not require a password.

## Disable the Guest Account

While we could simply change the password for the guest account, the organization within this lab does not have a need for it.
So we will simply be disable the account to address the security issue.

I log back into the administrator account and utilize active directory to disable the account. Here we see the guest user.

<img width="490" height="367" alt="image" src="https://github.com/user-attachments/assets/7ce38130-4740-45f6-b698-16a04a6a0019" />

I simply right click and disable the account.

To confirm the account is no longer accessible i will attempt to log back into the guest account.

Upon logging in with the username 'guest' and no password, we are no longer logged in. Confirming that our account deactivation was successful.

## Conclusion

While the technicality of this lab is very simple, it still teaches us a lot. Most importantly to not overlook the small things.
You can have every enterprise level security tool perfectly configured... but if you have a single guest account that an attacker exploit then it all comes crashing down.
Ensuring **ALL** security policies are upheld is crucial for minimizing operational risk, our security is only as good as our weakest link.




