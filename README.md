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
## Router Configurations

### For Interfaces
```
int fa 0/1
no shut
ip address 10.82.1.48 255.255.255.0
```

### For subinterfaces
```
int fa 0/1.10
encapsulation dot1Q 10
ip address 10.82.1.48 255.255.255.0

// native vlan

int fa 0/1.99
encapsulation dot1Q 99 native
ip address 10.82.1.1 255.255.255.0
```
