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

