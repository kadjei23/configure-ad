<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell ISE

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>

- Step 1 : Created a domain Controller with the windows server and named it DC-1 by creating a VM with it's own resource group and subnet.
<img src="https://i.imgur.com/7gcghpV.png" alt="DC-1"/>


- Step 2 : Set the domain controller's virtual NIC Private IP address to static so it doesn't change.

<img src="https://i.imgur.com/LvDGadF.png" alt="Network Settings"/>

<img src="https://i.imgur.com/ZmJmKfY.png" alt="IP Config"/>

<img src="https://i.imgur.com/fHHQ3Fk.png" alt="Static"/>


- Step 3 : Created another VM and named it client-1. Used the same Virtual network and resource group as DC-1

<img src="https://i.imgur.com/FR9Nrrl.png" alt="Client-1"/>

- Step 4 : Logged into client-1 with RDP to ping to DC-1's private IP address

<img src="https://i.imgur.com/fHNPBRI.png" alt="Ping"/>

- Step 5: Logged in to DC-1 and enabled ICMPv4

<img src="https://i.imgur.com/kOnccq6.png" alt="wf.msc"/>

<img src="https://i.imgur.com/Onthm4F.png" alt="ICMPv4"/>

- Step 6: Logged back into client 1 to see if ping was successful

<img src="https://i.imgur.com/Oc2qt2m.png" alt="Ping"/>

- Step 7: Logged into DC-1 to install Active Directory

<img src="https://i.imgur.com/LDSRBxB.png" alt="Install AD"/>

<img src="https://i.imgur.com/dMxRKRB.png" alt="Add roles"/>

<img src="https://i.imgur.com/g5OMpm3.png" alt="Hit Next"/>

<img src="https://i.imgur.com/NUNuMhD.png" alt="BYB"/>

<img src="https://i.imgur.com/WHvPqRp.png" alt="Role based"/>

<img src="https://i.imgur.com/H2hAcap.png" alt="Server selection"/>

<img src="https://i.imgur.com/L47tIaI.png" alt="Install selection"/>

- Step 8: Promoted server as a domain controller and set up a new forest as boatingdomain.com with a password.

<img src="https://i.imgur.com/QvXc7Lj.png" alt="Promote"/>

<img src="https://i.imgur.com/OakTu5f.png" alt="Domain"/>

<img src="https://i.imgur.com/z9maGMV.png" alt="Password"/>


- Step 9: RDP disconnected logged back in using a new username "boatingdomain.com\KBuser1"

<img src="https://i.imgur.com/9e3AMrK.png" alt="Signed out"/>

- Step 10: Created two organizational units named _EMPLOYEES and _ADMINS through active directory users and computers.

<img src="https://i.imgur.com/HL5TgUz.png" alt="ADUC"/>

<img src="https://i.imgur.com/xJaotSp.png" alt="OU"/>

<img src="https://i.imgur.com/Oyh6qyd.png" alt="_EMPLOYEES"/>

- Step 11: Created a user named John wick with the username john_admin and added john_admin to the doman admins security group

<img src="https://i.imgur.com/cPR1hGW.png" alt="John_Wick"/>

<img src="https://i.imgur.com/bSqth5e.png" alt="Properties"/>

<img src="https://i.imgur.com/L5YUxhi.png" alt="domain"/>

<img src="https://i.imgur.com/UdrLg8t.png" alt="added"/>

- Step 12: Logged out of DC-1 and used john wick as an admin with the log in john_wick@boatingdomain.com

<img src="https://i.imgur.com/96c6oHO.png" alt="JW"/>

- Step 13: Joined client-1 to boatingdomain.com from azure by changing client-1's DNS settings to DC-1'S private IP address.

<img src="https://i.imgur.com/q95RpeP.png" alt="C-1"/>

<img src="https://i.imgur.com/VVvyhNb.png" alt="NIC"/>

<img src="https://i.imgur.com/11qiQpN.png" alt="DNS"/>

- Step 14: Restarted Client 1 after changing to private IP Address.

<img src="https://i.imgur.com/0IRtzeJ.png" alt="Restart"/>


- Step 15: Logged back into client-1 and ipconfig all/ to make sure client-1 has the same DNS server as DC-1

<img src="https://i.imgur.com/4ZFh71M.png" alt="IP-Config"/>


- Step 16: Joined client-1 to boatingdomain.com

<img src="https://i.imgur.com/D2PNk1Q.png" alt="System"/>

<img src="https://i.imgur.com/7Js6iym.png" alt="rename-advanced"/>

<img src="https://i.imgur.com/CDbiwjG.png" alt="change-domain"/>

<img src="https://i.imgur.com/QsmUNI8.png" alt="boating"/>

<img src="https://i.imgur.com/RgoQrXt.png" alt="username"/>  Entered domain username "john_wick@boatingdomain.com"

<img src="https://i.imgur.com/evxAaVk.png" alt="welcome"/>

<img src="https://i.imgur.com/UouBmhr.png" alt="Restart pt-2"/>  Restarted client-1

- Step 17: Logged in to client 1 using domain username "john_wick@boatingdomain.com"

<img src="https://i.imgur.com/hW7uvHe.png" alt="log-in"/>

- Step 18: Opened system properties --> Remote desktop --> allow domain users to access remote desktop

<img src="https://i.imgur.com/Sw8tr47.png" alt="RDP"/>

<img src="https://i.imgur.com/0YotoMy.png" alt="add"/>

<img src="https://i.imgur.com/Ur63jK2.png" alt="check-names"/>

<img src="https://i.imgur.com/nas9M2J.png" alt="Domain"/>

- Step 19: Logged into DC-1 as "john_wick@boatingdomain.com" and ran poweshell ISE as administrator.

<img src="https://i.imgur.com/nas9M2J.png" alt="Powershell ISE"/>

- Step 20: Created new file and pasted script for generated usersnames

<img src="https://i.imgur.com/LmuFqh0.png" alt="File-New"/>

<img src="https://i.imgur.com/i6aRrXZ.png" alt="Script"/>

- Step 21: Ran Script

<img src="https://i.imgur.com/9tZOL7N.png" alt="RUN"/>

- Step 22: Watched as powershell generated 10,000 new users with Different usernames but same password.

<img src="https://i.imgur.com/Faje0EY.png" alt="User"/>

- Step 23: Went back to Active directory users and computers to refresh and observe all users that were created.

<img src="https://i.imgur.com/GN3983H.png" alt="Refresh-user"/>

- Step 24: Picked a random user and logged out of client one then logged in with the picked user

<img src="https://i.imgur.com/k33F3UK.png" alt="Random-user"/>

<img src="https://i.imgur.com/up40YbP.png" alt="welcome-dohu"/>


</p>
<br />
