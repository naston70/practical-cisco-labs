# STATIC ROUTING

### Static vs. Dynamic Routing

**Static:** someone (an admin) must manually enter all networks in a domian into the routing tables. If a change occurs within that domain, the admin must manually update the tables.

**Dynamic:** a protocol on a router communicates to that same protocol on neighbouring and other, adjacent routers in that domain. If a chnage occurs, the routers, using that protocol, inform each other of the change and as a result, update their tables automatically.




### Static Routing - The AD Parameter


AD is short for 'Administrative Distance', and it is the value used to mark router preference / rank the routes available in the routing table

```
R1(config)# ip route 2.0.0.0 255.255.255.252 s0/0/0 **150**
```
150 is an AD for netwok 2.0.0.0 through this route

A static route will by default get an AD of 0 or 1 (exit interface=0, next hop=1), where 0 is the best route and 255 is the worst.

The default AD values for the routing protocols are:

EIGRP AD: 90
OSPF AD : 110
RIP AD  : 120