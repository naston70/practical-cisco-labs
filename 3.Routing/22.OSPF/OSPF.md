# OSPF AREAS

An OSPF area is a logical grouping of contiguous networks and routers, and all routers within the same area share the same toplogy. 

Only border routers (ABR's) are aware of topologies in the two (or more) areas they are connecting

**Reasons to segment an OSPF network into areas:**

- Reduces the size of routing tables
- Faster convergence
- Less calculation during router discovery and fulfillment of the routing table
- Easier to troubleshoot

### OSPF METRICS

Unlike with RIP which only considers the number of hops, OSPF considers individual costs of each link on the path before choosing the best route. The cost of the entire path from source to destination is the sum of the costs of all outgoing interfaces along that path