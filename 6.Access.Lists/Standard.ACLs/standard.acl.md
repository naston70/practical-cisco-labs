# ACCESS CONTROL LISTS

An **Access Control List** is a list of rules configured on a network device, used to filter traffic flowing through that device.

**Each packet** that goes through that device is compared against **each rule** in the ACL

**If the packet doesnt match** the ***current*** rule, its compared to the ***next*** one.

As soon as the packet matches a rule, the rule is applied and all the rules that come after that are ignored.

At the end f the list, there is usually a **'catch all'** rule, that applies to packets that dont match any of the other rules

#### Configuring ACLs on Cisco Devices

Any number of ACLs can be created on a router (or other network device), but a list will not filter traffic **'until its applied to an interface'**

Its also enough to only apply an ACL to a chosen interface, the ***direction*** of packet flow must also be specified.

**Inbound ACL =** flters incoming traffic (packets are dropped/forwarded prior to being routed)

**Outbound ACL=** filters outgoing traffic (packets are dropped/forwarded after being routed)

#### Standard vs Extended ACLs

**Standard** ACLs can filter traffic based only on source IP.

**Extended** ACLs can filter traffic based on source and destination IPs and also ports and protocols

For **standard ACLs** we use numbers 1-99 and 1000-1399
For **extended ACLs** we use number 100-199 and 2000-2699