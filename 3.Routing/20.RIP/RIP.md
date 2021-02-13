# ROUTING INFORMATION PROTOCOL

***RIP FACTS:***

- Routers using RIP will send the entire routing table every 30 seconds through all active interfaces

- If a router doesnt hear back from one of its neighbours in 180 seconds (default value), it considers that neighbour no longer active, then it adjusts its routing table and propogates further

- The best routes are selected based on the number of hops

- AD is 120 (Administrative Distance)

### RIP VERSIONS

**RIP version 1** only supports classful addressing - routers using RIP will not propogate information on subnet masks to their neighbours

**RIP version 2** supports subnetting and will propogate inoformation on subnet masks

### RIP - CONFIGURATION

```
R1(config)# router rip
R1(config-router)# version 2
R1(config-router)# network 1.0.0.0
R1(config-router)# network 3.0.0.0

Disabling RIP:
R1(config)# no router rip

```

### RIP - ADDITIONAL CONFIGURATION

***Passive interface -*** if RIP is used on a Gateway router, WAN interfaces should not sending the routing table to the internet. This is achieved by configuring the following:

```
Router(config-router)# passive-interface serial 0/0/0
```
**No auto-summary -** disables automatic summarization of routers

Router(config-router)# no auto-summary



