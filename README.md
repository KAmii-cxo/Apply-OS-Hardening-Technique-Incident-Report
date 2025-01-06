# OS Hardening Techniques: Incident Report

## Section 1: Identify the network protocol involved in the incident

The protocol involved in this incident is the Hypertext Transfer Protocol (HTTP). Since the issue occurred while attempting to access the web server for yummyrecipesforme.com, we can confirm that HTTP traffic is used for web page requests. Additionally, when we ran tcpdump while accessing the website, the resulting log file indicated HTTP protocol usage during communication with the server. Furthermore, the malicious file was observed being delivered to users' computers via the HTTP protocol at the application layer.

## Section 2: Document the incident

Several customers reported to the website's helpdesk that after visiting the website, they were prompted to download and execute a file claiming to provide access to new recipes. Following this, their personal computers began operating slowly. Meanwhile, the website owner attempted to log in to the web server but discovered they were locked out of their account.

To investigate, a cybersecurity analyst accessed the website in a sandbox environment to isolate the potential threat from the company network. Using tcpdump to capture network traffic, the analyst replicated the issue. During the session, the analyst was prompted to download a file offering free recipes, which they executed. The browser then redirected to a fake website, greatrecipesforme.com.

Upon examining the tcpdump logs, the analyst observed that the browser initially contacted the IP address for yummyrecipesforme.com. After the file download, the logs indicated a shift in network traffic, as the browser redirected to a new IP address associated with greatrecipesforme.com.

Further analysis by a senior cybersecurity professional revealed that the website's source code had been compromised to include malicious code prompting users to download the disguised malware. It was determined that the attacker likely gained access to the admin account through a brute force attack, changing the password to lock out the legitimate owner. The downloaded file's execution led to the compromise of users' computers.

## Section 3: Recommend one or more remediations for brute force attacks

To enhance protection against brute force attacks, the team plans to implement several security measures. 

First, they will prevent the reuse of previous passwords, including default ones, during password resets. This step addresses the vulnerability exploited in the attack, where the attacker used a default password to gain access.

Second, the team will require more frequent password updates. Regular updates reduce the likelihood of unauthorized access since compromised passwords will be rendered obsolete sooner.

Lastly, the team will introduce two-factor authentication (2FA). This adds an extra layer of security by requiring users to authenticate using both their password and a one-time passcode (OTP) sent to their email or phone. Users must verify their identity with both credentials before gaining access. With 2FA in place, malicious actors attempting brute force attacks are less likely to succeed, as they would also need the OTP to bypass this added security.
