# OSPF Reminders

An OSPF area is a logical grouping of contiguous networks and routers, and all routers within the same area share the same topology. Only border routers (ABRs) are aware of topologies in the two (or more) areas theyre connecting

##### Reasons To segment an OSPF network into areas:

- Reduces the size of routing tables
- Faster convergence
- Less calculation during route discovery and fulfillment of the routing table
- Easier to troubleshoot