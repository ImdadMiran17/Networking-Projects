# Basic Commands

This is the basic overview of the commands for Router Configuration in Cisco Packet Tracer.

-> Types of modes in Command Line: 
```bash
Router> (This is User EXEC Mode.)
Router> en
Router# (This is Privileged EXEC Mode.)
Router# config terminal
Router(config)# (This is Configuration Mode.)
Router(config)# int fa0/0
Router(config-if)# (This is Interface level within configuration mode)
```

-> To change the Host name:

```bash
Router(config)# hostname HQ
HQ(config)#
```

-> To assign IP address to interface fa0/0 and  turn the port status ON:
```bash
HQ(config)#int fa0/0
HQ(config-if)# ip address 192.168.1.129 255.255.255.192
HQ(config-if)# no shutdown
HQ(config-if)# exit
HQ(config)#
```
  

-> To assign IP address to serial0/0/1 , turn the port status ON and set the clock rate to 64000
```bash
HQ(config)# int s0/0/1
HQ(config-if)# ip address 192.168.1.229 255.255.255.252
HQ(config-if)# clock rate 64000
HQ(config-if)# no shutdown
HQ(config-if)# exit
HQ(config)#
```

  
  

-> To set line console password to "cisco":

```bash
HQ(config)# line console 0
HQ(config-line)# password cisco
HQ(config-line)# login
HQ(config-line)# exit
HQ(config)#
```

  

-> To set vty password to "cisco":

```bash
HQ(config)# line vty 0
HQ(config-line)# password cisco
HQ(config-line)# login
HQ(config-line)# exit
HQ(config)#
```

  

-> To set privileged EXEC password to "cisco":

```bash
HQ(config)# enable secret class
```

  

-> To encrypt the clear text passwords:

```bash
HQ(config)# service password-encryption
```

  

-> To set a requirement that a minimum of 10 characters be used for all passwords:

```bash
HQ(config)# security passwords min-length 10
```

  

-> To create a banner that warns anyone accessing the device that "unauthorized access is prohibited".

```bash
HQ(config)# banner motd #Unauthorized access prohibited!#
```

  

-> To disable DNS lookup (prevent the router from attempting to translate incorrectly entered commands as though they were hostnames.)

```bash
HQ(config)# no ip domain-lookup
```

  

-> To set the clock on the router:

```bash
HQ# clock set 17:00:00 03 Oct 2023
```

  

-> To set the clock timezone on the router:

```bash
HQ# clock timezone BDT 6
```

  

-> To set line console idle EXEC sessions to 3 minutes and 30 seconds , and 4 minutes for vty:

```bash
HQ(config)#line con 0
HQ(config-line)# exec-timeout 3 30
HQ(config-line)# exit
HQ(config)#line vty 0 4
HQ(config-line)#exec-timeout 4 0
HQ(config-line)# exit
HQ(config)#
```

  

-> To set IP route for network 192.168.1.0/24 , subnet mask 255.255.255.0 and hop s0/0/0:

```bash
HQ(config)# ip route 192.168.1.0 255.255.255.0 s0/0/0
```

  

-> To save the running configuration to the startup configuration file:

```bash
HQ# copy running-config startup-config
Destination filename [startup-config]? (Press  enter)
Building configuration...
[OK]
HQ#
```

  

-> To display the routing table on the router:

```bash
HQ# show ip route
```

  

-> To Display a summary list of the interfaces on the router:

```bash
HQ# show ip interface brief
```

  

-> To displays statistics for the network interfaces:

```bash
HQ# show interfaces
```

  

-> To erase the startup configuration file from NVRAM:

```bash
HQ# erase startup-config
```

  

-> To reload switch to remove old configuration information:

```bash
HQ# reload
```

  

  

-> The router needs to send the default route information:

```bash
HQ(config)# router rip
HQ(config-router)# default-information originate
```

  

-> The router needs to disable RIP updates on FastEthernet0/0 interface:

```bash
HQ(config)# router rip
HQ(config-router)# passive-interface FastEthernet0/0
```

 
  

-> To configure Eigrp protocol on the router:

```bash
Router(config)# router eigrp <AS_NUMBER>
Router(config-router)# eigrp router-id <ROUTER_ID>
Router(config-router)# network <NETWORK_ADDRESS>  <WILDCARD_MASK>
or
Router(config-router)# network <Summary_NETWORK_ADDRESS>
```

  

-> To configure EIGRP Hello Interval on the interface in 30 seconds:

```bash
Router(config)# interface se0/0/1
Router(config-if)# ip hello-interval eigrp 100 30
```

  

-> To configure OSPF protocol on the router:

```bash
Router(config)# router ospf 1 # OSPF process ID (1-65535)
Router(config-router)# router-id 1.1.1.1 # Router ID
Router(config-router)# network 10.0.0.0 0.255.255.255 area 0 # network and WILDCARD_MASK and area
```

  

-> To configure OSPF Hello Interval on the interface in 30 seconds:

```bash
Router(config)# interface se0/0/1
Router(config-if)# ip ospf hello-interval 30
```

 
  

-> To configure BGP protocol on the router:

```bash
Router(config)# router bgp 100 # BGP Autonomous System number (AS)
Router(config-router)# network 192.168.1.0 mask 255.255.255.0 # Network advertisement
Router(config-router)# neighbor 192.168.2.2 remote-as 200 # Remote BGP neighbor IP and AS

```

 

  

-> To create a VLAN on the switch:

```bash
Switch(config)# vlan 10
Switch(config-vlan)# name SALES
Switch(config-vlan)# exit

  

Switch(config)# vlan 20
Switch(config-vlan)# name MARKETING
Switch(config-vlan)# exit

  

Switch(config)# vlan 99
Switch(config-vlan)# name NATIVE # Set Native VLAN
Switch(config-vlan)# exit
```

  

-> To assign ports to VLANs on the switch:

```bash
Switch(config)# interface range fa0/1 - 24
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
```

  

-> To set up trunk port for router-on-a-stick on the switch:

```bash
Switch(config)# interface fa0/0
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20
Switch(config-if)# switchport trunk native vlan 99 # Set Native VLAN
```

  

-> To configure subinterfaces for router-on-a-stick on the Router:

```bash
Router(config)# interface fa0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# exit

  

Router(config)# interface fa0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# exit
```

 

  

-> To configure DHCP on the switch:

```bash
Switch(config)# vlan 10
Switch(config-vlan)# name VLAN10
Switch(config-vlan)# exit

  

Switch(config)# interface vlan 10
Switch(config-if)# ip address 192.168.10.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit

  

# Configure DHCP pool with IP address range

Switch(config)# ip dhcp pool VLAN10_POOL
Switch(dhcp-config)# network 192.168.10.0 255.255.255.0
Switch(dhcp-config)# default-router 192.168.10.1
Switch(dhcp-config)# dns-server 8.8.8.8 # Optional: Specify DNS server
Switch(dhcp-config)# domain-name example.com # Optional: Specify domain name
Switch(dhcp-config)# range 192.168.10.10 192.168.10.50
Switch(dhcp-config)# exit

  

# Save the configuration

Switch# write memory
```

 
