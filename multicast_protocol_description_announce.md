# Multicast Announce

Multicast announce is a way for a level II node to announce that it is available and tell what it can do to other nodes in a a system. If a level II node can implement this interface it should implement it. A node that listen for at least one minute in the multicast announce channel will after that know the existence of all VSCP nodes on that system that want to be known. 

The group used for VSCP multicast announcements is the VSCP assigned *group 224.0.23.158* and the VSCP standard *port 9598* is reserved for this usage.

## Events


## Configuration

The configuration of the multicast announce interface can be done in the VSCP server configuration file (/etc/vscp/vscpd.conf) or in the configuration database. The configuratiion is [fully described here](./configuring_the_vscp_daemon.md#multicast_announce_interface).

The first option is to decide if the service should be enabled or not. This is set by setting enable equal to "true" or "false". It is strongly recommended that this service is enabled.

Next setting is to decide what interface of the machine should be used for announcements and what port they will be sent on. The default is udp://9598 which is announcements on all interfaces using the standard port 9598.

Next set **ttl (time to live)** for multicast frames. 

 | TTL | Scope                                                                            | 
 | :---: | -----                                                                            | 
 | 0   | Are restricted to the same host. Won't be output by any interface.               | 
 | 1   | Are restricted to the same subnet. Won't be forwarded by a router. (**default**) | 
 | 32  | Are restricted to the same site, organization or department.                     | 
 | 64  | Are restricted to the same region.                                               | 
 | 128 | Are restricted to the same continent.                                            | 
 | 255 | Are unrestricted in scope (global).                                              | 



## Sample code

You can find sample code (C/C++/Python) [here](https://github.com/grodansparadis/vscp/tree/master/tests/multicast) for both multicast announce and multicast channel interfacing. More will follow.


{% include "./bottom_copyright.md" %}
