

```

1. Hostname, banner
-------------------
Router(config)#hostname R1 
R1(config)#banner motd #Robert.G#

2. Access mode and VLANs
------------------------
S1(config)#interface range FastEthernet 0/1-8 
S1(config-if-range)#switchport mode access 
S1(config-if-range)#switchport access vlan 200
S1(config)#interface range FastEthernet 0/9-16 
S1(config-if-range)#switchport mode access 
S1(config-if-range)#switchport access vlan 100 % Access VLAN does not exist. Creating vlan 100
 
3. Trunk
--------
S3(config)#interface range GigabitEthernet 0/1-2 
S3(config-if-range)#switchport mode trunk

S2-R1 link:
-----------
S2(config)#interface FastEthernet 0/1
S2(config-if)#switchport mode trunk

4. Creating VLANs on switches
-----------------------------
S2(config)#vlan 100
S2(config)#vlan 200

5. Router on a stick
--------------------
R1(config)#interface FastEthernet 0/1 
R1(config-if)#no shutdown
R1(config)#interface FastEthernet 0/1.100 
R1(config-subif)#encapsulation dot1Q 100 
R1(config-subif)#ip address 192.168.1.1 255.255.255.0
R1(config)#interface FastEthernet 0/1.200 
R1(config-subif)#encapsulation dot1Q 200 
R1(config-subif)#ip address 192.168.2.1 255.255.255.0


DHCP server on R1
-----------------
R1(config)#ip dhcp excluded-address 192.168.1.0 192.168.1.10 
R1(config)#ip dhcp excluded-address 192.168.2.0 192.168.2.10
R1(config)#ip dhcp pool Vlan100 
R1(dhcp-config)#network 192.168.1.0 255.255.255.0 
R1(dhcp-config)#default-router 192.168.1.1
R1(config)#ip dhcp pool Vlan200 
R1(dhcp-config)#network 192.168.2.0 255.255.255.0 
R1(dhcp-config)#default-router 192.168.2.1

