Exercise Commands


```
=========================================
1. HOSTNAME AND BANNER
=========================================
Switch>enable
Switch#conf t

Switch(config)# hostname S1
S1(config)#banner motd #Robert.G#
=========================================

=========================================
2. ACCESS AND VLANS - switch 1
=========================================
S1(config)#interface FastEthernet 0/1
S1(config-if)#switchport mode access
S1(config-if)switchport access vlan 5
S1(config-if)#exit

S1(config)#int f0/2
S1(config-if)#sw mode acc
S1(config-if)#sw acc vlan 7
S1(config-if)#exit
S1(config)#interface GigabitEthernet 0/1
S1(config-if)#switchport mode trunk
=========================================

=========================================
Switch 2
=========================================
S2(config)#interface f01
S2(config-if)#switchport mode access
S2(config-if)#switchport access vlan 5
S2(config-if)#exit

sS2(config)#int range g0/1-2
S2(config-if-range)#switchport mode trunk
=========================================

=========================================
Switch 3
=========================================
S3(config)#interface f0/1
S3(config-if)#switcport mode access
S3(config-if)#switchport access vlan 7
S3(config-if)#exit

S3(config)#interface f0/2
S3(config-if)#switchport mode access
S3(config-if)#swichport access vlan 5
S3(config-if)#exit

S3(config)#int g0/2
S3(config-if)#sw mode trunk
=========================================

=========================================
3. TRUNKS - switch 1
=========================================
S1(config)#interface g0/1
S1(config-if)#switchport mode trunk
=========================================


=========================================
Switch2
=========================================
S2(config)#interface range GigabitEthernet 0/1-2 
S2(config-if-range)#switchport mode trunk
S2(config-if-range)#
=========================================

=========================================
Switch3
=========================================
S3(config)#interface GigabitEthernet 0/2 
S2(config-if)#switchport mode trunk
=========================================

```