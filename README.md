<h1>UNDER CONSTRUCTION</h1>

<h1>Nessus</h1>

<h2>Description</h2>
111111
<br />

<h2>Utilities Used</h2>
- <b>Nessus Essentials</b> 

<h2>Environments Used </h2>

- <b>Oracle VirtualBox</b> 
- <b>Windows 10 (Has Nessus Installed)</b> 
- <b>Windows 10 (Without Nessus)</b>




<h2>Host IP Addresses</h2>

- <b>Nessus Target: 192.168.1.17</b> 
- <b>Nessus Host: 192.168.1.18</b> 


<h2>Nessus Lab Demonstration</h2>

Nessus Host cannot reach Nessus Target.

![09_19_22_12_11_22](https://user-images.githubusercontent.com/112909705/191384959-6a95c215-d274-4b53-b6aa-1416388515f0.png)

Changed the Domain, Private, and Public firewall profiles for connectivity. Nessus Host can reach Nessus Target.

![09_19_22_12_13_53](https://user-images.githubusercontent.com/112909705/191394026-4423a4d3-132c-4e25-82b1-6e3109515988.png)

Nessus configured on Nessus Host.

![09_19_22_12_19_05](https://user-images.githubusercontent.com/112909705/191394086-cf8ccf5b-4ffe-4d83-9ff6-420c6a333410.png)

Custom scan for Nessus Target (192.168.1.17). Scanning for common ports and is non-credentialed. 

![09_19_22_12_28_05](https://user-images.githubusercontent.com/112909705/191394122-0629401e-0a67-4d2f-88cf-5893ae090724.png)

Inspected completed non-credentialed scan. 

![09_19_22_12_35_03 1](https://user-images.githubusercontent.com/112909705/191394163-fa34b7b9-c5ee-4ffe-908e-622acb6b2e9d.png)

Most severe vulnerability is "medium". Potential for man-in-the-middle attacks on the SMB server. This can be easily fixed with message signing. 5 resources are listed showing how to remediate.

![09_19_22_12_35_45 1](https://user-images.githubusercontent.com/112909705/191394181-3e4ddefb-820d-4e4e-9f15-a0551092858f.png)

Some addition steps needs to be performed to run credentialed scans with non-default Windows Administrator accounts. In other words, accounts that are not on the domain. The tenable link below shows how to configure this.

https://community.tenable.com/s/article/Scanning-with-non-default-Windows-Administrator-Account

Going to Services and enabling the Remote Registry to startup automatically will allow the scanner to connect and search the registry during credentialed scans. 

![09_19_22_12_55_33](https://user-images.githubusercontent.com/112909705/191394208-56ad2c11-f281-4a4d-92db-e9d9c2a8b1f1.png)

Changing User Account Control Settings will also help credentialed scans to run from outside of the domain. 

![09_19_22_13_01_28](https://user-images.githubusercontent.com/112909705/191394259-3f54e7e5-0474-4fc8-a3c9-148b42e489b2.png)

Tenable recommends creating a new DWORD registry entry named "LocalAccountTokenFilterPolicy", and modifying the value data box to 1. This is the final step to allow for full credentialed scans.  

![09_19_22_02_45_46](https://user-images.githubusercontent.com/112909705/191394311-fe839852-1818-4b9a-b681-584ab29b46d4.png)

The new credentialed scan will use netstat. Also, this scan will be much more thorough going through all ports between 1 and 65535. Hosts will be pinged with TCP, ARP, and ICMP. 

Instead of 16 vulnerabilities, there are now 34. There is one Critical which has a CVSS v3.0 Base Score of 10.0. It is because it has software that is no longer supported. 

![09_19_22_14_07_37](https://user-images.githubusercontent.com/112909705/191394360-201aebfc-e3c8-44cf-b770-c2108035e2c8.png)

Installing an unsupported version of FireFox on the target to test if Nessus can find it with another credentialed scan.  

![09_19_22_14_22_07](https://user-images.githubusercontent.com/112909705/191394391-dd3a0e88-0ed4-4c84-8377-80620aa9fd48.png)

![09_19_22_14_22_23](https://user-images.githubusercontent.com/112909705/191394400-3f816453-bb9b-4bc6-95ef-455094162d93.png)

170 vulnerabilities just from the outdated FireFox, ranging from medium to critical.  

![09_19_22_14_39_58](https://user-images.githubusercontent.com/112909705/191394429-5734cb18-d9b0-4e3a-891f-e833f41ef4fb.png)

![09_19_22_14_40_31](https://user-images.githubusercontent.com/112909705/191394467-cb02f907-869d-4326-9586-b145e2139d16.png)

![09_19_22_14_41_03](https://user-images.githubusercontent.com/112909705/191394561-17ba6b3b-0102-4b49-9916-ea56426ef6da.png)

Quick comparison of the different types of scans: 

Non-credentialed and common ports had 0 criticals.

![09_19_22_14_41_56](https://user-images.githubusercontent.com/112909705/191394596-428f75ac-f132-4aaa-839c-e4d6e17f03e4.png)

Credentialed with all ports had 1 critical. 

![09_19_22_14_43_03](https://user-images.githubusercontent.com/112909705/191394620-9f31a444-aa3c-4d14-8fda-30aca8493c6c.png)

Credentialed with all ports, with the older FireFox had 26 criticals and 29 highs.

![09_19_22_14_43_14](https://user-images.githubusercontent.com/112909705/191394664-d10c421d-ddef-4e8b-992c-8237506b0303.png)

This lab demonstrates why it is important to regularly perform credentialed and non-credentialed scans to remediate risks and keep vulnerabilities in your network as low as possible. One outdated program can create hundreds of possible attack vectors for an attacker. 




