# Network Configurations
### Commands for configuring switch
```bash
en
conf t

hostname HR-SW
line console 0
pass cisco
login
exit

enable password cisco
no ip domain-lookup
banner motd #Unautorized access#

service password-encryption

do wr
```

### Commands for configuring Core Routers

```bash
en
conf t

hostname CORE-R2
line console 0
pass cisco
login
exit

enable password cisco
no ip domain-lookup
banner motd #Unautorized access#

service password-encryption

do wr


ip domain-name cisco.net
username admin password cisco
crypto key generate rsa
1024
line vty 0 15
login local
transport input ssh
exit

ip ssh version 2

do wr
```

### Commands for configuring default static route

```bash
# for multilayer 1 & 2 switch both

ip route 0.0.0.0 0.0.0.0 gig1/0/1
ip route 0.0.0.0 0.0.0.0 gig1/0/2 70

do wr


============================================
# for core 1 & 2 router both

ip route 0.0.0.0 0.0.0.0 se0/2/0
ip route 0.0.0.0 0.0.0.0 se0/2/1 70

do wr 
```

### Commands for setting security

```bash
int range fa0/3-24
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation shutdown
```

### Inter VLAN Routing for multilayer switch

```bash
int vlan 10
ip address 172.16.1.1 255.255.255.128
ip helper-address 172.16.3.130
no sh

int vlan 20
ip address 172.16.1.129 255.255.255.128
ip helper-address 172.16.3.130
no sh

int vlan 30
ip address 172.16.2.1 255.255.255.128
ip helper-address 172.16.3.130
no sh

int vlan 40
ip address 172.16.2.129 255.255.255.128
ip helper-address 172.16.3.130
no sh

int vlan 50
ip address 172.16.3.1 255.255.255.128
ip helper-address 172.16.3.130
no sh

int vlan 60
ip address 172.16.3.129 255.255.255.240
ip helper-address 172.16.3.130
no sh


exit


do wr
```

### NAT configuration for core Router

```bash
# both core 1 2

ip nat inside source list 1 interface se0/2/0 overload 
ip nat inside source list 1 interface se0/2/1 overload 


access-list 1 permit 172.16.1.0 0.0.0.127
access-list 1 permit 172.16.1.128 0.0.0.127
access-list 1 permit 172.16.2.0 0.0.0.127
access-list 1 permit 172.16.2.128 0.0.0.127
access-list 1 permit 172.16.3.0 0.0.0.127
access-list 1 permit 172.16.3.128 0.0.0.15


int range gig0/0-1
ip nat inside 
exit

int se0/2/0
ip nat outside

int se0/2/1
ip nat outside 
exit


do wr
```

### OSPF configuration for core Router

```bash
# for core 1 router

router ospf 10

router-id 3.3.3.3

network 172.16.3.144 0.0.0.3 area 0
network 172.16.3.152 0.0.0.3 area 0
network 195.136.17.0 0.0.0.3 area 0
network 195.136.17.4 0.0.0.3 area 0

exit

do wr

=======================


# for core 2 router


router ospf 10

router-id 4.4.4.4

network 172.16.3.148 0.0.0.3 area 0
network 172.16.3.156 0.0.0.3 area 0
network 195.136.17.8 0.0.0.3 area 0
network 195.136.17.12 0.0.0.3 area 0

exit

do wr
```

### OSPF configuration for Multilayer
```bash
# for multilayer switch only
# for mutlayer 1 switch

ip routing 

router ospf 10

router-id 2.2.2.2

network 172.16.1.0 0.0.0.127 area 0
network 172.16.1.128 0.0.0.127 area 0
network 172.16.2.0 0.0.0.127 area 0
network 172.16.2.128 0.0.0.127 area 0
network 172.16.3.0 0.0.0.127 area 0
network 172.16.3.128 0.0.0.15 area 0


network 172.16.3.144 0.0.0.3 area 0
network 172.16.3.148 0.0.0.3 area 0



=======================


# for multilayer switch only
# for mutlayer 2 switch

ip routing 

router ospf 10

router-id 1.1.1.1

network 172.16.1.0 0.0.0.127 area 0
network 172.16.1.128 0.0.0.127 area 0
network 172.16.2.0 0.0.0.127 area 0
network 172.16.2.128 0.0.0.127 area 0
network 172.16.3.0 0.0.0.127 area 0
network 172.16.3.128 0.0.0.15 area 0


network 172.16.3.152 0.0.0.3 area 0
network 172.16.3.156 0.0.0.3 area 0
```

### OSPF configuration for ISP Router

```bash
router ospf 10

router-id 5.5.5.5

network 195.136.17.8 0.0.0.3 area 0
network 195.136.17.0 0.0.0.3 area 0

exit

do wr

=============================


router ospf 10

router-id 5.5.5.5

network 195.136.17.4 0.0.0.3 area 0
network 195.136.17.12 0.0.0.3 area 0

exit

do wr
```



