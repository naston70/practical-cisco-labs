# EIGRP

- **Proprietary,** owned and developed by Cisco
- **Distance vector** with some Link state features
- **For best path choice,** the following is considered: 1) lowest bandwidth on the path and 2) cumulative latency on all interfaces on the path
- **All paths** calculated by EIGRP are saved to the topology table, and the best ones are stored in the routing table

##### Conditions for neighbourship between two EIGRP routers:

- ACK or Hello is received
- Same Autonomous System
- Same subnet
- Same metrics for the link that connects them
- Successful Authentication (if used)