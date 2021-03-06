# Network Forensic Analysis Report

At least two users on the network have been wasting time on YouTube. Usually, IT wouldn't pay much mind to this behavior, but it seems these people have created their own web server on the corporate network. So far, Security knows the following about these time thieves:

They have set up an Active Directory network.
They are constantly watching videos on YouTube.
Their IP addresses are somewhere in the range 10.6.12.0/24.

## Time Thieves 


   - Domain name: frank-n-ted.com
   - Filter: ip.src ==10.6.12.0/24
 
![NetworkP12](https://user-images.githubusercontent.com/91024338/143691987-8ea4179c-a7a6-46ac-8b18-0bd0a34292ef.JPG)


   - IP address: 10.6.12.12 (Frank-n-Ted-DC.frank-n-ted.com)
   - Filter: ip.src==10.6.12.0/24

![net5](https://user-images.githubusercontent.com/91024338/143707990-df6fbd9a-2fdc-4b22-b5dd-5514930ed307.JPG)


   - Downloaded malware: june11.dll
   - Filter: ip.addr==10.6.12.203 and http.request.method==GET
   - Command to export: File > Export Objects > HTTP > Text Filter: june11.dll > Save > Desktop
 
![Networkp 11](https://user-images.githubusercontent.com/91024338/143693443-960e3c29-5f64-4aca-8942-31d1d140accf.JPG)
![net10](https://user-images.githubusercontent.com/91024338/143720586-a0109942-9add-4e3f-a547-bf2f2b9b6d0d.JPG)

       
 - Uploaded the file to [VirusTotal.com](https://www.virustotal.com/gui/). 

![net9](https://user-images.githubusercontent.com/91024338/143720547-b47ffc9c-4da9-4b42-b3b4-99780c0efbd8.JPG)

   
   - Malware classification: Trojan



## Vulnerable Windows Machine
The Security team received reports of an infected Windows host on the network. They know the following:

Machines in the network live in the range 172.16.4.0/24.
The domain mind-hammer.net is associated with the infected computer.
The DC for this network lives at 172.16.4.4 and is named Mind-Hammer-DC.
The network has standard gateway and broadcast addresses.


 - Information about the infected Windows machine:

   - Host name: ROTTERDAM-PC
   - IP address: 172.16.4.205
   - MAC address: 00:59:b0:63:a4

![net6](https://user-images.githubusercontent.com/91024338/143713406-d38d3088-6542-4337-89e4-0e75996b400d.JPG)

    
 - Username of the Windows user whose computer is infected:
   - matthijs.devries
  
![net7](https://user-images.githubusercontent.com/91024338/143719276-3a377e81-9468-4626-bd45-974863dccd14.JPG)
 
  
 - IP addresses used in the actual infection traffic:  
    - Statistics > Conversations > IPv4 > Packets (high to low)
  
     - 185.243.115.84
     - 172.16.4.205
     - 166.62.111.64 
   
![net8](https://user-images.githubusercontent.com/91024338/143719375-57778b08-9382-4987-9193-016e4ae0e44a.JPG)
 


## Illegal Downloads
IT was informed that some users are torrenting on the network. The Security team does not forbid the use of torrents for legitimate purposes, such as downloading operating systems. However, they have a strict policy against copyright infringement.
IT shared the following about the torrent activity:

The machines using torrents live in the range 10.0.0.0/24 and are clients of an AD domain.
The DC of this domain lives at 10.0.0.2 and is named DogOfTheYear-DC.
The DC is associated with the domain dogoftheyear.net.

Your task is to isolate torrent traffic.

 - Information about the machine with IP address `10.0.0.201`:
    - MAC address: 00:16:17:18:66:c8
    - Windows username: elmer.blanco
    - OS version: BLANCO-DESKTOP
    - Filter: ip.src==10.0.0.201 and kerberos.CName.String
    
    
![net4](https://user-images.githubusercontent.com/91024338/143702020-d8c6726c-cdbd-4b4e-a65c-58d696f53558.JPG)

 - Torrent file the user downloaded:
   - Torrent file: Betty_Boop_Rythm_on_the_Reservation.avi.torrent
   - Filter: ip.addr==10.0.0.201 and http.request.method==GET
   
![image](https://user-images.githubusercontent.com/91024338/143699192-758362a3-a846-417c-85eb-8ac603ca5cda.png)
![net3](https://user-images.githubusercontent.com/91024338/143699706-b4cb6b2b-0971-40ec-958e-ff5921bf6b64.JPG)

 
