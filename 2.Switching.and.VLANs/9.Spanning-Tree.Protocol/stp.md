# SPANNING TREE PROTOCOL

STP (IEEE 801.D) 'scans' the network to find all links, making sure that there are no loops - by 'switching off' all redundant links.

It first uses the STA (SPANNING TREE ALGORITHM) to figure out the topology, and then identifies the links that form loops. Those links are blocked one by one removing loops.

In order for this to function properly, all switches must cooperate: one of the switches is chosen to be a reference point - teh 'Root Bridge' and it becomes the root of the tree


#### STP STEPS

1. STP ELECTS A ROOT SWITCH. The switch with the lowest BID value (priority) becomes the RB. All 'working' interfaces on the root switch become Designated Ports (DPs)
	
	- BID, original format: Priority(2B) + Univeral, burned in MAC of the switch
	- BID, system ID extension:
		- Priority, multiplpe of 4096, from 0 to 61440 (4 bits), set at 32768 by default
		- System ID extension, typcially holds VLAN ID 
		- System ID = MAC address of the switch

2. EACH 'NONROOT BRIDGE' CHOOSES ITS ROOT PORT - the lowest cost interface to reach the RB, root switch, through. Root switches dont have RPs. Each switch in a given network has exactly one root port per VLAN. RB will send 'Root Cost = 0' in Hello packets

STP tiebreakers when choosing the Root Port:
	1. Cost to the RB -> when that ties ->
	2. Lowest neighbour BID

3. DESIGNATED PORT ELECTION: on each network segment, the port that advertises the lowest price to RB becomes DP. All other ports will, if theyre not RP, become designated ports and they will be put either into a 'blocking' or 'discarding' mode.

Access ports will also become DPs automatically because the switch is the only device on the segment to send Hellos -> switch is therefore sending least-cost Hellos.


STP - WHY CONFIGURE IT MANUALLY?
--------------------------------

When ou boot  switch STP is on by default. Still you should configure it manually.

- If you let STP configure the tree it might pick an older switch to be Root, which could end up getting more traffic than a newer/ better switch .

- STP is also unaware of any specific VLAN configs on a links. If one trunk can carry all VLANs but another cant and STP blocks the first link, this will cause problems.

As an ADMIN, you can pick the Root switch manually which will greatly influence the resulting tree.


## STP - How to Configure:
--------------------------

```
Switch(config)# spanning-tree vlan VLAN_ID root primary

Switch(config)# spanning-tree vlan VLAN_ID root secondary

Switch(config)# spanning-tree vlan VLAN_ID priority PRIORITY
```

The default priority is 32768, so its enough to set any vale lower than that for the given switch to become Root. Priority values must be an increment of 4096 with the highest possible value being 61440.

If the Priority value is already 20480, running the ```root primary```command will still lower that value -4096 to 16384 as it learns the lowest number through BPDU's

# STP - Multiple VLANs
----------------------

STP was initially designed to work with bridges and support only one LAN or one VLAN.

Even if you have multiple VLANs in your network, you can still only have a single instance of STP - all VLANs will share the same tree. In order to best utilize the gear, there should be a different tree for each VLAN.

This is acheived by running a seperate instance of STP per VLAN. Its called PVST - Per VLAN Spanning Tree.

For every VLAN, you will choose a different Root Bridge (switch) which means some redundant links in one VLAN will be used by another VLAN

# STP - PVST, but Faster

After a change is made a network will take 30-50 seconds to converge. In order to imrove this a rapid version of STP was introduced by the IEEE.

A network that uses RSTP ill converge faster but it still depends on the size of the network.















