<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<!--<h2>Video Demonstration</h2>

 ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups]/ !-->

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Virtual Machines within Azure
- Wireshark Installation and Utilization
- Network Security Group Usage and Network Traffic Flow
- Observe Various Types of Network Traffic

<h2>Actions and Observations</h2>

<h3>Step 1: Create your Resource Group (RG) within Microsoft Azure.</h3>

-  Create a Resource Group.
    -  Go to the [Azure Portal](https://portal.azure.com) --> Click RG --> Name Your Group --> Click Review + Create.
        - Once validated --> Click Create.
    <p>
    <img src="https://i.imgur.com/geivdgl.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/AR1557V.png" title="source: imgur.com" /></a>
    </p>

<h3>Step 2: Create your first Virtual Machine (VM).</h3>

-  Head Back to [Azure Portal](https://portal.azure.com) --> Click VM --> Select previous RG --> Name VM --> Windows 10 Pro, 22H2
    -  Select CPU Size --> Enter Credentials --> Hit next **twice** --> Note Vnet created --> Select Next
       
    <p>
    <img src="https://i.imgur.com/PKxwtlc.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/rWI8G6i.png" title="source: imgur.com" /></a>
    </p>

-  Allow Azure to create Virtual Netowork (Vnet) --> Select Review + Create
    -  Once Validation has passed --> Select Create.

    <p>
    <img src="https://i.imgur.com/f1mLtu6.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/PJGgnZw.png" title="source: imgur.com" /></a>
    </p>
  <br />

<h3>Step 3: Creat your second VM.</h3>

-  Head Back to [Azure Portal](https://portal.azure.com) --> Click VM --> Select previous RG --> Name VM --> Unbuntu Server 20.24 LTS
    -  Authentication Type --> Password --> Enter Credentials --> Hit next **twice**
         
    <p>
    <img src="https://i.imgur.com/zbNopXC.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/7xfyeIp.png" title="source: imgur.com" /></a>
    </p>
<br />

-  Be sure that the Vnet is the same as VM1 --> Select Review + Create
    - Once Validation has passed --> Click Create

    <p>
    <img src="https://i.imgur.com/IPSsNgM.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/B84BK91.png" title="source: imgur.com" /></a>    
    </p>
<br />

<h3>Step 4: Connect to VM1.</h3>

-  Use Remote Desktop to connect to your Windows 10 VM.
    -  Connect to VM1 using Remote Desktop.  Copy VM1's public IP address --> Paste into Remote Desktop Connection --> Click Connect.

    <p>
    <img src="https://i.imgur.com/gZMlG7Y.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/N6lUqmw.png" title="source: imgur.com" /></a>
    </p>

<h3>Step 5: Install Wireshark.</h3>

-  To install visit [Wireshark]() --> Click Download.
    - Be sure to download Windows x64 Installer --> Complete Installation

    <p>
    <img src="https://i.imgur.com/C6pngvu.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/E1Tkfwc.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/WmbIWyc.png" title="source: imgur.com" /></a>
    </p>

-  Once opened, wireshark should look like this:

    <p>
    <img src="https://i.imgur.com/cvAtI0n.png" title="source: imgur.com" /></a>
    </p>

-  Select Ethernet to start the program:

    <p>
    <img src="https://i.imgur.com/eVPa7Or.png" title="source: imgur.com" /></a>
    </p>
  
<h3>Step 6: Observe ICMP Traffic.</h3>

-  Go back to [Azure Portal](https://portal.azure.com) --> VM2 --> Copy VM2's private IP address.

    <p>
    <img src="https://i.imgur.com/FFjt6GG.png" title="source: imgur.com" /></a>  
    </p>

-  In Wireshark's toolbar type in ICMP and hit the blue arrow:

    <p>
    <img src="https://i.imgur.com/2BJ5IUM.png" title="source: imgur.com" /></a>
    </p>

-  Open Poweshell from the searchbar --> ping 10.0.0.5.
    -  Observe the traffic in Wireshark.

    <p>
    <img src="https://i.imgur.com/wUyH8zL.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/i1pci1S.png" title="source: imgur.com" /></a>
    </p>

-  Observe more traffic --> Ping Instagram.

    <p>
    <img src="https://i.imgur.com/uzN7XfZ.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/LQc6PTs.png" title="source: imgur.com" /></a>
    </p>
<br />

<h3>Step 7: Initiate perpetual ping from VM1 to VM2.</h3>

-  Poweshell --> enter ping 10.0.0.5 -t
    -  Observe Traffic in Wireshark

    <p>
    <img src="https://i.imgur.com/kry9OWR.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/ImRq1gk.png" title="source: imgur.com" /></a>
    <p>
<br />

<h3>Step 8: Utilize Network Security Groups (NSG) to influence the flow of internet traffic.</h3>

-  Head back to [Azure Portal](https://portal.azure.com) --> Search NSG --> Select VM1
   
    <p>
    <img src="https://i.imgur.com/FpJjSqd.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/oSnn2vc.png" title="source: imgur.com" /></a>
    </p>

-  Select Inbound Security Rules --> Add

    <p>
    <img src="https://i.imgur.com/mIFYWJt.png" title="source: imgur.com" /></a>
    </p>

-  Protocol --> ICMPv4 --> Deny Action --> Priotity 200. --> Save.
    -  Name: DENY_PING_FROM_ANYWHERE
        - Return to NSG to ensure ICMP ping is denied.

    <p>
    <img src="https://i.imgur.com/F058cCY.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/aCcp9L8.png" title="source: imgur.com" /></a>
    </p>

>[!TIP]
>Rules are executed in order of priority. In this instance, number your rule prior to anything smaller than 300.
<br />

-  Return to VM1 to observe blocked ICMP traffic in Powershell and Wireshark.

    <p>
    <img src="https://i.imgur.com/x6fD5qg.png" title="source: imgur.com" /></a>
    </p>

-  Resume ICMP traffic.
    -  In the [Azure Portal](https://portal.azure.com) --> Go back to NSG --> Click VM1 --> Click on your rule --> Allow --> Save.
        -  Observe resumed traffic in both Powershell and Wireshark.
    <p>
    <img src="https://i.imgur.com/4JqiwrX.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/nz6Mjky.png" title="source: imgur.com" /></a>
    </p>
<br />

<h3>Step 9: Observe SSH Traffic</h3>

-  Go to VM1 -->  Wireshark --> Toolbar --> Enter ssh --> Click blue arrow --> Continue without saving.
    -  Powershell --> Enter Command: ssh labuser@10.0.0.5 -t --> Yes --> Enter.
        -  Observe traffic in Powershell

    <p>
    <img src="https://i.imgur.com/h1sKR0V.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/HyFEVki.png" title="source: imgur.com" /></a>
    </p>
    
>[!NOTE]
>Since ssh is essentially Remote Desktop without a Graphic User Interface (GUI), WIreshark will show every keystoke you put into Poweshell.

-  Here is what the command "uname -a" appears in Wireshark:

    <p>
    <img src="https://i.imgur.com/laUIuOL.png" title="source: imgur.com" /></a>
    </p>

-  Disconnect the SSH Connection.
    -  Powershell --> @ the prompt, type exit. --> ipconfig (to verify) --> Notice IP address
        - Observe how traffic does not move in Wireshark.

    <p>
    <img src="https://i.imgur.com/EXdJT1S.png" title="source: imgur.com" /></a>
    </p>

-  You can also observe ssh traffic by entering in the port type and number in Wireshark.
    -  Toolbar --> tcp.port == 22 --> blue arrow --> Continue without Saving.

    <p>
    <img src="https://i.imgur.com/bqeSKIN.png" title="source: imgur.com" /></a>
    </p>
<br />

<h3>Step 10: Observe DHCP traffic.</h3>

-  Wireshark Toolbar --> DHCP --> Blue Arrow --> Continue.
    -  Powershell --> ipconfig --> Observe traffic

    <p>
    <img src="https://i.imgur.com/y3e9cYD.png" title="source: imgur.com" /></a>
    </p>
<br />

<h3>Step 11: Observe DNS Traffic.</h3>

-  Wireshark Toolbar --> DNS --> Blue Arrow --> Continue.
    -  Powershell --> nslookup www.google.com --> Observe Traffic
 
    <p>
    <img src="https://i.imgur.com/dQIekG4.png" title="source: imgur.com" /></a>
    </p>

-  Observe traffic using the type of port and port number.
      -  Wireshark Toolbar --> udp.port == 53 -- blue arrow --> Continue
    <p>
    <img src="https://i.imgur.com/T0LI0AN.png" title="source: imgur.com" /></a>
    </p>
<br />

<h3>Step 12: Observe RDP Traffic.</h3>

-  Wireshark Toolbar --> RDP --> Blue Arrow --> Continue without Saving.
    - Observe using port type and number: Toolbar --> tcp.port == 3389
 
    <p>
    <img src="https://i.imgur.com/xOP5j1P.png" title="source: imgur.com" /></a>
    <img src="https://i.imgur.com/MPaIo4f.png" title="source: imgur.com" /></a>
    </p>
<br />

<h3>Congrats! You have completed this tutorial on NSGs and Inspection of Network Traffic!</h3>


<br />

<br />
