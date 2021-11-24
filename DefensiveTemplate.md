# Blue Team: Summary of Operations
 
## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further
 
### Network Topology

The following machines were identified on the network:
- **Kali**
  - **Operating System**:
     - Debian Kali 5.4.0
  - **Purpose**:
     - Penetration Tester
  - **IP Address**:
     - 192.168.1.90
- **ELK**
  - **Operating System**:
     - Ubuntu 18.04
  - **Purpose**:
     - The ELK Stack (Elastic and Kibana)
  - **IP Address**:
     - 192.168.1.100
- **Capstone**
  - **Operating System**:
     - Ubuntu 18.04
  - **Purpose**:
     - Vulnerable Web Server
  - **IP Address**:
     - 192.168.1.105
- **Target 1**
  - **Operating System**:
     - Debian/Linux 8
  - **Purpose**:
     - WordPress Host
  - **IP Address**:
     - 192.168.1.110

-TODO:NETWORK DIAGRAM (SREECNSHOT HERE)
 
### Description of Targets
The target of this attack was: Target 1 (192.168.1.110)
 
Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. 
As such, the following alerts have been implemented:
 
### Monitoring the Targets
 
Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:
 
#### CPU Usage Monitor
 
CPU Usage Monitor is implemented as follows:
 
WHEN max() OF system.process.cpu.total.pct OVER all documents IS ABOVE 0.5 FOR THE LAST 5 minutes
 
  - **Metric**: WHEN max() OF system.process.cpu.total.pct OVER all documents
  - **Threshold**: IS ABOVE 0.5
  - **Vulnerability Mitigated**: Programs (viruses) or malicious software (malware) running on the system taking up valuable resources
  - **Reliability**: This alert is highly reliable. It can detect if there are malicious programs running as well as help improve on CPU usage. 
  
![blueteam1](https://user-images.githubusercontent.com/91024338/143162166-382498c9-510b-4384-ba71-8dc6c8793938.JPG)

  
#### HTTP Request Size Monitor

HTTP Request Size Monitor is implemented as follows:

WHEN sum() of http.request.bytes OVER all documents IS ABOVE 3500 FOR THE LAST 1 minute

  - **Metric**: WHEN sum() of http.request.bytes OVER all documents
  - **Threshold**: IS ABOVE 3500
  - **Vulnerability Mitigated**: DDOS attacks / Code injection in HTTP requests 
  - **Reliability**: This alert is a medium reliabilty as it can create some false positives. It could detect actual HTTP traffic as well as non malicious HTTP request. 
  
![Project 3 2](https://user-images.githubusercontent.com/91024338/143162384-795233e5-09e7-464f-bf5e-566a69b3946f.JPG)
![Project 3 1](https://user-images.githubusercontent.com/91024338/143162341-f6171742-1149-4bd1-bb7a-262100de1a5f.JPG)

#### Excessive HTTP Errors

Excessive HTTP Errors is implemented as follows:

WHEN count() GROUPED OVER top 5 'http.response.status_code' IS ABOVE 400 FOR THE LAST 5 minutes

  - **Metric**: WHEN count() GROUPED OVER top 5 'http.response.status_code'
  - **Threshold**: IS ABOVE 400
  - **Vulnerability Mitigated**: Brute Force/ Enumeration
  - **Reliability**: This alert is highly reliable. Any error code 400 and above are server and client errors and would be of high concern if they were being triggered at any rate but more importantly if the alert is happening at a high rate. Using the alert to trigger error codes 400 and higher will also filter out any successful responses.  
  
  TODO(SCREENSHOT HERE)
 
 
 
 


