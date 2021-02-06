# STP - SPANNING-TREE PROTOCOL


**STP** maintains loop free topologies in a redundant L2 network

**BPDU** (Bridge Protocol Data Unit) messages are frames that switches distribute in between themselves. Switches choose the Root Bridge, Designated and Root ports based on information from BPDUs.

# STP ATTACK

The attacker send BPDU messages to inform the switches that he is now Root (by giving himself the lowest priority)

If the two switches to which an attacker connects are linked, STP will block the link between them and they will only be able to communicate through the attacker  - a perfect example of a MitM attack

# STP ATTACK COUNTERMEASURES

**BPDU guard** is an addition to STP, introduced to protect ports to which end users connect.

BPDU messages are exchanged only **between switches** which means they are not expected to be received on access ports.

If a BPDU guard-enabled port receives a BPDU packet, that port will automatically be disabled - it will go into the **'errdisable'** state. 

**BPDU guard** can be configured globally on a switch - meaning it will be enabled on all Portfast ports:

```
Switch(config)# spanning-tree portfast bpduguard default
```

##### BPDU guard configuration per-port:
```
Switch(config)# spanning-tree bpduguard enable
Switch(config)# spanning-tree bpduguard disable
```

# A BPDU-guard-enabled port will NOT take part in STP!

**Root guard** is another STP addition, similar to BPDU guard - but inteded to protect ports on root switches, not access switches.

Root guard enabled ports can still receive and send BPDU messages, but will block those neighbours that try to become a Root bridge.

```
Switch(config)# spanning-tree guard root
``








