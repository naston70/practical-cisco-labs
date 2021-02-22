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

HSRP is configured in the ***interface config mode*** on the interface facing the internal network, where that interface is the default gateway.

**Virtual IP Address** is used by the active gateway:

R1(config-if)#standby 1 ip 192.168.1.1


***Priority*** is by default 100, and **a higher number means higher priority.** In other words, the router with the higher priority will become the active gateway, wheras, the router with lower priority will be a standby gateway. 

R1(config-if)#standby 1 priority 105

In case the interface we're configuring HSRP on fails, or another interface that is being ***tracked*** fails, this number will be reduced by 10, therefore making this router a lower priority one.

The goal of HSRP is to detect failures on an active gateway, so that a standby gateway can take over automatically. In order to achieve this, we should 'tell' HSRP what to monitor.

R1(config-if)#standby 1 track GigabitEthernet 0/0
-===============================================-

Preempt enables a router to take over the active role as soon as its priority surpasses the active routers priority.

This will happen if a new, higher-priority router is added to the network. 

R1(config-if)#standby 1 preempt