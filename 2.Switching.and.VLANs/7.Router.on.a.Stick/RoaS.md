#ROUTER-on-a-Stick

If there is a need for endpoints in different VLANs to communicte, a router is needed.

'Router on as stick' is a specific router configuration whose task is to connect different VLANs. The router is 'on a stick' because theres often several seperate networks connected to a single router interface.

This is acheived by creating virtual interfaces on top if a single physical interface. Each virtual interface is a gateway for its VLAN. 

##'dot1q'

Since a trunk link can carry packets belonging to different VLANs, there has to be a way to differetiate those packets, so that the receiving switch knows to which access port it should forward them to.

To solve this, tagging is used: an ID is attached to each frame transferred via trunk links. 

In short: an ID (or tag) is added to a frame before sending over a trunk link and is removed from frames before sending them to access links