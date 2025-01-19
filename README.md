Nessus-lab
 ## Nessus Lab Configuration   
 The Nessus lab utilizes a Kali Linux 2021 virtual machine (VM) for educational purposes. It focuses on assessing vulnerabilities through:  
     - Internal Network Scanning - Linux-Specific Scanning

This lab uses the Kali 2021 virtual machine (VM) as OVA file KALI-20.ova on Canvas. The credentials are as follows:
    Username: osboxes Password: osboxes.org

INSTALLING, CONFIGURING AND USING NESSUS

In this recipe, we install, configure, and start Nessus. Nessus depends on vulnerability checks in the form of feeds to locate vulnerabilities on our chosen target. Nessus comes into two flavors of feeds: Home and Professional.
• Home Feed: The Home Feed is for noncommercial/personal usage. Using Nessus in a
professional environment for any reason requires the use of the Professional Feed.
• Professional Feed: The Professional Feed is for commercial usage. It includes support and additional features 
such as unlimited concurrent connections and so on. If you are a consultant and are performing tests for a client,
the Professional Feed is the one for you. For our recipe, we will assume you are utilizing the Home Feed.

Notes:
1. Do this Lab in Kali-20.ova VM (username : osboxes ; password : osboxes.org) and metasploitable 2 (username : msfadmin ; password : msfadmin). Download Metasploitable using Microsoft edge or Firefox for download from “https://information.rapid7.com/download-metasploitable-2017.html”
Note: You can follow the instructions in https://www.youtube.com/watch?v=qSPT-YlIZAc
2. The network settings of Kali VM should be Attached to: Bridge Adapter. Example is shown in below screen shot. And change metasploitable2 and ubuntu-desktop network setting to Bridge Adapter.
3. Compiling plugins during initialization phase of Nessus might take lot of time depending on the size of RAM.
4. Allocate 8GB to Kali-20 if you have enough RAM space available.

![Screen Shot 2025-01-18 at 3 49 26 PM](https://github.com/user-attachments/assets/25223791-46a1-4fce-b3e3-72683589930c)

Let’s begin the installation, configuring, and starting of Nessus by opening a terminal window:
Note: If you are unable to download the Nessus please change Network settings to “NAT” and after installing all turn it Back to “Bridger Adapter” to perform the lab.
1. Open the firefox esr web browser and navigate to the following
   
URL: http://www.tenable.com/products/nessus/select-your-operating-system.

![Screen Shot 2025-01-18 at 3 52 42 PM](https://github.com/user-attachments/assets/e35fd93f-aafc-49e2-adcf-959a7d508806)

2. Select Nessus-10.4.1-ubuntu1404_amd64.deb or Latest Version of it.
3. Download the file to your local root directory.
4. Open a terminal window.
5. Execute the following command to install Nessus:
//Type the below command
- [SELECT DATE] 2
sudo dpkg -i "Nessus-10.4.1-ubuntu1404_amd64.deb" //Nessus will be installed under the /opt/nessus directory

![Screen Shot 2025-01-18 at 3 53 57 PM](https://github.com/user-attachments/assets/1302add0-f23f-4342-aa04-6c1d152d542a)

Once the installation completes, you can run Nessus by typing the following command: sudo /bin/systemctl start nessusd.service //this starts the Nessus and runs in the background

![Screen Shot 2025-01-18 at 3 55 27 PM](https://github.com/user-attachments/assets/094979d6-4e60-481a-9dbe-41d812801d5b)

NOTE: To register your copy of Nessus, you must have a valid license (product key), which can be obtained from http://www.tenable.com/products/nessus/nessus-essentials. After you register the activation key will be sent to your mail address specified.

![Screen Shot 2025-01-18 at 3 56 19 PM](https://github.com/user-attachments/assets/e65df7ec-6681-412a-aee5-dfd258b4f92e)

7. Enable your Nessus install by executing the following command. You need to register and obtain activation Code prior to this instruction. Registration details are in above instructions.
sudo /opt/nessus/sbin/nessuscli fetch --register XXXX-XXXX-XXXX-XXXX- XXXX
In this step, we will also grab the latest plugins from http://plugins.nessus.org.

![Screen Shot 2025-01-18 at 3 58 18 PM](https://github.com/user-attachments/assets/37cf7682-4338-4322-9c74-6c059bbaaf9a)

8. Now enter the following command in the terminal
sudo /opt/nessus/sbin/nessuscli adduser //adds the user to access nessus
9. At the login prompt, enter the login name of the user.
10. Enter the password of your choice twice.
11. Answer as Y (Yes) to make this user an administrator.

![Screen Shot 2025-01-18 at 3 59 30 PM](https://github.com/user-attachments/assets/76930173-9726-4891-994c-7ebe4b69787c)

12. Once complete, you can run Nessus by typing the following command (it won't work without a user account)
sudo /bin/systemctl start nessusd.service

![Screen Shot 2025-01-18 at 4 01 26 PM](https://github.com/user-attachments/assets/ebbbe580-8761-4b93-b6d4-81dbbf55a24c)

14. Now got to URL “https://127.0.0.1:8834/html5.html#/” which will bring you to below page. Add Exception and confirm the security Exception.

![Screen Shot 2025-01-18 at 4 02 15 PM](https://github.com/user-attachments/assets/0bd53684-8cc1-4d7b-a258-3ae9cf3ab783)

14. Use the login credentials which you gave in the previous step

![Screen Shot 2025-01-18 at 4 03 44 PM](https://github.com/user-attachments/assets/a4f919a8-d819-4cd7-b16f-a5a9e5171a40)

Q1. Provide Screen Shot of your above Logged in Nessus Page.

![Screen Shot 2025-01-18 at 4 06 00 PM](https://github.com/user-attachments/assets/09391126-df4d-4f3a-96ac-e3815a2d08ad)


Nessus – finding Local Vulnerabilities:
Now that we have Nessus installed and configured, we will be able to begin testing of our first set of vulnerabilities. Nessus allows us to attack a wide range of vulnerabilities depending on our feed, and we will confine our list of assessing the vulnerabilities of our target to those specific to the type of information we seek to gain from the assessment. In this recipe, we will begin by finding local vulnerabilities. These are vulnerabilities specific to the operating system we are using.
Disable Firewalls if you get empty reports after the scan.
Let's begin the process of finding vulnerabilities with Nessus by opening the web browser: 
1. Log in to Nessus at https://127.0.0.1:8834.
2. Click on “New Scans” on the Top Right corner.
   
![Screen Shot 2025-01-18 at 4 07 47 PM](https://github.com/user-attachments/assets/f2cd53c2-46df-47d1-8cdb-a8927ee91b5d)

3. Click on New Scan. You Will see the below window, select Advanced Scan.

![Screen Shot 2025-01-18 at 4 08 23 PM](https://github.com/user-attachments/assets/2c83695b-ebea-4295-b620-6f7c02c69b74)

4. Click on Advanced Scan, perform the following tasks:
  1. Under General Type,
  2. Enter a name for your scan. We chose Local Vulnerability Assessment.
  3. Let the Folder field be My Scans.
  4. Choose your targets considering the following points:
  • Targets must be entered one per line.
  • You can also enter ranges of targets on each line.
You may also upload a target's file (if you have one) or select Add Target IP Address.
To enter the host IP address, go to virtual box and start metasploitable 2 (network settings as bridged adapter)giving username and password as msfadmin.
Then type ifconfig to obtain the ipaddress

![Screen Shot 2025-01-18 at 4 11 16 PM](https://github.com/user-attachments/assets/9a1e35b5-0429-474e-a760-d59e98651e98)

![Screen Shot 2025-01-18 at 4 11 58 PM](https://github.com/user-attachments/assets/a3e17a7b-4bc0-48c3-af7c-5f9d10424e00)

5. On the Plugins tab, select Disable All and Enable the following specific vulnerabilities:
  ▪ Ubuntu Local Security Checks
  ▪ Default Unix Accounts
  ▪ DNS
  ▪ FTP
  ▪ SMTPProblems ▪ SNMP
  ▪ Settings
  ▪ Web Servers
  ▪ Denial of Service
  
![Screen Shot 2025-01-18 at 4 13 53 PM](https://github.com/user-attachments/assets/33e7e0a8-742f-4278-a3cb-91fcafbef29b)

6. Click on save to save your new scan.
7. Click on Launch.

10. You will get a confirmation and your test will complete (depending on how many targets are selected and the number of tests performed).
11. Once completed, you can export a report.

![Screen Shot 2025-01-18 at 4 15 39 PM](https://github.com/user-attachments/assets/39f8ecc8-4949-419b-9cbd-c79e11d8e167)

12. Double-click on the report to analyze the following points (on the Results tab):
   ▪ Each target in which vulnerability is found will be listed
   ▪ Double-click on the IP address to see the ports and issues on each port
   ▪ Click on the number under the column to get the list of specific issues/vulnerabilities found
   ▪ The vulnerabilities will be listed in detail
   
![Screen Shot 2025-01-18 at 4 17 32 PM](https://github.com/user-attachments/assets/0fbf0a3e-3541-4f34-87d1-f2d791410b8b)

13. Click on export Report - Complete List of Vulnerabilities by host.

Q2. Attach the Downloaded report while submitting and write down summary of
scanned analysis in brief.

Data Collection: Q2_Scan_L.V.A
![Screen Shot 2025-01-18 at 8 29 55 PM](https://github.com/user-attachments/assets/3da2e798-2e4a-4df2-a815-32f68c2f908b)
![Screen Shot 2025-01-18 at 8 32 33 PM](https://github.com/user-attachments/assets/1ffa9335-09ba-43d7-9ba9-4c594c6b3eb9)
![Screen Shot 2025-01-18 at 8 34 49 PM](https://github.com/user-attachments/assets/eec30816-d6b2-4bd5-936b-51719225a399)
![Screen Shot 2025-01-18 at 8 35 32 PM](https://github.com/user-attachments/assets/ea03399c-92b9-4e05-a043-4f6cb37574c0)
![Screen Shot 2025-01-18 at 8 36 11 PM](https://github.com/user-attachments/assets/39e04558-cf00-4ac2-a5d4-82787b201e3f)

Data analysis:
In the Complete List of Vulnerabilities Assessment by host I analyzed that the lab had a total of 32
vulnerabilities. I noticed that the category vulnerabilities were from critical, high, medium, and low, or info. I had a total of 3 severities critical. The 3 critical had average 9.64 for CVSS V3.0 and average of 5

for the VPR Score. There was a total of 1 severity high, a total of 6 severities medium, and 0 severity low, 22 severities info. The results show that the system had a lot of updates that need to be done.

Nessus – Finding network vulnerabilities:

Nessus allows us to attack a wide range of vulnerabilities depending on our feed, and we will confine our list of assessing the vulnerabilities of our target to those specific to the type of information we seek to gain from the assessment. In this recipe, we will configure Nessus to find network vulnerabilities on our targets. These are vulnerabilities specific to the machines or protocols on our network.
To complete this recipe, you will need a virtual machine(s) to test against: Start all VM’s with network settings as bridged adapter.
   • Metasploitable 2.0 (VM creds: msfadmin/msfadmin)
   • UbuntuDesktop VM (VM creds: sec-lab/untccdc) → Use the cscelab.ova file.

1. Log in to Nessus at https://127.0.0.1:8834.
2. Go to Scans.
3. Click on “New Scan” then Select “Advanced Scan”.
2. Under General Type,
3. Enter a name for your scan. We chose, Internal Network Scan.
4. Let the Folder field be My Scans.
5. Choose your targets considering the following points:
   • Targets must be entered one per line
   • You can also enter ranges of targets on each line
6. You may also upload a target's file (if you have one) or select Add Target IP Address.
7. To enter the host ip address go to virtual box and start metasploitable 2 giving username and password as msfadmin and Start Ubuntu desktop VM with user id as sec-lab 
   and password as untccdc. You can use your own windows IP address for use.
8. Then type ifconfig to obtain the ipaddress in Ubuntu and metasploitable.

![Screen Shot 2025-01-18 at 4 31 10 PM](https://github.com/user-attachments/assets/36c8e5a3-661f-4026-8a0f-d6fcdc631d7f)

![Screen Shot 2025-01-18 at 4 50 09 PM](https://github.com/user-attachments/assets/0ff6b938-d1e1-4f01-af4e-3a93bda5dbdc)


9 On the Plugins tab, click on Disable All and select the following specific vulnerabilities: • CISCO
• DNS
• Default Unix Accounts
• FTP
• Firewalls
• Gain a shell remotely
• General
• Netware
• Peer-To-Peer File Sharing • Policy Compliance
• SCADA
• SMTP Problems
• SNMP
- [SELECT DATE] 13
• Service Detection • Settings
10. Click on save to save your new scan
11. On the main menu, click on the Scan. Then Click on Launch button to start scanning.
12. Once completed, you will receive a report inside of the Results tab. 13. Double-click on the report to analyze the following points:
• Each target in which a vulnerability is found will be listed
• Double-click on the IP address to see the ports and issues on each port
• Click on the number under the column to get the list of specific issues vulnerabilities found
• The vulnerabilities will be listed in detail

![Screen Shot 2025-01-18 at 4 39 53 PM](https://github.com/user-attachments/assets/633f404e-b20b-4d87-80eb-0fa99ed1cd55)


14. Click on export Report – Complete List of Vulnerabilities by host
15. 
Q3. Attach the Downloaded report while submitting and write down summary of scanned analysis in brief.

Data Collection: Q3_Scan_Internal_NetworkNew
![Screen Shot 2025-01-18 at 8 46 38 PM](https://github.com/user-attachments/assets/b66e93e9-f345-436d-b774-a9873835382b)
![Screen Shot 2025-01-18 at 8 53 04 PM](https://github.com/user-attachments/assets/0237e325-2110-471f-952a-fb6bdd67c5c5)
![Screen Shot 2025-01-18 at 8 53 47 PM](https://github.com/user-attachments/assets/37ff224b-59f4-42cb-8861-dd440a4a46bb)
![Screen Shot 2025-01-18 at 8 54 18 PM](https://github.com/user-attachments/assets/b99f4084-a195-4fa5-aef0-0c18953f0a23)
![Screen Shot 2025-01-18 at 8 54 56 PM](https://github.com/user-attachments/assets/ad31008d-da5a-4cd4-92d3-a7ab177ed24a)
![Screen Shot 2025-01-18 at 8 55 29 PM](https://github.com/user-attachments/assets/70e44026-3a98-4b26-81b1-efcb8b0e5776)
![Screen Shot 2025-01-18 at 8 55 51 PM](https://github.com/user-attachments/assets/330c948c-fe61-4c04-a77a-6cad0a09649d)
![Screen Shot 2025-01-18 at 8 56 23 PM](https://github.com/user-attachments/assets/a6bc3b9a-2c48-425a-b31c-1cba0806e7be)


Data analysis:
In the Complete List of Vulnerabilities Assessment by host on the Metasploitable machine. I
analyzed that the lab had a total of 77 vulnerabilities. I noticed that the category vulnerabilities were from critical, high, medium, and low, or info. I had a total of 6 severities critical. The 6 critical had average 9.82 for CVSS V3.0 and average of 3.5 for the VPR Score. There was a total of 5 severities high, a total of 13 severities medium, and 1 severity low, 52 severities info. The results show that the Kali machine system had zero vulnerabilities and only 2 severities info.

Nessus – Finding Linux-specific vulnerabilities:
 To complete this recipe, you will need a virtual machine(s) to test against:
    • Ubuntu Desktop
    • Metasploitable
1. Log in to Nessus at https://127.0.0.1:8834.
2. Go to Scans.
3. Click on “New Scan” then Select “Advanced Scan”.
4. Under General Type,
5. Enter a name for your scan. We chose, Linux-specific Scan.
6. Let the Folder field be My Scans.
7. Choose your targets considering the following points:
    • Targets must be entered one per line
    • You can also enter ranges of targets on each line
8. You may also upload a target's file (if you have one) or select Add Target IP Address.
9. To enter the host ip address go to virtual box and start metasploitable 2 giving username and password as msfadmin and Start Ubuntu desktop VM with user id as sec-lab and password as untccdc. You can use your own windows IP address for use.
10. Then type ifconfig to obtain the ipaddress in Ubuntu and metasploitable.

![Screen Shot 2025-01-18 at 4 47 26 PM](https://github.com/user-attachments/assets/20109041-08a3-4d33-ad6b-64ce69b15cbb)


![Screen Shot 2025-01-18 at 4 50 09 PM](https://github.com/user-attachments/assets/dc6e3af7-1f41-4379-9bff-2691ca89df60)

9.
On the Plugins tab, click on Disable All and enter the following specific vulnerabilities. This list is going to be rather long as we are scanning for services that may be running on our Linux target:
• Backdoors
• Brute Force Attacks
• CentOS Local Security Checks
• DNS
• Debian Local Security Checks
• Default Unix Accounts
• Denial of Service
• FTP
• Fedora Local Security Checks
• Firewalls
• FreeBSD Local Security Checks
• Gain a shell remotely
• General
• Gentoo Local Security Checks
• HP-UX Local Security Checks
• Mandriva Local Security Checks
• Misc
• Red Hat Local Security Checks
• SMTP Problems
• SNMP
• Scientific Linux Local Security Checks
• Slackware Local Security Checks
• Solaris Local Security Checks
• SuSE Local Security Checks
• Ubuntu Local Security Checks
• Web Servers

11. Click on save to save your new scan
12. On the main menu, click on the Scan. Then Click on Launch button to start scanning.
13. Once completed, you will receive a report inside of the Results tab. 13. Double-click on the report to analyze the following points:
• Each target in which a vulnerability is found will be listed
• Double-click on the IP address to see the ports and issues on each port
• Click on the number under the column to get the list of specific issues vulnerabilities found
• The vulnerabilities will be listed in detail

![Screen Shot 2025-01-18 at 4 53 32 PM](https://github.com/user-attachments/assets/429f8d68-f186-455c-8bff-83dd19ce774f)

14. Click on export Report – Complete List of Vulnerabilities by host
Q4. Attach the Downloaded report while submitting and write down summary of scanned analysis in brief.

Data Collection: Q2_Scan_L.V.A
![Screen Shot 2025-01-18 at 8 29 55 PM](https://github.com/user-attachments/assets/3da2e798-2e4a-4df2-a815-32f68c2f908b)
![Screen Shot 2025-01-18 at 8 32 33 PM](https://github.com/user-attachments/assets/1ffa9335-09ba-43d7-9ba9-4c594c6b3eb9)
![Screen Shot 2025-01-18 at 8 34 49 PM](https://github.com/user-attachments/assets/eec30816-d6b2-4bd5-936b-51719225a399)
![Screen Shot 2025-01-18 at 8 35 32 PM](https://github.com/user-attachments/assets/ea03399c-92b9-4e05-a043-4f6cb37574c0)
![Screen Shot 2025-01-18 at 8 36 11 PM](https://github.com/user-attachments/assets/39e04558-cf00-4ac2-a5d4-82787b201e3f)


Data analysis:
In the Complete List of Vulnerabilities Assessment by host on the Metasploitable machine. I analyzed
that the lab had a total of 72 vulnerabilities. I noticed that the category vulnerabilities were from critical, high, medium, and low, or info. I had a total of 7 severities critical. The 7 critical had average 9.84 for CVSS V3.0 and average of 4 for the VPR Score. There was a total of 3 severities high, a total of 17 severities medium, and 4 severities low, 41 severities info. Also, the results show that the Kali machine system had zero vulnerabilities and only 3 severities info.




