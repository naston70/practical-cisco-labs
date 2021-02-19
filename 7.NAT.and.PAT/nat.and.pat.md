# NAT - NETWORK ADDRESS TRANSLATION & PAT - PORT ADDRESS TRANSLATION


**Network Address Translation** is a way to map private IPs into public IPs and vice versa. Its used at network edge - on routers, firewalls or other network devices.


There are two main NAT types:

- Static

- Dynamic

#### Static Network Address Translation

When using static NAT, we translate one private IP address into one public IP address. This is usually needed when a LAN device needs to be accessed from the outside.

```
R(config)# ip nat inside source static 192.168.0.1 217.3.250.6
```
When configuring dynamic NAT, we need to specify a range of addresses to be translated.

```
R(config)#ip access-list standard 1
R(config-std-nacl)#permit 192.168.1.0 0.0.0.255

R(config)#ip nat inside source list 1 interface f0/0 overload
```

