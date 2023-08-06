<h1>🦈Wireshark Network Analysis Home Lab</h1>

<h2>Description:</h2>

- <b>Capturing Live Traffic And Configuring Capture Filters.</b> 
- <b>Analysing PCAP Files</b>
- <b>Viewing Capture Statistics (Protocol Hierarchy, Conversations And Endpoints).</b>
<br />

<h2>Languages and Utilities Used:</h2>

- <b>Wireshark v4.0.7</b> 
- <b>2 x TEST PCAP Network Traffic Files (https://elearning.securityblue.team)</b> 

<h2>Environments Used: </h2>

- <b>Windows 10</b> (22H2)

<h2>Program walk-through:</h2>

<p align="center">
<b>Security Blue Team Wireshark Activity</b>  <br/>
 Activity questions below <br/>
<img src="https://i.imgur.com/GUd79T5.png" height="80%" width="80%" /><br />

<p align="center">
<b>PCAP File 1 (Wireshark Activity)</b>  <br/> 
 Q1 wants us to find the protocol for port 3942  <br/>
 Filter by command "tcp.port == 3942 or udp.port == 3942" SSDP protocol was used.<br/>
<img src="https://i.imgur.com/YsaiV0b.png" height="80%" width="80%" /><br />

<p align="center">
 Q2 wants us to find an IP address that has been pinged twice  <br/>
 Filter by ICMP and we can see 8.8.4.4 has been pinged twice <br/>
<img src="https://i.imgur.com/fJT1T7H.png" height="80%" width="80%" /><br />

<p align="center">
 Q3 wants us to find how many DNS query response packets  <br/>
 Filter by DNS > Sort by info > Select query response packets (Shift Lclick) > File > Export<br/>
 There were 90 DNS query response packets <br/>
<img src="https://i.imgur.com/S1welhE.png" height="80%" width="80%" /><br />
<img src="https://i.imgur.com/rSwACXr.png" height="80%" width="80%" /><br />

<p align="center">
 Q4 wants us to find IP of a host that sent the most bytes  <br/>
 Return to main file > Statistics > Endpoints > Filter by TX Bytes (Transmission bytes) <br/>
 115.178.9.18 returned as most bytes transmitted <br/>
<img src="https://i.imgur.com/LYFETCw.png" height="80%" width="80%" /><br />

<p align="center">
<b>PCAP File 2 (Wireshark Activity)</b>  <br/> 
 Q1 wants us to find out the WebAdmin password  <br/>
 Filter by http via "http.request" command <br/>
 Rclick password packet > Follow HTTP stream > webadmin password: sbt123 <br/>
<img src="https://i.imgur.com/JZPyGyz.png" height="80%" width="80%" /><br />
<img src="https://i.imgur.com/u4hmLls.png" height="80%" width="80%" /><br />

<p align="center">
 Q2 wants us to find version number of the attacker's FTP server  <br/>
 From Q1, we know that the attacker IP is 192.168.56.1 <br/>  
 Search for the attacker's FTP server via IP and FTP query; "ip.addr == 192.168.56.1 and FTP" <br/>
 We can see that the version used is 1.5.5 <br/>
<img src="https://i.imgur.com/poTSGSe.png" height="80%" width="80%" /><br />

<p align="center">
 Q3 wants us to find which port was used to gain access to Windows Host  <br/>
 If a host has been transmitting many packets and bytes to an unidentified IP address without receiving many packets in return, <br/>
 an exfiltration could have been occurring. <br/>
<p align="center">    
 We will search the attacker's IP (192.168.56.1) > Statistics > Conversations > TCP > Sort by most packets sent B to A <br/>
 (A being attacker's address and B (192.168.56.103) is likely to be Window Server's IP) <br/>
<p align="center"> 
 The port used is 8801, we can confirm this by following the TCP stream which confirms our findings as it looks like files are being <br/>
 sent to the attacker. <br/>
<img src="https://i.imgur.com/sgVCc2L.png" height="80%" width="80%" /><br />
<img src="https://i.imgur.com/0IoTBLA.png" height="80%" width="80%" /><br />

<p align="center">
 Q4 wants the file name of a confidential file.  <br/>
 From the image in Q3, the file name is Employee_Information_CONFIDENTIAL.txt.  <br/>

<p align="center">
 Q5 wants the file name created at 04.51 am  <br/>
 The file name is LogFile.log  <br/>
<img src="https://i.imgur.com/J2RxvhA.png" height="80%" width="80%" /><br />


</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
