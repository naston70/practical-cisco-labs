# HSRP

#### FHRP - FIRST HOP REDUNDANCY PROTOCOL

A **First Hop Redundancy Protocol** (FHRP) is a networkig protocol designed to provide redundancy of the default gateway used on a network, by allowing two or more routers to assume the same default gateway IP address.

- In the event of failure of an active gateway, the backup gateway will take over the address

- FHRPS are not the same as VSS/VPC

#### FHRPs

There are several First Hop Redundancy Protocols

1. HSRP - (Hot Standby Router Protocol) - Cisco proprietary
2. VRRP - (Virtual Router Redundancy Protocol) - open standard
3. GLBP - (Gateway Laod Balancing Protocol) - Cisco proprietary, enables load balancing + redundancy

#### HSRP - Hot Standby Router Protocol

- Cisco Proprietary

- Since a router can only use one IP address for the Default Gateway, HSRP routers can assume a single virtual IP address that is assigned to endpoint hosts

- Once a link, or the gateway router itself fails, the other (standby)router becomes the active gateway and takes the virtual gateway IP. Endpoint hosts never change their default gateway address

#### Configuring HSRP