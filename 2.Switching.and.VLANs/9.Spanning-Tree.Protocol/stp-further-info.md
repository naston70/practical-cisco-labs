#### STP - Spanning Tree Protocol (802.1D)

STP states do not change the other information about the interface: connected/ not connected and operational state - access or trunk, it only adds an additional STP state



#### STP versions and types

IEEE 802.1d (STP, CST – Common Spanning-Tree): really slow but requires very little bridge resources.

PVST+: Cisco proprietary enhancement for STP that provides a separate 802.1d spanning-tree instance for each VLAN. Creates more efficiency of the links in the network, but is just as slow as 802.1d, and it does use more bridge resources than 802.1d.

IEEE 802.1w (RSTP – Rapid Spanning-Tree Protocol): enhanced BPDU exchange, faster network convergence, but still allows only one RB per VLAN. Bridge resources used with RSTP are higher than CST’s but less than PVST+.

Rapid PVST+: Cisco’s version of RSTP that also uses PVST+ and provides a separate instance of 802.1w per VLAN. Fast convergence times and optimal traffic flow but requires the most CPU and memory of all.


#### Bridge port roles

**Forwarding Port** - forwards frames and will either be a root port or DR

**Blocking Port** - wont forward frames in order to prevent loops. A blocked port will still listen to BPDU frames from a neighbour switch, but it will drop any and all other received frames and will never transmit a frame

**Alternate Port** - corresponds to the BLOCKING state of 802.1d (STP), and is used with the newer802.1w (Rapid STP). An alternate port is located on a switch connected to a LAN segment with two or more switches connected, where one if the other switches holds the DP. Alternate port is backup for RP.

**Backup Port** - also corresponds to the blcoking state of 802.1d, and is a term now used with the newer 802.1w (RSTP) A backup port is connected to a LAN segment where another port on that switch is acting as the DP. Backup port is backup for the DP.
