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


















