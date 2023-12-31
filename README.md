<p align="center">
<img src="https://i.imgur.com/wJ6cg4s.png">
</p>

<h1>Azure Virtual Machines Traffic Inspection</h1>
In this tutorial, I observe and explore several network traffic protocols between two Azure Virtual Machines with Wireshark. This exercise helps those who want to learn how to observe network traffic and use protocols such as: </p>                                                               

- DNS (Domain Name System; Port 53)
- SSH (secure shell; Port 22)
- DHCP (Dynamic Host Configuration Protocol; Port 67 & 68)
- ICMP (Internet Control Message Protocol; No Port #)
- RDP (Remote Desktop Protocol; Port 3389)
<br />

<b> You will need a VM with Windows and another VM with Ubuntu. This tutorial assumes you have already created those two virtual machines. Need to create Virtual Machines?
                                                                 
<a href="https://github.com/AsiaPonder001/Resource-Groups-and-V-Ms">CLICK HERE</a>

<img src="https://i.imgur.com/xocmOjp.png">
</p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure Virtual Machines

- Remote Desktop Connection

- Network Protocols (SSH, RDH, DNS, ICMP, DHCP)

- Wireshark is the network traffic analyzer used to observe the different types of traffic being sent between both VMs.

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Linux/Ubuntu Server 20.04 


<h2> Sign into the Windows VM </h2>

<b> Copy Public IP address and paste it into the Remote desktop connection </b>

<img src="https://i.imgur.com/K79BJvW.png">

<b>After logging in to the VM, navigate to Microsoft Edge and Download and install Wireshark </b>

<img src="https://i.imgur.com/It0Ez7A.png">
<p>
<img src="i.https://imgur.com/IBt3KUh.png">
<img src="https://i.imgur.com/7PlTD8N.png">
</p>

<h2>Protocols and Observations </h2>
<b>Filter for RDP (Remote Desktop Protocol) or tcp.port==3389 traffic in the top bar</b>

<img src="https://i.imgur.com/xaqENca.png">
</p>
<br />


<b> Filter for DHCP (Dynamic Host Control Protocol) traffic </b>
- (1) Type in DHCP in Wireshark
- (2) Open Command line as an administrator and type in the command: ipconfig/renew
- (3) Check back to observe Traffic in Wireshark


<img src="https://i.imgur.com/LLUxpwa.png">
</p>
<br />


<b> Filter for DNS (Domain Name System) traffic</b>

- (1) Type in dns in Wireshark
- (2) Open Command line as an administrator and type in the nslook up for a website (ex: nslookup www.google.com)
- (3) Check back to observe dns traffic in Wireshark

<p>
<img src="https://i.imgur.com/KsiNQuO.png">
</p>
<br />


<b>Filter for SSH (Secure Shell) traffic </b>

- (1)Type in ssh
- (2) Open Powershell as an administrator
- (3) type command: <b>ssh (username of vm)@private ip address</b>
- (4) That will prompt you to put in the password
- (5) check back to observe ssh traffic in Wireshark

<p>
<img src="https://i.imgur.com/P5OasU5.png">
</p>
<br />


<b> Filter for ICMP (internet Control Message Protocol) traffic </b>

- (1) Type in ICMP
- (2) Open CMD and perpetually ping LinuxVM with the command (ping -t(private ip address)
- (3) Observe the constant pinging

<p> but there is NO traffic in Wireshark. It's pinging REQUEST TIMED OUT in CMD. Which means your firewall has ICMP blocked </p>

<br />
<p>
<img src="https://i.imgur.com/RGR15Wg.png">
</p>
<br />

<b>Change the Inbound firewall rule to allow ICMP traffic</b>

<p>In the Azure Portal to go your LinuxVm > Click on Networking > Click on Add inbound security rule</p>

- Select ICMP
- Select Allow 
- choose 200 for priority
- Click Add


<p>
<img src="https://i.imgur.com/YAtHAqw.png">
</p>
<br />


<b> Observe ping request after allowing ICMP rule </b> 

<p> It responds with reply now and we're able to receive icmp traffic </p>

<img src="https://i.imgur.com/tIMx7qw.png">
</p>
<br />
