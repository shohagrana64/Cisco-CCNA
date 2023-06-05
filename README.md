# Cisco CCNA
 
## Basic Configurations

```
en
conf t
hostname R1
no ip domain-lookup
enable secret class
line con 0
password cisco
logging synchronous
login
banner motd #Unauthorized Access Prohibited#
line vty 0 4
password cisco
login
```