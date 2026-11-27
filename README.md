# cyber


1. Perform an experiment for port scanning nmap. 
Aim 
To perform port scanning using Nmap in Kali Linux and identify open ports and services 
running on a target system. 
Tools and Requirements 
1. Kali Linux operating system. 
2. Nmap tool. 
3. Terminal. 
4. Target system (localhost or authorized machine). 
5. Internet connection (if required for installation). 
Procedure 
Step 1: Open the Kali Linux terminal. 
Step 2: Check whether Nmap is installed. 
nmap --version 
Step 3: If Nmap is not installed, install it. 
sudo apt install nmap -y 
Step 4: Scan your own system (localhost). 
nmap 127.0.0.1 
Step 5: Scan common ports. 
nmap -F 127.0.0.1 
Step 6: Scan all 65535 TCP ports. 
nmap -p- 127.0.0.1 
Step 7: Identify services and their versions. 
nmap -sV 127.0.0.1 
Step 8: Perform a detailed scan. 
nmap -A 127.0.0.1 
Step 9: Save the scan results into a file. 
nmap -oN scan.txt 127.0.0.1 
Step 10: Display the saved results. 
cat scan.txt 
Expected Output 
Example output (actual results may differ): 
Starting Nmap 
Nmap scan report for localhost (127.0.0.1) 
PORT     STATE  SERVICE 
22/tcp   open   ssh 
80/tcp   open   http 
443/tcp  open   https 
Nmap done: 1 IP address scanned 
If no services are running, Nmap may show all scanned ports as closed. 
Result 
Thus, port scanning was successfully performed using Nmap in Kali Linux. Open ports and 
their running services were identified.



2. Set Up a Honeypot and Monitor the Honeypot on the Network Using Cowrie 
Experiment: Set Up a Honeypot and Monitor the Honeypot on the Network Using Cowrie 
1. Aim 
To set up a honeypot using Cowrie in Kali Linux and monitor incoming SSH connections, login 
attempts, and user activities. 
2. Tools and Requirements 
1. Kali Linux operating system. 
2. Python 3. 
3. Git. 
4. Cowrie honeypot. 
5. OpenSSH client. 
6. Minimum 4 GB RAM. 
7. Network connection. 
3. Procedure 
1. Open Kali Linux terminal and update the system. 
sudo apt update 
2. Install required packages. 
sudo apt install git python3 python3-venv python3-dev build-essential libssl-dev libffi-dev -y 
3. Create a Cowrie user. 
sudo adduser --disabled-password cowrie 
4. Switch to the Cowrie user. 
sudo su - cowrie 
5. Download Cowrie. 
git clone https://github.com/cowrie/cowrie 
cd cowrie 
6. Create and activate a virtual environment. 
python3 -m venv cowrie-env 
source cowrie-env/bin/activate 
7. Install and initialize Cowrie. 
python -m pip install -e . 
cowrie init 
8. Start the honeypot. 
cowrie start 
cowrie status 
9. Connect to the honeypot. 
ssh -p 2222 root@127.0.0.1 
Enter a test password and execute simple commands. 
whoami 
pwd 
ls 
exit 
10. Monitor the honeypot activities. 
tail -F ~/cowrie/var/log/cowrie/cowrie.json 
Expected Output 
Cowrie status: 
Cowrie is running 
SSH connection: 
root@127.0.0.1's password: 
root@svr04:~# 
Monitoring output: 
Login attempt detected 
Command executed: whoami 
Command executed: pwd 
Command executed: ls 
Log file: 
var/log/cowrie/cowrie.json 
Result 
Thus, the Cowrie honeypot was successfully set up in Kali Linux. SSH connections, login 
attempts, and user activities were monitored and recorded in the log file.




4.  Explore and simulate real-world vulnerabilities from the OWASP Top 10–2021 list by 
completing guided hands-on tasks. 
Aim 
To explore and simulate real-world web application vulnerabilities based on the OWASP Top 
10–2021 list using Kali Linux and OWASP Juice Shop. 
Tools and Requirements 
1. Kali Linux OS. 
2. Terminal. 
3. Firefox web browser. 
4. Docker. 
5. OWASP Juice Shop. 
6. Nmap. 
7. Internet connection. 
Procedure with Commands 
Step 1: Update Kali Linux 
sudo apt update 
Step 2: Install required tools 
sudo apt install docker.io nmap -y 
Step 3: Start Docker 
sudo systemctl start docker 
Step 4: Download OWASP Juice Shop 
sudo docker pull bkimminich/juice-shop 
Step 5: Run OWASP Juice Shop 
sudo docker run -d -p 3000:3000 --name juice-shop bkimminich/juice-shop 
Step 6: Open the application 
Open Firefox and enter: 
http://localhost:3000 
Step 7: Perform the following ten vulnerability experiments 
1. A01 – Broken Access Control 
• Open the application. 
• Explore user profile and account access. 
• Check whether a user can access another user's protected information. 
• Observe the access control challenge in the scoreboard. 
Expected output: Understand unauthorized access to protected resources. 
2. A02 – Cryptographic Failures 
Execute: 
curl -I http://localhost:3000 
• Observe the HTTP response. 
• Understand that HTTP does not encrypt transmitted data. 
Expected output: HTTP response headers are displayed. 
3. A03 – Injection 
• Open the Juice Shop login page. 
• Open the scoreboard. 
• Find the SQL Injection challenge. 
• Follow the guided challenge in the local application. 
Expected output: Understand how unsafe input can manipulate database queries. 
4. A04 – Insecure Design 
• Open the shopping page. 
• Add products to the cart. 
• Explore shopping and business-logic challenges. 
• Observe how missing security rules can affect application behaviour. 
Expected output: Understand weaknesses in application business logic.



Experiment 7: Real-Time Traffic Analysis and Packet Logging Using Snort Tool: Snort
Recommended OS: Kali Linux / Ubuntu
1. Aim
To monitor network traffic and perform packet logging using Snort, an open-source network intrusion detection and prevention system.
2. Requirements
- Kali Linux or Ubuntu
- Snort 2 or Snort 3
- Active network interface
- Appropriate Snort configuration
3. Procedure
Step 1: Install Snort if it is available in your distribution repository.
sudo apt update
sudo apt install snort -y
Step 2: Check the version.
snort -V
Step 3: Identify the network interface.
ip -br link
Step 4A: For Snort 2, display live packet information.
sudo snort -i eth0 -v
Step 5A: For Snort 2, display detailed packet information.
sudo snort -i eth0 -dev
Step 6A: For Snort 2, log packets to a directory.
sudo mkdir -p /tmp/snort-logs
sudo snort -i eth0 -dev -l /tmp/snort-logs
Step 4B: For Snort 3, use its configuration file for live processing.
sudo snort -c /etc/snort/snort.lua -i eth0
Step 5B: For Snort 3, write packet data using the dump logger.
sudo mkdir -p /tmp/snort-logs
sudo snort -c /etc/snort/snort.lua -i eth0 -L dump -l /tmp/snort-logs
Step 7: Generate local test traffic in another terminal.
ping -c 4 127.0.0.1
Step 8: Stop monitoring and inspect the log directory.
sudo ls -l /tmp/snort-logs
4. Expected Output
Snort displays packet information in the terminal and/or writes packet logs, depending on the version and options used. Exact messages and log files depend on the Snort version, configuration and selected interface.
5. Result
Thus, network traffic monitoring and packet logging were performed using Snort.





8.  Perform Network analysis using the Network Minertool 
Aim 
To perform network analysis using the NetworkMiner tool and identify IP addresses, hosts, 
transferred files, images and other information from captured network traffic. 
Tools and Requirements 
1. NetworkMiner tool. 
2. Windows / Kali Linux operating system. 
3. PCAP file (sample.pcap). 
4. Internet connection. 
5. Wireshark (optional). 
Simple Procedure 
Step 1: Download NetworkMiner 
• Open the browser. 
• Visit the official website: NetworkMiner Download. 
• Download and extract the ZIP file. 
• Open NetworkMiner.exe in Windows. 
Step 2: Prepare a PCAP File 
Download a sample PCAP file from: 
Malware Traffic Analysis. 
Or capture network traffic using Wireshark and save it as a .pcap file. 
Step 3: Open NetworkMiner 
• Start NetworkMiner. 
• Click File → Open. 
• Select the sample.pcap file. 
Step 4: Analyze Network Traffic 
Wait until the analysis is completed. 
Check the following tabs: 
Tab 
Hosts 
Files 
Images 
Information displayed 
IP addresses, MAC addresses and hostnames 
Transferred files 
Extracted images 
Messages Emails and messages 
Credentials Detected usernames and passwords 
DNS 
DNS queries and responses 
Parameters HTTP GET/POST parameters 
Sessions 
TCP/UDP sessions 
Step 5: Observe the Results 
• Open the Hosts tab and identify IP addresses. 
• Open the Files tab and check transferred files. 
• Open the Images tab and view extracted images. 
• Check the DNS tab for visited domains. 
• Check the Sessions tab for network communication details. 
Expected Output 
NetworkMiner displays the extracted network information. 
Sample Observation Table: 
Item 
IP Address 
Hostname 
Observed Data 
192.168.1.10 
victim-pc.local 
Files Extracted invoice.pdf 
Username 
admin 
Visited Domain login.example.com 
Protocol 
Result 
TCP / UDP 
Thus, network analysis was successfully performed using the NetworkMiner tool. Network 
hosts, IP addresses, transferred files, images, DNS information and network sessions were 
analyzed from the captured PCAP file.




9.  Using Snort, perform real-time traffic analysis and packet logging 
Aim 
To use Snort in Kali Linux to monitor real-time network traffic, analyze packets and save 
captured packets in PCAP format for later analysis. 
Tools and Requirements 
1. Kali Linux operating system (VirtualBox). 
2. Snort 3 tool. 
3. Active network interface (eth0). 
4. Internet connection. 
5. Two terminal windows. 
6. tcpdump tool. 
Simple Procedure with Commands 
Step 1: Install Snort 
Open Kali Linux terminal and execute: 
sudo apt update 
sudo apt install snort -y 
Step 2: Identify Network Interface 
ip -br addr 
Check the active interface. Example: eth0. 
Step 3: Check Internet Connection 
ping -c 5 8.8.8.8 
Step 4: Verify Snort Installation 
snort -V 
Expected version: Snort 3. 
Step 5: Install tcpdump 
sudo apt install tcpdump -y 
Step 6: Check Network Packets 
In Terminal 1: 
sudo tcpdump -i eth0 -n icmp 
In Terminal 2: 
ping -c 5 8.8.8.8 
Observe the captured ICMP packets. Press Ctrl + C to stop tcpdump. 
Step 7: Start Real-Time Traffic Analysis 
In Terminal 1: 
sudo snort -i eth0 -L dump -d -e 
In Terminal 2: 
ping -c 5 8.8.8.8 
Observe the packets displayed by Snort. 
Step 8: Create Packet Log Directory 
Stop Snort using Ctrl + C. 
Execute: 
sudo mkdir -p /var/log/snort 
Step 9: Start Packet Logging 
In Terminal 1: 
sudo snort -i eth0 -L pcap -l /var/log/snort 
In Terminal 2, generate network traffic: 
ping -c 10 8.8.8.8 
curl http://example.com 
Step 10: Stop Snort and Check Logs 
Press Ctrl + C in Terminal 1. 
Execute: 
sudo ls -lh /var/log/snort/ 
A PCAP file should be created. 
Step 11: Read the Saved PCAP File 
Use the actual filename displayed in the previous step: 
sudo snort -r /var/log/snort/YOUR_FILE.pcap -L dump -d -e 
Replace YOUR_FILE.pcap with the actual filename. 
Expected Output 
1. Network Interface Output 
eth0    UP    10.0.2.15/24 
2. Snort Version Output 
Snort++ 3.12.2.0 
3. Packet Capture Output 
IP 10.0.2.15 > 8.8.8.8: ICMP echo request 
IP 8.8.8.8 > 10.0.2.15: ICMP echo reply 
4. Packet Log Output 
total 20K 
snort.log.xxxxxxxxx 
Sample output only. Actual interface, IP addresses and log filename may differ. 
Result 
Thus, Snort was successfully used in Kali Linux to monitor real-time network traffic, analyze 
packets and save captured network traffic in PCAP format for future analysis.



