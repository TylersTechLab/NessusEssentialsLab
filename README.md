<h1>UNDER CONSTRUCTION</h1>

grab screenies and write a proper description

<h1>Nessus</h1>

2 VMs: Windows 10 Enterprise Evaluation 
"Nessus Host" (Has Nessus Installed)
"Nessus Target" 


Nessus Target IP: 192.168.1.17


Nessus Host cannot reach Nessus Target.

![09_19_22_12_11_22](https://user-images.githubusercontent.com/112909705/191384959-6a95c215-d274-4b53-b6aa-1416388515f0.png)


Changed the Domain, Private, and Public firewall profiles for connectivity. Nessus Host can reach Nessus Target.

Nessus configured on Nessus Host.

Custom scan for Nessus Target (192.168.1.17). Scanning for common ports and is non-credentialed. 

Inspected completed non-credentialed scan. 

Most severe vulnerability is "medium". Potential for man-in-the-middle attacks on the SMB server. This can be easily fixed with message signing. 5 resources are listed showing how to remediate.

Some addition steps needs to be performed to run credentialed scans with non-default Windows Administrator accounts. In other words, accounts that are not on the domain. The tenable link below shows how to configure this.

https://community.tenable.com/s/article/Scanning-with-non-default-Windows-Administrator-Account

Going to Services and enabling the Remote Registry to startup automatically will allow the scanner to connect and search the registry during credentialed scans. 

Changing User Account Control Settings will also help credentialed scans to run from outside of the domain. 

Tenable recommends creating a new DWORD registry entry named "LocalAccountTokenFilterPolicy", and modifying the value data box to 1. This is the final step to allow for full credentialed scans.  


The new credentialed scan will use netstat. Also, this scan will be much more thorough going through all ports between 1 and 65535. Hosts will be pinged with TCP, ARP, and ICMP. 

Instead of 16 vulnerabilities, there are now 34. There is one Critical which has a CVSS v3.0 Base Score of 10.0. It is because it has software that is no longer supported. 


Installing an unsupported version of FireFox on the target to test if Nessus can find it with another credentialed scan.  

170 vulnerabilities just from the outdated FireFox, ranging from medium to critical.  


Quick comparison of the different types of scans: 

Non-credentialed and common ports had 0 criticals.

Credentialed with all ports had 1 critical. 

Credentialed with all ports, with the older FireFox had 26 criticals and 29 highs.

This lab demonstrates why it is important to regularly perform credentialed and non-credentialed scans to remediate risks and keep vulnerabilities in your network as low as possible. One outdated program can create hundreds of possible attack vectors for an attacker. 


<h2>Description</h2>
111111
<br />


<h2>Utilities Used</h2>

- <b>Nessus Essentials</b> 

<h2>Environments Used </h2>

- <b>Windows 10</b> 
- <b>Oracle VirtualBox</b> 

<h2>11111</h2>


