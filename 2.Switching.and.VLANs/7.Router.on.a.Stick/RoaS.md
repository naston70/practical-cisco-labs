#ROUTER-on-a-Stick

If there is a need for endpoints in different VLANs to communicte, a router is needed.

'Router on as stick' is a specific router configuration whose task is to connect different VLANs. The router is 'on a stick' because theres often several seperate networks connected to a single router interface.

This is acheived by creating virtual interfaces on top if a single physical interface. Each virtual interface is a gateway for its VLAN. 