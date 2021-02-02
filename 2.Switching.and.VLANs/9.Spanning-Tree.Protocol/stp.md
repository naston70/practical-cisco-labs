# SPANNING TREE PROTOCOL

STP (IEEE 801.D) 'scans' the network to find all links, making sure that there are no loops - by 'switching off' all redundant links.

It first uses the STA (SPANNING TREE ALGORITHM) to figure out the topology, and then identifies the links that form loops. Those links are blocked one by one removing loops.

In order for this to function properly, all switches must cooperate: one of the switches is chosen to be a reference point - teh 'Root Bridge' and it becomes the root of the tree