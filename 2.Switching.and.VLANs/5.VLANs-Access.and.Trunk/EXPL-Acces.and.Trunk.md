# VLANs - ACCESS AND TRUNK LINKS

### LAN Segmentation


There is often a need for communication to be restricted between hosts in the same network. 

The best way to do this is by using VLANs

![alttext](https://github.com/naston70/practical-cisco-labs/blob/main/img/access-trunk.png)

VLAN stands for Virtual Local Area Network.

It is used to seperate hosts residing in the same physical network or address space. To do that you configure switch ports to connect to end devices.

In the above example there are 2 VLAN's (5 & 7)

VLANs are configured on a switch.
For end point devices the interfaces from the switch must first be in access mode

Below uses PC1 in VLAN 5 

```
CREATE A VLAN
Switch(config)# vlan 5

CONFIGURE ACCESS/TRUNK
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 5


Switch(config)#interface FastEthernet 0/2
Switch(config-if) switchport mode trunk


```
Access VLANs can only carry one VLAN (5 in this case)
The link between Switch2 and Switch1 requires a trunk port to carry more than one VLAN on G0/1