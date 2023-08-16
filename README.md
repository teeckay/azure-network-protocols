<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines: Windows and Linux).
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)
- Microsoft Azure Network Security Groups ( Firewall ).

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1: In Azure, Create A Windows and Linux virtual machine. In turn the platform will create a           Network security group and resource group as the virtual machines are created. 
- Step 2: Connect to the Windows Virtual Machine and install Wireshark Protocol Analyzer an use it           to monitor and filter traffic between the two virtual machines.


<h2>Actions and Observations</h2>

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/7ad33f16-187d-4d77-bbea-39f0c0bec3b1)


</p>
<p>

Begin by creating a resource group and add your virtual machines ( Windows and Ubuntu ) Virtual Machines. The Azure platform will  create new virtual networks and subnets for the Virtual Machines created.

</p>
<br />


<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/e1d6a939-bf04-41e4-b940-4669a9af2731)


</p>
<p>

Connect to the Windows Virtual machine using windows remote desktop connection, the password used to create the virtual machine and the public IP address assigned to the virtual machine.

</p>
<br />

<p>

Next, install wireshark in the windows virtual machine to inspect traffic as you interact with the Ubuntu Virtual machine. Filter the traffic on wireshark to only show icmp traffic thenl ping the Ubuntu virtual machine using its private IP address on Windows powershell. This will show the icmp traffic between the two virtual machines.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/3dceeed2-7169-4c75-85e0-394cde4cf9e6)


</p>
<p>

Above, Wireshark is set to filter icmp traffic and before sending the ping to the Ubuntu Virtual Machine no icmp traffic is seen.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/70d6d26e-6e4a-4e32-ad83-3902b96fcbb0)


</p>
<p>

Now icmp traffic can be seen captured by Wireshark after sending the ping.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/9239d9cb-6c79-435d-8fe8-82979e771d41)


</p>
<p>

Next, send a perpetual ping to the Ubuntu virtual machine and change the firewall settings for the Ubuntu virtual machine to stop or block ICMP traffic. 

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/8ef6fc86-75c9-4988-abf5-f99724f9e48c)


</p>
<p>

Then set the Firewall (NSG - Network Security Group ) Rules to Deny ICMP traffic from anywhere. In this case, deny ICMP traffic from the Windows Virtual Machine. 

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/b34617da-af01-4e56-9472-7b1ad25d9269)


</p>
<p>

Next, the firewall rule is applied and the ping is being blocked by the Ubuntu virtual machine’s firewall. This leads to the request timing out and there are no replies or responses noted on Wireshark

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/7a1c7b38-4ab4-41d6-a3ac-1ccdbe685057)


</p>
<p>

Next, allow ICMP traffic to flow again to the Ubuntu Virtual machine by allowing it on the firewall rule meant to deny ICMP traffic  before to illustrate traffic flowing again.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/45fa5714-7852-4a12-9559-d799042d2586)


</p>
<p>

ICMP traffic is then allowed by the Ubuntu Virtual machine’s firewall and replies are sent back to the Windows virtual machine.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/935ecaf3-80bb-489c-8fb5-f762aca188c0)


</p>
<p>

Next, filter for SSH traffic on the Wireshark protocol analyzer and  ssh login to the Ubuntu virtual machine from the windows virtual machine Powershell. 
SSH Traffic is not seen before entering SSH information to log into the Ubuntu Virtual Machine at IP address 10.0.0.5

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/8673ad7b-0d68-4068-b4d7-ea41e962cdaf)


</p>
<p>

SSH traffic is seen on WireShark after login into the Ubuntu Virtual Machine via SSH. This shows the connection between the two virtual machines using SSH traffic.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/2d614bf4-e64c-4796-a93d-88dadbccc06a)


</p>
<p>

SSH login to the Ubuntu virtual machine is successful, SSH traffic on the traffic analyzer increases with each interaction between the two Virtual Machines.

</p>
<br />

<p>
  
image here

</p>
<p>

Next, filter for DHCP traffic on the Wireshark analyzer and flow DHCP traffic by ordering your DHCP client to renegotiate an IP address lease with the DHCP server on your router using the  ipconfig/ renew tool.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/e3dd12d2-fd41-4dbd-9cd0-7368c8e85221)


</p>
<p>

No DHCP traffic is seen before renegotiating my IP Address Lease.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/e9b049d6-8f19-4952-ab44-fdee66132c1a)


</p>
<p>

After renegotiating my IP Address lease, DHCP traffic is seen on the WireShark protocol analyzer.


</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/01df2525-e73b-4cf5-9408-07b7fa5a4f99)


</p>
<p>

Next, use nslookup for example using  www.google.com to filter DNS traffic on WireShark.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/azure-network-protocols/assets/64244011/42ac4c7a-b16b-4282-8f57-86a921a33dc0)


</p>
<p>

I then filter out RDP traffic using port number 3389 (tcp.port==3389) and traffic is expected since the two virtual machines connected for this exercise are exchanging RDP traffic; from the host Virtual machine to the Windows virtual machine. 

</p>
<br />

<p>

This exercise shows different types of network traffic between two computers and how you can monitor different types of traffic. You also see how a firewall works and how you can use it to block or allow traffic. You can also see that not only can you use specific filters for traffic, you can also filter by port numbers on the Wireshark Protocol Analyzer. 

</p>
<br />

