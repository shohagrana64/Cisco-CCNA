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

### OSPF

We have to add all the networks connected to each of the routers

```
router ospf 1
[network ip-address wildcard-mask area 0]
network 192.168.0.0 0.0.255.255 area 0
```

## Switch Configurations

### VLAN basic

```
vlan 10
name student
```
### VLAN ip

```
int vlan 10
ip address 192.168.1.10 255.255.255.0
exit
ip default gateway 192.168.1.1 255.255.255.0
```

### Switchport access to end devices and trunk to routers and switches

```
int g0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30,99
switchport trunk native vlan 99

int fa0/1
switchport mode access
switchport access vlan 10
```