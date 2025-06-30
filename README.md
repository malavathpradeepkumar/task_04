##  Task 4 Firewall Configuration Report

You can view the full report with step-by-step screenshots and explanations in this PDF:

[View Task 4 Firewall Report](https://drive.google.com/file/d/1Jtg4F3DWHf8U5wYVe_X25khn4g5c-Ehp/view?usp=sharing)


In this task, I worked on setting up and testing a firewall on both Kali Linux and Windows operating systems. I started by enabling the firewall on Kali using UFW, 
which stands for Uncomplicated Firewall. It is a simple front-end for managing iptables firewall rules in Linux.

First, I opened the terminal in Kali Linux and updated the package list using the command sudo apt update. This command updates the list of available packages and 
versions from the repositories. Then, I installed UFW by using the command sudo apt install ufw -y. This command installs the UFW firewall tool and the -y option 
automatically says yes to the confirmation prompt. After installation, I enabled the firewall with the command sudo ufw enable. This activates the firewall on the 
system. To confirm the firewall was running, I used the command sudo ufw status verbose. This command shows whether the firewall is active and lists all current 
rules with additional detail like logging status and default behavior.

Next, I switched to my Windows virtual machine to make sure the Windows Defender Firewall was turned on. I clicked on the Start menu and searched for "Control Panel". 
Inside Control Panel, I went to "System and Security" and then selected "Windows Defender Firewall". From the left-hand menu, I clicked on "Turn Windows Defender 
Firewall on or off". On the next screen, I made sure that the firewall was turned on for both Private and Public networks.

After ensuring the firewalls were active on both systems, I moved to Step 2, which was listing the current firewall rules. In Kali Linux, I used the same command 
again: sudo ufw status verbose. This showed me the default policy (which was usually to deny incoming and allow outgoing) and any rules that were already added. 
On Windows, I opened "Windows Defender Firewall with Advanced Security" by clicking "Advanced Settings" on the left side of the Firewall window. This opened a new 
window where I could see "Inbound Rules" and "Outbound Rules". These lists showed all the existing firewall rules for incoming and outgoing traffic on different 
ports and applications.

In Step 3, I created a new rule to block inbound traffic on port 23, which is used by the Telnet protocol. Telnet is considered insecure because it transmits data
in plain text, so it is commonly blocked in security setups. In Kali Linux, I added the rule using the command sudo ufw deny 23. This tells the firewall to deny all 
incoming traffic on TCP port 23. In Windows, I created the rule through the firewall GUI. Inside "Windows Defender Firewall with Advanced Security", I clicked on "Inbound
Rules", then clicked "New Rule" from the right-side panel. In the New Rule Wizard, I selected "Port", then clicked Next. I chose "TCP" and typed "23" in the Specific Local Ports box, then clicked Next. On the next screen, I selected "Block the connection" and clicked Next. Then I applied the rule to all three profiles — Domain, Private, and Public — and clicked Next. I gave the rule a name, such as "Block Telnet Port 23", and then clicked Finish.

In Step 4, I tested if the firewall rule was working. Since I had blocked port 23 on Kali, I tried to connect to it from my Windows VM. First, I checked if the telnet 
command was available by opening Command Prompt and typing telnet, but it was not recognized because Telnet was not installed by default. So I used PowerShell instead 
and ran the command Test-NetConnection -ComputerName <Kali-IP> -Port 23, where <Kali-IP> is the IP address of my Kali machine. This command checks if the specified port 
is open or blocked. The output showed "TcpTestSucceeded : False", which confirmed that the connection to port 23 was successfully blocked by the firewall in Kali.

Finally, in Step 5, I removed the firewall rule to clean up after the test. In Kali Linux, I first listed the rules with numbering using the command sudo ufw status 
numbered. This displayed the rules in a numbered list, for example, showing [ 1] 23 DENY IN Anywhere. Then I removed the rule by typing sudo ufw delete 1, assuming 
the Telnet rule was the first rule. In Windows, I went back to "Windows Defender Firewall with Advanced Security", clicked on "Inbound Rules", found the rule I created 
called "Block Telnet Port 23", right-clicked on it, and chose "Delete".

During the process, I took screenshots of every important step including enabling the firewall, listing the rules, adding the rule to block port 23, testing the 
connection using PowerShell, and finally deleting the rule. This helped me verify that each step was completed correctly and served as documentation. I also ran the
command ipconfig on Windows and took a screenshot of my private IP address to show my system's network configuration. The IP was in the private range, so it was safe
to include.

This task helped me understand how firewalls work on both Linux and Windows systems. I learned how to allow or block specific ports, test those changes, and remove 
them properly after use. I used basic Linux firewall commands and also explored Windows Defender Firewall’s advanced settings, making this a good hands-on practice 
for managing system security.


