# OSPF Area Virtual Link

Each OSPF area **must be linked with the backbone area** - if theyre not directly connected, then a ***virtual link*** must be established

The ***virtual link*** is configured on an ABR (Area Border Router), where a loopback IP of the ABR connected to **area 0** is added. The same is configured on the remote ABR - a virtual link is established from the **area 0** ABR to the remote area ABR