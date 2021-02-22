# Point-to-Point Protocol

**PPP** is a network protocol used to establish a direct connection between two nodes. It can provide authentication, transmission encryption and compression.

Originally designed to work with ***serial connections***, PPP was adopted by ISP's to provide dial up Internet access.

**PPPoE** PPP over Ethernet, extends the original capability of PPP by encapsulating the packets in Ethernet frames.

#### PPP - Authentication

**PAP** (Password Autentication Protocol) is the less secure method - passwords are transmitted in clear text.

**CHAP** (Challenge Handshake Authentication Protocol) still doesn't use encryption, but it uses hashing. 'Challenge' means that the credential are checked periodically, even after connection has been establsihed.