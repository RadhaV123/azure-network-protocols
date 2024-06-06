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

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 1. In Azure, Setup a Resource Groups
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 2. Create 2 Virtual Machines

- Create a Windows 10 Virtual Machine (VM-1)
- While creating the VM, select the previously created Resource Group
- While creating the VM, create a new Virtual Network (Vnet)
- Create a Linux (Ubuntu) Virtual Machine (VM-2)
- While create the VM, select the previously created Resource Group and Vnet
- Observe Your Virtual Network within Network Watcher
  
Note: Wait for VM-1 to finish Deploying before creating VM-2. If not, the Vnet you created on VM-1 wont show up when creating VM-2.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 3. Open Microsoft Remote Desktop (If on Mac)

- Click Add PC
- For PC name, use VM-1's Public IP Address
- Open VM-1 on the Microsoft Remote Desktop after adding the PC
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Part 4. Install Software Within Windows 10 VM-1

- Install WireShark
- Open Wireshark filter for ICMP traffic only by hitting the blue shark icon and typing in "ICMP"
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
- Retrieve the private IP address of the Ubuntu VM-2 and attempt to ping it from within the Windows 10 VM-1
- Observe ping request and replies within wireshark
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Part 5. Initiate a perpetual/non-stop ping from your Windows 10 VM-1 to your Ubuntu VM-2

- On PowerShell, type in the private IP again along with a nonspot pin "-t"
- Observe the ICMP traffic in WireShark and the command line Ping activity
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
- Open the Network Security Group your Ubuntu VM-2 is using and disable incoming (inbound) ICMP traffic
- Network Security group -> VM-2-nsg -? Inbound security rules -> Add
- Back in the Windows 10 VM-1, observe the ICMP traffic in WireShark and the command line Ping activity after adding a new rule
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
- "Request timed out" - Re-enable ICMP traffic for the Network Security Group your Ubuntu VM-2 is using - Back in the Windows 10 VM-1, observe the ICMP traffic in WireShark and the command line Ping activity (should start working) 
- Stop the ping activity with shift+control+C
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Part 6. Back in Wireshark, filter for SSH traffic only

- From your Windows 10 VM-1, “SSH" into your Ubuntu Virtual Machine (via its private IP address)
- Exit the SSH connection by typing ‘exit’ and pressing [Enter]
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
![img11](https://github.com/RadhaV123/azure-network-protocols/assets/171521525/e06a00cb-3d5f-4e9f-8be7-b6e89b6cf611)</p>
<p>
Part 7. Filter for DHCP traffic only

- From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
- Observe the DHCP traffic appearing in WireShark
</p>
<p>
<![image](https://github.com/RadhaV123/azure-network-protocols/assets/171521525/d6c45bec-521f-443a-9cb8-4883849ffd26)/>
</p>
</p>

<p>
Part 8. Filter for DNS traffic only

- From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
- Observe the DNS traffic being show in WireShark
</p>

<br />
