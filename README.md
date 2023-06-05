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
### NAT

NAT needs to be configured on the edge router connecting to the internet service provider.

Static NAT Configurations can be done to Servers that need a dedicated ip address to communicate with the internet.
ip nat outside for connection with the ISP. IP nat inside is for the interfaces that are connected to the edge router from within the network.
```
ip nat inside source static INTERNAL-IP PUBLIC-IP

int fa0/0
ip nat inside


int fa 0/1
ip nat outside
```
Dynamic nat configuration needs Access Control List (ACL) to be configured beforehand. It will need the nat list and acl list to configure dynamic nat.

1. Configure ACL
```
access-list 1 permit [Internal NETWORK-IP usually summary ip] [wildcard-mask]
```

2. Configure NAT POOL

```
ip nat pool NAT_POOL 209.165.200.194 209.165.200.206 255.255.255.240
```

3. Configure Dynamic NAT

```
ip nat inside source list 1 pool NAT_POOL overload
```

### Static Default route on edge router

```
ip route 0.0.0.0 0.0.0.0 fa0/0
ip route 0.0.0.0 0.0.0.0 [interface or next hop ip]
```

Also need a static route on ISP which has the NAT address of the network
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