<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Actions and Observations</h2>
Welcome to my tutorial on Network Security Groups and Inspecting Network Protocols. First you will need to create two Virtual Machines on Azure. One machine will be a Linux machine(Ubuntu) and the other will be a Windows 10 VM. Both will have two cpus and they must be on the same Virtual Network (VNET). Once that is done go on the Windows 10 VM and download Wireshark (protocol analizer- view traffic coming from and to our VMs). I will attach a link to the wireshark download. https://www.wireshark.org/download.html Once installed open Wireshark and filter for ICMP Traffic only. Internet Control Message Protocol (ICMP) is a network layer protocol that relays messages concerning network connection issues. Ping uses this protocol, ping tests connectivity between hosts. When we filter wirehsark to only capture ICMP packets and ping the private IP address of our linux Virtual machine, we can visually see the packets on wireshark.
<p>
<br /> 
<img src="https://i.imgur.com/CYQOkN1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We can inspect each individual packet and see the actual data that is being sent in each ping, the picture below demonstrates just that..
</p>
<br />

<p>
<img src="https://i.imgur.com/57Lm48l.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the next portion of the lab we will perpetually ping the Linux machine with the command 'ping private IP address -t'. This will continually ping the machine until we decide to stop it. While the Windows machine is pinging the Linux machine, we will go to the Linux machine and block inbound ICMP traffic on it's firewall (Network security group). Once we do that we will stop recieving echo replys from the Linux machine.
</p>
<br />

<p>
<img src="https://i.imgur.com/qSXqPBz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>  
<img src="https://i.imgur.com/54DVuNl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/EG36pcD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next we will use our Windows machine to SSH(Secure Shell; TCP Port 22) to the Linux machine. SSH mainly used when connecting to a computer running a Linux OS or network deveice like Cisco router. SSH has no GUI(Graphic User Interface) it just gives the user access to the machines command line. We will now set the wireshark filter to capture SSH packets only. When we ssh into the Linux machine with the command prompt "ssh Cyberdom1@10.0.0.5" we can see that wireshark starts to immediately capture SSH packets.
</p>
<br />


<p>
<img src="https://i.imgur.com/owqov2m.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we will use wireshark to filter for DHCP. DHCP is the Dynamic Host Configuration Protocol this works on ports 67/68. It is used to assign IP addresses to machines. We will first, release the current IP Address with the command "ipconfig /release" then request a new IP Address with the command "ipconfig /renew". Once we enter the command on windows wireshark will capture DHCP traffic.
</p>

<br />


<p>
<img src="https://i.imgur.com/Lnm8QPb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Now here we'll filter DNS (Domain Name Server port 53) traffic, (mainly used to give a website name an IP Addess that can be read on the web). We'll first set wireshark to filter DNS traffic. We will initiate DNS traffic by typing in the command "nslookup google.com" this command essentially asks our DNS server what is google's IP address.
</p>
<br />


<p>
<img src="https://i.imgur.com/SUr88eQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Lastly we will filter for RDP traffic. When we enter tcp.port==3389 traffic is spammed non stop because we are using Remote Desktop Protocol to connect to our Virtual Machine.
</p>
<br />


<p>
<img src="https://i.imgur.com/X0x1X9i.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
