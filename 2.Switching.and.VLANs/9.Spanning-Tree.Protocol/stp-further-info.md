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

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
#### STP port states

**Forwarding state** - use the interface as normal

**Blocking state** - block all user traffic, do not send or receive user traffic on that interface (in that VLAN) except STP messages. (+overhead)

**Disabled state** - tecnically not a transition state, a port in the administravitely disabled state doesnt participate in frame forwarding or STP.

**Listening state** - listens to BPDUs to make sure no loops occur on the network before passing data frames. A port in listening state prepares to forward data frames without populating the MAC address table. Old MAC addresses are removed from the table during this state. Switches populate MAC address tables in learning and forwarding modes only.

**Learning state** - listens to BPDUs and learns all the paths in the switched network. A port in learning state populates the MAC address table but still does not forwad the frame. 'Forward Delay' refers to the time it takes to transition a port from listening mode to learning mode, which is set to 15 secs by default. This can be seen using the command ```#show spanning-tree```
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

'Working' ports/interfaces (in a connected state) are all interfaces that **could** forward frames if STP placed them into a forwarding state. Failed interfaces or administratively shutdown interfaces are placed into an STP disabled state. 

'Port Cost' determines the best path when multiple links are used between two swtiches. the cost of the link is determined by its bandwidth
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

#### STP steps:

1. STP ELECTS A ROOT SWITCH (ROOT BRIDGE - RB) The switch with the lowest BID value (priority) ecomes the RB. ALl 'working' interfaces on the root switch become Designated ports (DPs)

2. EACH NONOROOT BRIDGE CHOOSES ITS ROOT PORT - The lowest cost interface to reach th RB through. Root switches dont have RPs. Each switch in a given network has exactly one root port per VLAN. RB will send 'Root Cost = 0' in Hello packets

3. DESIGNATED PORT ELECTION: On each network segment (link), the port that advertises the lowest price to RB becomes the DP. ALl other ports in that segment will, if theyre not RP, become non-designated port and theyll be put into either a blocking or discarding mode.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
#### How STP works in a steady-state (nothing changing in the topology)

1. The root creates and sends a Hello BPDU, with a root cost of 0 out all its forwarding interface

2. The non root switches receive the Hello on their root ports. After changing the Hello to list their own BID as the senders BID and listing their own root cost, the switch forwards the Hello out all designated ports.

3. Repeat until something changes.

When a switch ceases to receive Hellos or receives a changed Hello -> something has failed -> the switch starts the process of changing the spanning-tree topology

If an interface fails on a swtich, the switch can assume the Hellos wont be arriving in that interface anymore.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
#### Hello BPDU fields

1. Root Bridge ID -> BID of the switch that the sender of this Hello beleives to currently be the root switch

2. Senders BID -> BID of the switch sending the Hello BPDU

3. Senders ROOT COST -> STP cost between this switch and the current root

4. Timer values on the RB ->Hello timer, MaxAge and Forward delay timer

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
#### STP timers (RB dictates timers)

1. Hello (2 secs): the time period between Hellos created by the root

2. MaxAge (10 Hello's): how long any switch should wait after ceasing to hear Hello's before trying to change STP topology

3. Forward Delay (15 secs): when an interface canges from blocking to forwarding state, a port styas in an interim, listening state and then an interim learning state for 'forward delay' number of seconds. This prevents temporary loops.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
#### RSTP - RAPID STP

− RSTP calls the blocking state “the discarding state”

− STP converges in 50 seconds (by default), RSTP converges within a few seconds, and in slow
conditions, in about 10 seconds

− In RSTP, MaxAge is 3 times Hello

− RSTP Alternate Ports are the switch’s other ports that could be used as a Root Port if the existing RP
ever fails. To become an alternate port, an interface must receive Hellos that identify the same root switch (RB) as the root port. The alternate port can take over for the former RP very rapidly, without waiting in other interim STP states (listening, learning). There are no timers, the change (convergence) happens within a second

− RSTP Backup Port replaces a designated port when a DP fails. This is only needed in a network where a switch connects two ports to a Hub

− RSTP port types:
1) point-to-point ports -> ports that connect two switches;

2) point-to-point edge ports -> ports that connect to a single endpoint device at the edge of a
network, like PCs and servers;

3) shared ports -> ports connected to a hub (half duplex).
Both 1) and 2) are full duplex.


Portfast: allows a switch to immediately transition from blocking to forwarding, bypassing listening and learning states. Should only be enabled on ports where no other bridges, switches, or other STP-speaking devices will be connected. If enabled, the port will move to an STP forwarding state and forward traffic as soon as the NIC is active on the end device connected to the port.
BPDU guard: disables a port if any BPDUs are received on the port. Should only be enabled on access/Portfast interfaces.












