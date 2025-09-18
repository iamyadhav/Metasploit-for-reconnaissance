
# Metasploit-for-reconnaissance
# Metasploit
Metasploit for reconnaissance in pentesting
#### NAME: Yadhav G P
#### REGISTER NUMBER:212223230247
# AIM:

To get introduced to Metasploit Framework and to  perform reconnaissance  in pentesting .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## Architecture Diagram
```
+----------------------+              +--------------------+             +-------------------------+
|    Attacker Machine  |<----------->|  Target (MySQL DB) |<----------->|       Network           |
|  (Kali Linux + MSF)  |              |    Port 3306       |             | (LAN or External)      |
+----------------------+              +--------------------+             +-------------------------+
         |
         | Metasploit Initialized (msfdb init)
         |
         |-- db_nmap: Port Scan and Service Discovery
         |
         |-- auxiliary/scanner/mysql/mysql_version
         |      --> Detects MySQL Version
         |
         |-- auxiliary/scanner/mysql/mysql_login
                --> Brute-force user login
```

## EXECUTION STEPS AND ITS OUTPUT:

Find out the ip address of the attackers system
### OUTPUT:
Before beginning, set up the Metasploit database by starting the PostgreSQL server and initialize msfconsole database as follows:
```
sudo systemctl start postgresql
msfdb init
msfconsole
```
### OUTPUT:
<img width="834" height="456" alt="image" src="https://github.com/user-attachments/assets/f0670d7c-48ee-4a1e-8eb4-595072d26fd5" />
<img width="674" height="363" alt="image" src="https://github.com/user-attachments/assets/3917dcef-9aa4-45f4-a779-252f17f1791c" />
<img width="840" height="784" alt="image" src="https://github.com/user-attachments/assets/5624c3d6-b642-4b8e-acaf-b4af9df9df25" />

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
Port Scanning:
Following command is executed for scanning the systems on our local area network with a TCP scan (-sT) looking for open ports between 1 and 1000 (-p1-1000).
```
nmap -sT 192.168.1810/24 -p1-1000
```
### OUTPUT:
<img width="872" height="507" alt="image" src="https://github.com/user-attachments/assets/e9a9cb8b-96b9-45b7-8310-55beee68a104" />


**step4:**
use the db-nmap command to scan and save the results into Metasploit's postgresql attached database. In that way, you can use those results in the exploitation stage later.

scan the targets with the command db_nmap as follows.
```
db_nmap -sV -sC -p 3306 <target-ip>
```
### OUTPUT:
<img width="1029" height="431" alt="image" src="https://github.com/user-attachments/assets/f1a35750-50d2-4436-8323-8d8f8b720457" />

Metasploit has a multitude of scanning modules built in. If we open another terminal, we can navigate to Metasploit's auxiliary modules and list all the scanner modules.
```
cd /usr/share /metasploit-framework/modules/auxiliary
ls -l
```
### OUTPUT:
<img width="617" height="280" alt="image" src="https://github.com/user-attachments/assets/3125b312-5a6b-4219-a896-e9dc77b8f75a" />


Search is a powerful command in Metasploit that you can use to find what you want to locate. 
```
search name:Microsoft type:exploit
```
### OUTPUT:
<img width="977" height="802" alt="image" src="https://github.com/user-attachments/assets/338aa617-c476-4afa-9be7-3361529aa0d6" />


## MYSQL ENUMERATION
Find the IP address of the Metasploitable machine first. Then, use the db_nmap command in msfconsole with Nmap flags to scan the MySQL database at 3306 port.
```
db_nmap -sV -sC -p 3306 <metasploitable_ip_address>
```
### OUTPUT:
<img width="1029" height="431" alt="image" src="https://github.com/user-attachments/assets/f1a35750-50d2-4436-8323-8d8f8b720457" />

Use the search option to look for an auxiliary module to scan and enumerate the MySQL database.
```
search type:auxiliary mysql
```
### OUTPUT:
<img width="883" height="274" alt="image" src="https://github.com/user-attachments/assets/cc4dffc6-94f9-4a14-899f-79c642abea53" />

```
use the auxiliary/scanner/mysql/mysql_version
```
### OUTPUT:
<img width="1111" height="814" alt="image" src="https://github.com/user-attachments/assets/93352a6c-7bb2-4da8-9cfb-5bc71e0da3bb" />

module by typing the module name or associated number to scan MySQL version details.
```
use 11
```
Or:
```
use auxiliary/scanner/mysql/mysql_version
```
### OUTPUT:
<img width="916" height="536" alt="image" src="https://github.com/user-attachments/assets/2840314e-392f-4d9d-b1dd-e83562b39e0b" />

Use the set rhosts command to set the parameter and run the module, as follows:


After scanning, you can also brute force MySQL root account via Metasploit's auxiliary(scanner/mysql/mysql_login) module.

```set the PASS_FILE``` parameter to the wordlist path available inside /usr/share/wordlists:

```set PASS_FILE /usr/share/wordlists/rockyou.txt```

Then, specify the IP address of the target machine with the RHOSTS command.

```set RHOSTS <metasploitable-ip-address>```

Set BLANK_PASSWORDS to true in case there is no password set for the root account.

```set BLANK_PASSWORDS true```

### OUTPUT:
<img width="883" height="274" alt="image" src="https://github.com/user-attachments/assets/cc4dffc6-94f9-4a14-899f-79c642abea53" />
<img width="812" height="177" alt="image" src="https://github.com/user-attachments/assets/764bea5b-364a-48cd-8ecb-b32f9a9afacb" />

## RESULT:
The Metasploit framework for reconnaissance is  examined successfully
